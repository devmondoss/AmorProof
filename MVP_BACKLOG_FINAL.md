# 🎯 MVP Backlog — 9 Tarjetas Finales

**Versión Final de Adriana** — Copia estas 9 tarjetas a GitHub Issues

---

## 1️⃣ Onboarding

**Assignee:** @rodyxdev  
**Labels:** `backlog` `mvp` `frontend`

### Historia de usuario
Como persona nueva, quiero completar un registro breve y entender el propósito de la app, para empezar sin dar información financiera sensible de entrada.

### Criterios de aceptación
- [ ] Dado que la persona abre la app por primera vez, cuando completa el registro básico, entonces accede a la experiencia sin que se le pida ningún dato financiero sensible.
- [ ] El registro básico toma menos de 1 minuto en completarse.

---

## 2️⃣ Registro financiero

**Assignee:** @devmondoss  
**Labels:** `backlog` `mvp` `backend` `ia`

### Historia de usuario
Como persona con estrés financiero, quiero registrar una decisión de gasto con una foto, para que la app la clasifique sin que tenga que escribir nada.

### Criterios de aceptación
- [ ] Dado que la persona toma una foto de un gasto, cuando la sube, entonces la IA propone monto y categoría (Antojo / Lo de siempre / Guardé).
- [ ] La persona puede confirmar o ajustar la categoría y el monto en un toque.
- [ ] El registro queda guardado con fecha y hora automáticas.

---

## 3️⃣ Registro emocional

**Assignee:** @rodyxdev  
**Labels:** `backlog` `mvp` `frontend`

### Historia de usuario
Como persona con estrés financiero, quiero asociar un emoji a mi registro, para capturar cómo me sentí en ese momento.

### Criterios de aceptación
- [ ] Dado que la persona terminó de confirmar su registro financiero, cuando se le presenta la selección de emojis, entonces puede elegir uno en un solo toque.
- [ ] El registro queda incompleto hasta que se asocia un emoji.

---

## 4️⃣ Recompensa inmediata

**Assignee:** @nayelicz  
**Labels:** `backlog` `mvp` `backend` `gamification`

### Historia de usuario
Como persona con estrés financiero, quiero recibir tokens al completar un registro, para tener una razón tangible que me ayude a sostener el hábito.

### Criterios de aceptación
- [ ] Dado que un registro fue completado (financiero + emocional), cuando se guarda, entonces el sistema otorga tokens de inmediato.
- [ ] La racha de días consecutivos se actualiza y es visible en pantalla justo después del registro.
- [ ] Existe un techo semanal de tokens para evitar acumulación artificial.

---

## 5️⃣ Aprendizaje aplicado

**Assignee:** @nayelicz @elba333  
**Labels:** `backlog` `mvp` `backend` `content`

### Historia de usuario
Como persona con estrés financiero, quiero completar una micro-lección relacionada con lo que registré, para aprender un concepto aplicado a mi situación.

### Criterios de aceptación
- [ ] Dado que la persona completó un registro, cuando se le ofrece una micro-lección relacionada, entonces puede leerla en menos de 2 minutos.
- [ ] Al resolver el mini-cuestionario correctamente, el sistema otorga tokens adicionales.
- [ ] El contenido de la lección se relaciona con la categoría del registro.

---

## 6️⃣ Primera experiencia digital

**Assignee:** @devmondoss  
**Labels:** `backlog` `mvp` `frontend` `stellar` `blockchain`

### Historia de usuario
Como persona con estrés financiero, quiero ver y mover mis tokens en mi cuenta de Stellar, para tener mi primer activo digital sin necesitar conocimiento técnico previo.

### Criterios de aceptación
- [ ] Dado que la persona acumuló tokens suficientes, cuando accede a "mis activos", entonces ve su balance en Stellar Testnet.
- [ ] Puede mover sus tokens en un entorno controlado, sin pasos técnicos adicionales.

---

## 7️⃣ Verificación de integridad

**Assignee:** @devmondoss  
**Labels:** `backlog` `mvp` `architecture` `blockchain` `security`

### Historia de usuario
Como persona con estrés financiero, quiero confiar en que mi registro no fue alterado, para que el patrón que observo sea honesto.

### Criterios de aceptación
- [ ] Dado que un registro fue guardado, cuando el sistema lo requiere, entonces genera un hash del registro off-chain.
- [ ] El hash se ancla en Stellar sin exponer el contenido original del registro en la red.
- [ ] La persona puede verificar que su registro coincide con lo anclado.

---

## 8️⃣ Reflexión semanal

**Assignee:** @nayelicz @rodyxdev  
**Labels:** `backlog` `mvp` `backend` `frontend` `analytics`

### Historia de usuario
Como persona con estrés financiero, quiero ver un resumen de mis registros de la semana, para observar mi patrón sin que la app me diga qué hacer.

### Criterios de aceptación
- [ ] Dado que terminó una semana de registros, cuando la persona abre el resumen, entonces ve categorías, momentos del día y emociones asociadas.
- [ ] El resumen no incluye interpretación, diagnóstico ni recomendación alguna.

---

## 9️⃣ Medición de recurrencia

**Assignee:** @elba333 @nayelicz  
**Labels:** `backlog` `mvp` `analytics` `product`

### Historia de usuario
Como equipo de producto, quiero medir activación, frecuencia y retorno, para validar si el ciclo realmente genera un hábito sostenido.

### Criterios de aceptación
- [ ] El sistema registra activación (primer registro completado).
- [ ] El sistema registra retorno a 7, 14 y 28 días.
- [ ] El sistema registra registros por semana y micro-lecciones completadas por usuario.

---

## 🚀 Cómo Crear los Issues

### Opción 1: Manual (Recomendado si no tienes API access)
1. Ve a [GitHub Issues](https://github.com/devmondoss/AmorProof/issues)
2. Click **New Issue**
3. Copia título (ej: "1️⃣ Onboarding")
4. Copia descripción (Historia + Criterios)
5. Asigna a las personas mencionadas
6. Agrega los labels
7. Click Create

### Opción 2: Bulk (Si tienes gh CLI)
```bash
gh issue create --title "1️⃣ Onboarding" --body "[contenido]" --assignee rodyxdev --label backlog,mvp,frontend
```

---

**Versión:** Final (Semana 2)  
**Actualizado:** 2026-10-04  
**Base:** Problem Brief v2 + MVP Definition
