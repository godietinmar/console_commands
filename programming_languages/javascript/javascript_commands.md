# Comandos Básicos de JavaScript

Este documento recoge los comandos y sintaxis básica para trabajar con JavaScript en la consola del navegador o en entornos Node.js.

## Node.js

### node

**Descripción:**  
Ejecuta código JavaScript en el entorno de Node.js.

**Sintaxis:**
```bash
node [opciones] [archivo.js | -e "script" | - ] [argumentos]
```

**Opciones comunes:**
- `-v`, `--version`: Muestra la versión de Node.js
- `-e`, `--eval`: Evalúa el código pasado como argumento
- `--inspect`: Habilita el depurador
- `-r`, `--require`: Precargar módulo al inicio

**Ejemplos:**
```bash
# Ejecutar un archivo JavaScript
node app.js

# Mostrar versión
node -v

# Ejecutar código JavaScript directamente
node -e "console.log('Hola mundo')"

# Iniciar REPL (shell interactiva)
node

# Ejecutar con argumentos
node app.js arg1 arg2

# Cargar un módulo al inicio
node -r dotenv/config app.js
```

### npm

**Descripción:**  
Gestor de paquetes de Node.js.

**Sintaxis:**
```bash
npm <comando> [opciones]
```

**Comandos comunes:**
- `init`: Inicializa un nuevo proyecto npm
- `install`: Instala dependencias
- `uninstall`: Desinstala dependencias
- `update`: Actualiza paquetes
- `run`: Ejecuta scripts definidos en package.json
- `list`: Lista paquetes instalados
- `search`: Busca paquetes en el registro npm
- `publish`: Publica un paquete en el registro npm

**Ejemplos:**
```bash
# Inicializar proyecto
npm init

# Inicializar con valores predeterminados
npm init -y

# Instalar paquete
npm install express

# Instalar como dependencia de desarrollo
npm install --save-dev jest

# Instalar globalmente
npm install -g nodemon

# Desinstalar paquete
npm uninstall lodash

# Ejecutar script definido en package.json
npm run test

# Instalar todas las dependencias del proyecto
npm install

# Listar paquetes instalados
npm list

# Actualizar paquetes
npm update
```

### npx

**Descripción:**  
Ejecuta comandos de npm sin instalarlos globalmente.

**Sintaxis:**
```bash
npx [opciones] <comando> [argumentos]
```

**Opciones comunes:**
- `--no-install`: No instalar el paquete si no está disponible
- `--ignore-existing`: Ignorar binarios locales

**Ejemplos:**
```bash
# Ejecutar create-react-app sin instalarlo
npx create-react-app mi-aplicacion

# Ejecutar un paquete específico
npx cowsay "Hola mundo"

# Ejecutar con una versión específica
npx -p node@14 node -v
```

### yarn

**Descripción:**  
Gestor de paquetes alternativo para JavaScript.

**Sintaxis:**
```bash
yarn [comando] [opciones]
```

**Comandos comunes:**
- `init`: Inicializa un nuevo proyecto
- `add`: Instala dependencias
- `remove`: Elimina dependencias
- `upgrade`: Actualiza dependencias
- `run`: Ejecuta scripts

**Ejemplos:**
```bash
# Inicializar proyecto
yarn init

# Instalar todas las dependencias
yarn

# Instalar un paquete
yarn add express

# Instalar como dependencia de desarrollo
yarn add --dev jest

# Eliminar un paquete
yarn remove lodash

# Ejecutar script
yarn run test
```

## Herramientas de Desarrollo JavaScript

### babel

**Descripción:**  
Compilador de JavaScript que permite usar funciones modernas en navegadores antiguos.

**Sintaxis:**
```bash
babel [opciones] <archivo|directorio>
```

**Ejemplos:**
```bash
# Compilar un archivo
babel src/app.js --out-file dist/app.js

# Compilar un directorio completo
babel src --out-dir dist

# Usar configuración específica
babel src --config-file ./custom-babel.config.js
```

### webpack

**Descripción:**  
Empaquetador de módulos para JavaScript.

**Sintaxis:**
```bash
webpack [opciones]
```

**Opciones comunes:**
- `--mode`: Modo de construcción (development, production)
- `--config`: Archivo de configuración
- `--watch`: Observar cambios

**Ejemplos:**
```bash
# Construcción básica
webpack

# Usar configuración específica
webpack --config webpack.prod.js

# Modo desarrollo con observación de cambios
webpack --mode development --watch
```

### eslint

**Descripción:**  
Herramienta de linting para JavaScript.

**Sintaxis:**
```bash
eslint [opciones] [archivo|directorio|patrón]
```

**Opciones comunes:**
- `--fix`: Corregir automáticamente problemas
- `--init`: Inicializar configuración
- `--ext`: Extensiones de archivo a lintear

**Ejemplos:**
```bash
# Lintear archivo
eslint src/app.js

# Lintear directorio y autoarreglar
eslint src/ --fix

# Inicializar configuración
eslint --init

# Lintear archivos específicos
eslint --ext .js,.jsx src/
```

### prettier

**Descripción:**  
Formateador de código para JavaScript y otros lenguajes.

**Sintaxis:**
```bash
prettier [opciones] [archivo|directorio]
```

**Opciones comunes:**
- `--write`: Sobreescribir archivos formateados
- `--check`: Verificar si los archivos están formateados

**Ejemplos:**
```bash
# Formatear un archivo
prettier --write src/app.js

# Verificar formato sin modificar
prettier --check src/**/*.js

# Formatear todos los archivos
prettier --write "**/*.{js,jsx,json,css}"
```

### jest

**Descripción:**  
Framework de testing para JavaScript.

**Sintaxis:**
```bash
jest [opciones] [testNamePattern]
```

**Opciones comunes:**
- `--watch`: Ejecutar en modo observación
- `--coverage`: Generar informe de cobertura
- `--testPathPattern`: Patrón de rutas para tests

**Ejemplos:**
```bash
# Ejecutar todos los tests
jest

# Ejecutar en modo observación
jest --watch

# Ejecutar con cobertura
jest --coverage

# Ejecutar tests específicos
jest auth-tests
```

## Console API (Navegador/Node.js)

### console.log

**Descripción:**  
Imprime un mensaje en la consola.

**Sintaxis:**
```javascript
console.log([data][, ...args])
```

**Ejemplos:**
```javascript
// Mensaje simple
console.log('Hola mundo');

// Múltiples valores
console.log('Nombre:', 'Juan', 'Edad:', 30);

// Con interpolación
const nombre = 'María';
console.log(`Hola, ${nombre}!`);

// Con objetos
console.log({nombre: 'Juan', edad: 30});
```

### console.error

**Descripción:**  
Imprime un mensaje de error en la consola.

**Sintaxis:**
```javascript
console.error([data][, ...args])
```

**Ejemplos:**
```javascript
// Error simple
console.error('Error al cargar el archivo');

// Error con detalles
console.error('Error:', new Error('Archivo no encontrado'));
```

### console.warn

**Descripción:**  
Imprime un mensaje de advertencia en la consola.

**Sintaxis:**
```javascript
console.warn([data][, ...args])
```

**Ejemplos:**
```javascript
// Advertencia simple
console.warn('Esta función está obsoleta');
```

### console.info

**Descripción:**  
Imprime un mensaje informativo en la consola.

**Sintaxis:**
```javascript
console.info([data][, ...args])
```

**Ejemplos:**
```javascript
// Mensaje informativo
console.info('La aplicación se ha iniciado correctamente');
```

### console.table

**Descripción:**  
Muestra datos tabulares como una tabla.

**Sintaxis:**
```javascript
console.table(tabularData[, columns])
```

**Ejemplos:**
```javascript
// Mostrar array como tabla
console.table(['manzana', 'naranja', 'plátano']);

// Mostrar array de objetos como tabla
console.table([
  { nombre: 'Juan', edad: 30 },
  { nombre: 'María', edad: 25 },
  { nombre: 'Pedro', edad: 40 }
]);

// Mostrar columnas específicas
console.table([
  { nombre: 'Juan', edad: 30, ciudad: 'Madrid' },
  { nombre: 'María', edad: 25, ciudad: 'Barcelona' }
], ['nombre', 'edad']);
```

### console.time / console.timeEnd

**Descripción:**  
Mide el tiempo de ejecución entre dos puntos.

**Sintaxis:**
```javascript
console.time([label])
// código a medir
console.timeEnd([label])
```

**Ejemplos:**
```javascript
// Medir tiempo de ejecución
console.time('bucle');
for (let i = 0; i < 1000000; i++) {
  // Operación costosa
}
console.timeEnd('bucle');
```

### console.group / console.groupEnd

**Descripción:**  
Agrupa mensajes de consola juntos.

**Sintaxis:**
```javascript
console.group([label])
// mensajes de consola
console.groupEnd()
```

**Ejemplos:**
```javascript
// Agrupar mensajes relacionados
console.group('Información del usuario');
console.log('Nombre: Juan');
console.log('Edad: 30');
console.log('Email: juan@example.com');
console.groupEnd();
```

### console.trace

**Descripción:**  
Muestra una traza de pila en la consola.

**Sintaxis:**
```javascript
console.trace([message][, ...args])
```

**Ejemplos:**
```javascript
// Mostrar traza de pila
function funcionA() {
  funcionB();
}

function funcionB() {
  console.trace('Traza desde funcionB');
}

funcionA();
```

### console.clear

**Descripción:**  
Limpia la consola.

**Sintaxis:**
```javascript
console.clear()
```

**Ejemplos:**
```javascript
// Limpiar la consola
console.clear();
```

## Depuración en Navegador

### debugger

**Descripción:**  
Establece un punto de interrupción en el código.

**Sintaxis:**
```javascript
debugger;
```

**Ejemplos:**
```javascript
// Detener ejecución para depuración
function calcularTotal(items) {
  let total = 0;
  debugger; // El navegador pausa la ejecución aquí si las herramientas de desarrollo están abiertas
  for (const item of items) {
    total += item.precio * item.cantidad;
  }
  return total;
}
```

## Chrome DevTools Console

### $

**Descripción:**  
Atajo para `document.querySelector()` en la consola del navegador.

**Sintaxis:**
```javascript
$(selector)
```

**Ejemplos:**
```javascript
// Seleccionar el primer elemento que coincida
const header = $('#header');
```

### $$

**Descripción:**  
Atajo para `document.querySelectorAll()` en la consola del navegador.

**Sintaxis:**
```javascript
$$(selector)
```

**Ejemplos:**
```javascript
// Seleccionar todos los elementos que coincidan
const links = $$('a.external');
```

### $_

**Descripción:**  
Referencia al último resultado evaluado en la consola.

**Ejemplos:**
```javascript
// Usar el último resultado
[1, 2, 3, 4]
$_.map(x => x * 2) // [2, 4, 6, 8]
```

### $0 - $4

**Descripción:**  
Referencias a los últimos elementos DOM seleccionados en el panel de Elementos.

**Ejemplos:**
```javascript
// Acceder al elemento actualmente seleccionado
$0.style.color = 'red';
```

### copy

**Descripción:**  
Copia el argumento al portapapeles.

**Sintaxis:**
```javascript
copy(object)
```

**Ejemplos:**
```javascript
// Copiar un objeto al portapapeles
copy({nombre: 'Juan', edad: 30});
```

### keys / values

**Descripción:**  
Devuelve un array con las claves o valores de un objeto.

**Sintaxis:**
```javascript
keys(object)
values(object)
```

**Ejemplos:**
```javascript
// Obtener claves de un objeto
keys({nombre: 'Juan', edad: 30}); // ['nombre', 'edad']

// Obtener valores de un objeto
values({nombre: 'Juan', edad: 30}); // ['Juan', 30]
```

### monitor / unmonitor

**Descripción:**  
Monitorea las llamadas a una función.

**Sintaxis:**
```javascript
monitor(function)
unmonitor(function)
```

**Ejemplos:**
```javascript
// Monitorear llamadas a una función
function suma(a, b) { return a + b; }
monitor(suma);
suma(2, 3); // function suma called with arguments: 2, 3

// Dejar de monitorear
unmonitor(suma);
```

### monitorEvents / unmonitorEvents

**Descripción:**  
Monitorea eventos en un objeto (normalmente un elemento DOM).

**Sintaxis:**
```javascript
monitorEvents(object[, events])
unmonitorEvents(object[, events])
```

**Ejemplos:**
```javascript
// Monitorear todos los eventos en el cuerpo del documento
monitorEvents(document.body);

// Monitorear solo eventos de ratón
monitorEvents(document.body, ['click', 'mouseover']);

// Dejar de monitorear
unmonitorEvents(document.body);
```

## Node.js REPL

### .help

**Descripción:**  
Muestra ayuda en el REPL de Node.js.

**Ejemplos:**
```javascript
> .help
```

### .break / .clear

**Descripción:**  
Cancela la entrada actual o limpia el contexto en el REPL.

**Ejemplos:**
```javascript
> .break  // o Ctrl+C para cancelar entrada
> .clear  // para limpiar contexto
```

### .editor

**Descripción:**  
Entra en el modo editor para escribir código en múltiples líneas.

**Ejemplos:**
```javascript
> .editor
// Escribir código en múltiples líneas
// Ctrl+D para finalizar
```

### .exit / .quit

**Descripción:**  
Sale del REPL.

**Ejemplos:**
```javascript
> .exit  // o Ctrl+D para salir
```

### .save

**Descripción:**  
Guarda la sesión actual en un archivo.

**Sintaxis:**
```javascript
.save archivo
```

**Ejemplos:**
```javascript
> .save session.js
```

### .load

**Descripción:**  
Carga un archivo en la sesión actual.

**Sintaxis:**
```javascript
.load archivo
```

**Ejemplos:**
```javascript
> .load script.js
```

## Herramientas de JavaScript (Browser)

### `encodeURIComponent` / `decodeURIComponent`

**Descripción:**  
Codifica/decodifica componentes de una URL.

**Sintaxis:**
```javascript
encodeURIComponent(str)
decodeURIComponent(encodedURI)
```

**Ejemplos:**
```javascript
// Codificar caracteres especiales para URL
const param = encodeURIComponent('nombre=Juan&edad=30');
// Resultado: 'nombre%3DJuan%26edad%3D30'

// Decodificar
decodeURIComponent('nombre%3DJuan%26edad%3D30');
// Resultado: 'nombre=Juan&edad=30'
```

### `encodeURI` / `decodeURI`

**Descripción:**  
Codifica/decodifica una URL completa.

**Sintaxis:**
```javascript
encodeURI(uri)
decodeURI(encodedURI)
```

**Ejemplos:**
```javascript
// Codificar una URL
const url = encodeURI('https://example.com/path with spaces/');
// Resultado: 'https://example.com/path%20with%20spaces/'

// Decodificar
decodeURI('https://example.com/path%20with%20spaces/');
// Resultado: 'https://example.com/path with spaces/'
```

### `JSON.parse` / `JSON.stringify`

**Descripción:**  
Convierte entre cadenas JSON y objetos JavaScript.

**Sintaxis:**
```javascript
JSON.parse(text[, reviver])
JSON.stringify(value[, replacer[, space]])
```

**Ejemplos:**
```javascript
// Convertir cadena JSON a objeto
const obj = JSON.parse('{"nombre":"Juan","edad":30}');
// Resultado: {nombre: 'Juan', edad: 30}

// Convertir objeto a cadena JSON
const json = JSON.stringify({nombre: 'Juan', edad: 30}, null, 2);
// Resultado: '{\n  "nombre": "Juan",\n  "edad": 30\n}'

// Con función de reemplazo
JSON.stringify({nombre: 'Juan', edad: 30, contraseña: '123456'}, 
  (key, value) => key === 'contraseña' ? undefined : value);
// Resultado: '{"nombre":"Juan","edad":30}'
```

### `setTimeout` / `clearTimeout`

**Descripción:**  
Ejecuta una función después de un tiempo determinado.

**Sintaxis:**
```javascript
setTimeout(callback, delay[, arg1[, arg2[, ...]]])
clearTimeout(timeoutID)
```

**Ejemplos:**
```javascript
// Ejecutar función después de 2 segundos
const timeoutId = setTimeout(() => {
  console.log('Este mensaje aparece después de 2 segundos');
}, 2000);

// Cancelar timeout
clearTimeout(timeoutId);

// Con argumentos
setTimeout((nombre) => {
  console.log(`Hola, ${nombre}!`);
}, 1000, 'Juan');
```

### `setInterval` / `clearInterval`

**Descripción:**  
Ejecuta una función repetidamente con un intervalo de tiempo fijo.

**Sintaxis:**
```javascript
setInterval(callback, delay[, arg1[, arg2[, ...]]])
clearInterval(intervalID)
```

**Ejemplos:**
```javascript
// Ejecutar cada 3 segundos
const intervalId = setInterval(() => {
  console.log('Este mensaje aparece cada 3 segundos');
}, 3000);

// Detener después de 10 segundos
setTimeout(() => {
  clearInterval(intervalId);
  console.log('Intervalo detenido');
}, 10000);
```

### `localStorage` / `sessionStorage`

**Descripción:**  
Almacenamiento web en el navegador.

**Métodos:**
- `setItem(clave, valor)`: Guardar datos
- `getItem(clave)`: Obtener datos
- `removeItem(clave)`: Eliminar datos
- `clear()`: Eliminar todos los datos

**Ejemplos:**
```javascript
// Guardar datos
localStorage.setItem('usuario', 'Juan');
localStorage.setItem('preferencias', JSON.stringify({tema: 'oscuro', idioma: 'es'}));

// Obtener datos
const usuario = localStorage.getItem('usuario');
const preferencias = JSON.parse(localStorage.getItem('preferencias'));

// Eliminar datos
localStorage.removeItem('usuario');

// Eliminar todos los datos
localStorage.clear();

// Uso de sessionStorage (similar pero se pierde al cerrar pestaña)
sessionStorage.setItem('token', 'abc123');
```
