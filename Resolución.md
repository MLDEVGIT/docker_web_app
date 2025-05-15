# TP Docker - Práctica Formativa Obligatoria N°2

## Parte I: Uso de imágenes públicas y conexión entre contenedores

### Instalación de Docker y Docker Hub

* Descargar e instalar Docker Desktop desde [Docker Desktop](https://www.docker.com/products/docker-desktop).

---

### Descarga de imágenes públicas

* Buscar imagen de Apache:

  ```bash
  docker search httpd
  ```

* Descargar imagen de Apache:

  ```bash
  docker pull httpd
  ```

* Descargar imagen de MySQL:

  ```bash
  docker pull mysql:5.7
  ```

---

### Crear contenedores Apache y MySQL

* Crear contenedor Apache:

  ```bash
  docker run -d --name web_server -p 8080:80 httpd
  ```

* Crear contenedor MySQL:

  ```bash
  docker run -d --name mysql_server -e MYSQL_ROOT_PASSWORD=12345 -p 3306:3306 mysql:5.7
  ```

---

### Crear la base de datos y tabla de usuarios

* Acceder al contenedor MySQL:

  ```bash
  docker exec -it mysql_server /bin/bash
  ```

* Conectar a MySQL:

  ```bash
  mysql -u root -p
  ```

* Crear base de datos y tabla:

  ```sql
  CREATE DATABASE testdb;
  USE testdb;
  CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(50),
      email VARCHAR(50)
  );
  ```

* Insertar datos:

  ```sql
  INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
  INSERT INTO users (name, email) VALUES ('Jane Smith', 'jane@example.com');
  ```

---

### Crear aplicación web para mostrar los datos

* Crear archivo `index.php` en la carpeta del proyecto:

  ```php
  <?php
  $conn = new mysqli("mysql_server", "root", "12345", "testdb");

  if ($conn->connect_error) {
      die("Conexión fallida: " . $conn->connect_error);
  }

  $sql = "SELECT id, name, email FROM users";
  $result = $conn->query($sql);

  while ($row = $result->fetch_assoc()) {
      echo "ID: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
  }

  $conn->close();
  ?>
  ```

* Copiar `index.php` al contenedor Apache:

  ```bash
  docker cp index.php web_server:/usr/local/apache2/htdocs/
  ```

* Acceder a la aplicación:

  ```
  ```

[http://localhost:8080/index.php](http://localhost:8080/index.php)


---

## Parte II: Crear y configurar un repositorio con un proyecto web

### Crear repositorio en GitHub
- Crear un repositorio llamado `docker-web-project`.

---

### Clonar el repositorio localmente

```bash
cd C:\Users\martinlopez\Desktop
mkdir docker-web-project
cd docker-web-project
````

```bash
git clone https://github.com/malopezd/docker-web-project.git
```

---

### Crear `Dockerfile` y `docker-compose.yml`

* **Dockerfile:**

  ```dockerfile
  FROM php:7.4-apache
  COPY . /var/www/html/
  EXPOSE 80
  CMD ["apache2-foreground"]
  ```

* **docker-compose.yml:**

  ```yaml
  version: "3"
  services:
    web:
      build:
        context: .
        dockerfile: Dockerfile
      ports:
        - "8081:80"
  ```

---

### Ejecutar y probar la aplicación

* Construir la imagen:

  ```bash
  docker-compose build
  ```

* Levantar los contenedores:

  ```bash
  docker-compose up -d
  ```

* Acceder a la aplicación:

  ```
  ```

[http://localhost:8081](http://localhost:8081)



---

### Publicar la imagen en Docker Hub

- Crear la imagen:
```bash
docker build -t malopezd/docker-web-app .
````

* Etiquetar y subir:

  ```bash
  docker tag malopezd/docker-web-app:latest malopezd/docker-web-app:1.0
  docker push malopezd/docker-web-app:1.0
  ```

---
