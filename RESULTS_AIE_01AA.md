# Evaluación Support — AIE_01AA (Equipo 05)

## 1. Caso propio

Archivo: `evals/golden/support.AIE_01AA.jsonl` — un único caso, con id propio `support-AIE01AA`.

| Campo | Valor |
|---|---|
| Pregunta | ¿Puedo cerrar mi cuenta de ahorros si todavía tengo deudas con el banco? |
| Tipo / intención | answerable / product_question |
| Fuente esperada | `requirements-by-procedure.pdf` |
| Hecho clave | "deudas asociadas" |

**Por qué este caso:** el golden base y los demás participantes solo preguntan por el "saldo cero" para cerrar la cuenta. La segunda condición del mismo fragmento ("sin deudas asociadas") no la cubre nadie. Es una pregunta de sí o no, así que el agente tiene que responder "no" y justificarlo con el requisito correcto.

**Ajuste del hecho clave:** en la primera versión el hecho clave era "sin deudas". En la corrida completa el agente respondió "debe tener saldo cero y **no tener deudas asociadas**": la respuesta era correcta, pero no contenía el texto exacto y el control de hechos falló. Se cambió a "deudas asociadas", que aparece tanto en el corpus ("sin deudas asociadas") como en cualquier forma natural de responder.

## 2. Resultado del caso propio

```
caso            tipo        recall intención fuentes hechos apoyo relevancia  cita  datos personales
support-AIE01AA answerable    ok      ok       ok      ok     5.0        5.0   1.0  ok
```

Respuesta del agente: *"No. Para cerrar una cuenta de ahorros debe tener saldo cero y no tener deudas asociadas. El cierre se puede realizar en agencia o en la aplicación."* — cita `requirements-by-procedure.pdf`.

## 3. Corrida completa del golden set (top k = 3, juez local)

30 casos base + casos de todos los participantes (54 casos):

```
Resumen de 54 casos (juez local):
  recall@3: 1.00   intención: 0.94   fuentes: 0.98   hechos: 0.73
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 0
  tokens: 38811 de entrada, 25044 de salida
```

Solo los 30 casos base: recall 1.00, intención 0.90, fuentes 0.97, hechos 0.74, 0 citas prohibidas, 0 fugas.

La cita prohibida de support-25 se corrigió en el prompt del dominio (detalle en `RESULTS_AIE_26JC.md`, sección 3). El análisis de hechos por debajo de 0.75 y la mejora propuesta (que el agente copie tal cual los datos clave en vez de parafrasearlos) están en la sección 6 de ese mismo archivo.

## 4. Revisión final de metas

| Meta | Resultado final | ¿Cumple? |
|---|---|---|
| Caso propio único, con id propio, sin repetir ids del golden | `support-AIE01AA`, 1 caso | ✅ |
| `uv run pytest` en verde (con el golden base descargado) | 86 passed | ✅ |
| Caso propio pasa todas las métricas | recall, intención, fuentes, hechos ok; 5.0 / 5.0 / 1.0 | ✅ |
| 0 citas de fuentes prohibidas | 0 (54 casos) | ✅ |
| 0 fugas de datos personales | 0 (54 casos) | ✅ |
| Hechos ≥ 0.75 | 0.74 en los 30 base / 0.73 en los 54 | ❌ — mejora documentada en `RESULTS_AIE_26JC.md`, sección 6 |

## 5. Configuración final

| Parámetro | Valor |
|---|---|
| Dominio | `support` |
| Modelo de chat | `gpt-5-mini` (Microsoft Foundry, Entra ID) |
| Embeddings | `text-embedding-3-small` |
| Base de conocimiento | Azure AI Search (`idx-team-05`), híbrida con reranker semántico |
| `SEARCH_TOP_K` | 3 |
| `INGEST_CHUNK_MAX_CHARS` | 1500 |
| `MAX_TURNS` | 10 |
| Juez | `local` (G-Eval con `gpt-5-mini`); alternativo `azure_evaluation` (`decision-1`) |
