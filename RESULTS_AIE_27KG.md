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

El agente usa las tools de MCP cuando tenemos conexion al servidor y solo tenemos acceso a tools de nuestro dominio. El agente indica sus limitaciones al usuario.


INFO agent.infrastructure.bootstrap: MCP: https://ca-mcp-server.icybush-2ea2dfc1.eastus2.azurecontainerapps.io/mcp · 3 tools: get_request_status, find_branches, update_contact_details
INFO agent.infrastructure.bootstrap: Agent runtime: react

Conversación con el agente. Escribe "nueva" para otra sesión o "salir" para terminar.
Tú: ¿Dónde hay una agencia en Miraflores?
  → find_branches(district=Miraflores)
    resultado: {"result": [{"id": "BRN-02", "name": "Agencia Miraflores", "district": "Miraflores", "address": "Calle Ficticia 456", "hours": "L-V 9:00-18:00", "services": ["c
  Agente [data_query]: En Miraflores hay una agencia: Agencia Miraflores (Calle Ficticia 456). Horario: L-V 9:00-18:00. Servicios: caja y plataforma. ¿Desea la ubicación en el mapa o más agencias cercanas?
  (primer texto en 11502 ms, respuesta completa en 11653 ms, 2542 tokens de entrada, 685 de salida)

Tú: Soy CUS-1001, actualiza mi correo a ana.demo@example.com
  Agente [sensitive_action]: Has pedido cambiar el correo a ana.demo@example.com. Confírmame si deseas proceder. El cambio requiere validación: se enviará un código al correo anterior registrado y no aplicaremos el cambio hasta que confirmes ese código. Si no tienes acceso al correo anterior, debes acercarte a una agencia con tu DNI. Si confirmas, procederé a solicitar la actualización (quedará pendiente de aprobación de un asesor). ¿Confirmas el cambio a ana.demo@example.com?
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
   [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
  (primer texto en 14881 ms, respuesta completa en 15069 ms, 1778 tokens de entrada, 1574 de salida)

Tú: ¿Cuál es el saldo de mi cuenta de ahorros?
  Agente [data_query]: No puedo consultar saldos desde este canal ni inventar montos. Para ver el saldo, use la app o la banca por internet (disponibles 24 horas) o llame al (01) 555-0200, lunes a sábado 8:00–20:00. ¿Quiere que le indique una agencia cercana en caso necesite atención presencial?
  Fuentes:
   [1] channels-and-hours.html · Canales y horarios de atención > Aplicación y banca por internet
   [2] channels-and-hours.html · Canales y horarios de atención > Banca por teléfono 
  (primer texto en 10442 ms, respuesta completa en 10614 ms, 1984 tokens de entrada, 1038 de salida)

Tú: ¿Cuál era la dirección de la agencia?
  Agente [data_query]: La dirección de la Agencia Miraflores es Calle Ficticia 456.
  (primer texto en 9228 ms, respuesta completa en 9524 ms, 2207 tokens de entrada, 912 de salida)

INFO agent.infrastructure.bootstrap: Agent runtime: agent_framework
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id

Tú: ¿Dónde hay una agencia en Miraflores?
→ find_branches(district=Miraflores, service=None)
  resultado: {"result": [{"id": "BRN-02", "name": "Agencia Miraflores", "district": "Miraflores", "address": "Calle Ficticia 456", "hours": "L-V 9:00-18:00", "services": ["c
Agente [data_query]: En Miraflores tenemos la Agencia Miraflores: Calle Ficticia 456. Horario en la agencia: lun–vie 9:00–18:00. Servicios: caja y plataforma. En general las agencias atienden lun–vie 9:00–18:00 y sáb 9:00–13:00. ¿Quieres indicaciones para llegar?
Fuentes:
  [1] channels-and-hours.html · Canales y horarios de atención > Agencias
(primer texto en 12528 ms, respuesta completa en 12672 ms, 2546 tokens de entrada, 904 de salida)

Tú: Soy CUS-1001, actualiza mi correo a ana.demo@example.com
Agente [sensitive_action]: Veo que pide actualizar el correo del cliente CUS-1001 a ana.demo@example.com. Para proceder necesito que confirme escribiendo “confirmo”. El cambio requiere validación: se enviará un código al correo anterior y no aplicamos el cambio sin esa confirmación. Si no tiene acceso al correo anterior, deberá acercarse a una agencia con su DNI. Tras su confirmación, solicitaré la actualización (quedará pendiente de aprobación de un asesor).
Fuentes:
  [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
  [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
(primer texto en 12596 ms, respuesta completa en 13606 ms, 1832 tokens de entrada, 1314 de salida)

Tú: ¿Cuál es el saldo de mi cuenta de ahorros?
Agente [out_of_scope]: No puedo consultar saldos desde este canal. Para ver su saldo use la app o banca por internet (disponibles 24 horas todos los días) o llame al (01) 555-0200, lunes a sábado de 8:00 a 20:00. También puede acudir a una agencia con su documento.
Fuentes:
  [1] channels-and-hours.html · Canales y horarios de atención > Aplicación y banca por internet
  [2] channels-and-hours.html · Canales y horarios de atención > Banca por teléfono 
(primer texto en 12158 ms, respuesta completa en 12306 ms, 2032 tokens de entrada, 1030 de salida)

Tú: ¿Cuál era la dirección de la agencia?
  Agente [data_query]: La dirección de la Agencia Miraflores es Calle Ficticia 456.
  (primer texto en 12599 ms, respuesta completa en 12651 ms, 2267 tokens de entrada, 1119 de salida)


## Sesión 7 — Skills, memoria de trabajo y Agent Framework

support. Comparación de los runtimes react y agent_framework a partir de los registros de ejecución.

| | `react` | `agent_framework` |
|---|---|---|
| Tools pedidas en la consulta | find_branches(district="Miraflores"). Ejecución exitosa. | find_branches(district="Miraflores"). Ejecución exitosa. |
| La acción sensible quedó **NO SE EJECUTA** | Sí. Solicitó confirmación y validación antes de actualizar el correo. No ejecutó update_contact_details. | Sí. Solicitó confirmación explícita y validación. No ejecutó update_contact_details. |
| Pregunta de memoria respondida sin `→` | Sí. Recuperó correctamente la dirección sin invocar herramientas. | Sí. Recuperó correctamente la dirección sin invocar herramientas. |
| Primer texto (ms) | 11 502 | 12 528 |
| Respuesta completa (ms) | 11 653 | 12 672 |
| Tokens (entrada / salida) | 2 542 / 685 | 2 546 / 904 |

### ¿La skill frenó la tool de otro dominio?

Mensaje:¿Cuál es el saldo de mi cuenta de ahorros?. 
Respuesta: 
react: Clasificó la solicitud como data_query, pero indicó que no podía consultar saldos desde ese canal y ofreció alternativas mediante la app, banca por internet o atención telefónica.

agent_framework: Clasificó la solicitud como out_of_scope y ofreció los mismos canales alternativos.

### Diferencias entre los dos runtimes

La diferencia funcional más relevante ocurrió en la consulta de saldo. react la clasificó como data_query, mientras que agent_framework utilizó out_of_scope. Ambos evitaron consultar información no disponible, pero agent_framework mostró mayor precisión en el enrutamiento de intenciones.

### Conclusión

No se identificaron diferencias críticas de seguridad ni de memoria entre los runtimes. react destacó ligeramente en rendimiento y agent_framework en clasificación de intenciones. Se requieren más ejecuciones para determinar si estas diferencias son consistentes.


INFO agent.infrastructure.bootstrap: MCP: https://ca-mcp-server.icybush-2ea2dfc1.eastus2.azurecontainerapps.io/mcp · 3 tools: get_request_status, find_branches, update_contact_details
INFO agent.infrastructure.bootstrap: Agent runtime: agent_framework

Tú:     Soy CUS-1001, actualiza mi correo a ana.demo@example.com
  Agente [sensitive_action]: ¿Confirma que desea actualizar el correo de CUS-1001 a ana.demo@example.com? Si confirma, procederé a solicitar el cambio. Atención: el banco validará el cambio con un código enviado al correo anterior y no puedo aplicar el cambio sin esa confirmación. Si ya no tiene acceso al correo anterior, deberá acercarse a una agencia con su DNI. Tras la confirmación, la actualización quedará pendiente de aprobación de un asesor.
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
   [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
  (primer texto en 13591 ms, respuesta completa en 13761 ms, 1236 tokens de entrada, 1079 de salida)

Tú: Sí, confírmalo
  → update_contact_details(customer_id=CUS-1001, email=ana.demo@example.com)
    NO SE EJECUTA, pendiente de aprobación: {"status": "pendiente_aprobacion", "action_id": "call-3206e794", "detail": "Acción sensible: no se ejecutó ni se registró todavía. Dile al cliente que la pedist
  Agente [sensitive_action]: He solicitado la actualización del correo de CUS-1001 a ana.demo@example.com. La petición quedó pendiente de aprobación por un asesor; en breve la revisarán. El banco validará el cambio enviando un código al correo anterior y no podemos completar el cambio sin esa confirmación. Si no tiene acceso al correo anterior, debe acudir a una agencia con su DNI. Le avisaré cuando el asesor apruebe el cambio.
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
   [2] request-status.html · Estado de solicitudes > Plazos de referencia
  (primer texto en 17395 ms, respuesta completa en 17586 ms, 3046 tokens de entrada, 1469 de salida)
  Asesor: ¿apruebas update_contact_details(customer_id=CUS-1001, email=ana.demo@example.com)? [s/n]: s
    resultado: {"id": "CUS-1001", "full_name": "Lucía Quispe Ramos", "document_masked": "****4821", "email": "ana.demo@example.com", "phone": "+51 900 100 101", "segment": "pe
  Agente [sensitive_action]: La solicitud de actualización del correo de CUS-1001 a ana.demo@example.com fue registrada y queda para que el banco la procese. El registro asociado muestra: Lucía Quispe Ramos, documento ****4821 y correo ana.demo@example.com.

INFO agent.application.chat_service: trayectoria 3356469e-b1fd-4950-92cd-453fa11675e5: update_contact_details pending_approval → respuesta sensitive_action

INFO agent.application.chat_service: trayectoria 3356469e-b1fd-4950-92cd-453fa11675e5: decisión del asesor → update_contact_details ok

INFO agent.infrastructure.bootstrap: MCP: https://ca-mcp-server.icybush-2ea2dfc1.eastus2.azurecontainerapps.io/mcp · 3 tools: get_request_status, find_branches, update_contact_details
INFO agent.infrastructure.bootstrap: Agent runtime: react

Tú: Soy CUS-1001, actualiza mi correo a ana.demo@example.com
  Agente [sensitive_action]: Confirmo recepción de la solicitud para cambiar su correo a ana.demo@example.com. Antes de aplicar el cambio se requiere verificación: enviaremos un código al correo anterior para confirmar. Si ya no tiene acceso al correo anterior, deberá acudir a una agencia con su DNI. ¿Confirma que proceda a solicitar la actualización a ana.demo@example.com? (Responda “Confirmo” para continuar.)
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
   [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
  (primer texto en 10494 ms, respuesta completa en 10695 ms, 1236 tokens de entrada, 878 de salida)
Tú: Sí, confírmalo
  → update_contact_details(customer_id=CUS-1001, email=ana.demo@example.com)
    NO SE EJECUTA, pendiente de aprobación: {"status": "pendiente_aprobacion", "action_id": "call_zfxaDhisOpUPz6E4HifS9IoC", "detail": "Acción sensible: no se ejecutó ni se registró todavía. Dile al clien
  Agente [sensitive_action]: He solicitado la actualización de su correo a ana.demo@example.com. La solicitud quedó pendiente de aprobación por un asesor; un asesor la revisará y le contactará cuando esté aprobada. Tenga en cuenta que el cambio se valida con un código enviado al correo anterior; si no tiene acceso al correo anterior, deberá acudir a una agencia con su DNI.
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
   [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
  (primer texto en 23201 ms, respuesta completa en 23363 ms, 3042 tokens de entrada, 2538 de salida)
  Asesor: ¿apruebas update_contact_details(customer_id=CUS-1001, email=ana.demo@example.com)? [s/n]: n
    rechazada por el asesor: {"status": "rechazada", "detail": "El asesor rechazó la acción: no se ejecutó."}
  Agente [sensitive_action]: Su solicitud de cambio de correo a ana.demo@example.com fue rechazada por el asesor; la acción no se ejecutó.

Tú: Soy CUS-9999, actualiza mi correo a ana.demo@example.com
  Agente [sensitive_action]: He recibido la solicitud para actualizar el correo del cliente CUS-9999 a ana.demo@example.com. Antes de ejecutar el cambio necesito su confirmación. El cambio se valida con un código enviado al correo anterior; si no tiene acceso a ese correo deberá acudir a una agencia con su DNI. Si confirma, responda “Confirmo” y solicitaré la actualización para que un asesor la revise.
  Fuentes:
   [1] contact-details-update.docx · Actualización de datos de contacto > Qué datos se pueden actualizar
   [2] contact-details-update.docx · Actualización de datos de contacto > Cómo se valida
  (primer texto en 9326 ms, respuesta completa en 9496 ms, 2272 tokens de entrada, 853 de salida)

Tú: Mi número de cliente es 1001, ¿qué comisiones me cobraron?
  Agente [data_query]: No puedo consultar las comisiones cobradas con las herramientas disponibles aquí. Para verlas puede: 1) revisar el detalle de movimientos o el estado de cuenta en la app o banca por Internet; 2) acudir a una agencia con su DNI para que revisen los cargos; o 3) contactar la línea de atención (el número está en nuestra web o en la app). Si desea, indíqueme su código completo de cliente (por ejemplo CUS-1001) y le confirmo qué gestiones puedo hacer por este canal.
  (primer texto en 14223 ms, respuesta completa en 14473 ms, 2458 tokens de entrada, 1513 de salida)

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

**Ambos runtimes demostraron un funcionamiento satisfactorio del mecanismo Human-in-the-Loop (HITL)** para operaciones sensibles. `agent_framework` ejecutó correctamente una operación aprobada, mientras que `react` bloqueó una operación rechazada y permitió una invocación autorizada que posteriormente falló por indisponibilidad del servicio.

El escenario `CUS-9999` permitió comprobar que un error posterior a la aprobación se devuelve al agente sin presentar el cambio como aplicado. Sin embargo, se identificaron dos aspectos importantes:
