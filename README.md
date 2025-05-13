# Docker Web App - PHP & MySQL

Este proyecto contiene una aplicación web simple en PHP conectada a una base de datos MySQL, utilizando Docker.

## Comandos Docker:

### Construir la imagen:
docker build -t malopezd/docker_web_app -f ./web_app/Dockerfile .

### Etiquetar la imagen:

docker tag malopezd/docker_web_app:latest malopezd/docker_web_app:1.0

### Publicar la imagen en Docker Hub:

docker push malopezd/docker_web_app:1.0

### Ejecutar la imagen 

docker run -d -p 8081:80 malopezd/docker_web_app:1.0


---

## Acceso a la aplicación web:
- URL: [http://localhost:8081](http://localhost:8081)

---

## Acceso a la base de datos MySQL:
- Host: `localhost`
- Port: `3308`
- User: `root`
- Password: `12345`
- Database: `web_data`

---

## Problemas y Soluciones:
- **403 Forbidden:** Verificar los permisos de los archivos en `/var/www/html`.
- **MySQLi no encontrado:** Asegurarse de que la extensión `mysqli` esté habilitada en el `Dockerfile`.

