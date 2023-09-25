# control_stock
Proyecto usando Java 17+ en Spring Boot para crear una API. Se trata de un control de stock
# Inicio
Crea estas tablas en MySql:
### productos
```
CREATE TABLE `productos` (
  `id` int NOT NULL AUTO_INCREMENT,
  `nombre` text NOT NULL,
  `descripcion` text NOT NULL,
  `precio` float NOT NULL,
  `cantidad` text NOT NULL,
  `fecha_creacion` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `fecha_actualizacion` timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
### movimientos_tipo
```
CREATE TABLE `control_stock`.`movimientos_tipo` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nombre` TEXT NOT NULL,
  `descripcion` TEXT NOT NULL,
  PRIMARY KEY (`id`));
```
### depositos
```
CREATE TABLE `control_stock`.`depositos` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nombre` TEXT NOT NULL,
  PRIMARY KEY (`id`));
```
### movimientos
```
CREATE TABLE `control_stock`.`movimientos` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `cantidad` INT NOT NULL,
  `fecha` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP,
  `id_movimiento_tipo` INT NOT NULL,
  `id_producto` INT NOT NULL,
  `id_deposito` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `id_movimiento_tipo_idx` (`id_movimiento_tipo` ASC) VISIBLE,
  INDEX `id_producto_idx` (`id_producto` ASC) VISIBLE,
  INDEX `id_deposito_idx` (`id_deposito` ASC) VISIBLE,
  CONSTRAINT `id_movimiento_tipo`
    FOREIGN KEY (`id_movimiento_tipo`)
    REFERENCES `control_stock`.`movimientos_tipo` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `id_producto`
    FOREIGN KEY (`id_producto`)
    REFERENCES `control_stock`.`productos` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `id_deposito`
    FOREIGN KEY (`id_deposito`)
    REFERENCES `control_stock`.`depositos` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);
```

### productos_deposito
```
CREATE TABLE `productos_deposito` (
  `id` int NOT NULL AUTO_INCREMENT,
  `id_deposito` int NOT NULL,
  `id_producto` int NOT NULL,
  `cantidad` int NOT NULL,
  `fecha_actualizacion` timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  KEY `id_deposito_idx` (`id_deposito`),
  KEY `id_producto_idx` (`id_producto`),
  CONSTRAINT `id_deposito_foreign` FOREIGN KEY (`id_deposito`) REFERENCES `depositos` (`id`),
  CONSTRAINT `id_producto_foreign` FOREIGN KEY (`id_producto`) REFERENCES `productos` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
