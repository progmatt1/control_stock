# control_stock
Proyecto usando Java 17+ en Spring Boot para crear una API. Se trata de un control de stock
# Inicio
Crea estas tablas en MySql:
### deposito
```
CREATE TABLE `control_stock`.`deposito` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nombre` TEXT NOT NULL,
  `descripcion` TEXT NOT NULL,
  `direccion` TEXT NOT NULL,
  PRIMARY KEY (`id`));
```
### movimiento_tipo
```
CREATE TABLE `control_stock`.`movimiento_tipo` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nombre` TEXT NOT NULL,
  `descripcion` TEXT NOT NULL,
  PRIMARY KEY (`id`));
```
### producto
```
CREATE TABLE `control_stock`.`producto` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nombre` TEXT NOT NULL,
  `descripcion` TEXT NOT NULL,
  `precio` FLOAT NOT NULL,
  `cantidad` INT NOT NULL,
  PRIMARY KEY (`id`));
```
