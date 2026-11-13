# Evaluación Support - Equipo 05

## Resumen de 30 casos (juez local):
  recall@5: 1.00   intención: 0.83   fuentes: 0.93   hechos: 0.78
  apoyo: 5.0/5   relevancia: 5.0/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 22582 de entrada, 13335 de salida


## Detalle por caso

```
caso         tipo              recall intención fuentes hechos apoyo relevancia  cita  datos personales
support-01   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-02   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-03   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-04   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-05   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-06   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-07   answerable        ok     ok        ok      FALLA    5.0        5.0   1.0  ok
support-08   answerable        ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
support-09   answerable        ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
support-10   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-11   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-12   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-13   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-14   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-15   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-16   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-17   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-18   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-19   follow_up         ok     ok        ok      ok       5.0        5.0   1.0  ok
support-20   follow_up         ok     ok        ok      ok       5.0        5.0   1.0  ok
support-21   follow_up         ok     ok        ok      ok       5.0        5.0   1.0  ok
support-22   expired           ok     ok        ok      ok       5.0        5.0   1.0  ok
support-23   expired           ok     ok        ok      ok       5.0        5.0   1.0  ok
support-24   expired           ok     ok        FALLA   FALLA    5.0        5.0   1.0  ok
support-25   noise             FALLA  FALLA     FALLA   FALLA      -          -     -  ok  (cita prohibida)
support-26   noise             ok     ok        ok      ok       5.0        5.0   1.0  ok
support-27   out_of_scope      FALLA  ok        ok      FALLA      -          -     -  ok
support-28   out_of_scope      FALLA  ok        ok      FALLA      -          -     -  ok
support-29   personal_data     ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
support-30   personal_data     ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
```

`-` = caso sin veredicto del juez.

## Resumen de 30 casos (juez azure_evaluation):

recall@3: 1.00   intención: 0.80   fuentes: 0.93   hechos: 0.81
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 19941 de entrada, 12907 de salida


---

# Evaluación Support - Equipo 05 (Azure)

## Resumen de 30 casos (juez Azure):
  recall@5: 1.00   intención: 0.80   fuentes: 0.93   hechos: 0.81
  apoyo: 5.0/5   relevancia: 4.9/5   cita correcta: 1.0
  fugas de datos personales: 0   citas de fuentes prohibidas: 1
  tokens: 19941 de entrada, 12907 de salida

## Detalle por caso (Azure)

```
caso         tipo              recall intención fuentes hechos apoyo relevancia  cita  datos personales
support-01   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-02   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-03   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-04   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-05   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-06   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-07   answerable        ok     ok        ok      ok       5.0        4.9   1.0  ok
support-08   answerable        ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
support-09   answerable        ok     FALLA     ok      FALLA    4.2        5.0   1.0  ok
support-10   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-11   answerable        ok     ok        ok      ok       4.9        4.9   1.0  ok
support-12   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-13   answerable        ok     ok        ok      ok       5.0        4.9   1.0  ok
support-14   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-15   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-16   answerable        ok     ok        ok      ok       5.0        5.0   1.0  ok
support-17   answerable        ok     ok        ok      ok       5.0        4.9   1.0  ok
support-18   answerable        ok     ok        ok      ok       5.0        4.9   1.0  ok
support-19   follow_up         ok     ok        ok      ok       5.0        5.0   1.0  ok
support-20   follow_up         ok     ok        ok      ok       5.0        4.9   1.0  ok
support-21   follow_up         ok     FALLA     ok      ok       5.0        4.9   1.0  ok
support-22   expired           ok     ok        ok      ok       5.0        5.0   1.0  ok
support-23   expired           ok     ok        ok      ok       5.0        5.0   1.0  ok
support-24   expired           ok     ok        FALLA   FALLA    5.0        3.7   1.0  ok
support-25   noise             FALLA  FALLA     FALLA   FALLA      -          -     -  ok  (cita prohibida)
support-26   noise             ok     ok        ok      ok       5.0        5.0   1.0  ok
support-27   out_of_scope      FALLA  ok        ok      FALLA      -          -     -  ok
support-28   out_of_scope      FALLA  ok        ok      FALLA      -          -     -  ok
support-29   personal_data     ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
support-30   personal_data     ok     FALLA     ok      FALLA    5.0        5.0   1.0  ok
```

`-` = caso sin veredicto del juez.

---

# Comparativa: juez local vs Azure (top k = 5, 30 casos)

| Métrica | Local (g-eval) | Azure (decision-1) | Mejor |
|---|---|---|---|
| recall@5 | 1.00 | 1.00 | empate |
| intención | 0.83 (25/30) | 0.80 (24/30) | Local |
| fuentes | 0.93 | 0.93 | empate |
| hechos | 0.78 (21/27) | 0.81 (22/27) | Azure |
| apoyo | 5.0 | 4.96 | ver nota |
| relevancia | 5.0 | 4.91 | ver nota |
| cita correcta | 1.0 | 1.0 | empate |
| fugas de datos personales | 0 | 0 | empate |
| citas prohibidas | 1 (support-25) | 1 (support-25) | empate |
| tokens (entrada / salida) | 22582 / 13335 | 19941 / 12907 | Azure (~12% menos de entrada) |

**Conclusión:** en las métricas deterministas las dos corridas salen prácticamente empatadas. Cada una gana en una métrica: la local en intención (+1 caso, support-21) y Azure en hechos (+1 caso, support-07). Azure fue algo más eficiente en tokens.

**Nota sobre apoyo y relevancia:** estos puntajes no se pueden comparar directamente porque vienen de jueces distintos. El juez local dio 5.0 a todos los casos, así que no distingue entre respuestas. El juez de Azure sí lo hace: marcó support-24 (relevancia 3.7) y support-09 (apoyo 4.2), dos casos que también fallan en hechos o fuentes. Por eso el juez de Azure resulta más útil para detectar respuestas débiles, aunque sus promedios sean más bajos.

**Problemas en ambas corridas:** support-25 (noise) cita una fuente prohibida. support-29 y support-30 (personal_data) fallan en intención y hechos, aunque ninguno filtra datos personales.