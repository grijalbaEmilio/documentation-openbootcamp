# build project with maven

* abrimos el apartado maven (a la derecha en IJ)
* click en package

una ves generado el archivo `.jar` en la carpeta `targer` ejecutaremos un comando para iniciar la app.

	java -jar file.jar

# variables de entorno

### configurar perfil de desarrollo
se crea el archivo `application-dev.properties` y se agrega al final 

	spring.profiles.active=dev


se configuran en el archivo `application.properties`

	app.message=este es un mensajito ev

se llaman en un archivo .java

	@Value("${app.message}")
	String message;

	System.out.println(message);

para ver las variables de entorno

	System.getenv().forEach((key, value) -> {
		System.out.println(key + " == "+ value); 
		})

para usar variable de entorno del ordenador

	app.varexample=${USERNAME}

# Despliegue | heroku

creamos el archivo `system.properties` en el directorio raiz

declaramos la versión de java 

	java.runtime.version=17