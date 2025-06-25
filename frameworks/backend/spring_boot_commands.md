# Spring Boot Commands

Spring Boot es un framework de Java que facilita la creación de aplicaciones Spring independientes y de grado de producción.

## Instalación y Configuración

### Instalar Spring Boot CLI
```bash
# macOS con Homebrew
brew tap spring-io/tap
brew install spring-boot

# Linux con SDKMAN
curl -s "https://get.sdkman.io" | bash
sdk install springboot
```

### Verificar instalación
```bash
spring --version
```

### Crear proyecto con Spring Initializr
```bash
spring init --dependencies=web,jpa,h2 myproject
```

### Crear proyecto con opciones específicas
```bash
spring init --dependencies=web,security,jpa,mysql \
    --java-version=17 \
    --packaging=jar \
    --boot-version=3.1.0 \
    myproject
```

## Comandos de Desarrollo con Maven

### Compilar proyecto
```bash
./mvnw compile
```

### Ejecutar aplicación
```bash
./mvnw spring-boot:run
```

### Ejecutar con perfil específico
```bash
./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

### Ejecutar con argumentos
```bash
./mvnw spring-boot:run -Dspring-boot.run.arguments="--server.port=8080"
```

### Compilar y crear JAR
```bash
./mvnw clean package
```

### Ejecutar JAR generado
```bash
java -jar target/myproject-0.0.1-SNAPSHOT.jar
```

### Ejecutar tests
```bash
./mvnw test
```

### Ejecutar tests específicos
```bash
./mvnw test -Dtest=MyTestClass
```

### Generar reporte de coverage
```bash
./mvnw jacoco:report
```

## Comandos de Desarrollo con Gradle

### Compilar proyecto
```bash
./gradlew build
```

### Ejecutar aplicación
```bash
./gradlew bootRun
```

### Ejecutar con perfil específico
```bash
./gradlew bootRun --args='--spring.profiles.active=dev'
```

### Ejecutar tests
```bash
./gradlew test
```

### Crear JAR ejecutable
```bash
./gradlew bootJar
```

### Limpiar build
```bash
./gradlew clean
```

## Comandos de Spring Boot DevTools

### Habilitar restart automático
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>
```

### Configurar LiveReload
```bash
# Agregar en application.properties
spring.devtools.livereload.enabled=true
```

## Comandos de Actuator

### Agregar dependencia de Actuator
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

### Verificar health endpoint
```bash
curl http://localhost:8080/actuator/health
```

### Ver información de la aplicación
```bash
curl http://localhost:8080/actuator/info
```

### Ver métricas
```bash
curl http://localhost:8080/actuator/metrics
```

### Ver beans registrados
```bash
curl http://localhost:8080/actuator/beans
```

### Ver configuración
```bash
curl http://localhost:8080/actuator/configprops
```

## Comandos de Base de Datos

### Ejecutar migraciones Flyway
```bash
./mvnw flyway:migrate
```

### Limpiar base de datos Flyway
```bash
./mvnw flyway:clean
```

### Ver información de Flyway
```bash
./mvnw flyway:info
```

### Generar esquema con Hibernate
```bash
./mvnw spring-boot:run -Dspring.jpa.hibernate.ddl-auto=create
```

### Ejecutar scripts SQL al inicio
```properties
# En application.properties
spring.sql.init.mode=always
spring.sql.init.schema-locations=classpath:schema.sql
spring.sql.init.data-locations=classpath:data.sql
```

## Comandos de Testing

### Ejecutar tests de integración
```bash
./mvnw test -Dtest=*IntegrationTest
```

### Ejecutar tests con perfil de test
```bash
./mvnw test -Dspring.profiles.active=test
```

### Ejecutar con TestContainers
```bash
./mvnw test -Dtestcontainers.reuse.enable=true
```

### Generar reporte de tests
```bash
./mvnw surefire-report:report
```

## Comandos de Profiles

### Ejecutar con perfil específico
```bash
java -jar -Dspring.profiles.active=prod myapp.jar
```

### Múltiples perfiles
```bash
java -jar -Dspring.profiles.active=prod,metrics myapp.jar
```

### Variables de entorno
```bash
export SPRING_PROFILES_ACTIVE=prod
java -jar myapp.jar
```

## Comandos de Docker

### Crear imagen Docker
```bash
./mvnw spring-boot:build-image
```

### Crear imagen con nombre específico
```bash
./mvnw spring-boot:build-image -Dspring-boot.build-image.imageName=myorg/myapp
```

### Ejecutar con Docker Compose
```bash
docker-compose up -d
```

### Ver logs de contenedor
```bash
docker logs myapp-container
```

## Comandos de Deployment

### Crear WAR para deployment
```bash
./mvnw clean package -Pwar
```

### Ejecutar con configuración externa
```bash
java -jar myapp.jar --spring.config.location=classpath:/application.properties,/path/to/external/config/
```

### Configurar JVM para producción
```bash
java -Xmx2g -Xms1g -XX:+UseG1GC -jar myapp.jar
```

### Ejecutar como servicio systemd
```bash
sudo systemctl enable myapp
sudo systemctl start myapp
sudo systemctl status myapp
```

## Comandos de Monitoreo

### Habilitar JMX
```bash
java -Dcom.sun.management.jmxremote \
     -Dcom.sun.management.jmxremote.port=9999 \
     -Dcom.sun.management.jmxremote.authenticate=false \
     -Dcom.sun.management.jmxremote.ssl=false \
     -jar myapp.jar
```

### Conectar con JConsole
```bash
jconsole localhost:9999
```

### Generar heap dump
```bash
jcmd <pid> GC.run_finalization
jcmd <pid> VM.gc
jcmd <pid> GC.run
```

## Comandos de Seguridad

### Generar keystore para HTTPS
```bash
keytool -genkeypair -alias myapp -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore myapp.p12 -validity 3650
```

### Configurar HTTPS
```properties
server.ssl.key-store=classpath:myapp.p12
server.ssl.key-store-password=password
server.ssl.keyStoreType=PKCS12
server.ssl.keyAlias=myapp
```

## Utilidades de Desarrollo

### Instalar Spring Boot CLI con dependencias
```bash
spring install org.springframework:spring-core:5.3.21
```

### Ejecutar Groovy script con Spring Boot
```bash
spring run app.groovy
```

### Generar proyecto desde template
```bash
spring init --list
spring init --dependencies=web,jpa --type=gradle-project myproject
```

### Verificar dependencias
```bash
./mvnw dependency:tree
```

### Actualizar versiones
```bash
./mvnw versions:display-dependency-updates
```
