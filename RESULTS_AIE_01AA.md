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

## Sesión 6 — Agentes y MCP

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

## Sesión 7 — Skills, memoria de trabajo y Agent Framework

Dominio: `support`. La misma conversación con los dos runtimes (paso 7).

| | `react` | `agent_framework` |
|---|---|---|
| Tools pedidas en la consulta | `find_branches(district=Miraflores)` → BRN-02 | `find_branches(district=Miraflores)` → BRN-02 |
| La acción sensible quedó **NO SE EJECUTA** | No llegó a llamar `update_contact_details`: repitió el dato, pidió confirmación y explicó la validación por código y la aprobación del asesor | Igual: no llamó `update_contact_details`; pidió confirmación explícita antes de iniciar la solicitud |
| Pregunta de memoria respondida sin `→` | Sí: "Calle Ficticia 456", sin llamar tools | Sí: "Calle Ficticia 456", sin llamar tools |
| Primer texto (ms) | 12873 / 11710 / 12276 | 16457 / 15567 / 13403 |
| Respuesta completa (ms) | 13024 / 11979 / 12306 | 16600 / 15725 / 13406 |
| Tokens (entrada / salida) | 3293/843 · 2164/1049 · 2369/1048 | 2542/620 · 1776/1297 · 1963/1046 |

Los tiempos y tokens van por turno: consulta / acción sensible / pregunta de memoria.

### ¿La skill frenó la tool de otro dominio?

Mensaje: "Soy CUS-1001, ¿qué comisiones me cobraron?" (pide `get_charged_fees`, una tool del dominio `fees` que la skill `support` no ofrece).

Respuesta: **sí, la frenó en los dos runtimes.** Ninguno intentó llamar una tool (no hay `→`), los dos reconocieron que no pueden consultar comisiones "con las herramientas disponibles aquí" y derivaron a la app, al estado de cuenta o a una agencia. Además ofrecieron lo que sí está en la skill: buscar la agencia más cercana.

| | `react` | `agent_framework` |
|---|---|---|
| Intención | `data_query` | `data_query` |
| Tool llamada | ninguna | ninguna |
| Primer texto / completa (ms) | 16033 / 16322 | 9515 / 9814 |
| Tokens (entrada / salida) | 1195 / 1028 | 1195 / 692 |

Los dos la clasificaron como `data_query` y no como `out_of_scope`. No es grave porque no inventaron datos, pero el enrutamiento podría afinarse.

### Diferencias entre los dos runtimes

A nivel funcional el comportamiento fue idéntico: invocaron la misma herramienta con idénticos parámetros, frenaron la acción sensible hasta recibir confirmación, referenciaron las mismas fuentes del RAG y resolvieron la consulta de memoria sin repetir la llamada a find_branches.

### Conclusión

El comportamiento del agente se mantuvo intacto tras el cambio de runtime. Al delimitar la skill support las herramientas visibles para el modelo, ninguno de los dos entornos intentó acceder a las comisiones. Tampoco se ejecutaron acciones sensibles sin autorización previa, y gracias a la memoria de trabajo fue posible facilitar la dirección de la agencia sin volver a invocar la herramienta.

## Sesión 8 — Aprobación humana, validación y reintentos

**Dominio:** `support` (paso 6).

| Caso | Runtime | Mensaje | Qué pasó | Resultado o ID |
|---|---|---|---|---|
| Aprobar | `agent_framework` | "Soy CUS-1001, actualiza mi correo a ana.demo@example.com" → "Sí, confírmalo" | El agente solicitó confirmación antes de invocar `update_contact_details`. La herramienta quedó en `pending_approval` sin ejecutarse. El asesor aprobó (`s`) y la herramienta se ejecutó correctamente, devolviendo los datos del cliente con el correo actualizado. | `call-3206e794` → `pending_approval` → `ok`. |
| Rechazar | `react` | "Soy CUS-1001, actualiza mi correo a ana.demo@example.com" → "Sí, confírmalo" | El agente solicitó confirmación e invocó la herramienta, que quedó pendiente de aprobación. El asesor rechazó (`n`). La operación no se ejecutó y el agente comunicó el rechazo. | `call_zfxaDhisOpUPz6E4HifS9IoC` → `pending_approval` → `rechazada`. |
| Error de negocio (`CUS-9999`) | `react` | "Soy CUS-9999, actualiza mi correo a ana.demo@example.com" → "confirmo" | El agente solicitó confirmación, invocó `update_contact_details` y quedó pendiente de aprobación. El asesor aprobó (`s`), pero la herramienta devolvió un error indicando que el servicio bancario no respondía. El agente comunicó que el cambio no fue aplicado, aunque afirmó que la solicitud quedó registrada sin evidencia que lo confirmara. | `call_Z8Xj0daC8ObdBHHtShLWz0Pl` → `pending_approval` → `error`: "El servicio del banco no responde; intenta de nuevo en unos minutos". |
| Input inválido | `react` | "Mi número de cliente es 1001, ¿qué comisiones me cobraron?" | El agente clasificó la consulta como `data_query`, identificó que no disponía de herramientas para consultar comisiones y ofreció alternativas. Solicitó el código completo (`CUS-1001`). No se invocaron herramientas ni se comprobó una validación formal de parámetros inválidos. | Respuesta controlada, sin ejecución. Validación de input no verificada. |

### La trayectoria en el log

```text
INFO agent.application.chat_service: trayectoria 3356469e-b1fd-4950-92cd-453fa11675e5: update_contact_details pending_approval → respuesta sensitive_action

INFO agent.application.chat_service: trayectoria 3356469e-b1fd-4950-92cd-453fa11675e5: decisión del asesor → update_contact_details ok
```

### ¿Algo se ejecutó sin que lo aprobaras?

**No.** En los casos observados, ambos runtimes respetaron el mecanismo de aprobación humana.

- **Aprobación (`agent_framework`):** la herramienta se ejecutó únicamente después de recibir autorización del asesor.
- **Rechazo (`react`):** la herramienta no se ejecutó porque el asesor rechazó la operación.
- **Error (`react`):** la herramienta se invocó después de la aprobación, pero falló por falta de respuesta del servicio bancario.
- **Input inválido (`react`):** no se ejecutaron herramientas.

No se identificaron ejecuciones de acciones sensibles sin autorización previa.

### Conclusión

Los dos runtimes validaron con éxito el flujo Human-in-the-Loop (HITL) durante la gestión de operaciones sensibles. Por un lado, agent_framework completó sin inconvenientes una ejecución previamente autorizada; por otro, react detuvo una solicitud denegada y dio paso a una llamada aprobada que terminó fallando debido a una caída del servicio.

Asimismo, la prueba con el caso CUS-9999 confirmó que, si ocurre un fallo tras obtener la aprobación, dicho error se notifica de vuelta al agente evitando reportar el cambio como efectivo. No obstante, surgieron dos observaciones relevantes

## Sesión 9 — Despliegue en Azure

Equipo: `team-05`. Dominio: `support`.

| Comprobación | Resultado |
|---|---|
| Tests en el contenedor (paso 3) | 139 passed, 5 skipped |
| Acción aprobada después de reiniciar `uvicorn` (paso 2, Cosmos DB) | 144 passed |
| Imagen desplegada (`team-NN/agent:<sha>`) | acrworkshopjsu3.azurecr.io/team-05/agent |
| Revisión activa y duración del job `deploy` | https://github.com/arturoamapanqui/agent-scratch/actions/runs/45743594896/job/139654500818 |
| `/health` del agente desplegado | Agente en https://ca-agent-chat-05.icybush-2ea2dfc1.eastus2.azurecontainerapps.io: ok |
| Respuesta con `Fuentes:` contra Azure (y su tiempo en ms) | [4] channels-and-hours.html · Canales y horarios de atención > Aplicación y banca por internet (primer texto en 9235 ms, respuesta completa en 9374 ms, 1651 tokens de entrada, 975 de salida) |
| Acción aprobada contra Azure, con su `resultado:` | Agente [product_question]: Agencias: lunes a viernes de 9:00 a 18:00; sábados de 9:00 a 13:00 (domingos y feriados no atienden). Banca por teléfono: (01) 555-0200, lunes a sábado de 8:00 a 20:00. Aplicación y banca por internet: disponibles las 24 horas, todos los días. |

### Qué pone Azure y qué pone la imagen

- APPLICATIONINSIGHTS_CONNECTION_STRING
- AZURE_CLIENT_ID
- AZURE_OPENAI_ENDPOINT
- COSMOS_CONTAINER
- COSMOS_DATABASE
- COSMOS_ENDPOINT
- FOUNDRY_PROJECT_ENDPOINT
- KEY_VAULT_URI
- MCP_SCOPE
- MCP_URL
- SEARCH_ENDPOINT
- SEARCH_INDEX
- TEAM_ID

### Problemas que encontraste y cómo los resolviste

N/A 

### Conclusión

Tras completar el despliegue del agente en Azure, se llevaron a cabo las pruebas de validación correspondientes. Para ello, se utilizó un cliente desarrollado en Python desde un entorno local, lo que permitió verificar la correcta conectividad y el intercambio de peticiones y respuestas con el servicio alojado en Azure.