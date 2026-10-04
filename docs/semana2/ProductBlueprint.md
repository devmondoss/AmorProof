# Product Blueprint

**Nombre del proyecto:** Do-Own

**Repositorio (enlace obligatorio):** [Do-Own](https://github.com/devmondoss/AmorProof)

---

## Contenido

1. Priorización de historias
2. Propuesta de valor
3. Flujo de usuario
4. Alcance del MVP
5. Lean Canvas
6. Backlog priorizado (Kanban)
7. Arquitectura inicial
8. Uso de Stellar y justificación

---

## 1. Priorización de historias

**Criterio de priorización:** Impacto en validación del ciclo central (Observar → Aprender → Recibir → Poseer)

| Prioridad | Historia | Propuesta por | Por qué entra al backlog |
| :---: | --- | :---: | --- |
| 1 | Como persona con estrés financiero, quiero registrar una decisión de gasto con una foto, para que la app la clasifique sin que tenga que escribir nada. | Adriana | Sin observación de decisiones, no hay ciclo. Es la puerta de entrada. |
| 2 | Como persona con estrés financiero, quiero recibir tokens al completar un registro, para tener una razón tangible que me ayude a sostener el hábito. | Rodrigo | Sin recompensa inmediata, no hay motivación para repetir. Valida retención. |
| 3 | Como persona con estrés financiero, quiero ver y mover mis tokens en mi cuenta de Stellar, para tener mi primer activo digital sin necesitar conocimiento técnico previo. | Anthony | Es el diferenciador: recompensa digital → propiedad real. Valida cripto sin barrera. |
| 4 | Como persona nueva, quiero completar un registro breve y entender el propósito de la app, para empezar sin dar información financiera sensible de entrada. | Adriana | Sin onboarding claro, no hay activación. Esencial para entrada. |
| 5 | Como persona con estrés financiero, quiero asociar un emoji a mi registro, para capturar cómo me sentí en ese momento. | Adriana | Conecta decisión financiera con emoción. Requisito para "aprender". |
| 6 | Como persona con estrés financiero, quiero ver un resumen de mis registros de la semana, para observar mi patrón sin que la app me diga qué hacer. | Adriana | Cierra el ciclo: observar nuevamente. Valida identificación de patrones. |
| 7 | Como persona con estrés financiero, quiero completar una micro-lección relacionada con lo que registré, para aprender un concepto aplicado a mi situación. | Rodrigo | Valida si aprendizaje + recompensa sostienen hábito. Importante pero puede ser después. |
| 8 | Como persona con estrés financiero, quiero confiar en que mi registro no fue alterado, para que el patrón que observo sea honesto. | Anthony | Justificación blockchain. Valida diferenciador técnico, pero secundario en Fase 1. |
| 9 | Como equipo de producto, quiero medir activación, frecuencia y retorno, para validar si el ciclo realmente genera un hábito sostenido. | Anthony | Essential para análisis post-lanzamiento. Métricas internas. |

---

## 2. Propuesta de valor

**Usuario (del Problem Brief):** Adulto de 25–35 años, económicamente activo, con estrés financiero recurrente que sabe qué debería cambiar en sus hábitos de gasto pero no logra sostenerlo.

**Resultado que obtiene:** Observa sus decisiones financieras en tiempo real, aprende por qué las toma y recibe una recompensa digital tangible que convierte el aprendizaje en su primer activo digital real.

**Por qué elegiría esta solución:** Porque no es un curso abstracto (sigue siendo teórico), ni una app de presupuesto (solo registra datos), ni una promesa cripto lejana (está aquí, ahora). Es su propia vida financiera convertida en una experiencia práctica que paga desde el primer día.

**En qué se diferencia de cómo lo resuelve hoy:** 

Hoy: Prueba apps de presupuesto (solo registra), cursos de finanzas (solo teoría) o promesas cripto (no entiende). Cada herramienta es un silo. No hay conexión entre aprender y hacer. No hay recompensa.

Do-Own: Registra → Aprende → Actúa → Recibe → Posee. Todo en una sola experiencia. Aprendizaje que paga desde el primer registro.

---

## 3. Flujo de usuario

| Paso | Rol | Qué hace | Punto de interacción |
| :---: | :---: | --- | --- |
| 1 | Persona nueva | Abre la app, registra email/contraseña, ve explicación del propósito | Pantalla de onboarding |
| 2 | Persona con gasto | Toma foto de un gasto, confirma monto y categoría propuestos por IA | Pantalla de registro financiero |
| 3 | Persona reflexiva | Asocia un emoji a cómo se sintió con esa decisión | Pantalla de registro emocional |
| 4 | Persona activa | Recibe 1 token, ve progreso y racha actualizada | Pantalla de confirmación + saldo |
| 5 | Persona que aprende | Accede a micro-lección relacionada, responde cuestionario, gana 3 tokens | Pantalla de lección |
| 6 | Persona que acumula | Al alcanzar 50 tokens, visualiza y transfiere sus activos en Stellar | Pantalla de "Mis activos" (Stellar) |
| 7 | Persona reflexiva | Al finalizar la semana, ve resumen de categorías, momentos y emociones | Pantalla de "Reflexión semanal" |
| 8 | Persona retenida | Decide continuar o pausar. Sus datos, progreso y activos permanecen | Pantalla de "Semana siguiente" |

---

## 4. Alcance del MVP

| Dentro del MVP (funcionalidad central) | Fuera del MVP (deseable, para después) |
| --- | --- |
| Onboarding básico (email, contraseña, explicación) | Recomendaciones personalizadas |
| Registro financiero con foto + IA | Metas automáticas de ahorro |
| Registro emocional (emoji) | Interpretación avanzada de patrones |
| Tokens: recibir, visualizar, racha | Fondos compartidos |
| Micro-lecciones + cuestionario | Staking / Pools de inversión |
| Stellar: balance y transferencias | Funcionalidades B2B |
| Reflexión semanal (datos, no interpretación) | Administración de fondos de terceros |
| Hash inalterable de registros | Trading / Mercados |
| Medición de activación, retención, retorno | Recomendaciones de ahorro |

**Por qué el recorte sigue entregando valor:** El MVP valida el ciclo central (Observar → Aprender → Recibir → Poseer) sin necesidad de predicciones, recomendaciones o funcionalidades avanzadas. Responde la pregunta crítica: ¿Quieren las personas observar su comportamiento, aprender de él, recibir recompensa digital y volver a repetir? Si la respuesta es sí, todo lo demás es escalado. Si es no, las funcionalidades adicionales no importan.

---

## 5. Lean Canvas

**Enlace al Lean Canvas (obligatorio):** [Lean Canvas del proyecto](https://github.com/devmondoss/AmorProof/blob/main/docs/semana2/LeanCanvass2.md)

| Sección | Contenido |
|---------|-----------|
| **Problema** | • Repite patrones financieros sin identificar qué los dispara<br>• La educación financiera no se traduce en acción<br>• Entrar a cripto tiene barrera técnica |
| **Segmento** | Adultos 25–49 años, económicamente activos, estrés financiero recurrente. Early adopters: digitales y curiosos por cripto. |
| **Propuesta Única** | **Do-Own: Convierte el aprendizaje financiero en tu primer activo digital.** |
| **Solución** | Registro foto + emoji → Micro-lecciones → Tokens → Stellar (propiedad real) |
| **Canales** | Creadores fintech, comunidades Web3, programas innovación, Escuela Amor Propio, referidos |
| **Métricas** | Activación (primer registro), Retención (D7/D14/D28), Registros/semana, Lecciones completadas, % que accede a Stellar |
| **Ventaja** | Comportamiento financiero + aprendizaje aplicado + recompensa digital tangible = propiedad real |
| **Costos** | Desarrollo, IA, Stellar, contenido educativo, seguridad, adquisición usuarios |
| **Ingresos** | Freemium (MVP gratuito) → Premium (futuro), B2B (empresas), licencias |

---

## 6. Backlog priorizado (Kanban)

**Enlace al tablero (obligatorio):** [Backlog Semana 2 - Do-Own](https://github.com/devmondoss/AmorProof/projects/1)

El tablero contiene las 9 historias priorizadas, organizadas en columnas (Backlog, Ready, In progress, In review, Done) con criterios de aceptación por tarjeta, asignaciones y labels técnicos.

---

## 7. Arquitectura inicial

**Capa 1: Interfaz (Frontend)**
- Pantallas: Onboarding, Registro financiero, Registro emocional, Confirmación, Micro-lección, Mis activos, Reflexión semanal
- Interacción con usuario

**Capa 2: Lógica (Backend)**
- Autenticación y gestión de usuarios
- Clasificación de fotos (IA)
- Motor de recompensas (tokens, racha)
- Motor de aprendizaje (matcheo lecciones)
- Cálculo de hashes

**Capa 3: Datos Off-Chain (Base de datos)**
- Información financiera y emocional
- Fotografías
- Historial de registros
- Contenido educativo
- Progreso del usuario (tokens locales, racha)

**Capa 4: Stellar (Blockchain)**
- Cuenta usuario
- Activo digital (Do-Own token)
- Balance
- Transferencias
- Hashes verificables

**Regla arquitectónica:** "La aplicación guarda la experiencia; Stellar verifica y materializa la propiedad digital."

**En qué punto entra la red:** Stellar entra SOLO cuando hay necesidad de propiedad (crear cuenta, recibir tokens), transferencia (enviar tokens) o verificabilidad (anclar hash de integridad). El resto vive off-chain. Esto mantiene privacidad, velocidad y costo bajo.

---

## 8. Uso de Stellar y justificación

**Criterio de pertinencia (del Problem Brief):** "El histórico no puede alterarse." Aplicado aquí: el usuario debe poder confiar en que su recompensa es real, transferible y no alterada por nadie (ni la app, ni él mismo en un momento de duda).

| Componente de Stellar | Para qué lo usamos | Por qué ese y no otra alternativa |
| --- | --- | --- |
| Cuenta Stellar (keypair) | Propiedad real del usuario sobre sus activos | Ethereum requiere gas alto. Stellar es más simple y barato (~$0.000002 USD/tx). |
| Activo custom (Do-Own) | Emitir tokens como recompensa real | Bitcoin no permite activos custom. Stellar sí, diseñado para esto. |
| Transacciones | Transferir tokens entre usuarios | Validar que la transacción es real y verificable. |
| Memo (transacciones) | Anclar hash SHA256 de registros | Comprobar después que un registro no fue alterado sin revelar contenido. |

**Por qué Stellar específicamente:** Porque resuelve la necesidad exacta del producto (propiedad digital + transferencia + verificabilidad) sin requerir del usuario entender blockchain, sin costos prohibitivos y sin sacrificar privacidad (los datos sensibles permanecen off-chain).

---

**Fecha:** 2026-10-04  
**Estado:** Listo para entregar
