# ABVC API v1 — Contrato de interfaz

> Nota de doctrina: el stack de Gemini (FastAPI/Pydantic/PostgreSQL) NO es nuestra implementación. Nuestro core corre en Base44 (entidades + funciones). Este documento es el CONTRATO CANÓNICO: cualquier frontend (app de Google AI Studio, TV, móvil) habla este idioma; la implementación detrás puede cambiar sin romper nada.

## Mapeo a nuestro stack actual

| Contrato ABVC | Nuestra implementación hoy |
|---|---|
| LearnerProfile | Entidad `StudentProfile` (Base44) + expediente localStorage |
| AttemptEvent ingestion | Entidades `QuizResponse` / `PracticeSession` (Base44) + error-ledger |
| Router /evaluate | Función del Maestro v0 (reglas JSON, determinístico) |
| Router /override | La Maestra JJ pisa la ruta; se registra en la Mission |
| ToolRegistry | `tools/registry.json` (este repo) |

## 1. Learner Profile API

### GET /api/v1/profiles/{student_id}
Devuelve el expediente completo: `cefr_aggregate`, ramas (score + confidence por rama y subskill), macro_skills (listening, speaking_production, intelligibility, fluency_wpm).

### PATCH /api/v1/profiles/{student_id}
Actualización manual o por servicio (teacher override de scores).

### POST /api/v1/profiles/{student_id}/events
Ingesta un AttemptEvent / ErrorEvent. El servicio actualiza subskills y RECALCULA confidence. Respuesta:

```json
{
  "status": "ACCEPTED",
  "student_id": "usr_98f23a11",
  "updated_skills": [
    { "skill_path": "phonology.linking_connected_speech", "new_score": 0.31, "new_confidence": 0.82 }
  ],
  "recompute_triggered": true
}
```

## 2. Routing Engine (ARE) API

### POST /api/v1/router/evaluate
Entrada: `student_id`, `force_recalculate`, `context` (`session_type`, `hardware_target`, `max_duration_minutes`).
Salida: una **Mission** (ver `contracts/mission.schema.json`) — con `primary_target_skill`, `secondary_target_skill`, `estimated_duration_minutes` y el `pipeline` de pasos (tool_id, mode, target_configuration con difficulty, completion_criteria).

### POST /api/v1/router/override
La Maestra JJ pisa la ruta: `teacher_id`, `override_reason`, `pipeline_override`. El sistema responde `OVERRIDE_ACTIVE` con `active_until`. El rendimiento bajo override SE SIGUE REGISTRANDO (así el sistema aprende de la decisión humana).

### GET /api/v1/router/tools
Devuelve las herramientas registradas que el router puede descubrir.
