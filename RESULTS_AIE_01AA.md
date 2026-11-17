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

## Sesión 6 — Tools del MCP en el chat

Dominio: `support`. MCP usado en el chat: el compartido (`bank-mcp`, vía `MCP_URL`). Al arrancar, el agente registró `3 tools: get_request_status, find_branches, update_contact_details`.

### Tools de tu dominio

| MCP | Tools que lista `dev/mcp/mcp_tools.py` |
|---|---|
| Mock | `get_request_status` y `find_branches` (solo lectura), y `update_contact_details` (sensible), donde estas 3 tools están marcadas como `support`. |
| Compartido | `find_branches` (consulta: `district`, `service`), `get_request_status` (consulta: `request_id`), `update_contact_details` (acción sensible: `customer_id`, `email`, `phone`) |

### Conversación en `dev/chat.py` (paso 12)

| Prueba | Mensaje | Tool pedida (`→`) | Qué pasó | Primer texto / respuesta completa (ms) |
|---|---|---|---|---|
| Consulta de tu dominio | ¿Dónde hay una agencia en Miraflores? | `find_branches(district=Miraflores, service=None)` | `data_query`. Con los datos de BRN-02, respondió "Agencia Miraflores: Calle Ficticia 456", lun–vie 09:00–18:00, caja y plataforma. Esta vez no citó documentos: la respuesta sale solo de la tool. | 10584 / 10738 |
| Acción confirmada | Soy CUS-1001, actualiza mi correo a ana.demo@example.com | `update_contact_details(customer_id=CUS-1001, email=ana.demo@example.com, phone=None)` | `sensitive_action`. La tool la deja en `pendiente_aprobacion` y **no la ejecuta**. El agente informa que la solicitud espera la aprobación de un asesor y que se confirmará con un código enviado al correo anterior (o en agencia con DNI). Se apoya en `contact-details-update.docx`. | 13518 / 13676 |
| Sin tool que la resuelva | ¿Cuál es el tipo de cambio del dólar hoy? | — (ninguna) | `product_question`. Dice que no tiene el tipo de cambio y que "no puedo inventarlo". Remite a la app (24 h) o a una agencia, con el horario de `channels-and-hours.html`. | 10237 / 10400 |
| Tool de otro dominio | Soy CUS-1001, ¿puedo subir la línea de mi tarjeta CRD-2001 a 4000? | — (ninguna; `request_credit_line_increase` pertenece a `cards`) | `product_question`. No intenta ninguna tool. Reconoce que no tiene el procedimiento para aumentar la línea y sugiere consultarlo por teléfono o en la app. | — |

**Incidente:** en el primer intento de la consulta de Miraflores, el MCP compartido devolvió `"El servicio del banco no responde; intenta de nuevo en unos minutos"`. El agente no inventó ninguna agencia. Avisó que la búsqueda falló, ofreció reintentar y solo dio el horario general de agencias que está en el corpus (27701 / 27875 ms). Al reintentar, la tool respondió bien.

### ¿El modelo inventó algún dato cuando ninguna tool lo resolvía?

No. La prueba del tipo de cambio era la más propensa a que inventara una cifra, y el agente se negó explícitamente a darla. Lo mismo pasó con el aumento de línea y con la caída del MCP. En los tres casos, lo único que dio fueron canales y horarios, y todos están en `app-faq.md` y `channels-and-hours.html`.

### Conclusión

- **El filtro por dominio aísla bien.** El header `X-Bank-Domain` limita a `support` a sus 3 tools, y una petición de `cards` no genera ninguna llamada indebida.
- **La consulta usa la tool correcta,** con sus parámetros, y responde con lo que trajo.
- **Las acciones sensibles quedan retenidas:** `update_contact_details` espera aprobación humana y el agente lo explica sin decir que el cambio ya está hecho.
- **Cuando falta la información o la tool falla, no rellena con datos:** lo dice claramente y deriva a un canal oficial.
