```
Data Engineering Zoomcamp - Module 2 Homework
```

```
📝 Question 1: Uncompressed File Size
Answer: 128.3 MiB
```

```
!gunzip yellow_tripdata_2020-12.csv.gz
!ls -lh yellow_tripdata_2020-12.csv
```

```
📝 Question 2: Rendered Value
Answer: green_tripdata_2020-04.csv
```

```
📝 Question 3: Yellow Taxi March 2021 Rows
Answer: 1,925,152
```

```
💻 Data Processing Script (Extraction & Helper)
```

```
import pandas as pd
Combinaciones: Homework + todo Yellow 2020
combinations = [
("yellow", 2021, 3),
("green", 2020, 1),
("green", 2020, 2),
("green", 2020, 3),
("green", 2020, 4),
("green", 2020, 5),
("green", 2020, 6),
("green", 2020, 7),
("green", 2020, 8),
("green", 2020, 9),
("green", 2020, 10),
("green", 2020, 11),
("green", 2020, 12)
] + [("yellow", 2020, m) for m in range(1, 13)]
for taxi, year, month in combinations:
if taxi == "yellow":
url = f"github.com{taxi}tripdata{year}-{str(month).zfill(2)}.csv.gz"
else:
url = f"github.com{taxi}tripdata{year}-{str(month).zfill(2)}.csv.gz"
try:
# Cargamos solo una columna para evitar errores de memoria
df = pd.read_csv(url, compression='gzip', low_memory=False, usecols=[0])
rows = len(df)
print(f"Taxi {taxi}, Año {year}, Mes {month}: {rows} filas")
except Exception as e:
print(f"Error en taxi {taxi}, año {year}, mes {month}: {e}")
def calcular_total_filas(lista_resultados, filtro_taxi="yellow", filtro_año=2020):
"""
Suma las filas de una lista de diccionarios basada en taxi y año.
"""
total = sum(
item["rows"]
for item in lista_resultados
if item["taxi"] == filtro_taxi and item["year"] == filtro_año
)
print(f"📊 Total acumulado para {filtro_taxi.upper()} en {filtro_año}: {total:,} filas.")
return total
```



```
📝 Question 4: Green Taxi 2020 Total Rows
Answer: 1,734,051
```



```
def total_rows_2020_green(data_string):
import re
# Buscamos todos los números que están al final de la frase "filas"
filas = re.findall(r'(\d+)\s+filas', data_string)
# Transformar a int (parseInt) y sumar
total = sum(int(f) for f in filas)
return total
Tu bloque de texto
results = """
Taxi green, Año 2020, Mes 1: 447770 filas
Taxi green, Año 2020, Mes 2: 398632 filas
Taxi green, Año 2020, Mes 3: 223406 filas
Taxi green, Año 2020, Mes 4: 35612 filas
Taxi green, Año 2020, Mes 5: 57360 filas
Taxi green, Año 2020, Mes 6: 63109 filas
Taxi green, Año 2020, Mes 7: 72257 filas
Taxi green, Año 2020, Mes 8: 81063 filas
Taxi green, Año 2020, Mes 9: 87987 filas
Taxi green, Año 2020, Mes 10: 95120 filas
Taxi green, Año 2020, Mes 11: 88605 filas
Taxi green, Año 2020, Mes 12: 83130 filas
"""
print(f"Total: {total_rows_2020_green(results)}")
```


```
📝 Question 5: Yellow Taxi 2020 Total Rows
Answer: 24,648,499
```


```
def total_rows_2020_yellow(data_string):
import re
# Buscamos todos los números que están al final de la frase "filas"
filas = re.findall(r'(\d+)\s+filas', data_string)
# Transformar a int (parseInt) y sumar
total = sum(int(f) for f in filas)
return total
Tu bloque de texto
results = """
Taxi yellow, Año 2020, Mes 1: 6405008 filas
Taxi yellow, Año 2020, Mes 2: 6299354 filas
Taxi yellow, Año 2020, Mes 3: 3007292 filas
Taxi yellow, Año 2020, Mes 4: 237993 filas
Taxi yellow, Año 2020, Mes 5: 348371 filas
Taxi yellow, Año 2020, Mes 6: 549760 filas
Taxi yellow, Año 2020, Mes 7: 800412 filas
Taxi yellow, Año 2020, Mes 8: 1007284 filas
Taxi yellow, Año 2020, Mes 9: 1341012 filas
Taxi yellow, Año 2020, Mes 10: 1681131 filas
Taxi yellow, Año 2020, Mes 11: 1508985 filas
Taxi yellow, Año 2020, Mes 12: 1461897 filas
"""
print(f"Total: {total_rows_2020_yellow(results)}")
```
```


```
```
📝 Question 6: Scheduling Timezone
Answer: Add a timezone property set to UTC to the schedule trigger
```
```
