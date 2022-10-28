# configuración de la base de datos para la persistencia

instalar mysql

abrir mysql ejecutndo en un terminal

	sudo mysql --password

create new database

	create database database_name; -- Creates the new database

creamos un usuario para administrar la base de datos

	create user 'userName'@'%' identified by 'ThePassword'; -- Creates the user

le damos los privilejos a dicho usuario

	grant all on database_name.* to 'userName'@'%'; -- Gives all privileges to the new user on the newly created database

se crea el archivo `src/main/resources/application.properties`

```properties
spring.jpa.hibernate.ddl-auto=none
spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/database_name
spring.datasource.username=userName
spring.datasource.password=ThePassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
#spring.jpa.show-sql: true
```