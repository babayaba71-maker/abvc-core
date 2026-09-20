# Router v0 — Determinístico (0 LLM para decidir)

**Regla de oro: el router decide con MATEMÁTICA sobre datos. El LLM narra el mensaje cálido, JAMÁS decide el destino.**

## Orden de decisión (la persona antes que el pronóstico)

1. ¿Sin personality? → Personality Assessment. Siempre primero.
2. ¿Sin level? → Level Assessment.
3. Ambos → construir la dosis:

## Reglas de dosis v0

```
IF dominant_channel == "oido"  → dosis entra por audio (Trainer ?tab=realvowels, SoundMap listening)
IF dominant_channel == "ojo"   → dosis entra visual (Trainer ?tab=vowels, AR Labeler, video)
IF dominant_channel == "boca"  → dosis entra producción (Trainer ?tab=warmup, twisters, /call)

IF modo_hugo → observación vicaria primero (video, demo) ANTES de exigir producción

IF error_ledger.top_pattern == T-floja        → pestaña Betty butter (flap T)
IF error_ledger.top_pattern == E-contrabando  → Sazón + AR Labeler
IF error_ledger.top_pattern == vocal-larga/corta → homófonos quiz

IF best_cefr >= A2  → añadir paso AMERICA (pares con micrófono)
IF best_cefr >= B1a → añadir paso PALACE (trabalenguas con score)
IF skill.score < 0.5 AND skill.confidence > 0.6 → prioridad de ruta
```

## Confidence (doctrina N2)

`confidence` crece con cada dato capturado. Un score 0.4 con confidence 0.9 ES una debilidad real. Un score 0.4 con confidence 0.2 es "todavía no lo sabemos" → ruta de diagnóstico suave, no de remedio.

## Teacher override

La Maestra JJ siempre puede pisar la ruta (`teacher_override: true` en Mission). El sistema registra la decisión y aprende del resultado.

---

## Regla MVP determinística (canónica, del blueprint Gemini v2)

La regla de arranque del router, escrita como matemática pura:

```
IF (LearnerProfile.phonology.linking_connected_speech.score < 0.4
    AND LearnerProfile.phonology.linking_connected_speech.confidence > 0.8)
THEN
  route = [
    1 → Ear Training   (mode: AUDITORY_DISCRIMINATION, accuracy >= 0.80)
    2 → SoundMap        (mode: VISUAL_LINKING_MAP, interaction completed)
    3 → Valerie AI      (mode: PRODUCTION_CHECK, intelligibility >= 0.75)
  ]
```

Es la misma lógica v0 del Trainer (trackError → pestaña), expresada en el nuevo contrato. Un solo patrón de ejemplo basta para validar el loop; los demás umbrales se aprenden del piloto (N2).

## Semántica del teacher override (contrato v2)

`POST /api/v1/router/override` con `teacher_id`, `override_reason` y `pipeline_override`. La Mission sale con `teacher_override_active: true` y `active_until`. Regla pedagógica sellada: **el rendimiento bajo override SE SIGUE REGISTRANDO** — la Maestra JJ pisa la ruta, y el sistema aprende del resultado de su decisión.
