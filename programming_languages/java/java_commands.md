# ☕ Comandos Java

## Herramientas de Línea de Comandos

### javac
**Descripción:** Compilador de Java que convierte código fuente (.java) en bytecode (.class)
**Sintaxis básica:**
```bash
javac [opciones] archivo.java
```

### java
**Descripción:** Intérprete de Java que ejecuta aplicaciones Java compiladas
**Sintaxis básica:**
```bash
java [opciones] ClasePrincipal [argumentos]
```

### jar
**Descripción:** Herramienta para crear y manipular archivos JAR (Java Archive)
**Sintaxis básica:**
```bash
jar [opciones] archivo.jar [archivos...]
```

### javadoc
**Descripción:** Generador de documentación API de Java a partir de comentarios en el código
**Sintaxis básica:**
```bash
javadoc [opciones] paquetes|archivos
```

---

## Compilación y Ejecución

### Compilación Básica
```bash
# Compilar un archivo Java
javac MiClase.java

# Compilar múltiples archivos
javac *.java

# Compilar con classpath específico
javac -cp /ruta/a/libs/* MiClase.java

# Compilar con destino específico
javac -d build/ src/*.java
```

### Ejecución
```bash
# Ejecutar clase compilada
java MiClase

# Ejecutar con argumentos
java MiClase arg1 arg2

# Ejecutar con classpath
java -cp ".:lib/*" MiClase

# Ejecutar JAR
java -jar aplicacion.jar

# Ejecutar con configuración de memoria
java -Xms512m -Xmx2g MiClase
```

---

## Gestión de Archivos JAR

### Crear JAR
```bash
# Crear JAR básico
jar cf aplicacion.jar *.class

# Crear JAR con manifest
jar cfm aplicacion.jar MANIFEST.MF *.class

# Crear JAR ejecutable
jar cfe aplicacion.jar MiClase *.class

# Crear JAR desde directorio
jar cf aplicacion.jar -C build/ .
```

### Manipular JAR
```bash
# Listar contenido de JAR
jar tf aplicacion.jar

# Extraer JAR
jar xf aplicacion.jar

# Actualizar JAR
jar uf aplicacion.jar NuevaClase.class

# Ver manifest
jar xf aplicacion.jar META-INF/MANIFEST.MF
```

---

## Maven

### Comandos Básicos
```bash
# Crear proyecto Maven
mvn archetype:generate -DgroupId=com.ejemplo -DartifactId=mi-app

# Compilar proyecto
mvn compile

# Ejecutar tests
mvn test

# Empaquetar (crear JAR)
mvn package

# Instalar en repositorio local
mvn install

# Limpiar proyecto
mvn clean

# Ciclo completo
mvn clean compile test package install
```

### Gestión de Dependencias
```bash
# Descargar dependencias
mvn dependency:resolve

# Ver árbol de dependencias
mvn dependency:tree

# Copiar dependencias
mvn dependency:copy-dependencies

# Analizar dependencias
mvn dependency:analyze
```

### Spring Boot con Maven
```bash
# Crear proyecto Spring Boot
mvn archetype:generate -DgroupId=com.ejemplo -DartifactId=mi-app-spring -DarchetypeArtifactId=maven-archetype-quickstart

# Ejecutar aplicación Spring Boot
mvn spring-boot:run

# Crear JAR ejecutable
mvn spring-boot:build-image

# Ejecutar tests de integración
mvn integration-test
```

---

## Gradle

### Comandos Básicos
```bash
# Inicializar proyecto Gradle
gradle init

# Compilar proyecto
./gradlew build

# Ejecutar tests
./gradlew test

# Ejecutar aplicación
./gradlew run

# Limpiar proyecto
./gradlew clean

# Ver tareas disponibles
./gradlew tasks
```

### Gestión de Dependencias
```bash
# Ver dependencias
./gradlew dependencies

# Refrescar dependencias
./gradlew --refresh-dependencies

# Ver proyectos
./gradlew projects
```

---

## Herramientas de Desarrollo

### JDB (Java Debugger)
```bash
# Iniciar debugger
jdb MiClase

# Debugger con classpath
jdb -classpath . MiClase

# Comandos dentro de jdb
run                  # Ejecutar programa
stop at MiClase:10   # Punto de interrupción en línea 10
list                 # Ver código
print variable       # Ver valor de variable
step                 # Paso a paso
cont                 # Continuar ejecución
```

### JConsole (Monitoreo JVM)
```bash
# Iniciar JConsole
jconsole

# Conectar a proceso específico
jconsole <pid>

# Conectar remotamente
jconsole <hostname>:<port>
```

### VisualVM
```bash
# Iniciar VisualVM
jvisualvm

# Profiling de aplicación
jvisualvm --jdkhome $JAVA_HOME
```

---

## Gestión de Versiones Java

### SDKMAN
```bash
# Instalar SDKMAN
curl -s "https://get.sdkman.io" | bash

# Listar versiones Java disponibles
sdk list java

# Instalar Java
sdk install java 17.0.2-open

# Usar versión específica
sdk use java 17.0.2-open

# Cambiar versión por defecto
sdk default java 17.0.2-open

# Ver versión actual
sdk current java
```

### Verificación de Instalación
```bash
# Ver versión de Java
java -version

# Ver versión del compilador
javac -version

# Ver información de JVM
java -XshowSettings:properties -version

# Ver variables de entorno
echo $JAVA_HOME
```

---

## Ejemplos de Uso Común

### Proyecto Java Básico
```bash
# 1. Crear estructura de directorios
mkdir -p mi-proyecto/src/main/java/com/ejemplo
mkdir -p mi-proyecto/src/test/java/com/ejemplo
cd mi-proyecto

# 2. Crear archivo Java
cat > src/main/java/com/ejemplo/HolaMundo.java << 'EOF'
package com.ejemplo;

public class HolaMundo {
    public static void main(String[] args) {
        System.out.println("¡Hola Mundo!");
    }
}
EOF

# 3. Compilar
javac -d build src/main/java/com/ejemplo/HolaMundo.java

# 4. Ejecutar
java -cp build com.ejemplo.HolaMundo
```

### Proyecto Maven Spring Boot
```bash
# 1. Crear proyecto
mvn archetype:generate \
    -DgroupId=com.ejemplo \
    -DartifactId=mi-api-rest \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false

cd mi-api-rest

# 2. Agregar dependencias Spring Boot al pom.xml
# (Editar pom.xml manualmente)

# 3. Compilar y ejecutar
mvn spring-boot:run

# 4. Crear JAR
mvn clean package

# 5. Ejecutar JAR
java -jar target/mi-api-rest-1.0-SNAPSHOT.jar
```

### Testing con JUnit
```bash
# Compilar tests
javac -cp ".:junit-4.12.jar:hamcrest-core-1.3.jar" src/test/java/*.java

# Ejecutar tests
java -cp ".:junit-4.12.jar:hamcrest-core-1.3.jar:build" org.junit.runner.JUnitCore TestClass

# Con Maven
mvn test

# Con Gradle
./gradlew test
```

---

## Scripts de Utilidad

### Script de Build Completo
```bash
#!/bin/bash
# build.sh - Script de construcción completa

echo "🏗️  Iniciando build de proyecto Java..."

# Limpiar build anterior
echo "🧹 Limpiando build anterior..."
rm -rf build/
mkdir -p build/classes build/jar

# Compilar código fuente
echo "⚙️  Compilando código fuente..."
find src -name "*.java" | xargs javac -d build/classes -cp "lib/*"

if [ $? -eq 0 ]; then
    echo "✅ Compilación exitosa"
else
    echo "❌ Error en compilación"
    exit 1
fi

# Crear JAR
echo "📦 Creando JAR..."
jar cfm build/jar/aplicacion.jar manifest.txt -C build/classes .

# Ejecutar tests
echo "🧪 Ejecutando tests..."
java -cp "build/classes:lib/*:lib/test/*" org.junit.runner.JUnitCore TestSuite

echo "🎉 Build completo exitoso!"
```

### Script de Desarrollo Local
```bash
#!/bin/bash
# dev.sh - Script para desarrollo local

# Función para compilar y ejecutar
compile_and_run() {
    echo "🔄 Recompilando..."
    javac -d build -cp "lib/*" src/**/*.java
    
    if [ $? -eq 0 ]; then
        echo "🚀 Ejecutando aplicación..."
        java -cp "build:lib/*" com.ejemplo.Main
    else
        echo "❌ Error de compilación"
    fi
}

# Función para watch de archivos
watch_files() {
    echo "👀 Monitoreando cambios en archivos..."
    
    while inotifywait -r -e modify src/; do
        compile_and_run
    done
}

# Menú interactivo
echo "🛠️  Herramientas de Desarrollo Java"
echo "1. Compilar y ejecutar"
echo "2. Ejecutar tests"
echo "3. Modo watch (auto-recompilación)"
echo "4. Generar documentación"

read -p "Selecciona una opción: " option

case $option in
    1) compile_and_run ;;
    2) mvn test ;;
    3) watch_files ;;
    4) javadoc -d docs src/**/*.java ;;
    *) echo "Opción inválida" ;;
esac
```

### Script de Deploy
```bash
#!/bin/bash
# deploy.sh - Script de despliegue

APP_NAME="mi-aplicacion"
VERSION=$(grep -o '<version>.*</version>' pom.xml | head -1 | sed 's/<version>\(.*\)<\/version>/\1/')
JAR_FILE="target/${APP_NAME}-${VERSION}.jar"

echo "🚀 Desplegando ${APP_NAME} v${VERSION}..."

# Build del proyecto
echo "📦 Construyendo aplicación..."
mvn clean package -DskipTests

if [ ! -f "$JAR_FILE" ]; then
    echo "❌ No se encontró el JAR: $JAR_FILE"
    exit 1
fi

# Backup de versión anterior
if [ -f "/opt/apps/${APP_NAME}.jar" ]; then
    echo "💾 Creando backup..."
    cp "/opt/apps/${APP_NAME}.jar" "/opt/apps/${APP_NAME}.jar.backup"
fi

# Copiar nueva versión
echo "📋 Copiando nueva versión..."
sudo cp "$JAR_FILE" "/opt/apps/${APP_NAME}.jar"

# Reiniciar servicio
echo "🔄 Reiniciando servicio..."
sudo systemctl restart ${APP_NAME}

# Verificar estado
sleep 5
if sudo systemctl is-active --quiet ${APP_NAME}; then
    echo "✅ Despliegue exitoso!"
    echo "🌐 Aplicación disponible en: http://localhost:8080"
else
    echo "❌ Error en el despliegue"
    echo "📋 Logs del servicio:"
    sudo journalctl -u ${APP_NAME} --lines=20
fi
```

---

## Configuraciones y Optimización

### Configuración de JVM
```bash
# Variables de entorno comunes
export JAVA_OPTS="-Xms512m -Xmx2g -XX:+UseG1GC"
export MAVEN_OPTS="-Xmx1024m"

# Configuración para producción
java -server \
     -Xms2g -Xmx4g \
     -XX:+UseG1GC \
     -XX:MaxGCPauseMillis=200 \
     -XX:+HeapDumpOnOutOfMemoryError \
     -XX:HeapDumpPath=/var/log/heapdumps/ \
     -Djava.awt.headless=true \
     -jar aplicacion.jar
```

### Perfilado y Monitoreo
```bash
# Profiling con Flight Recorder
java -XX:+FlightRecorder \
     -XX:StartFlightRecording=duration=60s,filename=perfil.jfr \
     -jar aplicacion.jar

# Análisis de memoria
jmap -histogram <pid>
jmap -dump:live,format=b,file=heap.hprof <pid>

# Stack traces
jstack <pid> > stack-trace.txt

# Información de GC
jstat -gc -t <pid> 1s
```

Esta documentación cubre los comandos más importantes de Java, desde lo básico hasta herramientas avanzadas de desarrollo y despliegue.
