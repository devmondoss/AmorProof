# 🔧 Mis Issues Refinados — Anthony López (Full Stack)

Estos son tus 4 Issues principales + 2 parciales. Usa esto para actualizar en GitHub.

---

## #2 REGISTRO FINANCIERO (IA) — TÚ ASIGNADO

**Estado actual:** Muy vago  
**Criticidad:** ALTA  
**Acción:** Refinar antes de implementar

### Propuesta Refinada para GitHub

```markdown
## Historia de usuario
Como persona con estrés financiero, quiero registrar una decisión de gasto con una foto, para que la app la clasifique sin que tenga que escribir nada.

## Criterios de aceptación
- [ ] Dado que la persona toma una foto de un gasto (jpg/png, max 5MB), cuando la sube, entonces la IA analiza y propone monto, categoría y confianza.
- [ ] La IA propone categoría: Antojo / Lo de siempre / Guardé
- [ ] Si confianza > 70%: mostrar confirmación directa
- [ ] Si confianza < 70%: pedir entrada manual
- [ ] El registro queda guardado con foto_url, monto, categoría, timestamp automático

## Notas Técnicas (Backlog Interno)

### Tecnología IA
- [ ] Decidir: Cloud Vision API (Google) O Tesseract OCR O modelo custom
- [ ] Latencia objetivo: < 3 segundos por foto
- [ ] Precisión objetivo: > 85% en recibos mexicanos

### Modelo de Datos
```sql
CREATE TABLE registros (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES usuarios(id),
  foto_url VARCHAR(255),
  monto DECIMAL(10,2),
  categoria ENUM('Antojo', 'Lo de siempre', 'Guardé'),
  confianza_ia FLOAT,
  confirmado_por_usuario BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP
);
```

### API
POST /registros/clasificar
Content-Type: multipart/form-data
- foto: binary file

Respuesta (200):
```json
{
  "monto_propuesto": 150.00,
  "categoria": "Antojo",
  "confianza": 0.92,
  "requiere_confirmacion": false
}
```

### Dependencias
- Requiere #1 (Onboarding) completado
- Depende de: Usuario autenticado
- Bloquea: #4 (Tokens), #8 (Resumen semanal)

## Decisiones Pendientes
- [ ] Modelo IA a usar (costo/precisión trade-off)
- [ ] Almacenamiento de fotos (local vs cloud)
- [ ] Fallback si IA falla
```

---

## #6 PRIMERA EXPERIENCIA DIGITAL (Stellar) — TÚ ASIGNADO

**Estado actual:** Incompleto, falta arquitectura Stellar  
**Criticidad:** ALTA  
**Acción:** Definir modelo custodial

### Propuesta Refinada para GitHub

```markdown
## Historia de usuario
Como persona con estrés financiero, quiero ver y mover mis tokens en mi cuenta de Stellar, para tener mi primer activo digital sin necesitar conocimiento técnico previo.

## Criterios de aceptación
- [ ] Usuario autenticado ve su balance de tokens en UI
- [ ] Balance se actualiza en tiempo real (query cada 30 seg)
- [ ] Puede transferir tokens a otro usuario (por email)
- [ ] Transacción procesada sin pasos técnicos (sin direcciones, keys, etc.)
- [ ] Confirmación visual: "Transacción enviada" con ID

## Notas Técnicas (Backlog Interno)

### Arquitectura Stellar
**Modelo:** CUSTODIAL (backend maneja keys, más simple)
- 1 cuenta Stellar maestra por usuario
- Activo custom: AmorProof (código único)
- Red: Stellar Testnet (desarrollo), mainnet (producción)
- Costo: ~0.00001 XLM por transacción (~$0.000002 USD)

### Modelo de Datos
```sql
CREATE TABLE stellar_accounts (
  id UUID PRIMARY KEY,
  user_id UUID UNIQUE REFERENCES usuarios(id),
  public_key VARCHAR(56) NOT NULL,
  private_key_encrypted TEXT NOT NULL, -- stored encrypted with KMS
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE transferencias (
  id UUID PRIMARY KEY,
  sender_user_id UUID REFERENCES usuarios(id),
  recipient_email VARCHAR(255),
  monto DECIMAL(10,2),
  stellar_tx_id VARCHAR(64),
  estado ENUM('pendiente', 'procesando', 'completada', 'fallida'),
  created_at TIMESTAMP,
  completada_at TIMESTAMP
);
```

### API
GET /mi-cuenta/saldo
Respuesta:
```json
{
  "saldo": 42.50,
  "moneda": "AmorProof",
  "cuenta_publica": "GXXXXXX...YYZZ", // últimos 8 chars
  "actualizado_en": "2026-10-04T12:30:45Z"
}
```

POST /transferencia/enviar
```json
{
  "monto": 10,
  "destinatario_email": "otro@example.com"
}
```
Respuesta:
```json
{
  "transaccion_id": "uuid-xxxx",
  "estado": "procesando",
  "monto": 10,
  "mensaje": "Transacción enviada. Se procesará en segundos."
}
```

### Seguridad
- [ ] Private keys NUNCA al frontend
- [ ] Requests requieren JWT válido
- [ ] 2FA opcional para transferencias > 100 tokens
- [ ] Rate limit: 10 transferencias/hora
- [ ] Logs de auditoría completos

### Dependencias
- Requiere #4 (Tokens) completado
- Requiere #2 (Registros) para acumular tokens
- Bloquea: #7 (Hash en Stellar)

## Decisiones Pendientes
- [ ] KMS para encriptación de keys (AWS KMS, Vault, etc.)
- [ ] Testnet vs Mainnet timing
- [ ] Limits por usuario (max/min transferencia)
```

---

## #7 VERIFICACIÓN DE INTEGRIDAD (Hash en Stellar) — TÚ ASIGNADO

**Estado actual:** Incompleto, falta hashing + batching  
**Criticidad:** ALTA  
**Acción:** Definir flujo de anclaje

### Propuesta Refinada para GitHub

```markdown
## Historia de usuario
Como persona con estrés financiero, quiero confiar en que mi registro no fue alterado, para que el patrón que observo sea honesto.

## Criterios de aceptación
- [ ] Dado que un registro fue guardado (foto + emoji), cuando el sistema lo procesa, entonces genera hash SHA256 del registro.
- [ ] El hash se envía a Stellar (anclado en memo de transacción) sin exponer contenido original.
- [ ] Usuario ve: "✓ Verificado en Stellar [fecha]"
- [ ] Si hace click: muestra primeros 16 chars del hash (sin exponer detalles)

## Notas Técnicas (Backlog Interno)

### Algoritmo Hash
- SHA256(user_id + monto + categoria + emoji + timestamp)
- Resultado: 64 caracteres hexadecimales
- Guardado en DB local Y anclado en Stellar

### Modelo de Datos
```sql
CREATE TABLE registros_hashes (
  id UUID PRIMARY KEY,
  registro_id UUID REFERENCES registros(id),
  hash_sha256 VARCHAR(64) NOT NULL,
  stellar_tx_id VARCHAR(64),
  stellar_verified BOOLEAN DEFAULT false,
  anclado_en TIMESTAMP,
  intentos INT DEFAULT 0
);
```

### Flujo de Anclaje
1. Registro completado (foto + emoji)
2. Backend calcula hash (inmediato)
3. Hash guardado en DB local
4. Hash encolado para anclaje (batch processing)
5. Cada 1 hora: enviar batch de hashes a Stellar
6. Si transacción exitosa: marcar como verificado
7. Si falla: reintentar (max 3 intentos)

### API (interna)
GET /registro/{id}/verificacion
Respuesta:
```json
{
  "verificado": true,
  "hash_preview": "a7b3c9d2...",
  "anclado_en": "2026-10-04T11:30:00Z",
  "stellar_tx": "txXXXXX..." (si user es admin)
}
```

### Consideraciones
- [ ] Batch size: 50-100 hashes por transacción Stellar
- [ ] Retry logic: exponential backoff
- [ ] Cost: ~0.00001 XLM = ~$0.000002 USD (negligible)
- [ ] Mostrar solo hash preview (primeros 16 chars)

### Seguridad
- [ ] Hash es one-way (no se puede revertir)
- [ ] Registro original se encripta en DB (si sensible)
- [ ] Stellar memo es público pero hash = 64 chars random

### Dependencias
- Requiere #6 (Stellar funcionando)
- Bloquea: nada (es independiente)

## Decisiones Pendientes
- [ ] Interval de batch (cada 1 hr vs inmediato)
- [ ] Encriptación adicional de registros
- [ ] UI para mostrar verificación
```

---

## #5 APRENDIZAJE APLICADO (PARCIAL) — TÚ + NAYELI

Tu parte: Backend (entregar lecciones, registrar completitud, otorgar tokens)

```markdown
### Tu Responsabilidad (Backend)

## Criterios de aceptación (Tu parte)
- [ ] API GET /leccion/{categoria} retorna lección del día
- [ ] API POST /leccion/{id}/responder recibe respuestas, valida, otorga tokens
- [ ] Base de datos con tabla lecciones (título, contenido, preguntas, categoría)
- [ ] Tracking de lecciones completadas por usuario

## Modelo de Datos (Tu parte)
```sql
CREATE TABLE lecciones (
  id UUID PRIMARY KEY,
  categoria VARCHAR(50), -- Antojo, Lo de siempre, Guardé
  titulo VARCHAR(200),
  contenido TEXT,
  tiempo_estimado INT, -- segundos
  created_at TIMESTAMP
);

CREATE TABLE leccion_preguntas (
  id UUID PRIMARY KEY,
  leccion_id UUID REFERENCES lecciones(id),
  numero INT,
  pregunta TEXT,
  opciones JSON, -- ["A) ...", "B) ...", "C) ..."]
  respuesta_correcta VARCHAR(1), -- "A", "B", "C"
  created_at TIMESTAMP
);

CREATE TABLE leccion_respuestas_usuario (
  id UUID PRIMARY KEY,
  usuario_id UUID REFERENCES usuarios(id),
  leccion_id UUID REFERENCES lecciones(id),
  respuestas JSON, -- {"1": "A", "2": "B", "3": "C"}
  correctas INT,
  completada BOOLEAN,
  tokens_otorgados INT,
  fecha TIMESTAMP
);
```

## API (Tu parte)
GET /leccion/{categoria}
Respuesta:
```json
{
  "id": "uuid",
  "titulo": "Reconocer impulsos vs. necesidades",
  "contenido": "...",
  "tiempo_estimado": 120,
  "preguntas": [
    {"numero": 1, "pregunta": "¿Qué es un impulso?", "opciones": ["A) ...", "B) ..."]}
  ]
}
```

POST /leccion/{id}/responder
```json
{
  "respuestas": {"1": "A", "2": "B", "3": "C"}
}
```
Respuesta:
```json
{
  "correctas": 3,
  "completada": true,
  "tokens_otorgados": 3,
  "mensaje": "¡Felicidades! Ganaste 3 tokens"
}
```

### Dependencias
- Requiere #2 (Registros) para categoría
- Requiere #4 (Tokens) para otorgar
- Nayeli: Contenido y UI
```

---

## #9 MEDICIÓN DE RECURRENCIA (PARCIAL) — TÚ + NAYELI + ELBA

Tu parte: Backend (eventos, tracking, métricas)

```markdown
### Tu Responsabilidad (Backend)

## Criterios de aceptación (Tu parte)
- [ ] API registra eventos: signup, primer_registro, retorno_d7, retorno_d14, retorno_d28
- [ ] API calcula cohorts: usuarios agrupados por fecha de activación
- [ ] Métricas diarias: DAU, activación, retorno, racha promedio
- [ ] Dashboard interno (solo Elba/Adriana) con KPIs

## Modelo de Datos (Tu parte)
```sql
CREATE TABLE eventos_usuario (
  id UUID PRIMARY KEY,
  usuario_id UUID REFERENCES usuarios(id),
  evento_tipo ENUM('signup', 'primer_registro', 'retorno_d7', 'retorno_d14', 'retorno_d28', 'leccion_completada'),
  created_at TIMESTAMP
);

CREATE TABLE metricas_diarias (
  id UUID PRIMARY KEY,
  fecha DATE,
  total_usuarios INT,
  nuevos_hoy INT,
  activos_hoy INT, -- DAU
  promedio_registros FLOAT,
  promedio_racha FLOAT,
  calculado_at TIMESTAMP
);

CREATE TABLE metricas_cohort (
  id UUID PRIMARY KEY,
  cohort_fecha DATE, -- fecha en que se activaron
  total_usuarios INT,
  retorno_d7_count INT,
  retorno_d7_pct FLOAT,
  retorno_d14_count INT,
  retorno_d14_pct FLOAT,
  retorno_d28_count INT,
  retorno_d28_pct FLOAT
);
```

## API (Tu parte - Solo admin)
GET /admin/metricas/diarias?fecha=2026-10-04
GET /admin/metricas/cohort?desde=2026-10-01
GET /admin/metricas/retorno?dias=7

### Dependencias
- Requiere #2 (Registros) para trackear
- Requiere #4 (Racha) para promedios
- Elba: Dashboard UI
```

---

## 📋 RESUMEN DE TUS ISSUES

| # | Nombre | Criticidad | Status |
|---|--------|-----------|--------|
| 2 | Registro IA | ALTA | Refinar |
| 6 | Stellar | ALTA | Refinar |
| 7 | Hash | ALTA | Refinar |
| 5 (parcial) | Lecciones | Media | Refinar |
| 9 (parcial) | Métricas | ALTA | Refinar |

**Total de trabajo:** ~4-5 issues completos (Full Stack heavy)

**¿Siguiente paso?** Edita estos en los Issues #2, #5, #6, #7, #9 en GitHub.

---

**Preparado por:** Claude  
**Para:** Anthony López (Full Stack)  
**Uso:** Actualizar Issues en GitHub con estos detalles técnicos
