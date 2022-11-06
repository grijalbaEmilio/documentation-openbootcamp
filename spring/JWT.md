
se puede ver una implemetació en el [github openbootcamp](https://github.com/Open-Bootcamp/spring/tree/main/sesiones_13_14_15_16/ob-spring-security-jwt) 

## JWT 

https://jwt.io/introduction

Es un estándar abierto que permite transmitir información entre dos partes.

JSON Web Token

## Funcionamiento Session

1. Cliente envía una petición a un servidor (/api/login)
2. Servidor valida username y password, si no son válidos devolverá una respuesta 401 unauthorized
3. Servidor valida username y password, si sí son válidos entonces se almacena el usuario en session
4. Se genera una cookie en el Cliente
5. En próximas peticiones se comprueba que el cliente está en session 

Desventajas: 

* La información de la session se almacena en el servidor, lo cual consume recursos.


## Funcionamiento JWT

1. Cliente envía una petición a un servidor (/api/login)
2. Servidor valida username y password, si no son válidos devolverá una respuesta 401 unauthorized
3. Servidor valida username y password, si sí son válidos entonces genera un token JWT utilizando una secret key
4. Servidor devuelve el token JWT generado al Cliente 
5. Cliente envía peticiones a los endpoints REST del servidor utilizando el token JWT en las cabeceras
6. Servidor valida el token JWT en cada petición y si es correcto permite el acceso a los datos

Ventajas: 

* El token se almacena en el Cliente, de manera que consume menos recursos en el Servidor, lo cual permite mejor escalabilidad

Desventajas: 

* El token está en el navegador, no podríamos invalidarlo antes de la fecha de expiración asignada cuando se creó
  * Lo que se realiza es dar la opción de logout, lo cual simplemente borra el token

## Estructura del token JWT 

3 partes separadas por un punto (.) y codificadas en base 64 cada una: 

1. Header

```json
{   
    "alg": "HS512",
    "typ": "JWT"
}
```

2. Payload (información, datos del usuario, no sensibles)

```json
{
  "name": "John Doe",
  "admin": true
}
```

3. Signatura

```
HMACKSHA256(
base64UrlEncode(header) + "." + base64UrlEncode(payload), secret
)
```

Ejemplo del token generado: 

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

El User-Agent envía el token JWT en las cabeceras: 

```
Authorization: Bearer <token>
```

## Configuración Spring

Crear proyecto Spring Boot con:

* Spring Security 
* Spring Web 
* Spring boot devtools
* Spring Data JPA 
* PostgreSQL 
* Dependencia jwt (se añade manualmente en pom.xml)

```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

agregar en `application.properties`
```
app.jwt.secret=pendb
app.jwt.expiration-ms=86400000
```

se agrega la fonfiguración para spring security

```java
import com.example.demo.security.jwt.JwtAuthEntryPoint;
import com.example.demo.security.jwt.JwtRequestFilter;
import com.example.demo.security.service.UserDetailsServiceImpl;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.CorsConfigurationSource;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;

import java.util.List;

/**
 * Clase para la configuración de seguridad Spring Security
 */
@Configuration
@EnableWebSecurity // permite a Spring aplicar esta configuracion a la configuraicon de seguridad global
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsServiceImpl userDetailsService;

    @Autowired
    private JwtAuthEntryPoint unauthorizedHandler;

    // ================ CREACIÓN DE BEANS ======================
    @Bean
    public JwtRequestFilter authenticationJwtTokenFilter() {
        return new JwtRequestFilter();
    }

    @Bean
    @Override
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    /**
     * Configuracion global de CORS para toda la aplicacion
     */
    @Bean
    CorsConfigurationSource corsConfigurationSource()
    {
        CorsConfiguration configuration = new CorsConfiguration();
        // configuration.setAllowedOrigins(List.of("http://localhost:4200", "https://angular-springboot-*.vercel.app"));
        configuration.setAllowedOriginPatterns(List.of("http://localhost:4200", "https://angular-springboot1-beta.vercel.app"));
        configuration.setAllowedMethods(List.of("GET", "POST", "OPTIONS", "DELETE", "PUT", "PATCH"));
        configuration.setAllowedHeaders(List.of("Access-Control-Allow-Origin", "X-Requested-With", "Origin", "Content-Type", "Accept", "Authorization"));
        configuration.setAllowCredentials(true);
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration);
        return source;
    }

    // ========================= OVERRIDE: SOBREESCRIBIR FUNCIONALIDAD SECURITY POR DEFECTO ======
    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        // Cross-Site Request Forgery CSRF
        // CORS (Cross-origin resource sharing)
        http.cors().and().csrf().disable()
                .exceptionHandling().authenticationEntryPoint(unauthorizedHandler).and()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS).and()
                .authorizeRequests().antMatchers("/api/auth/**").permitAll()
                .antMatchers("/v2/api-docs", "/configuration/**", "/swagger*/**", "/webjars/**").permitAll()
                .antMatchers("/api/hello/**").permitAll()
                .antMatchers("/").permitAll()
                .anyRequest().authenticated();

        http.addFilterBefore(authenticationJwtTokenFilter(), UsernamePasswordAuthenticationFilter.class);
    }

}

```