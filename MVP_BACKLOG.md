# 🎯 MVP Backlog — 8 Tarjetas

Copia cada una a **GitHub Issues** → New Issue

---

## 1. Onboarding — Registro básico sin datos sensibles

**Rol:** Frontend  
**Asignado a:** @rodyxdev  
**Labels:** `backlog` `mvp` `frontend`

**Historia de usuario:**
Como persona nueva, quiero completar un registro breve y entender el propósito de la app, para empezar sin dar información financiera sensible de entrada.

**Criterios de aceptación:**
- [ ] La persona abre la app por primera vez
- [ ] Se le presenta un formulario breve (nombre, email, contraseña)
- [ ] NO se pide información financiera en esta etapa
- [ ] Después del registro, accede a la experiencia principal
- [ ] Se muestra un breve tutorial del propósito de la app

---

## 2. Registro financiero (foto + clasificación IA)

**Rol:** Backend/IA  
**Asignado a:** @devmondoss  
**Labels:** `backlog` `mvp` `backend` `ia`

**Historia de usuario:**
Como persona con estrés financiero, quiero registrar una decisión de gasto con una foto, para que la app la clasifique sin que tenga que escribir nada.

**Criterios de aceptación:**
- [ ] La persona puede tomar una foto de un gasto (recibo, ticket, etc.)
- [ ] La IA analiza la foto y propone: monto, categoría (Antojo / Lo de siempre / Guardé)
- [ ] La persona puede confirmar o ajustar los datos propuestos en un toque
- [ ] El registro se guarda con esta información

---

## 3. Registro emocional — Emoji asociado

**Rol:** Frontend  
**Asignado a:** @rodyxdev  
**Labels:** `backlog` `mvp` `frontend`

**Historia de usuario:**
Como persona con estrés financiero, quiero asociar un emoji a mi registro, para capturar cómo me sentí en ese momento.

**Criterios de aceptación:**
- [ ] Después de confirmar el registro financiero, se presenta una selección de emojis
- [ ] La persona puede elegir el que represente su emoción
- [ ] El emoji se asocia al registro financiero
- [ ] El registro queda completo con esta información

---

## 4. Recompensa inmediata — Tokens + racha

**Rol:** Backend  
**Asignado a:** @nayelicz  
**Labels:** `backlog` `mvp` `backend` `gamification`

**Historia de usuario:**
Como persona con estrés financiero, quiero recibir tokens al completar un registro, para tener una razón tangible que me ayude a sostener el hábito.

**Criterios de aceptación:**
- [ ] Un registro fue completado (financiero + emocional)
- [ ] El sistema otorga tokens de inmediato
- [ ] Se actualiza la racha visible en pantalla
- [ ] La persona ve la confirmación de tokens recibidos

---

## 5. Aprendizaje aplicado — Micro-lección + cuestionario

**Rol:** Backend + Contenido  
**Asignado a:** @nayelicz @elba333  
**Labels:** `backlog` `mvp` `backend` `content`

**Historia de usuario:**
Como persona con estrés financiero, quiero completar una micro-lección relacionada con lo que registré, para aprender un concepto aplicado a mi situación.

**Criterios de aceptación:**
- [ ] La persona completó un registro
- [ ] Se le ofrece una micro-lección relacionada con la categoría del gasto
- [ ] Puede leer la lección (formato breve, 2-3 minutos)
- [ ] Resuelve un mini-cuestionario al final
- [ ] Al aprobar, recibe tokens adicionales

---

## 6. Primera experiencia digital — Ver y mover tokens en Stellar

**Rol:** Frontend + Integración  
**Asignado a:** @devmondoss  
**Labels:** `backlog` `mvp` `frontend` `stellar` `blockchain`

**Historia de usuario:**
Como persona con estrés financiero, quiero ver y mover mis tokens en mi cuenta de Stellar, para tener mi primer activo digital sin necesitar conocimiento técnico previo.

**Criterios de aceptación:**
- [ ] La persona acumuló tokens suficientes
- [ ] Accede a la sección 'Mis activos'
- [ ] Ve su balance en Stellar Testnet (sin exponer complejidad técnica)
- [ ] Puede mover sus tokens en un entorno controlado
- [ ] No hay pasos técnicos adicionales (dirección, keys, etc. ocultos)

---

## 7. Verificación de integridad — Hash anclado

**Rol:** Arquitectura  
**Asignado a:** @devmondoss  
**Labels:** `backlog` `mvp` `architecture` `blockchain` `security`

**Historia de usuario:**
Como persona con estrés financiero, quiero confiar en que mi registro no fue alterado, para que el patrón que observo sea honesto.

**Criterios de aceptación:**
- [ ] Un registro fue guardado
- [ ] El sistema genera un hash del registro off-chain
- [ ] El hash se ancla en Stellar (sin exponer el contenido original)
- [ ] La persona puede verificar que su registro no fue modificado
- [ ] El contenido sensible permanece privado (no en la blockchain)

---

## 8. Reflexión semanal — Resumen de patrones

**Rol:** Backend + Frontend  
**Asignado a:** @nayelicz @rodyxdev  
**Labels:** `backlog` `mvp` `backend` `frontend` `analytics`

**Historia de usuario:**
Como persona con estrés financiero, quiero ver un resumen de mis registros de la semana, para observar mi patrón sin que la app me diga qué hacer.

**Criterios de aceptación:**
- [ ] Terminó una semana de registros
- [ ] La persona abre el resumen semanal
- [ ] Ve categorías de gasto más frecuentes
- [ ] Ve momentos del día en que más gastó
- [ ] Ve emociones asociadas a cada tipo de gasto
- [ ] NO hay interpretación ni recomendación (solo datos)

---

## 📌 Cómo crear estos Issues en GitHub

1. Ve a [Repositorio → Issues](https://github.com/devmondoss/AmorProof/issues)
2. Click en **New Issue**
3. Copia el título, descripción y labels de arriba
4. **Asigna a la persona** mencionada
5. Repite para cada una

---

**Creado por:** Anthony López (@devmondoss)  
**Fecha:** 2026-10-04  
**Basado en:** Problem Brief v2 + Propuesta de MVP de Adriana
