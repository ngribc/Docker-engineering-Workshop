# Docker-engineering-Workshop
Docker Workshop

In this homework we'll prepare the environment and practice Docker and SQL

When submitting your homework, you will also need to include a link to your GitHub repository or other public code-hosting site.

This repository should contain the code for solving the homework.

When your solution has SQL or shell commands and not code (e.g. python files) file format, include them directly in the README file of your repository.

Pregunta 1:
docker run -it --entrypoint bash python:3.13
Unable to find image 'python:3.13' locally
3.13: Pulling from library/python
Digest: sha256:c8b03b4e98b39cfb180a5ea13ae5ee39039a8f75ccf52fe6d5c216eed6e1be1d
Status: Downloaded newer image for python:3.13
root@2bb99b287ea5:/# pip --version
pip 25.3 from /usr/local/lib/python3.13/site-packages/pip (python 3.13)
root@2bb99b287ea5:/# 

Pregunta 2: db:5432  

Pregunta 3: Viajes cortos (Distancia ≤ 1 milla)
Esta consulta cuenta los viajes realizados en noviembre de 2025 cuya distancia fue menor o igual a 1 milla.

SELECT 
    count(1)
FROM 
    green_tripdata2025
WHERE 
    lpep_pickup_datetime >= '2025-11-01 00:00:00' 
    AND lpep_pickup_datetime < '2025-12-01 00:00:00'
    AND trip_distance <= 1;

Pregunta 4: Día con el viaje más largo
Buscar el día con la distancia máxima, filtrando errores de datos (viajes de más de 100 millas).

SELECT 
    CAST(lpep_pickup_datetime AS DATE) AS pickup_day,
    MAX(trip_distance) AS max_dist
FROM 
    green_tripdata2025
WHERE 
    trip_distance < 100
GROUP BY 
    1
ORDER BY 
    max_dist DESC
LIMIT 1;


Pregunta 5: Zona con mayor monto total el 18 de noviembre
Sumar el total_amount agrupado por zona de inicio para ese día específico.

SELECT 
    z."Zone",
    SUM(t.total_amount) AS sum_total
FROM 
    green_tripdata2025 t
JOIN 
    zones z ON t."PULocationID" = z."LocationID"
WHERE 
    CAST(t.lpep_pickup_datetime AS DATE) = '2025-11-18'
GROUP BY 
    1
ORDER BY 
    sum_total DESC
LIMIT 1;

Pregunta 6: Propina más grande desde "East Harlem North"
Buscar la zona de destino (DOLocationID) que tuvo la propina individual más alta partiendo desde East Harlem North.

SELECT 
    zdo."Zone" AS dropoff_zone,
    MAX(t.tip_amount) AS max_tip
FROM 
    green_tripdata2025 t
JOIN 
    zones zpu ON t."PULocationID" = zpu."LocationID"
JOIN 
    zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE 
    zpu."Zone" = 'East Harlem North'
    AND t.lpep_pickup_datetime >= '2025-11-01 00:00:00'
    AND t.lpep_pickup_datetime < '2025-12-01 00:00:00'
GROUP BY 
    1
ORDER BY 
    max_tip DESC
LIMIT 1;

Pregunta 7: terraform init, terraform apply -auto-approve, terraform destroy 

RESUME:
p1) The version of pip in the python:3.13 image is 24.3.1. 
p2) db:5432 
p3) 8007
p4) "2025-11-14"	88.03
p5) East Harlem North 9281.919999999991
p6) Yorkville West
p7) terraform init, terraform apply -auto-approve, terraform destroy 