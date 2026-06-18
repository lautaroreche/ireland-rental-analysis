# NOTES

---

## Key decisions
- **Nivel geográfico:** voy por nivel condado. La columna
  Location mezcla condados, distritos y barrios. Me quedo solo con
  filas de condado entero para tener comparación limpia. Descarto sub-zonas.
- Como STATISTIC Label tiene un mismo valor para todos los registros se decide eliminar la columna en la fase de limpieza

---

## Open problems / doubts
- [x] Ver si STATISTIC Label tiene más de un valor
- [ ] Confirmar cómo conviven condados y sub-zonas en Location
- [ ] Revisar los 7 valores de Number of Bedrooms y 6 de Property Type para confirmar si hay categorías que abarquen otras como totales agregados (all, portions)

---

## Findings
- STATISTIC Label tiene un mismo valor para todos los registros que es "RTB Average Monthly Rent Report"
- Cada Location tiene exactamente 2310 registros posibles, que son los resultados de combinar Quarter, Number of Bedrooms y Property Type independientemente de si tienen un valor o si están en blanco o nulos.
- Hay categorías dentro de los campos que abarcan otras categorías, ya que son rangos o totales como por ejemplo en el campo Property Type la selección "All property types" abarca otras como por ejemplo "Apartment", "Detached house" y "Other flats". Lo mismo ocurre con Number of Bedrooms ya que al seleccionar opciones como "1 to 3 bed" se solapa con las opciones de "One bed", "Two bed" y "Three bed".

---

## Logs

### 18/06/2026
- Descargué la base de datos RIQ02 de la CSO en formato CSV.
- Columnas: STATISTIC Label, Quarter, Number of Bedrooms, Property Type, Location, UNIT, VALUE.
- Detecté que el campo Location mezcla niveles geográficos, ya que el archivo es a nivel nacional y tiene datos de condado, distritos y barrios. Decidí quedarme con el nivel de condado por la escala del análisis, descartando las sub-zonas.
- 