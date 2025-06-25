# Comandos SQL (MySQL)

Este archivo contiene una lista de comandos SQL comunes para MySQL, organizados por categoría.

## Conexión y Administración Básica

### mysql (Cliente de línea de comandos)

**Descripción:**  
Conectarse a un servidor MySQL.

**Sintaxis:**
```bash
mysql [opciones]
```

**Opciones comunes:**
- `-h`, `--host`: Host del servidor MySQL
- `-P`, `--port`: Puerto del servidor
- `-u`, `--user`: Nombre de usuario
- `-p`, `--password`: Solicitar contraseña
- `-D`, `--database`: Base de datos a usar

**Ejemplos:**
```bash
# Conectar al servidor local
mysql -u root -p

# Conectar a servidor remoto con base de datos específica
mysql -h 192.168.1.10 -u usuario -p -D mi_base_datos

# Conectar a servidor con puerto personalizado
mysql -h localhost -P 3307 -u usuario -p
```

### mysqldump

**Descripción:**  
Herramienta para crear copias de seguridad (dumps) de bases de datos.

**Sintaxis:**
```bash
mysqldump [opciones] [base_datos] [tablas]
```

**Opciones comunes:**
- `-h`, `--host`: Host del servidor MySQL
- `-u`, `--user`: Nombre de usuario
- `-p`, `--password`: Solicitar contraseña
- `--all-databases`: Volcar todas las bases de datos
- `--no-data`: Solo estructura (sin datos)
- `--no-create-db`: No incluir sentencias CREATE DATABASE
- `--no-create-info`: No incluir sentencias CREATE TABLE

**Ejemplos:**
```bash
# Backup de una base de datos específica
mysqldump -u root -p nombre_base > backup.sql

# Backup de todas las bases de datos
mysqldump -u root -p --all-databases > full_backup.sql

# Backup solo de la estructura
mysqldump -u root -p --no-data nombre_base > estructura.sql

# Backup de tablas específicas
mysqldump -u root -p nombre_base tabla1 tabla2 > tablas_backup.sql
```

### mysqladmin

**Descripción:**  
Herramienta para administrar un servidor MySQL.

**Sintaxis:**
```bash
mysqladmin [opciones] comando [argumentos]
```

**Comandos comunes:**
- `create`: Crear una base de datos
- `drop`: Eliminar una base de datos
- `ping`: Verificar si el servidor está activo
- `status`: Mostrar estado breve del servidor
- `extended-status`: Mostrar estado extendido del servidor
- `variables`: Mostrar las variables del sistema
- `shutdown`: Apagar el servidor

**Ejemplos:**
```bash
# Crear base de datos
mysqladmin -u root -p create nueva_db

# Eliminar base de datos
mysqladmin -u root -p drop vieja_db

# Comprobar si el servidor está funcionando
mysqladmin -u root -p ping

# Ver estado del servidor
mysqladmin -u root -p status
```

## Administración de Bases de Datos

### CREATE DATABASE

**Descripción:**  
Crea una nueva base de datos.

**Sintaxis:**
```sql
CREATE DATABASE [IF NOT EXISTS] nombre_db
[CHARACTER SET charset_name]
[COLLATE collation_name];
```

**Ejemplos:**
```sql
-- Crear base de datos simple
CREATE DATABASE mi_base_datos;

-- Crear si no existe
CREATE DATABASE IF NOT EXISTS mi_base_datos;

-- Crear con juego de caracteres específico
CREATE DATABASE mi_base_datos
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
```

### SHOW DATABASES

**Descripción:**  
Muestra las bases de datos disponibles.

**Sintaxis:**
```sql
SHOW DATABASES [LIKE 'patrón'];
```

**Ejemplos:**
```sql
-- Mostrar todas las bases de datos
SHOW DATABASES;

-- Mostrar bases de datos que coincidan con un patrón
SHOW DATABASES LIKE 'test%';
```

### USE

**Descripción:**  
Selecciona una base de datos para trabajar.

**Sintaxis:**
```sql
USE nombre_db;
```

**Ejemplos:**
```sql
-- Seleccionar base de datos
USE mi_base_datos;
```

### DROP DATABASE

**Descripción:**  
Elimina una base de datos y todos sus objetos.

**Sintaxis:**
```sql
DROP DATABASE [IF EXISTS] nombre_db;
```

**Ejemplos:**
```sql
-- Eliminar base de datos
DROP DATABASE mi_base_datos;

-- Eliminar si existe
DROP DATABASE IF EXISTS mi_base_datos;
```

## Administración de Tablas

### CREATE TABLE

**Descripción:**  
Crea una nueva tabla.

**Sintaxis:**
```sql
CREATE TABLE [IF NOT EXISTS] nombre_tabla (
    columna1 tipo [restricciones],
    columna2 tipo [restricciones],
    ...
    [restricciones_tabla]
);
```

**Ejemplos:**
```sql
-- Crear tabla simple
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Crear tabla con clave foránea
CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario_id INT,
    fecha DATETIME,
    total DECIMAL(10,2),
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE
);

-- Crear tabla con índice
CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(200),
    precio DECIMAL(10,2),
    categoria VARCHAR(50),
    INDEX (categoria)
);
```

### SHOW TABLES

**Descripción:**  
Muestra las tablas en la base de datos actual.

**Sintaxis:**
```sql
SHOW TABLES [LIKE 'patrón'];
```

**Ejemplos:**
```sql
-- Mostrar todas las tablas
SHOW TABLES;

-- Mostrar tablas que coincidan con un patrón
SHOW TABLES LIKE 'user%';
```

### DESCRIBE / DESC / SHOW COLUMNS

**Descripción:**  
Muestra la estructura de una tabla.

**Sintaxis:**
```sql
DESCRIBE nombre_tabla;
DESC nombre_tabla;
SHOW COLUMNS FROM nombre_tabla;
```

**Ejemplos:**
```sql
-- Ver estructura de una tabla
DESCRIBE usuarios;

-- Alternativa
DESC productos;

-- Otra forma
SHOW COLUMNS FROM pedidos;
```

### ALTER TABLE

**Descripción:**  
Modifica la estructura de una tabla existente.

**Sintaxis:**
```sql
ALTER TABLE nombre_tabla acción;
```

**Acciones comunes:**
- `ADD columna tipo [restricciones]`: Añadir columna
- `DROP COLUMN columna`: Eliminar columna
- `MODIFY COLUMN columna tipo [restricciones]`: Modificar tipo de columna
- `CHANGE COLUMN viejo_nombre nuevo_nombre tipo [restricciones]`: Renombrar columna
- `ADD INDEX (columna)`: Añadir índice
- `ADD PRIMARY KEY (columna)`: Añadir clave primaria
- `ADD FOREIGN KEY (columna) REFERENCES tabla(columna)`: Añadir clave foránea
- `RENAME TO nuevo_nombre`: Renombrar tabla

**Ejemplos:**
```sql
-- Añadir columna
ALTER TABLE usuarios ADD apellido VARCHAR(100);

-- Eliminar columna
ALTER TABLE usuarios DROP COLUMN apellido;

-- Modificar tipo de columna
ALTER TABLE productos MODIFY COLUMN precio DECIMAL(12,2);

-- Renombrar columna
ALTER TABLE usuarios CHANGE COLUMN nombre nombre_completo VARCHAR(150);

-- Añadir índice
ALTER TABLE usuarios ADD INDEX idx_email (email);

-- Añadir clave foránea
ALTER TABLE pedidos ADD FOREIGN KEY (producto_id) REFERENCES productos(id);

-- Renombrar tabla
ALTER TABLE usuarios RENAME TO clientes;
```

### DROP TABLE

**Descripción:**  
Elimina una tabla.

**Sintaxis:**
```sql
DROP TABLE [IF EXISTS] nombre_tabla;
```

**Ejemplos:**
```sql
-- Eliminar tabla
DROP TABLE usuarios;

-- Eliminar si existe
DROP TABLE IF EXISTS usuarios;
```

### TRUNCATE TABLE

**Descripción:**  
Elimina todos los datos de una tabla, pero mantiene su estructura.

**Sintaxis:**
```sql
TRUNCATE TABLE nombre_tabla;
```

**Ejemplos:**
```sql
-- Vaciar una tabla
TRUNCATE TABLE logs;
```

## Manipulación de Datos

### INSERT

**Descripción:**  
Inserta nuevas filas en una tabla.

**Sintaxis:**
```sql
INSERT INTO nombre_tabla [(columna1, columna2, ...)]
VALUES (valor1, valor2, ...);

-- O insertar múltiples filas:
INSERT INTO nombre_tabla [(columna1, columna2, ...)]
VALUES 
    (valor1, valor2, ...),
    (valor1, valor2, ...),
    ...;

-- O insertar desde otra tabla:
INSERT INTO nombre_tabla [(columna1, columna2, ...)]
SELECT columna1, columna2, ... FROM otra_tabla WHERE condición;
```

**Ejemplos:**
```sql
-- Insertar una fila (todas las columnas)
INSERT INTO usuarios VALUES (NULL, 'Juan', 'juan@example.com', NOW());

-- Insertar una fila (columnas específicas)
INSERT INTO usuarios (nombre, email) VALUES ('María', 'maria@example.com');

-- Insertar múltiples filas
INSERT INTO productos (nombre, precio) VALUES
    ('Producto 1', 19.99),
    ('Producto 2', 29.99),
    ('Producto 3', 9.99);

-- Insertar datos desde otra tabla
INSERT INTO usuarios_backup
SELECT * FROM usuarios WHERE fecha_registro < '2023-01-01';
```

### SELECT

**Descripción:**  
Recupera datos de una o más tablas.

**Sintaxis:**
```sql
SELECT [DISTINCT] columna1, columna2, ...
FROM tabla
[JOIN otra_tabla ON condición_join]
[WHERE condición]
[GROUP BY columnas]
[HAVING condición_grupo]
[ORDER BY columnas [ASC|DESC]]
[LIMIT n [OFFSET m]];
```

**Ejemplos:**
```sql
-- Seleccionar todas las columnas
SELECT * FROM usuarios;

-- Seleccionar columnas específicas
SELECT id, nombre, email FROM usuarios;

-- Filtrar con WHERE
SELECT * FROM productos WHERE precio > 20;

-- Ordenar resultados
SELECT * FROM usuarios ORDER BY nombre ASC;

-- Limitar resultados
SELECT * FROM usuarios LIMIT 10;

-- Paginación
SELECT * FROM usuarios LIMIT 10 OFFSET 20;

-- Uso de DISTINCT para valores únicos
SELECT DISTINCT categoria FROM productos;

-- Selección con JOIN
SELECT u.nombre, p.fecha, p.total
FROM usuarios u
JOIN pedidos p ON u.id = p.usuario_id
WHERE p.total > 100;

-- Agrupación con GROUP BY
SELECT categoria, COUNT(*) as total, AVG(precio) as precio_medio
FROM productos
GROUP BY categoria
HAVING precio_medio > 50
ORDER BY total DESC;
```

### UPDATE

**Descripción:**  
Actualiza filas existentes en una tabla.

**Sintaxis:**
```sql
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2, ...
[WHERE condición];
```

**Ejemplos:**
```sql
-- Actualizar todas las filas
UPDATE productos SET impuesto = precio * 0.21;

-- Actualizar con condición
UPDATE usuarios SET activo = 1 WHERE id = 5;

-- Actualización basada en otra columna
UPDATE productos SET precio = precio * 1.1 WHERE categoria = 'Electrónica';

-- Actualización con JOIN
UPDATE productos p
JOIN categorias c ON p.categoria_id = c.id
SET p.precio = p.precio * 1.05
WHERE c.nombre = 'Lujo';
```

### DELETE

**Descripción:**  
Elimina filas de una tabla.

**Sintaxis:**
```sql
DELETE FROM nombre_tabla [WHERE condición];
```

**Ejemplos:**
```sql
-- Eliminar todas las filas (¡cuidado!)
DELETE FROM logs;

-- Eliminar con condición
DELETE FROM usuarios WHERE fecha_registro < '2020-01-01';

-- Eliminar con JOIN
DELETE u FROM usuarios u
JOIN marcas_bloqueadas m ON u.email LIKE CONCAT('%@', m.dominio)
WHERE m.activo = 1;

-- Eliminar con límite
DELETE FROM logs ORDER BY fecha ASC LIMIT 1000;
```

## Consultas Avanzadas

### JOIN

**Descripción:**  
Combina filas de dos o más tablas.

**Tipos:**
- `INNER JOIN`: Retorna filas cuando hay coincidencia en ambas tablas
- `LEFT JOIN`: Retorna todas las filas de la tabla izquierda y las coincidentes de la derecha
- `RIGHT JOIN`: Retorna todas las filas de la tabla derecha y las coincidentes de la izquierda
- `FULL JOIN`: Retorna filas cuando hay coincidencia en cualquiera de las tablas (no soportado directamente en MySQL)

**Ejemplos:**
```sql
-- INNER JOIN
SELECT u.nombre, p.total
FROM usuarios u
INNER JOIN pedidos p ON u.id = p.usuario_id;

-- LEFT JOIN
SELECT u.nombre, p.total
FROM usuarios u
LEFT JOIN pedidos p ON u.id = p.usuario_id;

-- RIGHT JOIN
SELECT u.nombre, p.total
FROM usuarios u
RIGHT JOIN pedidos p ON u.id = p.usuario_id;

-- Múltiples JOINs
SELECT u.nombre, p.fecha, d.cantidad, pr.nombre as producto
FROM usuarios u
JOIN pedidos p ON u.id = p.usuario_id
JOIN detalles_pedido d ON p.id = d.pedido_id
JOIN productos pr ON d.producto_id = pr.id;

-- FULL JOIN (emulado en MySQL)
SELECT u.nombre, p.total
FROM usuarios u
LEFT JOIN pedidos p ON u.id = p.usuario_id
UNION
SELECT u.nombre, p.total
FROM usuarios u
RIGHT JOIN pedidos p ON u.id = p.usuario_id
WHERE u.id IS NULL;
```

### Subconsultas

**Descripción:**  
Consultas anidadas dentro de otras consultas.

**Ejemplos:**
```sql
-- Subconsulta en SELECT
SELECT nombre, 
       (SELECT COUNT(*) FROM pedidos WHERE usuario_id = u.id) as total_pedidos
FROM usuarios u;

-- Subconsulta en WHERE
SELECT * FROM productos 
WHERE precio > (SELECT AVG(precio) FROM productos);

-- Subconsulta con IN
SELECT * FROM usuarios
WHERE id IN (SELECT DISTINCT usuario_id FROM pedidos WHERE total > 1000);

-- Subconsulta con EXISTS
SELECT * FROM proveedores p
WHERE EXISTS (SELECT 1 FROM productos WHERE proveedor_id = p.id AND stock = 0);

-- Subconsulta en FROM
SELECT categoria, avg_price
FROM (
    SELECT categoria, AVG(precio) as avg_price
    FROM productos
    GROUP BY categoria
) as cat_stats
WHERE avg_price > 100;
```

### Funciones Agregadas

**Descripción:**  
Realizan cálculos sobre conjuntos de valores.

**Funciones comunes:**
- `COUNT()`: Cuenta filas o valores no NULL
- `SUM()`: Suma valores
- `AVG()`: Calcula el promedio
- `MIN()`: Valor mínimo
- `MAX()`: Valor máximo

**Ejemplos:**
```sql
-- Contar filas
SELECT COUNT(*) FROM usuarios;

-- Contar valores no NULL
SELECT COUNT(email) FROM usuarios;

-- Calcular suma
SELECT SUM(total) FROM pedidos WHERE fecha >= '2023-01-01';

-- Promedio, min y max
SELECT 
    AVG(precio) as precio_promedio,
    MIN(precio) as precio_minimo,
    MAX(precio) as precio_maximo
FROM productos;

-- Con GROUP BY
SELECT categoria, 
    COUNT(*) as cantidad, 
    AVG(precio) as precio_promedio
FROM productos
GROUP BY categoria;
```

### UNION / UNION ALL

**Descripción:**  
Combina los resultados de dos o más consultas.

**Sintaxis:**
```sql
SELECT columnas FROM tabla1
UNION [ALL]
SELECT columnas FROM tabla2;
```

**Ejemplos:**
```sql
-- Combinar resultados eliminando duplicados
SELECT nombre, email FROM clientes
UNION
SELECT nombre, email FROM proveedores;

-- Combinar resultados manteniendo duplicados
SELECT nombre, email FROM clientes
UNION ALL
SELECT nombre, email FROM proveedores;

-- Con diferentes columnas (mismo número y tipos compatibles)
SELECT id, nombre, 'Cliente' as tipo FROM clientes
UNION
SELECT id, nombre_empresa, 'Proveedor' as tipo FROM proveedores
ORDER BY nombre;
```

## Índices y Optimización

### CREATE INDEX

**Descripción:**  
Crea un índice en una tabla para optimizar consultas.

**Sintaxis:**
```sql
CREATE [UNIQUE] INDEX nombre_indice
ON nombre_tabla (columna1, columna2, ...);
```

**Ejemplos:**
```sql
-- Crear índice simple
CREATE INDEX idx_apellido ON usuarios(apellido);

-- Índice único
CREATE UNIQUE INDEX idx_email ON usuarios(email);

-- Índice compuesto
CREATE INDEX idx_ciudad_fecha ON pedidos(ciudad, fecha);

-- Índice parcial (MySQL 8+)
CREATE INDEX idx_activos ON usuarios(nombre) WHERE activo = 1;
```

### SHOW INDEX

**Descripción:**  
Muestra los índices de una tabla.

**Sintaxis:**
```sql
SHOW INDEX FROM nombre_tabla;
```

**Ejemplos:**
```sql
-- Ver todos los índices de una tabla
SHOW INDEX FROM usuarios;
```

### DROP INDEX

**Descripción:**  
Elimina un índice.

**Sintaxis:**
```sql
DROP INDEX nombre_indice ON nombre_tabla;
```

**Ejemplos:**
```sql
-- Eliminar un índice
DROP INDEX idx_apellido ON usuarios;
```

### EXPLAIN

**Descripción:**  
Analiza cómo MySQL ejecuta una consulta.

**Sintaxis:**
```sql
EXPLAIN SELECT ...;
```

**Ejemplos:**
```sql
-- Analizar plan de ejecución
EXPLAIN SELECT * FROM usuarios WHERE email = 'test@example.com';

-- Análisis detallado
EXPLAIN FORMAT=JSON SELECT * FROM usuarios WHERE email = 'test@example.com';
```

## Transacciones

### BEGIN / START TRANSACTION

**Descripción:**  
Inicia una nueva transacción.

**Sintaxis:**
```sql
BEGIN;
-- o
START TRANSACTION;
```

**Ejemplos:**
```sql
-- Iniciar transacción
BEGIN;
-- Operaciones aquí
```

### COMMIT

**Descripción:**  
Confirma la transacción actual.

**Sintaxis:**
```sql
COMMIT;
```

**Ejemplos:**
```sql
-- Iniciar transacción
BEGIN;
-- Operaciones
UPDATE cuentas SET balance = balance - 100 WHERE id = 1;
UPDATE cuentas SET balance = balance + 100 WHERE id = 2;
-- Confirmar cambios
COMMIT;
```

### ROLLBACK

**Descripción:**  
Revierte la transacción actual.

**Sintaxis:**
```sql
ROLLBACK;
```

**Ejemplos:**
```sql
-- Iniciar transacción
BEGIN;
-- Operaciones
UPDATE cuentas SET balance = balance - 100 WHERE id = 1;
-- Oh no, error
ROLLBACK;
```

### SAVEPOINT

**Descripción:**  
Establece un punto de guardado dentro de una transacción.

**Sintaxis:**
```sql
SAVEPOINT nombre_savepoint;
```

**Ejemplos:**
```sql
-- Iniciar transacción
BEGIN;
-- Primera operación
UPDATE cuentas SET balance = balance - 100 WHERE id = 1;
-- Punto de guardado
SAVEPOINT despues_retiro;
-- Segunda operación
UPDATE cuentas SET balance = balance + 100 WHERE id = 2;
-- Revertir a punto de guardado
ROLLBACK TO despues_retiro;
-- Otras operaciones
UPDATE cuentas SET balance = balance + 100 WHERE id = 3;
-- Confirmar transacción
COMMIT;
```

## Vistas y Procedimientos Almacenados

### CREATE VIEW

**Descripción:**  
Crea una vista (consulta guardada).

**Sintaxis:**
```sql
CREATE [OR REPLACE] VIEW nombre_vista AS
consulta_select;
```

**Ejemplos:**
```sql
-- Crear vista simple
CREATE VIEW usuarios_activos AS
SELECT * FROM usuarios WHERE activo = 1;

-- Crear o reemplazar vista
CREATE OR REPLACE VIEW resumen_ventas AS
SELECT 
    DATE(fecha) as dia,
    SUM(total) as ventas_totales,
    COUNT(*) as num_pedidos
FROM pedidos
GROUP BY DATE(fecha);

-- Vista con JOIN
CREATE VIEW detalles_pedido_completo AS
SELECT 
    p.id, p.fecha, 
    u.nombre as cliente, 
    p.total,
    GROUP_CONCAT(pr.nombre SEPARATOR ', ') as productos
FROM pedidos p
JOIN usuarios u ON p.usuario_id = u.id
JOIN detalles_pedido dp ON p.id = dp.pedido_id
JOIN productos pr ON dp.producto_id = pr.id
GROUP BY p.id;
```

### DROP VIEW

**Descripción:**  
Elimina una vista.

**Sintaxis:**
```sql
DROP VIEW [IF EXISTS] nombre_vista;
```

**Ejemplos:**
```sql
-- Eliminar vista
DROP VIEW usuarios_activos;

-- Eliminar si existe
DROP VIEW IF EXISTS resumen_ventas;
```

### CREATE PROCEDURE

**Descripción:**  
Crea un procedimiento almacenado.

**Sintaxis:**
```sql
DELIMITER //
CREATE PROCEDURE nombre_procedimiento([parametros])
BEGIN
    -- código SQL
END //
DELIMITER ;
```

**Ejemplos:**
```sql
-- Procedimiento simple
DELIMITER //
CREATE PROCEDURE obtener_usuarios()
BEGIN
    SELECT * FROM usuarios;
END //
DELIMITER ;

-- Procedimiento con parámetros
DELIMITER //
CREATE PROCEDURE usuarios_por_ciudad(IN p_ciudad VARCHAR(100))
BEGIN
    SELECT * FROM usuarios WHERE ciudad = p_ciudad;
END //
DELIMITER ;

-- Procedimiento con parámetros de entrada y salida
DELIMITER //
CREATE PROCEDURE contar_usuarios(IN p_activo BOOLEAN, OUT p_total INT)
BEGIN
    SELECT COUNT(*) INTO p_total FROM usuarios WHERE activo = p_activo;
END //
DELIMITER ;
```

### CALL

**Descripción:**  
Ejecuta un procedimiento almacenado.

**Sintaxis:**
```sql
CALL nombre_procedimiento([argumentos]);
```

**Ejemplos:**
```sql
-- Llamar procedimiento sin parámetros
CALL obtener_usuarios();

-- Llamar procedimiento con parámetros
CALL usuarios_por_ciudad('Madrid');

-- Llamar procedimiento con parámetro de salida
SET @total = 0;
CALL contar_usuarios(1, @total);
SELECT @total as total_usuarios_activos;
```

### CREATE FUNCTION

**Descripción:**  
Crea una función definida por el usuario.

**Sintaxis:**
```sql
DELIMITER //
CREATE FUNCTION nombre_funcion([parametros]) RETURNS tipo
[características]
BEGIN
    -- código SQL
    RETURN valor;
END //
DELIMITER ;
```

**Ejemplos:**
```sql
-- Función simple
DELIMITER //
CREATE FUNCTION total_pedidos(p_usuario_id INT) RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE total INT;
    SELECT COUNT(*) INTO total FROM pedidos WHERE usuario_id = p_usuario_id;
    RETURN total;
END //
DELIMITER ;

-- Uso de la función
SELECT id, nombre, total_pedidos(id) as num_pedidos FROM usuarios;
```

## Seguridad y Permisos

### CREATE USER

**Descripción:**  
Crea un nuevo usuario de MySQL.

**Sintaxis:**
```sql
CREATE USER 'usuario'@'host' IDENTIFIED BY 'contraseña';
```

**Ejemplos:**
```sql
-- Crear usuario local
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'secret_password';

-- Crear usuario remoto
CREATE USER 'app_user'@'%' IDENTIFIED BY 'secret_password';
```

### GRANT

**Descripción:**  
Otorga permisos a un usuario.

**Sintaxis:**
```sql
GRANT privilegios ON objeto TO 'usuario'@'host' [WITH GRANT OPTION];
```

**Ejemplos:**
```sql
-- Otorgar todos los permisos en una base de datos
GRANT ALL PRIVILEGES ON mi_base_datos.* TO 'app_user'@'localhost';

-- Permisos específicos
GRANT SELECT, INSERT, UPDATE ON mi_base_datos.usuarios TO 'app_user'@'localhost';

-- Otorgar permisos en todas las bases de datos
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;

-- Permisos de solo lectura
GRANT SELECT ON mi_base_datos.* TO 'analista'@'%';
```

### REVOKE

**Descripción:**  
Revoca permisos a un usuario.

**Sintaxis:**
```sql
REVOKE privilegios ON objeto FROM 'usuario'@'host';
```

**Ejemplos:**
```sql
-- Revocar permisos específicos
REVOKE INSERT ON mi_base_datos.usuarios FROM 'app_user'@'localhost';

-- Revocar todos los permisos
REVOKE ALL PRIVILEGES ON *.* FROM 'app_user'@'localhost';
```

### DROP USER

**Descripción:**  
Elimina un usuario.

**Sintaxis:**
```sql
DROP USER 'usuario'@'host';
```

**Ejemplos:**
```sql
-- Eliminar usuario
DROP USER 'app_user'@'localhost';
```

### SHOW GRANTS

**Descripción:**  
Muestra los permisos de un usuario.

**Sintaxis:**
```sql
SHOW GRANTS FOR 'usuario'@'host';
```

**Ejemplos:**
```sql
-- Ver permisos de un usuario
SHOW GRANTS FOR 'app_user'@'localhost';

-- Ver permisos del usuario actual
SHOW GRANTS;
```
