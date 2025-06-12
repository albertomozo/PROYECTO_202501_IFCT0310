# POSTGRES - PHP

Alojamiento php + postgres. 

# Pasos para cambiar de PostgreSQL a MySQL usando PDO

## 1. Instalar los drivers necesarios
Primero asegúrate de tener instalado el driver PDO para MySQL:
```bash
# En sistemas basados en Debian/Ubuntu
sudo apt-get install php-mysql

# Reiniciar el servidor web después de instalar
sudo service apache2 restart
# o
sudo systemctl restart apache2
```

## 2. Modificar la cadena de conexión PDO
Cambia los parámetros de conexión en tu código:

```php
// Conexión PostgreSQL original (ejemplo)
// $pdo = new PDO("pgsql:host=localhost;dbname=basedatos", "usuario", "contraseña");

// Nueva conexión MySQL
$pdo = new PDO("mysql:host=localhost;dbname=basedatos", "usuario", "contraseña", [
    PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES 'utf8'",
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
]);
```

## 3. Ajustar consultas SQL
PostgreSQL y MySQL tienen algunas diferencias sintácticas:

- `LIMIT/OFFSET`: 
  - PostgreSQL: `LIMIT 10 OFFSET 20`
  - MySQL: `LIMIT 20, 10`

- Funciones de fecha:
  - PostgreSQL: `NOW()`, `CURRENT_DATE`
  - MySQL también las soporta pero hay otras alternativas

- Secuencias:
  - PostgreSQL usa `SERIAL` o secuencias explícitas
  - MySQL usa `AUTO_INCREMENT`

## 4. Migrar los datos
Puedes usar herramientas como:
- `pg_dump` para exportar de PostgreSQL
- `mysqldump` para importar a MySQL
- Herramientas gráficas como DBeaver, MySQL Workbench o phpMyAdmin

## 5. Verificar tipos de datos
Algunos tipos de datos difieren:
- `boolean`: PostgreSQL usa `TRUE/FALSE`, MySQL usa `1/0`
- `text`: Similar en ambos pero con implementaciones internas diferentes
- `varchar`: Similar pero con límites diferentes

## 6. Ajustar transacciones y bloqueos
MySQL (con InnoDB) y PostgreSQL manejan transacciones de forma similar, pero verifica:
- Niveles de aislamiento
- Comportamiento de bloqueos

## 7. Probar exhaustivamente
Después de la migración, prueba:
- Consultas básicas
- Transacciones
- Funciones almacenadas (si las hay)
- Rendimiento

# POSTGRES TO MYSQL

- Exporta los SCHEMAS DE POSTGRES A  fichero mibase_pg.sql . 
- Pasalo por alguna IA o aplicación y genera el fichero mibase_mysql.sql

Ahpora puedes dar la posibilidad de que los que quieran usar tu aplicación usen  una de estas 2 BD. DEbes reflejarlo en el README.md

