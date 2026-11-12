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
Resumen de 31 casos (juez local):
  recall@5: 1.00   intención: 0.87   fuentes: 0.94   hechos: 0.71
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 23343 de entrada, 14514 de salida

menos fragmentos:
Resumen de 31 casos (juez local):
  recall@3: 1.00   intención: 0.84   fuentes: 0.94   hechos: 0.82
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 20559 de entrada, 13183 de salida

más fragmentos:
Resumen de 31 casos (juez local):
  recall@8: 1.00   intención: 0.84   fuentes: 0.94   hechos: 0.79
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 27634 de entrada, 13736 de salida

base local, sin reranker:
Resumen de 31 casos (juez local):
  recall@8: 1.00   intención: 0.87   fuentes: 0.90   hechos: 0.71
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 27881 de entrada, 14235 de salida

La mejor configuración, según los resultados, es mantener el tamaño original de los chunks, reducir a 3 fragmentos recuperados y conservar el reranker.

Comparar jueces:
Resumen de 31 casos (juez azure_evaluation):
  recall@3: 1.00   intención: 0.87   fuentes: 0.94   hechos: 0.79
  apoyo: 5.0/5   relevancia: 4.8/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 20563 de entrada, 13120 de salida

Resumen de 31 casos (juez local):
  recall@3: 1.00   intención: 0.84   fuentes: 0.94   hechos: 0.68
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 20542 de entrada, 13175 de salida

Entre estos dos resultados, Azure Evaluation presenta mejores métricas de intención y precisión factual