# 🔍 Análisis Técnico del Backlog MVP — Deficiencias y Mejoras

**Fecha:** 2026-10-04  
**Revisado por:** Anthony López (Full Stack)  
**Conclusión:** Los Issues tienen buenas intenciones pero **carecen de detalles técnicos y tienen ambigüedades** que necesitan clarificación antes de implementar.

---

## 🚨 CRÍTICAS GENERALES

### 1. **Criterios de Aceptación Muy Vagos**
Muchos criterios usan lenguaje de negocio sin especificar **cómo** implementarlos técnicamente.

**Ejemplo:**
- "El sistema otorga tokens de inmediato" ¿Dónde se guardan? ¿API? ¿Base de datos? ¿Blockchain?
- "La IA propone monto y categoría" ¿Qué modelo de IA? ¿Costo? ¿Latencia?

### 2. **Falta de Dependencias Claras**
No queda claro el **orden de implementación**. Algunos issues dependen de otros.

**Ejemplo:**
- #4 (Tokens) depende de #2 (Registro)
- #6 (Stellar) depende de #4 (Sistema de tokens)

### 3. **Falta de Detalles Técnicos**
- Modelos de datos (qué tablas, qué campos)
- APIs (endpoints, métodos, payloads)
- Tecnologías (IA, blockchain, base de datos)
- Limitaciones y constraints

### 4. **Duplicación en Issue #7 y #8**
Issue #7 tiene título "8️⃣ Reflexión semanal" (duplica a #8)  
Issue #5 tiene título "6️⃣ Primera experiencia digital" (numbering inconsistente)

---

## 📋 ANÁLISIS POR ISSUE

### ✅ #1 ONBOARDING
**Criticidad:** Media | **Complejidad:** Baja | **Riesgo:** Bajo

#### Deficiencias:
- "Registro básico toma menos de 1 minuto" — ¿Cuáles son los campos obligatorios? Está vacío.
- No especifica validaciones (email válido, contraseña strength, etc.)
- No menciona cómo se guarda (base de datos, qué campos)
- No hay "tutorial del propósito" especificado en criterios

#### Mejoras Técnicas Sugeridas:
```markdown
### Campos del Registro Básico
- Email (única)
- Contraseña (min 8 chars, 1 mayúscula, 1 número)
- Nombre (opcional)
- Acepta términos (checkbox)

### Validaciones
- Email válido (regex)
- Contraseña hashed con bcrypt
- Email único en DB

### API Sugerida
POST /auth/register
{
  "email": "user@example.com",
  "password": "****",
  "name": "Juan"
}

### Respuesta
201 Created
{
  "user_id": "uuid",
  "email": "user@example.com"
}
```

---

### ✅ #2 REGISTRO FINANCIERO
**Criticidad:** ALTA | **Complejidad:** ALTA | **Riesgo:** ALTO

#### Deficiencias:
- "IA propone monto y categoría" — ¿Qué modelo IA? ¿OCR? ¿Custom?
- ¿Cuál es el formato de la foto? (jpg, png, tamaño máximo)
- ¿Cuál es la latencia aceptable? (segundos para clasificar)
- No especifica qué pasa si la IA no reconoce la foto
- No hay persistencia de datos especificada

#### Mejoras Técnicas Sugeridas:
```markdown
### Tecnología de IA
- Usar Cloud Vision API (Google) O Tesseract OCR
- Modelo custom entrenado en recibos mexicanos (si presupuesto lo permite)
- Fallback a manual si confianza < 70%

### Flujo Técnico
1. Cliente: Captura foto (max 5MB, jpg/png)
2. Backend: Envía a IA service
3. IA: Retorna {monto, confianza%, categoría_propuesta}
4. Si confianza > 70%: mostrar confirmación
5. Si confianza < 70%: pedir manual

### Modelo de Datos
```sql
CREATE TABLE registros (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES usuarios(id),
  foto_url VARCHAR(255),
  monto DECIMAL(10,2),
  categoria ENUM('Antojo', 'Lo de siempre', 'Guardé'),
  confianza_ia FLOAT,
  confirmado_por_usuario BOOLEAN,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);
```

### API
POST /registros/clasificar
multipart/form-data
- foto: binary
Respuesta:
{
  "monto_propuesto": 150.00,
  "categoria": "Antojo",
  "confianza": 0.92,
  "requiere_confirmacion": false
}
```

---

### ✅ #3 REGISTRO EMOCIONAL
**Criticidad:** Media | **Complejidad:** Baja | **Riesgo:** Bajo

#### Deficiencias:
- Muy simple pero correcto
- Solo falta: ¿Cuáles son los emojis disponibles? (lista, número)
- ¿Se puede cambiar después? (edit)

#### Mejoras:
```markdown
### Emojis Disponibles (9 opciones)
😊 Bien | 😐 Neutral | 😢 Mal
😡 Enojado | 😰 Ansioso | 😌 Relajado
😍 Feliz | 🤔 Confundido | 😑 Indiferente

### Permite Edit?
Sí, hasta 1 hora después del registro.

### Modelo de Datos
ALTER TABLE registros ADD COLUMN emoji VARCHAR(2);
```

---

### ✅ #4 RECOMPENSA INMEDIATA
**Criticidad:** ALTA | **Complejidad:** Media | **Riesgo:** MEDIO

#### Deficiencias:
- "Techo semanal de tokens" — ¿Cuánto es? ¿50? ¿100? ¿1000?
- ¿Qué es una "racha"? ¿Días consecutivos sin faltar?
- ¿Se resetea a medianoche UTC o local del usuario?
- No especifica cómo se almacenan tokens (base de datos, blockchain, Stellar)
- ¿Qué pasa si alguien registra 100 veces en un día?

#### Mejoras:
```markdown
### Reglas de Recompensa
- 1 registro completo (foto + emoji) = 1 token
- Máximo 10 tokens/día
- Máximo 50 tokens/semana (lunes-domingo UTC)
- Bonus: Si registra 7 días consecutivos = +5 tokens

### Modelo de Datos
```sql
CREATE TABLE tokens (
  id UUID PRIMARY KEY,
  user_id UUID,
  cantidad INT,
  tipo ENUM('registro', 'leccion', 'bonus'),
  fecha_otorgado TIMESTAMP,
  semanal_count INT (resetearse cada lunes)
);

CREATE TABLE racha (
  user_id UUID PRIMARY KEY,
  dias_consecutivos INT,
  ultimo_registro_date DATE
);
```

### Lógica
```javascript
if (registro_completado) {
  if (tokens_hoy < 10 && tokens_semana < 50) {
    otorgar_token();
    incrementar_racha();
    if (racha == 7) otorgar_bonus_5_tokens();
  }
}
```

### API
POST /tokens/registrar-completado
{
  "registro_id": "uuid"
}
Respuesta:
{
  "tokens_otorgados": 1,
  "racha_actual": 3,
  "tokens_semana": 12,
  "tokens_max_semana": 50
}
```

---

### ✅ #5 APRENDIZAJE APLICADO
**Criticidad:** Media | **Complejidad:** Media | **Riesgo:** Bajo

#### Deficiencias:
- "Micro-lección relacionada con la categoría" — ¿Cómo se matchean? ¿Tabla predefinida?
- "Mini-cuestionario correctamente" — ¿Cuántas preguntas? ¿1, 3, 5?
- ¿Se puede saltear la lección? (obligatoria o opcional)
- No especifica dónde vive el contenido (CMS, base de datos, hardcoded)

#### Mejoras:
```markdown
### Mapeo Lección-Categoría
| Categoría | Lección |
|-----------|---------|
| Antojo | "Reconocer impulsos vs. necesidades" |
| Lo de siempre | "Hábitos saludables vs. gastos fijos" |
| Guardé | "Técnicas de ahorro efectivo" |

### Estructura de Lección
- Título
- Cuerpo (max 300 palabras)
- 3 preguntas de selección múltiple
- Tiempo estimado: 2 minutos
- Tokens si pasa (3/3 correctas)

### Modelo de Datos
```sql
CREATE TABLE lecciones (
  id UUID PRIMARY KEY,
  categoria VARCHAR(50),
  titulo VARCHAR(200),
  contenido TEXT,
  tiempo_estimado INT (segundos),
  created_at TIMESTAMP
);

CREATE TABLE lecciones_respuestas (
  id UUID PRIMARY KEY,
  usuario_id UUID,
  leccion_id UUID,
  respuestas_correctas INT,
  completada BOOLEAN,
  tokens_otorgados INT,
  fecha TIMESTAMP
);
```

### Flujo
1. Usuario completa registro
2. Sistema sugiere lección (si no la ha hecho esta semana)
3. Usuario lee (2 min)
4. Contesta 3 preguntas
5. Si 3/3 correctas → +3 tokens
6. Si < 3/3 correctas → puede reintentar
```

---

### ✅ #6 PRIMERA EXPERIENCIA DIGITAL (Stellar)
**Criticidad:** ALTA | **Complejidad:** ALTA | **Riesgo:** ALTO (blockchain)

#### Deficiencias:
- "Ver y mover tokens en Stellar Testnet" — ¿Cómo se crean las cuentas Stellar?
- ¿Quién paga las fees de Stellar?
- ¿Es custodial (app maneja keys) o no-custodial (usuario maneja keys)?
- No especifica cómo se transfieren tokens del sistema a Stellar
- "Sin pasos técnicos adicionales" — pero ¿cómo ve la dirección? ¿QR? ¿Oculta?
- Seguridad: ¿Dónde se guardan las claves privadas?

#### Mejoras:
```markdown
### Arquitectura Stellar
- Modelo CUSTODIAL: App maneja keys en backend (más simple, menos seguro)
- Una cuenta Stellar maestra por usuario
- Tokens custom: AmorProof (código de activo)
- Red: Stellar Testnet (desarrollo), mainnet en producción

### Flujo Técnico
1. Usuario crea cuenta en app (salva en DB)
2. Backend genera Stellar account (publica key guardada)
3. Backend genera y guarda secret key (encrypted en DB)
4. Usuario ve balance en UI (query Stellar API cada vez)
5. Usuario "mueve" tokens = backend firma + envía transacción Stellar

### Modelo de Datos
```sql
CREATE TABLE stellar_accounts (
  id UUID PRIMARY KEY,
  user_id UUID UNIQUE,
  public_key VARCHAR(56),
  private_key_encrypted TEXT (stored encrypted),
  created_at TIMESTAMP
);
```

### API
GET /mi-cuenta/saldo
Respuesta:
{
  "saldo": 42.5,
  "moneda": "AmorProof",
  "cuenta_publica": "GXXXXXX..." (últimos 8 caracteres)
}

POST /transferencia/enviar
{
  "monto": 10,
  "destinatario_email": "otro@example.com"
}
Respuesta:
{
  "transaccion_id": "uuid",
  "estado": "procesando",
  "verificada_en_stellar": false
}

### Consideraciones de Seguridad
- Private keys NUNCA se exponen al frontend
- Transacciones requieren 2FA (opcional pero recomendado)
- Límite de transferencia: max 100 tokens/día
- Logs de auditoría completos
```

---

### ✅ #7 VERIFICACIÓN DE INTEGRIDAD (Hash en Stellar)
**Criticidad:** ALTA | **Complejidad:** ALTA | **Riesgo:** ALTO

#### Deficiencias:
- "Hash del registro off-chain" — ¿Qué algoritmo? SHA256? ¿Qué campos hasheados?
- "Sin exponer el contenido original" — ¿Cómo verifica el usuario que coincide?
- No especifica cuándo se ancla (inmediato vs. batch diario)
- No menciona costo (Stellar cobra por transacciones)
- ¿Se puede verificar sin conocimiento técnico?

#### Mejoras:
```markdown
### Algoritmo de Hash
- SHA256(user_id + monto + categoria + emoji + timestamp)
- Resultado hexadecimal de 64 caracteres
- Guardado en Stellar Testnet Memo de transacción

### Modelo de Datos
```sql
CREATE TABLE registros_hashes (
  id UUID PRIMARY KEY,
  registro_id UUID,
  hash_sha256 VARCHAR(64),
  stellar_tx_id VARCHAR(64),
  stellar_verified BOOLEAN,
  anclado_en TIMESTAMP
);
```

### Flujo
1. Usuario completa registro (foto + emoji)
2. Backend calcula hash
3. Backend guarda hash en DB local
4. Backend envía hash a Stellar (batch cada 1 hora o inmediato si priority)
5. Stellar retorna transaction_id
6. Backend marca como verified
7. Usuario puede ver: "✓ Verificado en Stellar en [fecha]"

### UI de Verificación
- Mostrar solo: "Verificado ✓ [fecha]"
- Si hacen click: mostrar primeros 16 caracteres del hash
- NOT mostrar: hash completo, detalles técnicos

### Costo
- ~0.00001 XLM por transacción
- Aprox. $0.000002 USD
- Backend absorbe el costo (imperceptible)

### Consideraciones
- Batch processing para no saturar Stellar
- Retry logic si falla transacción
- Notificar al usuario cuando se verificó
```

---

### ✅ #8 REFLEXIÓN SEMANAL
**Criticidad:** Media | **Complejidad:** Media | **Riesgo:** Bajo

#### Deficiencias:
- **DUPLICADO:** Issue #8 y #7 tienen el mismo título (8️⃣ Reflexión semanal)
- "Categorías, momentos del día y emociones asociadas" — muy vago
- No especifica visualización (tabla, gráfico, cards)
- ¿Qué períodos muestra? (solo última semana o histórico)
- No menciona si es en tiempo real o calculated batch

#### Mejoras:
```markdown
### Datos del Resumen Semanal
**Período:** Lunes 00:00 UTC - Domingo 23:59 UTC

**Mostrar:**
1. **Por Categoría:**
   - Antojo: 8 registros ($120)
   - Lo de siempre: 12 registros ($480)
   - Guardé: 5 registros ($250)

2. **Por Momento del Día:**
   - Mañana (6-12): 5 registros
   - Tarde (12-18): 12 registros
   - Noche (18-24): 8 registros

3. **Por Emoción:**
   - 😊: 10 registros
   - 😢: 5 registros
   - 😰: 10 registros

4. **Resumen:**
   - Total gastado: $850
   - Total registros: 25
   - Racha: 5 días
   - Tokens ganados: 25

### Modelo de Datos
```sql
CREATE TABLE resumen_semanal (
  id UUID PRIMARY KEY,
  user_id UUID,
  fecha_inicio DATE,
  fecha_fin DATE,
  total_gasto DECIMAL(10,2),
  total_registros INT,
  datos_json JSON, -- almacenar breakdown por categoría, hora, emoji
  generado_at TIMESTAMP
);
```

### API
GET /resumen-semanal?semana=2026-W40
Respuesta:
{
  "semana": "2026-10-04 to 2026-10-10",
  "total_gasto": 850.00,
  "total_registros": 25,
  "por_categoria": {...},
  "por_hora": {...},
  "por_emocion": {...}
}

### UI
- Cards grandes con números
- Pequeño gráfico de barras (categorías)
- Heatmap de horas
- Nada de interpretación o recomendación
```

---

### ✅ #9 MEDICIÓN DE RECURRENCIA (Analytics)
**Criticidad:** ALTA | **Complejidad:** Media | **Riesgo:** Bajo

#### Deficiencias:
- "Activación (primer registro completado)" — ¿cuándo se cuenta? ¿con emoji o sin?
- "Retorno a 7, 14, 28 días" — ¿qué cuenta como "retorno"? ¿1 registro = retorno?
- No especifica dónde se guardan estos eventos (tabla específica, evento, log)
- No menciona cómo se reportan (dashboard, email, API)
- ¿Se incluyen datos de Elba en esta métrica o es interno del backend?

#### Mejoras:
```markdown
### Definiciones Claras

**Activación:** User completa su PRIMER registro con emoji
- Evento: user_signup → primer_registro_completado
- Fecha: timestamp del evento

**Retorno D7:** User registró algo entre día 7-8 (post-activación)
**Retorno D14:** User registró algo entre día 14-15
**Retorno D28:** User registró algo entre día 28-29

### Modelo de Datos
```sql
CREATE TABLE eventos_usuario (
  id UUID PRIMARY KEY,
  user_id UUID,
  evento_tipo ENUM('signup', 'primer_registro', 'retorno_d7', 'retorno_d14', 'retorno_d28', 'leccion_completada'),
  created_at TIMESTAMP
);

CREATE TABLE metricas_cohort (
  id UUID PRIMARY KEY,
  cohort_fecha DATE (fecha en que se activaron),
  total_usuarios INT,
  retorno_d7_count INT,
  retorno_d7_pct FLOAT,
  retorno_d14_count INT,
  retorno_d14_pct FLOAT,
  retorno_d28_count INT,
  retorno_d28_pct FLOAT,
  avg_registros_semana FLOAT,
  avg_lecciones_completadas FLOAT,
  calculado_at TIMESTAMP
);
```

### Métricas a Calcular (semanal/mensual)
- Activación diaria
- Retorno (D1, D7, D14, D28)
- DAU (Daily Active Users)
- Registros por usuario (promedio)
- Tasa de completación de lecciones
- Racha promedio
- Churn (usuarios que no vuelven en X días)

### API (solo interna/admin)
GET /admin/metricas/cohort?desde=2026-10-01&hasta=2026-10-31
GET /admin/metricas/retorno?dias=7
GET /admin/metricas/usuarios/activos?periodo=semana

### Dashboard (Elba/Adriana)
- Gráfico de retención (curva típica)
- KPIs principales (DAU, activación, racha promedio)
- Tabla de cohortes
- Alertas si caen métricas > 10%
```

---

## 📊 RESUMEN DE DEFICIENCIAS

| Issue | Deficiencia Principal | Severidad | Acción |
|-------|------------------------|-----------|--------|
| #1 | Campos no especificados | Media | Agregar validaciones |
| #2 | IA sin definir | ALTA | Elegir modelo, specs |
| #3 | Básicamente OK | Baja | Listar emojis |
| #4 | Techo y racha sin números | ALTA | Definir límites |
| #5 | Contenido no centralizado | Media | Crear tabla de lecciones |
| #6 | Seguridad Stellar no clara | ALTA | Definir custodial/no-custodial |
| #7 | Costo y flujo de verificación | ALTA | Especificar hashing + batching |
| #8 | DUPLICADO + vago | ALTA | Eliminar duplicado, especificar vizs |
| #9 | Eventos no definidos | ALTA | Definir activación, retorno |

---

## 🎯 PRIORIDAD DE CLARIFICACIÓN (antes de implementar)

**CRÍTICO (esta semana):**
1. #2 — Elegir modelo IA
2. #4 — Definir límites de tokens/racha
3. #6 — Arquitectura Stellar (custodial vs no-custodial)
4. #7 — Flujo de hashing y costo
5. #8 — Eliminar duplicado, visualización clara
6. #9 — Definiciones de eventos

**IMPORTANTE (próxima semana):**
7. #1 — Validaciones y campos
8. #5 — Estructura de lecciones
9. #3 — Listar emojis (puede ser último)

---

## ✅ CONCLUSIÓN

**Calidad general:** 6/10

**Lo que está bien:**
- Historias de usuario claras (negocio)
- Criterios de aceptación en formato BDD (Dado/Cuando/Entonces)
- Asignaciones de responsables claras

**Lo que falta:**
- **Detalles técnicos:** Modelos de datos, APIs, algoritmos
- **Ambigüedades:** Límites numéricos, flujos exactos
- **Seguridad:** Especialmente en #6 y #7
- **Dependencias:** No está claro el orden de implementación

**Recomendación:** Antes de comenzar código (Semana 4), necesitas **refinement meeting** con Adriana para aclarar estos puntos. Son 2-3 horas que ahorran 20+ horas de desarrollo.

---

**Preparado por:** Anthony López  
**Para:** Full Stack Review  
**Próximo paso:** Meetings de refinement antes de Semana 4
