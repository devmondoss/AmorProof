# 🎯 Workflow AmorProof — Guía Oficial

## Regla de Oro
**TODO va en GitHub.** Punto final.

- Google Docs = borrador temporal SOLAMENTE
- GitHub = fuente de verdad
- Cambios al problema, historias, decisiones: acá

---

## 📁 Estructura de Carpetas

```
docs/
├── semana1/
│   └── ProblemBrief.md          ← versión actual, única fuente de verdad
├── semana2/
│   ├── AdrianaLhada.md          ← historias de usuario
│   ├── AnthonyLopez.md          ← historias de usuario
│   ├── Rodrigo.md               ← historias de usuario (ACTUALIZAR a v2)
│   ├── Nayeli.md                ← historias de usuario (por hacer)
│   └── Elba.md                  ← historias de usuario (por hacer)
├── semana3/
│   └── LeanCanvas.md            ← (por hacer)
└── ...

.github/projects/
├── MVP Backlog                  ← 8 tarjetas del backlog en Issues
└── Tracking por semana
```

---

## 📝 Cómo Contribuir

### 1. Cambios al Problem Brief
- Edita `/docs/semana1/ProblemBrief.md` directo en GitHub
- Haz commit con mensaje claro: `Update ProblemBrief: [qué cambió]`
- **NO copies a Google Docs después** — GitHub es la versión oficial

### 2. Historias de Usuario (Semana 2)
**Archivo:** `docs/semana2/TuNombre.md`

**Formato:**
```markdown
## Mis historias de usuario

[5-7 historias]

1. Como [rol], quiero [acción], para [beneficio].
```

**Criterios (según Adriana):**
- ✅ Se entiende sin explicación — nadie necesita que te la aclares
- ✅ Un verbo y un rol por paso — una acción, un rol, no mezcles
- ✅ Sin palabras técnicas — nada de "blockchain", "base de datos", "backend", etc.
- ✅ Solo el camino principal — flujo normal, no casos raros

**Base:** Todas las historias deben estar alineadas con el Problem Brief actual (v2 - estrés financiero)

### 3. MVP Backlog (Tarjetas)
Están en **GitHub Issues** con labels:
- `backlog` — por hacer
- `in-progress` — en desarrollo
- `done` — completado
- Label de asignado (tu nombre)

No muevas tarjetas a Google Docs. El estado real está acá.

### 4. Lean Canvas (Semana 3)
**Archivo:** `docs/semana3/LeanCanvas.md` o `docs/semana3/LeanCanvas.png`

Si lo haces en Canva:
1. Crea el canvas en Canva
2. Exporta como PNG
3. Súbelo a la carpeta `docs/semana3/`
4. Linkea en el repo

---

## 🔄 Flujo de Cambios

```
1. Alguien propone un cambio (en Discord)
   ↓
2. Se hace en GitHub (Edit/Commit)
   ↓
3. Se anuncia en Discord: "Actualizado [archivo]"
   ↓
4. NO hay Google Docs después
```

---

## 📌 Responsables por Área

| Área | Responsable |
|------|------------|
| Problem Brief v2 | Adriana |
| Historias de usuario | Cada quien su archivo |
| MVP Backlog (Issues) | Anthony (crear) + Todo el equipo (trabajar) |
| Lean Canvas | Nayeli |
| Coordinación repo | Anthony |

---

## ❌ Qué NO Hacer

- Documentar en Google Docs y esperar que alguien lo copie
- Cambiar el Problem Brief en Google Docs sin actualizar el repo
- Dejar historias de usuario desactualizadas respecto al Problem Brief
- Crear tarjetas en Google Sheets en lugar de Issues

---

## ✅ Checklist para cada Entrega

- [ ] Todo está en GitHub (no en Google Docs)
- [ ] Las historias de usuario siguen los criterios
- [ ] Están alineadas con el Problem Brief actual
- [ ] No hay repeticiones entre las historias del equipo
- [ ] Cada tarjeta del backlog tiene descripción clara (criterios de aceptación)

---

## 🚀 Próximos Pasos

1. **Hoy:** Migrar v2 del Google Docs a ProblemBrief.md
2. **Hoy:** Actualizar historias de Rodrigo a v2
3. **Mañana:** Crear las 8 tarjetas del MVP como Issues
4. **Mañana:** Nayeli hace Lean Canvas
5. **Semana 3:** Continuar con prototipado

---

**Preguntas?** Abre un Issue o comenta en Discord, pero documenta todo acá después.
