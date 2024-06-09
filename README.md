

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
### 2.2.1 INSERTAR DATOS

1. **Inserción de Usuarios:**
```sql
-- Inserta al menos 5 nuevos usuarios
INSERT INTO Users (UserName, Email, Password) VALUES
('usuario1', 'usuario1@example.com', 'contraseña1'),
('usuario2', 'usuario2@example.com', 'contraseña2'),
('usuario3', 'usuario3@example.com', 'contraseña3'),
('usuario4', 'usuario4@example.com', 'contraseña4'),
('usuario5', 'usuario5@example.com', 'contraseña5');
````
![img](g) 
-- Inserta al menos 5 nuevos productos
```sql
INSERT INTO Products (ProductName, Price, Stock, CategoryID) VALUES
('Producto1', 25.00, 50, 1),
('Producto2', 35.00, 30, 2),
('Producto3', 40.00, 20, 1),
('Producto4', 15.00, 100, 3),
('Producto5', 50.00, 10, 2);
````
![img](g) 
 ACTUALIZAR DATOS
Cambiar Nombre de Producto:
````sql
-- Cambia el nombre de un producto por su ID
UPDATE Products SET ProductName = 'NuevoNombre' WHERE ProductID = 1;
````
Cambiar Precio de Producto:
````sql
-- Cambia el precio de un producto por su ID
UPDATE Products SET Price = 50.00 WHERE ProductID = 2;
````
 OBTENER DATOS
Seleccionar Productos con Precio Superior a 20€:
````sql
-- Selecciona todos los productos con precio superior a 20€
SELECT * FROM Products WHERE Price > 20.00;
````
Mostrar Productos en Orden Descendente de Precio:
````sql
-- Muestra todos los productos ordenados en forma descendente por precio
SELECT * FROM Products ORDER BY Price DESC;
````
Seleccionar Productos con Categoría:
````sql
-- Selecciona todos los productos con su respectiva categoría
SELECT p.*, c.CategoryName 
FROM Products p
INNER JOIN Categories c ON p.CategoryID = c.CategoryID;
````
Seleccionar Usuarios con sus Pedidos: (Continúa con el mismo formato para las consultas restantes)

Ejecución de Consultas
Para ejecutar las consultas SQL, sigue estos pasos:

Copia cada consulta en tu cliente de MySQL o herramienta de gestión de bases de datos.
Ejecuta las consultas una por una en el orden especificado.
¡Listo! Ahora tendrás una base de datos de E-Commerce poblada con datos y podrás realizar consultas para obtener información relevante.
Autor
Este proyecto fue realizado por [Viktoriya Pashkouskaya].
Licencia
Este proyecto está licenciado bajo la Licencia MIT.

