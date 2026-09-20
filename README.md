# ABVC — AccentBridges Virtual Classroom (Core)

El sistema nervioso central del ecosistema **Myl AccentBridges**. Este repo es el **laboratorio de contratos y ruteo**: esquemas de datos, registro de herramientas y reglas del router determinístico.

> Regla de oro: **el router decide con MATEMÁTICA sobre datos. El LLM narra, jamás decide.**

## Qué vive aquí (y qué no)

| Capa | Qué es | Dónde corre |
|---|---|---|
| Contratos de datos | Schemas JSON (perfil, herramientas, misiones, eventos) | Aquí (fuente de verdad) |
| Tool Registry | Fichas técnicas de cada herramienta del ecosistema | `tools/registry.json` |
| Router v0 | Reglas determinísticas (umbrales, prioridades) | `router/` |
| Piloto Culiacán | Trainer, assessments, bot, voz, episodios | **Base44 + GitHub Pages (NO se toca)** |

Este repo se despliega como app experimental en **Google AI Studio** para expandir ideas sin arriesgar el piloto que corre en Culiacán.

## El loop ABVC

```
DIAGNOSE → BUILD PROFILE → ROUTE → PRACTICE → MEASURE → ADAPT ↺
```

El perfil es **multidimensional** (5 ramas lingüísticas + macro-skills), CEFR es el mapa, no el camino. Cada skill tiene `score` (0–1) y `confidence` (0–1) que crece con cada dato capturado.

## Contratos (v0)

1. `contracts/learner-profile.schema.json` — expediente del estudiante (5 ramas, subskills, macro skills)
2. `contracts/tool-manifest.schema.json` — ficha técnica de una herramienta
3. `contracts/mission.schema.json` — la dosis: SECUENCIA de pasos con criterios de terminación
4. `contracts/attempt-event.schema.json` — telemetría que regresa de cada intento

## Herramientas registradas (el ecosistema real)

Trainer (fundación A0-A1), Level Assessment, Personality Assessment, AR Labeler, Vapi /call, Telegram Group, YouTube, TikTok, AMERICA (PronounceAI, A2m-B1a), PALACE (PronunLab, B1a-B2b), PANEL (dashboard), SOUNDMAP (40 lecciones + duelos), Valerie 1 (Botpress, presentadora).

Ver `tools/registry.json` — cada puerta con rama, skills, rango CEFR, mic, TV.

## Desplegar en Google AI Studio

1. Abre https://aistudio.google.com → **Build**
2. Importa este repo de GitHub (授权: `babayaba71-maker/abvc-core`)
3. El router lee los contratos y el registry; la UI narra decisiones (LLM), nunca las toma.

## Doctrinas selladas (no negociables)

- Bilingual Bridge: instrucción en español, práctica en inglés (100% español A0/A1)
- Morfología antes que gramática (la gramática nombra el edificio ya construido)
- Score Formativo: el motor es gimnasio, nunca certificación
- Filtro afectivo primero (Krashen): el bloqueo se quita antes del músculo
- Piloto ~$0: la cartera de JJ no financia experimentos
