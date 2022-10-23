# Spring

# Beans
se utilizan para la inyección de dependencias, es decir que spring crea los objetos y nos los entrega mediante un patrón singlenton.

## estructura de proyecto maven
```text
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           ├── Main.java
│   │   └── resources
│   │       └── beans.xml
│   └── test
│       └── java

```

## pom.xml
se agrega la dependencia [spring contextet](https://mvnrepository.com/artifact/org.springframework/spring-context/5.3.23) de [maven repository.](https://mvnrepository.com/) 

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.23</version>
</dependency>
```

## src/main/java/resources/beans.xml
en éste archivo se pondrá la [plantilla](https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/xsd-configuration.html) para alojar los beans.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean definitions here -->

</beans>
```

## definición de un bean para la inyección de dependencias.
`id` indica el nombre con el que nos referiremos al bean y `class` le indica al bean el objeto que creará.
```xml
<bean id="User" class="org.example.User" />
```
en caso de no querer que se entreguen los objetos mediante el patron singlenton se agrega la propiedad `scope="prototype"`
```xml
<bean id="UserButDiffRef" class="org.example.User" scope="prototype" />
```
si la el consructor de la clase resibe parámetros. <br/>
se usa `ref` en lugar de `value` para pasar como valor otro bean.
```xml
<bean id="UserCtrl" class="org.example.UserCtrl">
        <constructor-arg name="user" ref="user"></constructor-arg>
        <constructor-arg name="name" value="Controller 3000"></constructor-arg>
</bean>
```
## beans scanner
Escanea automáticamente las clases a las que se les agregue el decorador `@Component` <br/>
se agrega una plantilla diferente en `src/main/java/resources/beans.xml` [que contenga context](https://www.baeldung.com/spring-application-context).


```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:context="http://www.springframework.org/schema/context"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">
  
  <context:component-scan base-package="com.example"/>

</beans>
```

## uso en main
```java
package org.example;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {

    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        // create normal object
        User oUser = new User();

        // ask / request object to spring
        User oJuan = (User)context.getBean("user");
        User oJuan2 = (User)context.getBean("user");

        System.out.println(oJuan == oLuisa ? "they are equals" : "they aren't equals");

        // create object with dependencies -> bean within bean
        UserCtrl ctrl = (UserCtrl) context.getBean("userCtrl");
        System.out.println("name ctrl: "+ctrl.getName());

        //create child class
        User student = (Student)context.getBean("student");

    }
}
```

# Spring Boot
Se genera el proyecto dese [SpringInitialzr](https://start.spring.io/) <br/>
se agregan las dependncia necesarias.

## recomedadas 

* `Spring Data JPA` para la intefración con BD
* `para la BD` (se usa en proyectos de peueba)
* `String Web` para montar la aplicación rest
* `Spring Boot DevTools` una especie de nodemon(en js)

<hr/>

`NOTA` si se presentan problemas en el pom.xml `<buil/>` agregamos la version en `<plugin/>` `<version>2.7.5</version>`
<hr/>

## configuración de `Spring boot Devtools`
configurar auto guardar en IJ

<img src="./img/IJconfig1.png" alt="noimg" />

configurar auto crear para cada proyecto spring boot

<img src="./img/IJconfig2.png" alt="noimg" />

## anotaciones / decoradores 

## a clases
para indicar que los objetos de una clase se almacenarán en base de datos

	@Entity

para indicar el nombre de la tabla

	@Table(name = "books_tbl")

para servicios rest con JSON

	@RestController

## a interfaces 
para indicar que será un repositorio 

	@Repository

además se extiende de JpaRepository

	extends JpaRepository<Class, ClassIsd>

## métodos
para generar endPoint 

	 @GetMapping("/path")
	
	 @PostMapping("/path")

## a atributos
para indicar que un atributo será id

	@Id

para indicar la estrategia de generación del id

	@GeneratedValue(strategy = GenerationType.IDENTITY)

## parámetros 
para obtner los valores de petiiones(@GetMapping("/hello/{id}"))

	@PathVariable

para obtener un body

	@RequestBody	 
