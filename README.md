# Proyecto REST API - Spring Boot 3.2 + Java 21 + Virtual Threads + Native Build






Este es un ejemplo de proyecto completo.


Este es un proyecto de ejemplo diseñado con buenas prácticas para que sirva como base sólida para construir APIs REST en Java, utilizando:





- **Java 21**


- **Spring Boot 3.2**


- **Threads virtuales (Virtual Threads)** para mejorar el rendimiento


- **Compilación nativa con GraalVM**


- **OpenAPI (API First)** para definir el contrato de la API REST


- **MapStruct** para mapear DTOs a entidades


- **JPA (Hibernate)** para persistencia


- **Validaciones personalizadas** con lógica de negocio


- **Pruebas completas**: unitarias, de integración y de carga (con Gatling en Java)


- **Versionado de API**: `/api/v1/`





---





## 🧱 Estructura del Proyecto





```


springboot-java21-native-virtualthreads/


│


├── src/


│   ├── main/


│   │   ├── java/


│   │   │   └── com.ejemplo.demo/


│   │   │       ├── controller/


│   │   │       ├── service/


│   │   │       ├── model/


│   │   │       ├── repository/


│   │   │       ├── mapper/


│   │   │       └── DemoApplication.java


│   │   └── resources/


│   │       ├── application.yml


│   │       └── openapi.yaml


│   └── test/


│       └── java/...


│


├── scripts/


│   ├── build.sh


│   ├── run.sh


│   └── clean.sh


│


├── README.md


└── pom.xml


```





---





## 🚀 Requisitos





- **Java 21**


- **Maven 3.9+**


- (Opcional) **GraalVM** si deseas compilar a nativo





---





## ⚙️ ¿Qué es API First?





Significa que **primero definimos la API** en un archivo `openapi.yaml` y luego generamos el código automáticamente.





Esto permite:





- Documentación clara desde el inicio


- Contratos compartidos entre frontend y backend


- Generación automática de clases DTO, interfaces y validaciones





---





## 📦 ¿Cómo generar clases desde OpenAPI?





Usamos el plugin de Maven `openapi-generator-maven-plugin`.





Ejecuta:





```bash


mvn clean install


mvn generate-sources


```





Esto generará las clases a partir de `src/main/resources/openapi.yaml`.





---





## 🧵 ¿Qué son los Virtual Threads?





Son una nueva característica de Java 21 que permite tener **miles de hilos concurrentes** sin el coste de los tradicionales.





- Permite que el servidor maneje muchas más peticiones sin bloquear


- Ideal para apps web y microservicios





Ya están **habilitados por defecto** en este proyecto (ver `application.yml` y configuración del `Tomcat`).





---





## 🧊 ¿Cómo funciona la compilación nativa?





Usamos GraalVM para convertir la app en un binario nativo:





```bash


./build.sh


```





Ventajas:





- 🏎️ Mucho más rápido al arrancar


- 🐏 Menor uso de memoria


- 🔐 Mayor seguridad (todo está embebido)





---





## ✅ Validaciones y lógica de negocio





La validación no se hace solo con anotaciones. También se incluye lógica personalizada, por ejemplo:





- Verificar si el usuario existe externamente


- Validar reglas de negocio





Ejemplo en `UserService`:





```java


if (!externalValidatorService.isValid(user.getEmail())) {


    throw new IllegalArgumentException("Email inválido");


}


```





---





## 🔄 Mapeos con MapStruct





MapStruct convierte fácilmente entre DTOs y entidades:





```java


@Mapper(componentModel = "spring")


public interface UserMapper {


    User toEntity(UserDto dto);


    UserDto toDto(User entity);


}


```





Esto mantiene el código limpio y desacoplado.





---





## 📁 Scripts útiles





```bash


./build.sh    # Compila y genera el binario nativo


./run.sh      # Arranca la app


./clean.sh    # Limpia archivos generados


```





---





## 🧪 Pruebas incluidas





- **Unitarias**: lógica de negocio (`UserServiceTest`)


- **Integración**: llamadas REST (`UserApiIntegrationTest`)


- **Carga**: con **Gatling en Java**





Ejecutar las pruebas:





```bash


mvn test


```





Para Gatling:





```bash


cd src/test/gatling


mvn gatling:test


```





---





## 🔀 Versionado de API





La API está expuesta bajo `/api/v1/...` para permitir futuras versiones sin romper clientes actuales.





---





## 🐳 ¿Futuro? Docker y despliegue





Puedes agregar un `Dockerfile` y dockerizar el binario nativo para tener una imagen ultraligera. Pídelo si quieres incluirlo.





---





## 🤝 Licencia





MIT — úsalo libremente para aprender o comenzar tus propios proyectos.





---





¿Tienes dudas? ¿Quieres que se incluya autenticación, Docker, Kafka o Swagger UI?  Add commentMore actions


Solo pídelas 😄