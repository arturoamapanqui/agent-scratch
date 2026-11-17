Resumen de 30 casos (juez local):
  recall@5: 1.00   intención: 0.87   fuentes: 0.93   hechos: 0.78
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 22579 de entrada, 13540 de salida

Se eligió la pregunta: ¿Cuál es el costo de una carta de presentación bancaria?
Debido a que la respuesta solo es S/25 para retar al agente a encontrar una respuesta corta.
Los resultados se muestran abajo siendo exitoso.

support-AIE27KG answerable       ok      ok       ok      ok     5.0        5.0   1.0  ok

Resumen de 1 casos (juez local):
  recall@5: 1.00   intención: 1.00   fuentes: 1.00   hechos: 1.00
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 0
  tokens: 739 de entrada, 178 de salida

CAMBIOS:

chunks más chicos:
Resumen de 30 casos (juez local):
  recall@5: 1.00   intención: 0.87   fuentes: 0.94   hechos: 0.71
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 23343 de entrada, 14514 de salida

menos fragmentos:
Resumen de 30 casos (juez local):
  recall@3: 1.00   intención: 0.84   fuentes: 0.94   hechos: 0.82
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 20559 de entrada, 13183 de salida

más fragmentos:
Resumen de 30 casos (juez local):
  recall@8: 1.00   intención: 0.84   fuentes: 0.94   hechos: 0.79
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 27634 de entrada, 13736 de salida

base local, sin reranker:
Resumen de 30 casos (juez local):
  recall@8: 1.00   intención: 0.87   fuentes: 0.90   hechos: 0.71
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 27881 de entrada, 14235 de salida

La mejor configuración, según los resultados, es mantener el tamaño original de los chunks, reducir a 3 fragmentos recuperados y conservar el reranker.

Comparar jueces:
Resumen de 30 casos (juez azure_evaluation):
  recall@3: 1.00   intención: 0.87   fuentes: 0.94   hechos: 0.79
  apoyo: 5.0/5   relevancia: 4.8/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 20563 de entrada, 13120 de salida

Entre estos dos resultados, Azure Evaluation presenta mejores métricas de intención y precisión factual

## Sesión 6 — Tools del MCP en el chat

Dominio: `support`. MCP: el mock (`http://127.0.0.1:8200/mcp`) y, si ya tienes `MCP_URL`, el compartido (`bank-mcp`).

### Tools de tu dominio

| MCP | Tools que lista `dev/mcp/mcp_tools.py` |
|---|---|
| Mock | tools find_branches, get_request_status, update_contact_details |
| Compartido | _(anotar)_ |

### Conversación en `dev/chat.py` (paso 12)

| Prueba | Mensaje | Tool pedida (`→`) | Qué pasó | Primer texto / respuesta completa (ms) |
|---|---|---|---|---|
| Consulta de tu dominio | ¿Dónde hay una agencia en Miraflores? | find_branches | Encontré una agencia en Miraflores: Agencia Miraflores, Calle Ficticia 456. Horario: lunes a viernes 9:00–18:00. Servicios: caja y plataforma. ¿Deseas indicaciones o que te confirme otro detalle? | primer texto en 17437 ms, respuesta completa en 17653 ms, 2160 tokens de entrada, 620 de salida |
| Acción confirmada | Soy CUS-1001, actualiza mi correo a ana.demo@example.com | update_contact_details | NO SE EJECUTA, pendiente de aprobación | primer texto en 23653 ms, respuesta completa en 23834 ms, 2516 tokens de entrada, 2027 de salida |
| Sin tool que la resuelva | ¿Cuál es el saldo de mi cuenta de ahorros? | Ninguna tool | No puedo consultar saldos desde aquí ni acceder a tu cuenta. | primer texto en 11056 ms, respuesta completa en 11301 ms, 1499 tokens de entrada, 998 de salida |
| Tool de otro dominio | ¿Cuánto pagaría al mes por un préstamo de 20000 soles a 24 meses? | NINGUNA tool | En los fragmentos proporcionados no aparece la tasa de interés ni los datos necesarios para calcular la cuota mensual de un préstamo de S/20,000 a 24 meses, por lo que no puedo calcular el pago. | primer texto en 17240 ms, respuesta completa en 17395 ms, 1801 tokens de entrada, 1857 de salida |

### ¿El modelo inventó algún dato cuando ninguna tool lo resolvía?

No inventa datos, solo indica sus limitaciones para responder la pregunta.

### Conclusión

El agente usa las tools de MCP cuando tenemos conexion al servidor y solo tenemos acceso a tools de nuestro dominio. El agente indica sus limitaciones al usuario