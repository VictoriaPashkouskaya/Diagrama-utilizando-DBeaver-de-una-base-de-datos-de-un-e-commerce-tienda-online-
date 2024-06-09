

# E-Commerce Database with DBeaver

Este proyecto contiene las instrucciones para crear y visualizar una base de datos de e-commerce en DBeaver, incluyendo las tablas `Users`, `Products`, `Orders`, `Categories`, y `OrderDetails`, así como las relaciones entre ellas.

## Tabla de Contenidos

- [Requisitos Previos](#requisitos-previos)
- [Creación de las Tablas](#creación-de-las-tablas)
- [Creación del Diagrama en DBeaver](#creación-del-diagrama-en-dbeaver)
- [Consultas SQL](#consultas-sql)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

## Requisitos Previos

1. **DBeaver**: Asegúrate de tener instalado DBeaver.
2. **Conexión a la Base de Datos**: Configura una conexión a tu base de datos en DBeaver.

## Creación de las Tablas

Ejecuta las siguientes consultas SQL en DBeaver para crear las tablas necesarias para el e-commerce.
  ![img](https://github.com/VictoriaPashkouskaya/VictoriaPashkouskaya/blob/main/Captura%20de%20pantalla%202024-06-09%20114955.png) 
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
````
Creación del Diagrama en DBeaver
Abrir el Editor de Diagrama:
Haz clic derecho en la base de datos donde creaste las tablas y selecciona ER Diagram.
Añadir las Tablas al Diagrama:
En el editor de diagramas, haz clic derecho y selecciona Add Table.
![img](https://github.com/VictoriaPashkouskaya/VictoriaPashkouskaya/blob/main/Captura%20de%20pantalla%202024-06-09%20114911.png) 
Selecciona las tablas Users, Products, Orders, Categories y OrderDetails para añadirlas al diagrama.

Visualizar las Relaciones:
DBeaver debería automáticamente detectar y mostrar las relaciones entre las tablas basadas en las claves foráneas que has definido en las consultas SQL.
Consultas SQL
Ejecuta las siguientes consultas SQL para interactuar con tu base de datos de e-commerce:

Seleccionar todos los usuarios:
```sql
SELECT * FROM Users;
````

Seleccionar todos los productos y sus categorías:
```sql
SELECT Products.id, Products.name, Categories.name AS category
FROM Products
JOIN Categories ON Products.category_id = Categories.id;
````

Seleccionar todas las órdenes y los usuarios que las hicieron:
```sql
SELECT Orders.id, Users.name, Orders.order_date, Orders.status
FROM Orders
JOIN Users ON Orders.user_id = Users.id;
````

Seleccionar los detalles de una orden específica (por ejemplo, orden con id 1):

```sql
SELECT Orders.id AS order_id, Users.name AS user_name, Products.name AS product_name, OrderDetails.quantity
FROM OrderDetails
JOIN Orders ON OrderDetails.order_id = Orders.id
JOIN Users ON Orders.user_id = Users.id
JOIN Products ON OrderDetails.product_id = Products.id
WHERE Orders.id = 1;
````


Licencia
Este proyecto está licenciado bajo la Licencia MIT.

