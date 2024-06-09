# E-Commerce Database with DBeaver

Este proyecto contiene las instrucciones para crear y visualizar una base de datos de e-commerce en DBeaver, incluyendo las tablas `Users`, `Products`, `Orders`, `Categories`, y `OrderDetails`, así como las relaciones entre ellas.

## Tabla de Contenidos

- [Requisitos Previos](#requisitos-previos)
- [Creación de las Tablas](#creación-de-las-tablas)
- [Creación del Diagrama en DBeaver](#creación-del-diagrama-en-dbeaver)
- [Consultas SQL](#consultas-sql)

## Requisitos Previos

1. **DBeaver**: Asegúrate de tener instalado DBeaver.
2. **Conexión a la Base de Datos**: Configura una conexión a tu base de datos en DBeaver.

## Creación de las Tablas

Ejecuta las siguientes consultas SQL en DBeaver para crear las tablas necesarias para el e-commerce.

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL
);

CREATE TABLE Categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE Products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL,
    category_id INT,
    FOREIGN KEY (category_id) REFERENCES Categories(id)
);

CREATE TABLE Orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

CREATE TABLE OrderDetails (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES Orders(id),
    FOREIGN KEY (product_id) REFERENCES Products(id)
);
