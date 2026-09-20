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
