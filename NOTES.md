# NOTES

---

## Key decisions
- Nivel geográfico: voy por nivel condado. La columna Location mezcla condados, distritos y barrios. Me quedo solo con filas de condado entero para tener comparación limpia. Descarto sub-zonas.
- Se decide eliminar las columnas STATISTIC y UNIT en la etapa de limpieza de datos ya que contienen los mismos valores para todos los registros.
- Se van a utilizar solamente los datos que contengan un nombre de condado puro en el campo Location ya que el RTB ya hizo el cálculo de promedio a nivel condado a la hora de crear la tabla.
- Se eliminan categorías agregadas en los campos Number of Bedrooms y Property Type ya que se decide dejar solamente los valores individuales para no duplicar datos.
- Se eliminan valores null dentro del campo VALUE ya que eran combinaciones sin dato oficial por parte del RTB.
- Se excluye el análisis del encarecimiento del tipo Apartment en grandes urbes para no desviar el foco del objetivo; queda registrado como posible análisis futuro (detalle en Findings).

---

## Open problems / doubts
- [x] Ver si STATISTIC Label tiene más de un valor
- [x] Confirmar cómo conviven condados y sub-zonas en Location
- [x] Revisar los 7 valores de Number of Bedrooms y 6 de Property Type para confirmar si hay categorías que abarquen otras como totales agregados (all, portions)
- [x] Confirmar si los 26 condados de Irlanda existen como valores independientes además de ser en formato "barrio - condado"

---

## Findings
- STATISTIC Label tiene un mismo valor para todos los registros que es "RTB Average Monthly Rent Report".
- Cada Location tiene exactamente 2310 registros posibles, que son los resultados de combinar Quarter, Number of Bedrooms y Property Type independientemente de si tienen un valor o si están en blanco o nulos.
- Hay categorías dentro de los campos que abarcan otras categorías, ya que son rangos o totales. Por ejemplo, en Property Type la selección "All property types" abarca todos los tipos individuales (Apartment, Detached house, Semi detached house, Terrace house y Other flats). Lo mismo ocurre en Number of Bedrooms, donde opciones como "1 to 3 bed" se solapan con "One bed", "Two bed" y "Three bed".
- Los 26 condados existen como valores independientes, así que se confirma la decisión de usar nivel geográfico de condados.
- Las semi-detached houses fueron el tipo de propiedad que más se encareció, en un 134% entre 2012 y 2025, por lo cual queda por encima del promedio general de 124%. El tipo que menos se encareció fue Apartment, con un 112,87%. La diferencia entre el primero y el último es acotada, por lo que la lectura general es que todos los tipos crecieron de forma fuerte y relativamente pareja.
- Posible análisis futuro: a nivel general Apartment es el tipo que menos se encareció en el período, pero este patrón se invierte en centros urbanos grandes como Dublin, Cork y Galway, donde Apartment pasa a ser el tipo de propiedad con mayor aumento de renta. Hipótesis: se debería a la fuerte demanda por este tipo de vivienda en grandes urbes. No verificado en este análisis; queda para un análisis individual futuro.
- El condado más económico para viviendas familiares (3+ beds) es Donegal. Hipótesis: se explicaría por su lejanía de los grandes centros urbanos y económicos. No verificado con este dataset, que solo contiene datos de renta.
- Dublin es el condado con mayor renta promedio del período y crece más que proporcionalmente frente a condados como Donegal. Esta brecha se amplía al filtrar por viviendas familiares (3+ beds). (Pendiente: cuantificar la brecha con un número concreto para cerrar la pregunta secundaria.)

---

## Logs

### 18/06/2026
- Descargué la base de datos RIQ02 de la CSO en formato CSV.
- Columnas: STATISTIC Label, Quarter, Number of Bedrooms, Property Type, Location, UNIT, VALUE.
- Detecté que el campo Location mezcla niveles geográficos, ya que el archivo es a nivel nacional y tiene datos de condado, distritos y barrios. Decidí quedarme con el nivel de condado por la escala del análisis, descartando las sub-zonas.

### 21/06/2026
- Confirmé que los 26 condados existen como valores independientes en el campo Location.

### 22/06/2026
- Limpié los datos usando Power Query. Se eliminaron las columnas STATISTIC y UNIT, se modificó el campo VALUE a tipo currency y se descartaron datos que no tengan en Location un valor que coincida exactamente con el nombre de alguno de los 26 condados de Irlanda.
- Se eliminan categorías que agrupan valores en los campos Number of Bedrooms y Property Type ya que se decide dejar solamente los valores individuales para no duplicar datos.
- Se eliminan valores null dentro del campo VALUE ya que eran combinaciones sin dato oficial por parte del RTB.
- Se separa la columna Quarter en 2, siendo una para Year y otra propiamente para Quarter.

### 24/06/2026
- Creé el dashboard en Power BI utilizando una virtual machine de Windows 11.
- Se crea la medida calculada de promedio de renta por localidad, siendo Dublin la de valor más alto por diferencia.

### 29/06/2026
- Continué con el dashboard en Power BI en un entorno Windows 11 sin utilizar virtual machine.
- Creé medidas calculadas para obtener rentas promedio, el promedio general del primer y último año y el tipo de propiedad que más se encareció.
- Detecté un posible análisis a hacer en el futuro, el cual se explica en Findings.
- Se responden las dos hipótesis principales del análisis.