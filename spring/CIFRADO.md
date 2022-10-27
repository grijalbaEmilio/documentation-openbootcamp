## Cifrado 

Es el proceso de codificar la información de su representación original (texto plano) 
a texto cifrado, de manera que solamente pueda ser descifrado utilizando una clave.

Historia del cifrado: 

1. Almacenar contraseñas en texto plano
2. Almacenar contraseñas cifradas con una función hash
3. Almacenar contraseñas cifradas con una función hash + salt
4. Almacenar contraseñas cifradas con una función adaptativa + factor de trabajo

La seguridad se gana haciendo que la validación de contraseñas sea costosa computacionalmente. 

## Algoritmos en Spring Security

* BCrypt 
* PBKDF2
* scrypt 
* argon2

un ejemplo del `BCrypt`

```java
@Test
void bcryptTest(){

    BCryptPasswordEncoder passwordEncoder = new BCryptPasswordEncoder();
    String hashedPassword = passwordEncoder.encode("admin"); // codifica la contraseña "admin"
    System.out.println(hashedPassword);

    boolean matches = passwordEncoder.matches("admin", hashedPassword); // verifica que la contraseña coincida
    System.out.println(matches);

}
```

Hay varias formas de implemetar el cifrado

```java
@Test
    void bcryptCheckMultiplePasswords(){

        BCryptPasswordEncoder passwordEncoder = new BCryptPasswordEncoder();
        for (int i = 0; i < 30; i++)
            System.out.println(passwordEncoder.encode("admin"));

    }


    @Test
    void pbkdf2() {
        Pbkdf2PasswordEncoder passwordEncoder = new Pbkdf2PasswordEncoder();
        for (int i = 0; i < 30; i++)
            System.out.println(passwordEncoder.encode("admin"));
    }

    @Test
    void argon() {
        Argon2PasswordEncoder passwordEncoder = new Argon2PasswordEncoder();
        for (int i = 0; i < 30; i++)
            System.out.println(passwordEncoder.encode("admin"));
    }

    @Test
    void scrypt() {
        SCryptPasswordEncoder passwordEncoder = new SCryptPasswordEncoder();
        for (int i = 0; i < 30; i++)
            System.out.println(passwordEncoder.encode("admin"));
    }

      @Test
    void springPasswordEncoders(){

        Map<String, PasswordEncoder> encoders = new HashMap<>();
        encoders.put("bcrypt", new BCryptPasswordEncoder());
        encoders.put("pbkdf2", new Pbkdf2PasswordEncoder());
        encoders.put("argon2", new Argon2PasswordEncoder());
        encoders.put("scrypt", new SCryptPasswordEncoder());
        // no seguro:
        encoders.put("noop", NoOpPasswordEncoder.getInstance());
        encoders.put("sha256", new StandardPasswordEncoder());

        PasswordEncoder passwordEncoder = new DelegatingPasswordEncoder("bcrypt", encoders);

        String hashedPassword = passwordEncoder.encode("admin");
        System.out.println(hashedPassword);

    }
```
