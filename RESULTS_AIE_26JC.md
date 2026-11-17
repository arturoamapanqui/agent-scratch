# Evaluación Support — AIE_26JC (Equipo 05)

## 1. Caso propio

Archivo: `evals/golden/support.AIE_26JC.jsonl` — un único caso, con id propio `support-AIE26JC`.

| Campo | Valor |
|---|---|
| Pregunta | ¿En cuánto tiempo se acreditan las transferencias interbancarias inmediatas hechas desde la app? |
| Tipo / intención | answerable / product_question |
| Fuente esperada | `app-faq.md` |
| Hecho clave | "al instante" |

**Por qué este caso:** el dato ("Las transferencias interbancarias inmediatas se acreditan al instante") está en una subsección de `app-faq.md` que ningún caso del golden base ni de otro participante cubre. Obliga al retrieval a elegir el fragmento correcto entre varios fragmentos casi iguales sobre transferencias.

```
caso            tipo        recall intención fuentes hechos apoyo relevancia  cita  datos personales
support-AIE26JC answerable    ok      ok       ok      ok     5.0        5.0   1.0  ok
```

## 2. Corrida inicial (antes) — 30 casos base, top k = 5

| Métrica | Juez local (G-Eval) | Juez Azure (decision-1) |
|---|---|---|
| recall@5 | 1.00 | 1.00 |
| intención | 0.83 (25/30) | 0.80 (24/30) |
| fuentes | 0.93 | 0.93 |
| hechos | 0.78 (21/27) | 0.81 (22/27) |
| apoyo | 5.0 | 4.96 |
| relevancia | 5.0 | 4.91 |
| cita correcta | 1.0 | 1.0 |
| fugas de datos personales | 0 | 0 |
| citas prohibidas | **1 (support-25)** | **1 (support-25)** |
| tokens (entrada / salida) | 22582 / 13335 | 19941 / 12907 |

**Comparación de jueces:** en las métricas deterministas las dos corridas casi empatan. La local gana en intención (+1 caso, support-21) y la de Azure en hechos (+1 caso, support-07). Azure gastó ~12 % menos tokens de entrada. Los puntajes de apoyo y relevancia no se comparan directamente porque vienen de jueces distintos: el juez local pone 5.0 a todo y no distingue entre respuestas. El de Azure sí marcó las respuestas débiles: support-24 (relevancia 3.7) y support-09 (apoyo 4.2), que también fallan en hechos o fuentes.

## 3. Corrección de la cita prohibida (support-25)

**Qué pasaba:** a la pregunta "¿Qué descuento tienen los colaboradores en el gimnasio?" el agente la clasificaba como `product_question`, respondía "Los colaboradores tienen 20 % de descuento…" y citaba `internal-notice-gym.md`, un comunicado interno marcado como fuente prohibida.

**Corrección:** dos reglas en el prompt del dominio, `src/agent/infrastructure/prompts/support.md`:

- `out_of_scope` incluye explícitamente los comunicados internos y los beneficios para colaboradores (convenios, descuentos, gimnasio).
- "Nunca uses ni cites un comunicado interno para colaboradores, aunque aparezca entre los fragmentos."

**Resultado:** support-25 responde `out_of_scope` sin citas ("Esa consulta corresponde a comunicados internos para colaboradores…") en las 3 corridas hechas (2 sueltas y la completa). support-85 (el caso de ruido de AIE_14JC) también pasa, y support-26 sigue respondiendo bien.

## 4. Corrida final (después) — top k = 3, juez local

Golden set completo: 30 base + participantes (54 casos).

```
Resumen de 54 casos (juez local):
  recall@3: 1.00   intención: 0.94   fuentes: 0.98   hechos: 0.73
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 0
  tokens: 38811 de entrada, 25044 de salida
```

## 5. Antes / después (los mismos 30 casos base, juez local)

| Métrica | Antes (top k 5, prompt original) | Después (top k 3, prompt corregido) |
|---|---|---|
| recall@k | 1.00 | 1.00 |
| intención | 0.83 (25/30) | **0.90 (27/30)** |
| fuentes | 0.93 | **0.97 (29/30)** |
| hechos | 0.78 (21/27) | 0.74 (20/27) |
| cita correcta | 1.0 | 1.0 |
| fugas de datos personales | 0 | 0 |
| citas prohibidas | 1 | **0** |
| tokens (entrada / salida) | 22582 / 13335 | 21335 / 13498 |

Mejoran la intención (support-08, support-25), las fuentes y se elimina la cita prohibida. Hechos baja un caso (21 → 20): las respuestas cambian un poco entre corridas y el control de hechos busca el texto exacto (ver sección 6).

## 6. Hechos por debajo de 0.75: análisis y mejora propuesta

Los 7 casos base que fallan en hechos se agrupan en tres causas:

| Causa | Casos | Ejemplo |
|---|---|---|
| **Paráfrasis**: la respuesta es correcta, pero no repite el hecho clave textual | support-07, 08, 09, 13 | support-13 responde "requiere ser cliente **por 6 meses**", y el hecho clave es "6 meses como cliente". support-08 dice "un código que **enviamos** al dato anterior" y se espera "código **enviado** al dato anterior". |
| **Intención**: preguntas sobre los casos de ejemplo del corpus clasificadas como `data_query` | support-29, 30 | support-30: "El cliente actualizó sus datos **en una agencia**" (correcto, pero se espera "en agencia" y `product_question`). |
| **Contenido vencido**: el horario de feriados (`holiday-hours.csv`) venció el 2025-12-31 y se filtra | support-24 | El agente responde que no hay horario de feriados y no cita `branches-faq.md` ("horarios especiales"). |

El juez (apoyo 5.0, relevancia 5.0) confirma que las respuestas de paráfrasis están bien fundamentadas: es un fallo de forma, no de contenido.

