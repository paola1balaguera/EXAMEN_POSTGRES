# EXAMEN POSTGRES

## SCRIPT CREACION Y POBLAMIENTO DE TABLAS

CREATE DATABASE ventas;

CREATE TABLE cliente (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100) NOT NULL,
    apellido2 VARCHAR(100),
    ciudad VARCHAR(100),
    categoría INTEGER 
);

CREATE TABLE comercial (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100) NOT NULL,
    apellido2 VARCHAR(100),
    comisión FLOAT 
);


CREATE TABLE pedido (
  id SERIAL PRIMARY KEY,
  total FLOAT NOT NULL,
  fecha DATE,
  id_cliente INT NOT NULL,
  id_comercial INT NOT NULL,
  FOREIGN KEY (id_cliente) REFERENCES cliente(id),
  FOREIGN KEY (id_comercial) REFERENCES comercial(id)
);




INSERT INTO cliente VALUES(1, 'Aarón', 'Rivero', 'Gómez', 'Almería', 100);
INSERT INTO cliente VALUES(2, 'Adela', 'Salas', 'Díaz', 'Granada', 200);
INSERT INTO cliente VALUES(3, 'Adolfo', 'Rubio', 'Flores', 'Sevilla', NULL);
INSERT INTO cliente VALUES(4, 'Adrián', 'Suárez', NULL, 'Jaén', 300);
INSERT INTO cliente VALUES(5, 'Marcos', 'Loyola', 'Méndez', 'Almería', 200);
INSERT INTO cliente VALUES(6, 'María', 'Santana', 'Moreno', 'Cádiz', 100);
INSERT INTO cliente VALUES(7, 'Pilar', 'Ruiz', NULL, 'Sevilla', 300);
INSERT INTO cliente VALUES(8, 'Pepe', 'Ruiz', 'Santana', 'Huelva', 200);
INSERT INTO cliente VALUES(9, 'Guillermo', 'López', 'Gómez', 'Granada', 225);
INSERT INTO cliente VALUES(10, 'Daniel', 'Santana', 'Loyola', 'Sevilla', 125);

INSERT INTO comercial VALUES(1, 'Daniel', 'Sáez', 'Vega', 0.15);
INSERT INTO comercial VALUES(2, 'Juan', 'Gómez', 'López', 0.13);
INSERT INTO comercial VALUES(3, 'Diego','Flores', 'Salas', 0.11);
INSERT INTO comercial VALUES(4, 'Marta','Herrera', 'Gil', 0.14);
INSERT INTO comercial VALUES(5, 'Antonio','Carretero', 'Ortega', 0.12);
INSERT INTO comercial VALUES(6, 'Manuel','Domínguez', 'Hernández', 0.13);
INSERT INTO comercial VALUES(7, 'Antonio','Vega', 'Hernández', 0.11);
INSERT INTO comercial VALUES(8, 'Alfredo','Ruiz', 'Flores', 0.05);

INSERT INTO pedido VALUES(1, 150.5, '2017-10-05', 5, 2);
INSERT INTO pedido VALUES(2, 270.65, '2016-09-10', 1, 5);
INSERT INTO pedido VALUES(3, 65.26, '2017-10-05', 2, 1);
INSERT INTO pedido VALUES(4, 110.5, '2016-08-17', 8, 3);
INSERT INTO pedido VALUES(5, 948.5, '2017-09-10', 5, 2);
INSERT INTO pedido VALUES(6, 2400.6, '2016-07-27', 7, 1);
INSERT INTO pedido VALUES(7, 5760, '2015-09-10', 2, 1);
INSERT INTO pedido VALUES(8, 1983.43, '2017-10-10', 4, 6);
INSERT INTO pedido VALUES(9, 2480.4, '2016-10-10', 8, 3);
INSERT INTO pedido VALUES(10, 250.45, '2015-06-27', 8, 2);
INSERT INTO pedido VALUES(11, 75.29, '2016-08-17', 3, 7);
INSERT INTO pedido VALUES(12, 3045.6, '2017-04-25', 2, 1);
INSERT INTO pedido VALUES(13, 545.75, '2019-01-25', 6, 1);
INSERT INTO pedido VALUES(14, 145.82, '2017-02-02', 6, 1);
INSERT INTO pedido VALUES(15, 370.   , '2019-03-11', 1, 5);
INSERT INTO pedido VALUES(16, 2389.23, '2019-03-11', 1, 5); 

## CONSULTAS SOBRE UNA TABLA

### 1. Devuelve un listado con todos los pedidos que se han realizado. Los pedidos deben estar ordenados por la fecha de realización, mostrando en primer lugar los pedidos más recientes.

```sql
SELECT id AS "PEDIDO", fecha AS "FECHA" FROM pedido
ORDER BY fecha DESC 
```

RESULTADO

| PEDIDO | FECHA      |
|--------|------------|
| 16     | 2019-03-11 |
| 15     | 2019-03-11 |
| 13     | 2019-01-25 |
| 8      | 2017-10-10 |
| 1      | 2017-10-05 |
| 3      | 2017-10-05 |
| 5      | 2017-09-10 |
| 12     | 2017-04-25 |
| 14     | 2017-02-02 |
| 9      | 2016-10-10 |
| 2      | 2016-09-10 |
| 11     | 2016-08-17 |
| 4      | 2016-08-17 |
| 6      | 2016-07-27 |
| 7      | 2015-09-10 |
| 10     | 2015-06-27 |

### 2. Devuelve todos los datos de los dos pedidos de mayor valor.

``` sql 
SELECT * FROM pedido
ORDER BY total DESC
```

RESULTADO

| Pedido | Total  | Fecha       | Cliente | Comercial |
|--------|--------|-------------|---------|-----------|
| 7      | 5760   | 2015-09-10  | 2       | 1         |
| 12     | 3045.6 | 2017-04-25  | 2       | 1         |
| 9      | 2480.4 | 2016-10-10  | 8       | 3         |
| 6      | 2400.6 | 2016-07-27  | 7       | 1         |
| 16     | 2389.23| 2019-03-11  | 1       | 5         |
| 8      | 1983.43| 2017-10-10  | 4       | 6         |
| 5      | 948.5  | 2017-09-10  | 5       | 2         |
| 13     | 545.75 | 2019-01-25  | 6       | 1         |
| 15     | 370    | 2019-03-11  | 1       | 5         |
| 2      | 270.65 | 2016-09-10  | 1       | 5         |
| 10     | 250.45 | 2015-06-27  | 8       | 2         |
| 1      | 150.5  | 2017-10-05  | 5       | 2         |
| 14     | 145.82 | 2017-02-02  | 6       | 1         |
| 4      | 110.5  | 2016-08-17  | 8       | 3         |
| 11     | 75.29  | 2016-08-17  | 3       | 7         |
| 3      | 65.26  | 2017-10-05  | 2       | 1         |


### 3. Devuelve un listado con los identificadores de los clientes que han realizado algún pedido. Tenga en cuenta que no debe mostrar identificadores que estén repetidos.

``` sql 
SELECT id FROM pedido
WHERE id IS NULL;
```


RESULTADO

| ID |
|----|

### 4. Devuelve un listado de todos los pedidos que se realizaron durante el año 2017, cuya cantidad total sea superior a 500€.

``` sql 
SELECT id from pedido
WHERE fecha BETWEEN '2017-1-1' AND '2017-12-31' AND total > 500;
```

RESULTADO

| ID |
|----|
| 5  |
| 8  |
| 12 |


### 5. Devuelve un listado con el nombre y los apellidos de los comerciales que tienen una comisión entre 0.05 y 0.11.

``` sql 
SELECT CONCAT(nombre, ' ', apellido1) AS "NOMBRE" FROM comercial
WHERE comisión BETWEEN 0.05 AND 0.11;
```


RESULTADO

| Nombre        |
|---------------|
| Diego Flores  |
| Antonio Vega  |
| Alfredo Ruiz  |

### 6.Devuelve el valor de la comisión de mayor valor que existe en la tabla comercial.

``` sql 
SELECT MAX(comisión) AS "COMISION" FROM comercial;
```

RESULTADO

| Comision |
|----------|
| 0.15     |


### 7. Devuelve el identificador, nombre y primer apellido de aquellos clientes cuyo segundo apellido no es NULL. El listado deberá estar ordenado alfabéticamente por apellidos y nombre.

``` sql 
SELECT id AS "ID", CONCAT(nombre,' ',apellido1) AS "NOMBRE" FROM cliente
WHERE apellido2 IS NOT NULL;
```

RESULTADO

| ID  | Nombre            |
|-----|-------------------|
| 6   | María Santana     |
| 1   | Aarón Rivero      |
| 2   | Adela Salas       |
| 3   | Adolfo Rubio      |
| 5   | Marcos Loyola     |
| 8   | Pepe Ruiz         |
| 9   | Guillermo López   |
| 10  | Daniel Santana    |


### 8. Devuelve un listado de los nombres de los clientes que empiezan por A y terminan por n y también los nombres que empiezan por P. El listado deberá estar ordenado alfabéticamente.

``` sql 
SELECT CONCAT(nombre, ' ',apellido2) AS "NOMBRE" FROM cliente
WHERE SUBSTRING(nombre, 1, 1) = 'A' AND SUBSTRING(nombre,LENGTH(nombre),LENGTH(nombre)) = 'n';
```

RESULTADO

| Nombre         |
|----------------|
| Aarón Gómez    |
| Adrián         |


### 9. Devuelve un listado de los nombres de los clientes que no empiezan por A. El listado deberá estar ordenado alfabéticamente.

``` sql 
SELECT CONCAT(nombre, ' ',apellido2) AS "NOMBRE" FROM cliente
WHERE NOT SUBSTRING(nombre, 1, 1) ='A';
```

RESULTADO

| Nombre          |
|-----------------|
| María Moreno    |
| Marcos Méndez   |
| Pilar           |
| Pepe Santana    |
| Guillermo Gómez |
| Daniel Loyola   |

### 10. Devuelve un listado con los nombres de los comerciales que terminan por el o o. Tenga en cuenta que se deberán eliminar los nombres repetidos.

``` sql 
SELECT DISTINCT CONCAT(nombre, ' ', apellido1, ' ', apellido2) AS "NOMBRE"
FROM comercial
WHERE nombre LIKE '%o' OR nombre LIKE '%el';
```

RESULTADO

| Nombre                       |
|------------------------------|
| Daniel Sáez Vega             |
| Antonio Vega Hernández       |
| Diego Flores Salas           |
| Alfredo Ruiz Flores          |
| Manuel Domínguez Hernández   |
| Antonio Carretero Ortega     |


## Consultas multitabla (Composición interna)

### 1. Devuelve un listado con el identificador, nombre y los apellidos de todos los clientes que han realizado algún pedido. El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.

``` sql 
SELECT cliente.id, CONCAT(nombre,' ', apellido1,' ', apellido2) AS "NOMBRE" FROM cliente
JOIN pedido ON cliente.id = pedido.id_cliente
WHERE total<>0
GROUP BY cliente.id
ORDER BY NOMBRE ASC
```

RESULTADO

| ID  | Nombre                |
|-----|-----------------------|
| 1   | Aarón Rivero Gómez    |
| 2   | Adela Salas Díaz      |
| 3   | Adolfo Rubio Flores   |
| 4   | Adrián Suárez         |
| 5   | Marcos Loyola Méndez  |
| 6   | María Santana Moreno  |
| 7   | Pepe Ruiz Santana     |
| 8   | Pilar Ruiz            |


### 2. Devuelve un listado que muestre todos los pedidos que ha realizado cada cliente. El resultado debe mostrar todos los datos de los pedidos y del cliente. El listado debe mostrar los datos de los clientes ordenados alfabéticamente.

``` sql 
SELECT c.id AS id_cliente, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_cliente,
       p.id AS id_pedido, p.total AS total_pedido, p.fecha AS fecha_pedido
FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
ORDER BY nombre_cliente;
```

RESULTADO

| id_cliente | nombre_cliente       | id_pedido | total_pedido | fecha_pedido |
|------------|----------------------|-----------|--------------|--------------|
| 1          | Aarón Rivero Gómez   | 1         | 150.5        | 2017-10-05   |
| 1          | Aarón Rivero Gómez   | 2         | 270.65       | 2016-09-10   |
| 1          | Aarón Rivero Gómez   | 3         | 65.26        | 2017-10-05   |
| 2          | Adela Salas Díaz     | 4         | 110.5        | 2016-08-17   |
| 2          | Adela Salas Díaz     | 5         | 948.5        | 2017-09-10   |
| 2          | Adela Salas Díaz     | 6         | 2400.6       | 2016-07-27   |
| 2          | Adela Salas Díaz     | 7         | 5760         | 2015-09-10   |
| 2          | Adela Salas Díaz     | 12        | 3045.6       | 2017-04-25   |
| 2          | Adela Salas Díaz     | 13        | 545.75       | 2019-01-25   |
| 2          | Adela Salas Díaz     | 14        | 145.82       | 2017-02-02   |
| 3          | Adolfo Rubio Flores  | 11        | 75.29        | 2016-08-17   |
| 4          | Adrián Suárez        | 8         | 1983.43      | 2017-10-10   |
| 5          | Marcos Loyola Méndez | 5        | 948.5        | 2017-09-10   |
| 5          | Marcos Loyola Méndez | 15        | 370          | 2019-03-11   |
| 6          | María Santana Moreno | 13        | 545.75       | 2019-01-25   |
| 6          | María Santana Moreno | 14        | 145.82       | 2017-02-02   |
| 8          | Pepe Ruiz Santana    | 10        | 250.45       | 2015-06-27   |
| 8          | Pepe Ruiz Santana    | 9         | 2480.4       | 2016-10-10   |
| 8          | Pepe Ruiz Santana    | 15        | 370          | 2019-03-11   |
| 8          | Pepe Ruiz Santana    | 4         | 110.5        | 2016-08-17   |
| 7          | Pilar Ruiz           | 6         | 2400.6       | 2016-07-27   |

### 3. Devuelve un listado que muestre todos los pedidos en los que ha participado un comercial. <br> El resultado debe mostrar todos los datos de los pedidos y de los comerciales. <br> El listado debe mostrar los datos de los comerciales ordenados alfabéticamente.

``` sql 
SELECT c.id AS id_comercial, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_comercial,
       p.id AS id_pedido, p.total AS total_pedido, p.fecha AS fecha_pedido
FROM comercial c
JOIN pedido p ON c.id = p.id_comercial
ORDER BY nombre_comercial;
```

RESULTADO

| id_comercial | nombre_comercial           | id_pedido | total_pedido | fecha_pedido |
|--------------|----------------------------|-----------|--------------|--------------|
| 5            | Antonio Carretero Ortega   | 16        | 2389.23      | 2019-03-11   |
| 5            | Antonio Carretero Ortega   | 15        | 370          | 2019-03-11   |
| 5            | Antonio Carretero Ortega   | 2         | 270.65       | 2016-09-10   |
| 7            | Antonio Vega Hernández     | 11        | 75.29        | 2016-08-17   |
| 1            | Daniel Sáez Vega           | 7         | 5760         | 2015-09-10   |
| 1            | Daniel Sáez Vega           | 14        | 145.82       | 2017-02-02   |
| 1            | Daniel Sáez Vega           | 13        | 545.75       | 2019-01-25   |
| 1            | Daniel Sáez Vega           | 12        | 3045.6       | 2017-04-25   |
| 1            | Daniel Sáez Vega           | 3         | 65.26        | 2017-10-05   |
| 1            | Daniel Sáez Vega           | 6         | 2400.6       | 2016-07-27   |
| 3            | Diego Flores Salas         | 9         | 2480.4       | 2016-10-10   |
| 3            | Diego Flores Salas         | 4         | 110.5        | 2016-08-17   |
| 2            | Juan Gómez López           | 10        | 250.45       | 2015-06-27   |
| 2            | Juan Gómez López           | 1         | 150.5        | 2017-10-05   |
| 2            | Juan Gómez López           | 5         | 948.5        | 2017-09-10   |
| 6            | Manuel Domínguez Hernández | 8         | 1983.43      | 2017-10-10   |

### 4. Devuelve un listado que muestre todos los clientes, con todos los pedidos que han realizado y con los datos de los comerciales asociados a cada pedido.

``` sql
SELECT c.id AS id_cliente, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_cliente,
       p.id AS id_pedido, p.total AS total_pedido, p.fecha AS fecha_pedido,
       CONCAT(co.nombre, ' ', co.apellido1, ' ', co.apellido2) AS nombre_comercial
FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
JOIN comercial co ON p.id_comercial = co.id
ORDER BY nombre_cliente, nombre_comercial;
```

RESULTADO

| id_cliente | nombre_cliente       | id_pedido | total_pedido | fecha_pedido | nombre_comercial           |
|------------|----------------------|-----------|--------------|--------------|----------------------------|
| 1          | Aarón Rivero Gómez   | 16        | 2389.23      | 2019-03-11   | Antonio Carretero Ortega   |
| 1          | Aarón Rivero Gómez   | 2         | 270.65       | 2016-09-10   | Antonio Carretero Ortega   |
| 1          | Aarón Rivero Gómez   | 15        | 370          | 2019-03-11   | Antonio Carretero Ortega   |
| 2          | Adela Salas Díaz     | 12        | 3045.6       | 2017-04-25   | Daniel Sáez Vega           |
| 2          | Adela Salas Díaz     | 3         | 65.26        | 2017-10-05   | Daniel Sáez Vega           |
| 2          | Adela Salas Díaz     | 7         | 5760         | 2015-09-10   | Daniel Sáez Vega           |
| 3          | Adolfo Rubio Flores  | 11        | 75.29        | 2016-08-17   | Antonio Vega Hernández     |
| 4          | Adrián Suárez        | 8         | 1983.43      | 2017-10-10   | Manuel Domínguez Hernández |
| 5          | Marcos Loyola Méndez | 1         | 150.5        | 2017-10-05   | Juan Gómez López           |
| 5          | Marcos Loyola Méndez | 5         | 948.5        | 2017-09-10   | Juan Gómez López           |
| 6          | María Santana Moreno | 13        | 545.75       | 2019-01-25   | Daniel Sáez Vega           |
| 6          | María Santana Moreno | 14        | 145.82       | 2017-02-02   | Daniel Sáez Vega           |
| 8          | Pepe Ruiz Santana    | 9         | 2480.4       | 2016-10-10   | Diego Flores Salas         |
| 8          | Pepe Ruiz Santana    | 4         | 110.5        | 2016-08-17   | Diego Flores Salas         |
| 8          | Pepe Ruiz Santana    | 10        | 250.45       | 2015-06-27   | Juan Gómez López           |
| 7          | Pilar Ruiz           | 6         | 2400.6       | 2016-07-27   | Daniel Sáez Vega           |



### 5. Devuelve un listado de todos los clientes que realizaron un pedido durante el año 2017, cuya cantidad esté entre 300 € y 1000 €.

``` sql
SELECT nombre AS "NOMBRE", apellido1 AS "APELLIDO" FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
WHERE total > 300 AND total < 1000;
```

RESULTADO

| NOMBRE | APELLIDO |
|--------|----------|
| Aarón  | Rivero   |
| Marcos | Loyola   |
| María  | Santana  |

### 6. Devuelve el nombre y los apellidos de todos los comerciales que ha
participado en algún pedido realizado por María Santana Moreno.

``` sql
SELECT CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS "NOMBRE" FROM comercial co
JOIN pedido p ON co.id = p.id_comercial
JOIN cliente c ON p.id_cliente = c.id
WHERE co.nombre = 'María' AND co.apellido1 = 'Santana' AND co.apellido2 = 'Moreno';
```

RESULTADO

| NOMBRE               |
|----------------------|
| Daniel Sáez Vega     |

### 7. Devuelve el nombre de todos los clientes que han realizado algún pedido con el comercial Daniel Sáez Vega.

``` sql
SELECT CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS "NOMBRE"
FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
JOIN comercial co ON p.id_comercial = co.id
WHERE co.nombre = 'Daniel' AND co.apellido1 = 'Sáez' AND co.apellido2 = 'Vega';
```

RESULTADO

| NOMBRE               |
|----------------------|
| Adela Salas Díaz     |
| Pilar Ruiz           |
| Adela Salas Díaz     |
| Adela Salas Díaz     |
| María Santana Moreno |
| María Santana Moreno |

## Consultas multitabla (Composición externa)

### 1. Devuelve un listado con todos los clientes junto con los datos de los pedidos que han realizado. Este listado también debe incluir los clientes que no han realizado ningún pedido. <br> El listado debe estar ordenadoalfabéticamente por el primer apellido, segundo apellido y nombre de los clientes.

``` sql
SELECT CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_cliente,
    p.id AS id_pedido, p.total AS total_pedido, p.fecha AS fecha_pedido
FROM pedido p
LEFT JOIN cliente c ON p.id_cliente = c.id
ORDER BY nombre_cliente;
```

RESULTADO

| nombre_cliente       | id_pedido | total_pedido | fecha_pedido |
|----------------------|-----------|--------------|--------------|
| Aarón Rivero Gómez   | 16        | 2389.23      | 2019-03-11   |
| Aarón Rivero Gómez   | 2         | 270.65       | 2016-09-10   |
| Aarón Rivero Gómez   | 15        | 370          | 2019-03-11   |
| Adela Salas Díaz     | 12        | 3045.6       | 2017-04-25   |
| Adela Salas Díaz     | 3         | 65.26        | 2017-10-05   |
| Adela Salas Díaz     | 7         | 5760         | 2015-09-10   |
| Adolfo Rubio Flores  | 11        | 75.29        | 2016-08-17   |
| Adrián Suárez        | 8         | 1983.43      | 2017-10-10   |
| Marcos Loyola Méndez | 1         | 150.5        | 2017-10-05   |
| Marcos Loyola Méndez | 5         | 948.5        | 2017-09-10   |
| María Santana Moreno | 13        | 545.75       | 2019-01-25   |
| María Santana Moreno | 14        | 145.82       | 2017-02-02   |
| Pepe Ruiz Santana    | 10        | 250.45       | 2015-06-27   |
| Pepe Ruiz Santana    | 9         | 2480.4       | 2016-10-10   |
| Pepe Ruiz Santana    | 4         | 110.5        | 2016-08-17   |
| Pilar Ruiz           | 6         | 2400.6       | 2016-07-27   |


### 2. Devuelve un listado con todos los comerciales junto con los datos de los pedidos que han realizado. <br> Este listado también debe incluir los comerciales que no han realizado ningún pedido. <br> El listado debe estar ordenado alfabéticamente por el primer apellido, segundo apellido y nombre de los comerciales.

``` sql
SELECT co.id AS id_comercial, co.nombre AS nombre_comercial, co.apellido1, co.apellido2, 
       p.id AS id_pedido, p.total, p.fecha
FROM comercial co
LEFT JOIN pedido p ON co.id = p.id_comercial
ORDER BY co.apellido1, co.apellido2, co.nombre;
```

RESULTADO

| id_comercial | nombre_comercial | apellido1 | apellido2 | id_pedido | total   | fecha      |
|--------------|------------------|-----------|-----------|-----------|---------|------------|
| 5            | Antonio          | Carretero | Ortega    | 16        | 2389.23 | 2019-03-11 |
| 5            | Antonio          | Carretero | Ortega    | 2         | 270.65  | 2016-09-10 |
| 5            | Antonio          | Carretero | Ortega    | 15        | 370     | 2019-03-11 |
| 6            | Manuel           | Domínguez | Hernández | 8         | 1983.43 | 2017-10-10 |
| 3            | Diego            | Flores    | Salas     | 9         | 2480.4  | 2016-10-10 |
| 3            | Diego            | Flores    | Salas     | 4         | 110.5   | 2016-08-17 |
| 2            | Juan             | Gómez     | López     | 1         | 150.5   | 2017-10-05 |
| 2            | Juan             | Gómez     | López     | 5         | 948.5   | 2017-09-10 |
| 2            | Juan             | Gómez     | López     | 10        | 250.45  | 2015-06-27 |
| 4            | Marta            | Herrera   | Gil       |           |         |            |
| 8            | Alfredo          | Ruiz      | Flores    |           |         |            |
| 1            | Daniel           | Sáez      | Vega      | 13        | 545.75  | 2019-01-25 |
| 1            | Daniel           | Sáez      | Vega      | 14        | 145.82  | 2017-02-02 |
| 1            | Daniel           | Sáez      | Vega      | 6         | 2400.6  | 2016-07-27 |
| 1            | Daniel           | Sáez      | Vega      | 3         | 65.26   | 2017-10-05 |
| 1            | Daniel           | Sáez      | Vega      | 7         | 5760    | 2015-09-10 |
| 1            | Daniel           | Sáez      | Vega      | 12        | 3045.6  | 2017-04-25 |
| 7            | Antonio          | Vega      | Hernández | 11        | 75.29   | 2016-08-17 |

### 3. Devuelve un listado que solamente muestre los clientes que no han realizado ningún pedido.

``` sql
SELECT CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS "NOMBRE"
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE p.id IS NULL;
```

RESULTADO

| NOMBRE                |
|-----------------------|
| Daniel Santana Loyola |
| Guillermo López Gómez |

### 4. Devuelve un listado que solamente muestre los comerciales que no han realizado ningún pedido.

``` sql
SELECT co.id AS id_comercial, CONCAT(co.nombre, ' ', co.apellido1, ' ', co.apellido2) AS nombre_comercial
FROM comercial co
LEFT JOIN pedido p ON co.id = p.id_comercial
WHERE p.id IS NULL;
```

RESULTADO

| id_comercial | nombre_comercial    |
|--------------|---------------------|
| 8            | Alfredo Ruiz Flores |
| 4            | Marta Herrera Gil   |


### 5. Devuelve un listado con los clientes que no han realizado ningún pedido y de los comerciales que no han participado en ningún pedido. Ordene el listado alfabéticamente por los apellidos y el nombre. <br> En en listado deberá diferenciar de algún modo los clientes y los comerciales.

``` sql
SELECT 'Cliente' AS "CLASE", CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_cliente
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE p.id IS NULL
UNION
SELECT 'Comercial' AS tipo, CONCAT(co.nombre, ' ', co.apellido1, ' ', co.apellido2) AS nombre_completo
FROM comercial co
LEFT JOIN pedido p ON co.id = p.id_comercial
WHERE p.id IS NULL
ORDER BY nombre_cliente;
```

RESULTADO

| CLASE     | nombre_cliente        |
|-----------|-----------------------|
| Comercial | Alfredo Ruiz Flores   |
| Cliente   | Daniel Santana Loyola |
| Cliente   | Guillermo López Gómez |
| Comercial | Marta Herrera Gil     |


### 6. ¿Se podrían realizar las consultas anteriores con NATURAL LEFT JOIN o NATURAL RIGHT JOIN? <br> Justifique su respuesta.

RESPUESTA

```
Estas dos se usan para unir tablas, estas se unen debido a que ambas columnas tienen el mismo nombre
en las 2 tablas, pero en las consultas tenemos que hacer comparaciones y filtraciones de datos
por tal razon no es posible utilizarlo en consultas
```

## Consultas resumen


RESULTADO

### 1. Calcula la cantidad total que suman todos los pedidos que aparecen en la tabla pedido.

``` sql
SELECT SUM(total) AS "TOTAL" FROM pedido
```

| TOTAL    |
|----------|
| 20991.98 |

### 2. Calcula la cantidad media de todos los pedidos que aparecen en la tabla pedido.

``` sql
SELECT AVG(total) AS "PROMEDIO" FROM pedido
```

| PROMEDIO   |
|------------|
| 1311.99875 |

### 3. Calcula el número total de comerciales distintos que aparecen en la tabla pedido.

``` sql
SELECT COUNT(DISTINCT id_comercial) AS "TOTAL_COMERCIALES" FROM pedido;
```

| TOTAL_COMERCIALES |
|-------------------|
| 6                 |

### 4. Calcula el número total de clientes que aparecen en la tabla cliente.

``` sql
SELECT COUNT(nombre) AS "TOTAL_CLIENTES" FROM cliente;
```

| TOTAL_CLIENTES |
|----------------|
| 10             |

### 5. Calcula cuál es la mayor cantidad que aparece en la tabla pedido.

``` sql
SELECT MAX(total) AS "MAYOR_TOTAL" FROM pedido;
```

| MAYOR_TOTAL |
|-------------|
| 5760        |

### 6. Calcula cuál es la menor cantidad que aparece en la tabla pedido.

``` sql
SELECT MIN(total) AS "MENOR_TOTAL" FROM pedido;
```

| MENOR_TOTAL |
|-------------|
| 65.26       |


### 7. Calcula cuál es el valor máximo de categoría para cada una de las ciudades que aparece en la tabla cliente.

``` sql
SELECT MAX(categoría) AS "VALOR_MAXIMO_CATEGORIA" FROM cliente
GROUP BY ciudad;
```

| VALOR_MAXIMO_CATEGORIA |
|------------------------|
| 200                    |
| 200                    |
| 300                    |
| 225                    |
| 300                    |
| 100                    |


### 8. Calcula cuál es el máximo valor de los pedidos realizados durante el mismo día para cada uno de los clientes. Es decir, el mismo cliente puede haber realizado  varios pedidos de diferentes cantidades el mismo día. Se pide que se calcule cuál es el pedido de máximo valor para cada uno de los días en los que un cliente ha realizado un pedido. Muestra el identificador del cliente, nombre, apellidos, la fecha y el valor de la cantidad.

``` sql
SELECT MAX(total) AS valor_Maximo_Pedido , fecha FROM pedido
GROUP BY fecha;
```

| valor_maximo_pedido | fecha      |
|---------------------|------------|
| 545.75              | 2019-01-25 |
| 145.82              | 2017-02-02 |
| 3045.6              | 2017-04-25 |
| 2480.4              | 2016-10-10 |
| 2400.6              | 2016-07-27 |
| 270.65              | 2016-09-10 |
| 110.5               | 2016-08-17 |
| 250.45              | 2015-06-27 |
| 948.5               | 2017-09-10 |
| 2389.23             | 2019-03-11 |
| 1983.43             | 2017-10-10 |
| 5760                | 2015-09-10 |
| 150.5               | 2017-10-05 |


### 9. Calcula cuál es el máximo valor de los pedidos realizados durante el mismo día para cada uno de los clientes, teniendo en cuenta que sólo queremos mostrar aquellos pedidos que superen la cantidad de 2000 €.

``` sql
SELECT MAX(total) AS valor_Maximo_Pedido , fecha FROM pedido
WHERE total > 2000
GROUP BY fecha;
```

| valor_maximo_pedido | fecha      |
|---------------------|------------|
| 3045.6              | 2017-04-25 |
| 2480.4              | 2016-10-10 |
| 2400.6              | 2016-07-27 |
| 2389.23             | 2019-03-11 |
| 5760                | 2015-09-10 |


### 10.Calcula el máximo valor de los pedidos realizados para cada uno de los comerciales durante la fecha 2016-08-17. Muestra el identificador del comercial, nombre, apellidos y total.

``` sql
SELECT co.id, co.nombre, co.apellido1,co.apellido2 FROM comercial co
JOIN pedido p ON co.id = p.id_comercial
WHERE fecha = '2016-08-17' 
```

| id | nombre  | apellido1 | apellido2 |
|----|---------|-----------|-----------|
| 3  | Diego   | Flores    | Salas     |
| 7  | Antonio | Vega      | Hernández |


### 11. Devuelve un listado con el identificador de cliente, nombre y apellidos y el número total de pedidos que ha realizado cada uno de clientes. Tenga en cuenta que pueden existir clientes que no han realizado ningún pedido. Estos clientes también deben aparecer en el listado indicando que el número de pedidos realizados es 0.

``` sql
SELECT c.id AS id_cliente, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_completo, COUNT(p.id) AS total_pedidos
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
GROUP BY c.id;
```
| id_cliente | nombre_completo       | total_pedidos |
|------------|-----------------------|---------------|
| 4          | Adrián Suárez         | 1             |
| 10         | Daniel Santana Loyola | 0             |
| 6          | María Santana Moreno  | 2             |
| 2          | Adela Salas Díaz      | 3             |
| 9          | Guillermo López Gómez | 0             |
| 7          | Pilar Ruiz            | 1             |
| 3          | Adolfo Rubio Flores   | 1             |
| 1          | Aarón Rivero Gómez    | 3             |
| 5          | Marcos Loyola Méndez  | 2             |
| 8          | Pepe Ruiz Santana     | 3             |


### 12. Devuelve un listado con el identificador de cliente, nombre y apellidos y el número total de pedidos que ha realizado cada uno de clientes durante el año 2017.

``` sql
SELECT c.id AS id_cliente, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_completo, COUNT(p.id) AS total_pedidos_2017
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE YEAR(p.fecha) = '2017'
GROUP BY c.id;
```

  +----+--------+-----------+-----------+------------+---------------+
  | id | nombre | apellido1 | apellido2 | fecha      | total_pedidos |
  +----+--------+-----------+-----------+------------+---------------+
  |  5 | Marcos | Loyola    | Méndez    | 2017-10-05 |             1 |
  |  2 | Adela  | Salas     | Díaz      | 2017-10-05 |             1 |
  |  5 | Marcos | Loyola    | Méndez    | 2017-09-10 |             1 |
  |  4 | Adrián | Suárez    | NULL      | 2017-10-10 |             1 |
  |  2 | Adela  | Salas     | Díaz      | 2017-04-25 |             1 |
  |  6 | María  | Santana   | Moreno    | 2017-02-02 |             1 |
  +----+--------+-----------+-----------+------------+---------------+

### 13. Devuelve un listado que muestre el identificador de cliente, nombre, primer apellido y el valor de la máxima cantidad del pedido realizado por cada uno de los clientes. El resultado debe mostrar aquellos clientes que no han realizado ningún pedido indicando que la máxima cantidad de sus pedidos realizados es 0. Puede hacer uso de la función IFNULL.

``` sql
SELECT c.id AS "ID", CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS "NOMBRE",
    COALESCE(MAX(p.total), 0) AS "MAXIMA_CANTIDAD_PEDIDO"
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
GROUP BY c.id;
```

| ID | NOMBRE                | MAXIMA_CANTIDAD_PEDIDO |
|----|-----------------------|------------------------|
| 4  | Adrián Suárez         | 1983.43                |
| 10 | Daniel Santana Loyola |                        |
| 6  | María Santana Moreno  | 545.75                 |
| 2  | Adela Salas Díaz      | 5760                   |
| 9  | Guillermo López Gómez |                        |
| 7  | Pilar Ruiz            | 2400.6                 |
| 3  | Adolfo Rubio Flores   | 75.29                  |
| 1  | Aarón Rivero Gómez    | 2389.23                |
| 5  | Marcos Loyola Méndez  | 948.5                  |
| 8  | Pepe Ruiz Santana     | 2480.4                 |


### 14. Devuelve cuál ha sido el pedido de máximo valor que se ha realizado cada año.


``` sql
SELECT DATE_PART('Year', fecha) AS año, MAX(total) AS maximo_valor_pedido
FROM pedido
GROUP BY DATE_PART('Year', fecha);
```

| año   | valor_maximo_pedido |
|-------|----------------------|
| 2019  | 2389.23              |
| 2015  | 5760                 |
| 2016  | 2480.4               |
| 2017  | 3045.6               |

### 15. Devuelve el número total de pedidos que se han realizado cada año.

``` sql
SELECT SUM(total) AS TOTAL_ANUAL FROM pedido
GROUP BY YEAR(fecha);
```

| total_anual |
|-------------|
| 3304.98     |
| 6010.45     |
| 5337.44     |
| 6339.11     |

## CON OPERADORES BASICOS DE COMPARACION

### 1. Devuelve un listado con todos los pedidos que ha realizado Adela Salas Díaz. (Sin utilizar INNER JOIN).

``` sql
SELECT * FROM pedido 
WHERE id_cliente = (
    SELECT id 
    FROM cliente 
    WHERE nombre = 'Adela' AND apellido1 = 'Salas' AND apellido2 = 'Díaz'
);
```

| id | total  | fecha      | id_cliente | id_comercial |
|----|--------|------------|------------|--------------|
| 3  | 65.26  | 2017-10-05 | 2          | 1            |
| 7  | 5760   | 2015-09-10 | 2          | 1            |
| 12 | 3045.6 | 2017-04-25 | 2          | 1            |


### 2. Devuelve el número de pedidos en los que ha participado el comercial Daniel Sáez Vega. (Sin utilizar INNER JOIN)

``` sql
SELECT COUNT(*) FROM pedido 
WHERE id_comercial = (
    SELECT id 
    FROM comercial 
    WHERE nombre = 'Daniel' AND apellido1 = 'Sáez' AND apellido2 = 'Vega'
);
```

| count |
|-------|
| 6     |


### 3. Devuelve los datos del cliente que realizó el pedido más caro en el año 2019. (Sin utilizar INNER JOIN)

``` sql
SELECT * FROM cliente 
WHERE id = (
    SELECT id_cliente 
    FROM pedido 
    WHERE fecha BETWEEN '2019-01-01' AND '2019-12-31' 
    ORDER BY total DESC 
    LIMIT 1
);
```

| id | nombre | apellido1 | apellido2 | ciudad  | categoría |
|----|--------|-----------|-----------|---------|-----------|
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       |


### 4.Devuelve la fecha y la cantidad del pedido de menor valor realizado por el cliente Pepe Ruiz Santana.

``` sql
SELECT p.fecha, p.total
FROM pedido p
WHERE id_cliente = (
    SELECT id 
    FROM cliente 
    WHERE nombre = 'Pepe' AND apellido1 = 'Ruiz' AND apellido2 = 'Santana'
)
ORDER BY p.total ASC
LIMIT 1;
```

| fecha      | total |
|------------|-------|
| 2016-08-17 | 110.5 |


### 5. Devuelve un listado con los datos de los clientes y los pedidos, de todos los clientes que han realizado un pedido durante el año 2017 con un valor mayor o igual al valor medio de los pedidos realizados durante ese mismo año.

``` sql
SELECT c.*, p.* 
FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
WHERE c.id = p.id_cliente 
AND p.fecha BETWEEN '2017-01-01' AND '2017-12-31' 
AND p.total >= (
    SELECT AVG(total) 
    FROM pedido
    WHERE fecha BETWEEN '2017-01-01' AND '2017-12-31'
);
```

| clienteID | nombre | apellido1 | apellido2 | ciudad  | categoría | pedidoID | total   | fecha      | id_cliente | id_comercial |
|-----------|--------|-----------|-----------|---------|-----------|----------|---------|------------|------------|--------------|
| 2         | Adela  | Salas     | Díaz      | Granada | 200       | 12       | 3045.6  | 2017-04-25 | 2          | 1            |
| 4         | Adrián | Suárez    |           | Jaén    | 300       | 8        | 1983.43 | 2017-10-10 | 4          | 6            |


## Subconsultas con ALL y ANY

### 1. Devuelve el pedido más caro que existe en la tabla pedido si hacer uso de MAX, ORDER BY ni LIMIT.

``` sql
SELECT * FROM pedido p1 
WHERE NOT EXISTS (
    SELECT * 
    FROM pedido p2 
    WHERE p2.total > p1.total
);
```

| id | total | fecha      | id_cliente | id_comercial |
|----|-------|------------|------------|--------------|
| 7  | 5760  | 2015-09-10 | 2          | 1            |


### 2. Devuelve el número de pedidos en los que ha participado el comercial Daniel Sáez Vega. (Sin utilizar INNER JOIN)

``` sql
SELECT * FROM cliente 
WHERE id NOT IN (
    SELECT id_cliente 
    FROM pedido
);
```

| id | nombre    | apellido1 | apellido2 | ciudad  | categoría |
|----|-----------|-----------|-----------|---------|-----------|
| 9  | Guillermo | López     | Gómez     | Granada | 225       |
| 10 | Daniel    | Santana   | Loyola    | Sevilla | 125       |


### 3. Devuelve los datos del cliente que realizó el pedido más caro en el año 2019. (Sin utilizar INNER JOIN)

``` sql
SELECT * FROM comercial 
WHERE id NOT IN (
    SELECT id_comercial 
    FROM pedido
);
```

| id | nombre  | apellido1 | apellido2 | comisión |
|----|---------|-----------|-----------|----------|
| 4  | Marta   | Herrera   | Gil       | 0.14     |
| 8  | Alfredo | Ruiz      | Flores    | 0.05     |

### 4. Devuelve la fecha y la cantidad del pedido de menor valor realizado por el cliente Pepe Ruiz Santana.

``` sql
SELECT MIN(total) AS menor_valor, fecha
FROM pedido
JOIN cliente ON pedido.id_cliente = cliente.id
WHERE cliente.nombre = 'Pepe' AND cliente.apellido1 = 'Ruiz' AND cliente.apellido2 = 'Santana'
GROUP BY pedido.fecha;
```
| menor_valor | fecha      |
|-------------|------------|
| 110.5       | 2016-08-17 |
| 250.45      | 2015-06-27 |
| 2480.4      | 2016-10-10 |

### 5. Devuelve un listado con los datos de los clientes y los pedidos, de todos los clientes que han realizado un pedido durante el año 2017 con un valor mayor o igual al valor medio de los pedidos realizados durante ese mismo año.

``` sql
--
SELECT c.id AS id_cliente, CONCAT(c.nombre, ' ', c.apellido1, ' ', c.apellido2) AS nombre_cliente,
       p.id AS id_pedido, p.total, p.fecha
FROM cliente c
JOIN pedido p ON c.id = p.id_cliente
WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31'
  AND p.total >= (SELECT AVG(total) FROM pedido WHERE DATE_PART('Year', fecha) = 2017);
  ```
| id_cliente | nombre_cliente   | id_pedido | total   | fecha      |
|------------|------------------|-----------|---------|------------|
| 2          | Adela Salas Díaz | 12        | 3045.6  | 2017-04-25 |
| 4          | Adrián Suárez    | 8         | 1983.43 | 2017-10-10 |


## Subconsultas con IN y NOT IN

### 1. Devuelve un listado de los clientes que no han realizado ningún pedido. (Utilizando IN o NOT IN).

``` sql
SELECT * FROM cliente 
WHERE id NOT IN (
    SELECT id_cliente 
    FROM pedido
);
  ```


| id | nombre    | apellido1 | apellido2 | ciudad   | categoría |
|----|-----------|-----------|-----------|----------|-----------|
| 1  | Guillermo | López     | Gómez     | Granada  | 225       |
| 2  | Daniel    | Santana   | Loyola    | Sevilla  | 125       |

### 2.Devuelve un listado de los comerciales que no han realizado ningún pedido. (Utilizando IN o NOT IN).

``` sql
SELECT * FROM comercial 
WHERE id NOT IN (
    SELECT id_comercial 
    FROM pedido
);
  ```

| id | nombre  | apellido1 | apellido2 | comisión |
|----|---------|-----------|-----------|----------|
| 1  | Marta   | Herrera   | Gil       | 0.14     |
| 2  | Alfredo | Ruiz      | Flores    | 0.05     |


## Subconsultas con EXISTS y NOT EXISTS

### 1.Devuelve un listado de los clientes que no han realizado ningún pedido. (Utilizando EXISTS o NOT EXISTS).

``` sql
SELECT * FROM cliente c
WHERE NOT EXISTS (
    SELECT * 
    FROM pedido p
    WHERE p.id_cliente = c.id
);
  ```

| id | nombre    | apellido1 | apellido2 | ciudad   | categoría |
|----|-----------|-----------|-----------|----------|-----------|
| 1  | Daniel    | Santana   | Loyola    | Sevilla  | 125       |
| 2  | Guillermo | López     | Gómez     | Granada  | 225       |

### 2. Devuelve un listado de los comerciales que no han realizado ningún pedido. (Utilizando EXISTS o NOT EXISTS).

``` sql
SELECT * FROM comercial c
WHERE NOT EXISTS (
    SELECT * 
    FROM pedido p
    WHERE p.id_comercial = c.id
);
  ```

| id | nombre  | apellido1 | apellido2 | comisión |
|----|---------|-----------|-----------|----------|
| 1  | Alfredo | Ruiz      | Flores    | 0.05     |
| 2  | Marta   | Herrera   | Gil       | 0.14     |