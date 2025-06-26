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

## JavaScript AI/ML Commands

### Machine Learning with TensorFlow.js

#### TensorFlow.js Installation and Setup
```bash
# Instalar TensorFlow.js para Node.js
npm install @tensorflow/tfjs-node

# Para usar GPU (si está disponible)
npm install @tensorflow/tfjs-node-gpu

# Para aplicaciones web
npm install @tensorflow/tfjs

# Instalar utilidades adicionales
npm install @tensorflow/tfjs-vis  # Para visualizaciones
npm install @tensorflow/tfjs-data  # Para manejo de datos
```

#### Training Models with TensorFlow.js
```bash
# Crear script de entrenamiento básico
node -e "
const tf = require('@tensorflow/tfjs-node');

// Crear datos sintéticos
const trainData = tf.randomNormal([1000, 10]);
const trainLabels = tf.randomUniform([1000, 1], 0, 2, 'int32');

// Crear modelo
const model = tf.sequential({
  layers: [
    tf.layers.dense({inputShape: [10], units: 64, activation: 'relu'}),
    tf.layers.dropout({rate: 0.2}),
    tf.layers.dense({units: 32, activation: 'relu'}),
    tf.layers.dense({units: 1, activation: 'sigmoid'})
  ]
});

// Compilar modelo
model.compile({
  optimizer: 'adam',
  loss: 'binaryCrossentropy',
  metrics: ['accuracy']
});

// Entrenar modelo
async function trainModel() {
  console.log('Training model...');
  const history = await model.fit(trainData, trainLabels, {
    epochs: 10,
    validationSplit: 0.2,
    callbacks: {
      onEpochEnd: (epoch, logs) => {
        console.log(\`Epoch \${epoch + 1}: loss = \${logs.loss.toFixed(4)}, accuracy = \${logs.acc.toFixed(4)}\`);
      }
    }
  });
  
  // Guardar modelo
  await model.save('file://./my-model');
  console.log('Model saved successfully');
}

trainModel().catch(console.error);
"

# Hacer predicciones con modelo guardado
node -e "
const tf = require('@tensorflow/tfjs-node');

async function loadAndPredict() {
  try {
    // Cargar modelo
    const model = await tf.loadLayersModel('file://./my-model/model.json');
    console.log('Model loaded successfully');
    
    // Datos de prueba
    const testData = tf.randomNormal([5, 10]);
    
    // Hacer predicciones
    const predictions = model.predict(testData);
    const predictionData = await predictions.data();
    
    console.log('Predictions:', Array.from(predictionData));
    
    // Limpiar memoria
    testData.dispose();
    predictions.dispose();
    
  } catch (error) {
    console.error('Error:', error.message);
  }
}

loadAndPredict();
"
```

#### Computer Vision with TensorFlow.js
```bash
# Instalar dependencias para visión por computadora
npm install @tensorflow-models/mobilenet
npm install @tensorflow-models/coco-ssd  # Para detección de objetos
npm install canvas  # Para Node.js image processing

# Clasificación de imágenes con MobileNet
node -e "
const tf = require('@tensorflow/tfjs-node');
const mobilenet = require('@tensorflow-models/mobilenet');
const fs = require('fs');

async function classifyImage() {
  try {
    // Cargar modelo preentrenado
    console.log('Loading MobileNet model...');
    const model = await mobilenet.load();
    console.log('Model loaded');
    
    // Para Node.js, necesitarías procesar la imagen
    // Este es un ejemplo conceptual
    console.log('Image classification ready');
    console.log('Model can classify 1000 different object classes');
    
  } catch (error) {
    console.error('Error:', error);
  }
}

classifyImage();
"

# Detección de objetos
node -e "
const tf = require('@tensorflow/tfjs-node');

async function loadObjectDetectionModel() {
  try {
    // Para Node.js necesitarías @tensorflow-models/coco-ssd
    console.log('Object detection models available:');
    console.log('- COCO-SSD: Real-time object detection');
    console.log('- YOLOv5: You Only Look Once v5');
    console.log('- Custom trained models');
    
  } catch (error) {
    console.error('Error:', error);
  }
}

loadObjectDetectionModel();
"
```

### Natural Language Processing

#### Basic NLP Operations
```bash
# Instalar bibliotecas de NLP
npm install natural  # Natural Language Processing library
npm install sentiment  # Sentiment analysis
npm install compromise  # NLP suite

# Análisis de sentimientos
node -e "
const sentiment = require('sentiment');
const Sentiment = new sentiment();

const texts = [
  'I love this product!',
  'This is terrible',
  'It is okay, not great but not bad',
  'Amazing experience, highly recommended!'
];

texts.forEach(text => {
  const result = Sentiment.analyze(text);
  console.log(\`Text: \${text}\`);
  console.log(\`Score: \${result.score}, Comparative: \${result.comparative}\`);
  console.log(\`Positive: \${result.positive.join(', ')}\`);
  console.log(\`Negative: \${result.negative.join(', ')}\`);
  console.log('---');
});
"

# Procesamiento de texto con Natural
node -e "
const natural = require('natural');

const text = 'Natural language processing is fascinating and useful';

// Tokenización
const tokens = natural.WordTokenizer().tokenize(text);
console.log('Tokens:', tokens);

// Stemming
const stemmed = tokens.map(token => natural.PorterStemmer.stem(token));
console.log('Stemmed:', stemmed);

// Distancia de strings
const distance = natural.JaroWinklerDistance('hello', 'helo');
console.log('String similarity:', distance);

// N-gramas
const nGrams = natural.NGrams.bigrams(tokens);
console.log('Bigrams:', nGrams);
"

# Análisis de texto con Compromise
node -e "
const nlp = require('compromise');

const text = 'John Smith is a software engineer at Google in California';

const doc = nlp(text);

// Extraer personas
const people = doc.people().out('array');
console.log('People:', people);

// Extraer lugares
const places = doc.places().out('array');
console.log('Places:', places);

// Extraer organizaciones
const orgs = doc.organizations().out('array');
console.log('Organizations:', orgs);

// POS tagging
console.log('POS Tags:');
doc.terms().forEach(term => {
  console.log(\`\${term.text}: \${term.tags.join(', ')}\`);
});
"
```

### API Integration for AI Services

#### OpenAI API Integration
```bash
# Instalar cliente de OpenAI
npm install openai

# Configurar y usar OpenAI API
node -e "
const { Configuration, OpenAIApi } = require('openai');

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});

const openai = new OpenAIApi(configuration);

async function chatWithGPT() {
  if (!process.env.OPENAI_API_KEY) {
    console.log('Please set OPENAI_API_KEY environment variable');
    return;
  }

  try {
    const completion = await openai.createChatCompletion({
      model: 'gpt-3.5-turbo',
      messages: [
        {
          role: 'user', 
          content: 'Explain machine learning in simple terms'
        }
      ],
      max_tokens: 150
    });

    console.log('ChatGPT Response:');
    console.log(completion.data.choices[0].message.content);
    
  } catch (error) {
    console.error('Error:', error.response?.data || error.message);
  }
}

chatWithGPT();
"

# Generar embeddings
node -e "
const { Configuration, OpenAIApi } = require('openai');

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});

const openai = new OpenAIApi(configuration);

async function generateEmbedding() {
  if (!process.env.OPENAI_API_KEY) {
    console.log('Please set OPENAI_API_KEY environment variable');
    return;
  }

  try {
    const response = await openai.createEmbedding({
      model: 'text-embedding-ada-002',
      input: 'Machine learning is a subset of artificial intelligence'
    });

    const embedding = response.data.data[0].embedding;
    console.log(\`Embedding dimension: \${embedding.length}\`);
    console.log(\`First 5 values: \${embedding.slice(0, 5).join(', ')}\`);
    
  } catch (error) {
    console.error('Error:', error.response?.data || error.message);
  }
}

generateEmbedding();
"
```

#### Google Cloud AI Integration
```bash
# Instalar cliente de Google Cloud
npm install @google-cloud/vision
npm install @google-cloud/language
npm install @google-cloud/translate

# Vision API
node -e "
// Requires GOOGLE_APPLICATION_CREDENTIALS environment variable
// pointing to service account key file

const vision = require('@google-cloud/vision');

async function analyzeImage() {
  try {
    const client = new vision.ImageAnnotatorClient();
    
    // Analizar imagen desde URL
    const [result] = await client.labelDetection({
      image: {
        source: {
          imageUri: 'https://example.com/image.jpg'
        }
      }
    });
    
    const labels = result.labelAnnotations;
    console.log('Labels detected:');
    labels.forEach(label => {
      console.log(\`- \${label.description}: \${(label.score * 100).toFixed(2)}%\`);
    });
    
  } catch (error) {
    console.error('Error:', error.message);
    console.log('Make sure GOOGLE_APPLICATION_CREDENTIALS is set');
  }
}

analyzeImage();
"

# Natural Language API
node -e "
const language = require('@google-cloud/language');

async function analyzeText() {
  try {
    const client = new language.LanguageServiceClient();
    
    const text = 'I love this new AI technology! It is amazing.';
    
    // Análisis de sentimiento
    const [sentiment] = await client.analyzeSentiment({
      document: {
        content: text,
        type: 'PLAIN_TEXT',
      },
    });
    
    console.log(\`Text: \${text}\`);
    console.log(\`Sentiment score: \${sentiment.documentSentiment.score}\`);
    console.log(\`Sentiment magnitude: \${sentiment.documentSentiment.magnitude}\`);
    
    // Análisis de entidades
    const [entities] = await client.analyzeEntities({
      document: {
        content: text,
        type: 'PLAIN_TEXT',
      },
    });
    
    console.log('Entities:');
    entities.entities.forEach(entity => {
      console.log(\`- \${entity.name}: \${entity.type}\`);
    });
    
  } catch (error) {
    console.error('Error:', error.message);
  }
}

analyzeText();
"
```

### Data Processing for AI

#### CSV and Data Manipulation
```bash
# Instalar bibliotecas para manejo de datos
npm install csv-parser
npm install csv-writer
npm install lodash

# Procesar datos CSV
node -e "
const fs = require('fs');
const csv = require('csv-parser');
const createCsvWriter = require('csv-writer').createObjectCsvWriter;
const _ = require('lodash');

const results = [];

// Leer CSV
fs.createReadStream('data.csv')
  .pipe(csv())
  .on('data', (data) => results.push(data))
  .on('end', () => {
    console.log(\`Loaded \${results.length} records\`);
    
    // Análisis básico
    if (results.length > 0) {
      const keys = Object.keys(results[0]);
      console.log('Columns:', keys);
      
      // Estadísticas básicas para columnas numéricas
      keys.forEach(key => {
        const values = results.map(row => parseFloat(row[key])).filter(v => !isNaN(v));
        if (values.length > 0) {
          console.log(\`\${key}: min=\${_.min(values)}, max=\${_.max(values)}, mean=\${_.mean(values).toFixed(2)}\`);
        }
      });
      
      // Filtrar y guardar datos procesados
      const filtered = results.filter(row => {
        // Ejemplo: filtrar filas válidas
        return Object.values(row).every(value => value !== '');
      });
      
      // Escribir CSV procesado
      const csvWriter = createCsvWriter({
        path: 'processed_data.csv',
        header: keys.map(key => ({id: key, title: key}))
      });
      
      csvWriter.writeRecords(filtered)
        .then(() => console.log(\`Processed data saved to processed_data.csv (\${filtered.length} records)\`));
    }
  })
  .on('error', (error) => {
    console.log('CSV file not found. Creating sample data...');
    
    // Crear datos de ejemplo
    const sampleData = Array.from({length: 100}, (_, i) => ({
      id: i + 1,
      feature1: Math.random() * 100,
      feature2: Math.random() * 50,
      target: Math.random() > 0.5 ? 1 : 0
    }));
    
    const csvWriter = createCsvWriter({
      path: 'data.csv',
      header: [
        {id: 'id', title: 'ID'},
        {id: 'feature1', title: 'Feature1'},
        {id: 'feature2', title: 'Feature2'},
        {id: 'target', title: 'Target'}
      ]
    });
    
    csvWriter.writeRecords(sampleData)
      .then(() => console.log('Sample data created in data.csv'));
  });
"
```

### Web Scraping for AI Data

#### Puppeteer for Data Collection
```bash
# Instalar Puppeteer
npm install puppeteer

# Web scraping básico
node -e "
const puppeteer = require('puppeteer');

async function scrapeData() {
  const browser = await puppeteer.launch({headless: true});
  const page = await browser.newPage();
  
  try {
    await page.goto('https://example.com');
    
    // Extraer texto de la página
    const content = await page.evaluate(() => {
      return {
        title: document.title,
        headings: Array.from(document.querySelectorAll('h1, h2, h3')).map(h => h.textContent.trim()),
        paragraphs: Array.from(document.querySelectorAll('p')).map(p => p.textContent.trim()).filter(text => text.length > 20)
      };
    });
    
    console.log('Scraped Data:');
    console.log('Title:', content.title);
    console.log('Headings:', content.headings);
    console.log('Paragraphs:', content.paragraphs.length);
    
    // Guardar datos
    const fs = require('fs');
    fs.writeFileSync('scraped_data.json', JSON.stringify(content, null, 2));
    console.log('Data saved to scraped_data.json');
    
  } catch (error) {
    console.error('Scraping error:', error.message);
  } finally {
    await browser.close();
  }
}

scrapeData();
"
```

### AI Model Serving

#### Express.js API for AI Models
```bash
# Instalar Express y middleware
npm install express cors helmet morgan

# Crear API para servir modelos AI
node -e "
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(helmet());
app.use(cors());
app.use(morgan('combined'));
app.use(express.json({ limit: '10mb' }));

// Simular carga de modelo AI
let model = null;
const initializeModel = () => {
  // Aquí cargarías tu modelo real (TensorFlow.js, etc.)
  model = {
    predict: (input) => {
      // Simulación de predicción
      return {
        prediction: Math.random() > 0.5 ? 'positive' : 'negative',
        confidence: Math.random()
      };
    }
  };
  console.log('AI Model loaded successfully');
};

// Rutas
app.get('/health', (req, res) => {
  res.json({ 
    status: 'healthy', 
    model_loaded: model !== null,
    timestamp: new Date().toISOString()
  });
});

app.post('/predict', (req, res) => {
  if (!model) {
    return res.status(503).json({ error: 'Model not loaded' });
  }
  
  try {
    const { input } = req.body;
    
    if (!input) {
      return res.status(400).json({ error: 'Input data required' });
    }
    
    const result = model.predict(input);
    
    res.json({
      success: true,
      result: result,
      timestamp: new Date().toISOString()
    });
    
  } catch (error) {
    console.error('Prediction error:', error);
    res.status(500).json({ error: 'Prediction failed' });
  }
});

app.post('/batch-predict', (req, res) => {
  if (!model) {
    return res.status(503).json({ error: 'Model not loaded' });
  }
  
  try {
    const { inputs } = req.body;
    
    if (!Array.isArray(inputs)) {
      return res.status(400).json({ error: 'Inputs must be an array' });
    }
    
    const results = inputs.map(input => model.predict(input));
    
    res.json({
      success: true,
      results: results,
      count: results.length,
      timestamp: new Date().toISOString()
    });
    
  } catch (error) {
    console.error('Batch prediction error:', error);
    res.status(500).json({ error: 'Batch prediction failed' });
  }
});

// Inicializar modelo y servidor
initializeModel();

app.listen(PORT, () => {
  console.log(\`AI API server running on port \${PORT}\`);
  console.log(\`Health check: http://localhost:\${PORT}/health\`);
  console.log(\`Prediction endpoint: http://localhost:\${PORT}/predict\`);
});
" > ai_api.js

# Ejecutar API
node ai_api.js &

# Probar API
sleep 2
echo "Testing API..."
curl -X GET http://localhost:3000/health | node -e "
const data = JSON.parse(require('fs').readFileSync(0, 'utf8'));
console.log('Health Check:', JSON.stringify(data, null, 2));
"

curl -X POST http://localhost:3000/predict \
     -H "Content-Type: application/json" \
     -d '{"input": "This is a test input"}' | node -e "
const data = JSON.parse(require('fs').readFileSync(0, 'utf8'));
console.log('Prediction Result:', JSON.stringify(data, null, 2));
"
```

### Automation Scripts for AI/ML

#### Model Training Pipeline
```bash
#!/bin/bash
# Crear pipeline de entrenamiento
cat > train_pipeline.js << 'EOF'
const tf = require('@tensorflow/tfjs-node');
const fs = require('fs');

class MLPipeline {
  constructor() {
    this.model = null;
    this.trainingHistory = null;
  }

  // Generar datos sintéticos
  generateData(samples = 1000) {
    console.log(`Generating ${samples} synthetic data points...`);
    
    const features = tf.randomNormal([samples, 5]);
    const noise = tf.randomNormal([samples, 1], 0, 0.1);
    const labels = features.sum(1, true).add(noise);
    
    return { features, labels };
  }

  // Crear modelo
  createModel() {
    console.log('Creating model architecture...');
    
    this.model = tf.sequential({
      layers: [
        tf.layers.dense({
          inputShape: [5],
          units: 64,
          activation: 'relu',
          name: 'hidden1'
        }),
        tf.layers.dropout({ rate: 0.2 }),
        tf.layers.dense({
          units: 32,
          activation: 'relu',
          name: 'hidden2'
        }),
        tf.layers.dense({
          units: 1,
          name: 'output'
        })
      ]
    });

    this.model.compile({
      optimizer: tf.train.adam(0.001),
      loss: 'meanSquaredError',
      metrics: ['mae']
    });

    console.log('Model created and compiled');
    this.model.summary();
  }

  // Entrenar modelo
  async trainModel(features, labels, epochs = 50) {
    console.log(`Training model for ${epochs} epochs...`);
    
    const validationSplit = 0.2;
    
    this.trainingHistory = await this.model.fit(features, labels, {
      epochs: epochs,
      validationSplit: validationSplit,
      shuffle: true,
      callbacks: {
        onEpochEnd: (epoch, logs) => {
          if (epoch % 10 === 0) {
            console.log(`Epoch ${epoch + 1}/${epochs}:`);
            console.log(`  Loss: ${logs.loss.toFixed(4)}`);
            console.log(`  MAE: ${logs.mae.toFixed(4)}`);
            console.log(`  Val Loss: ${logs.val_loss.toFixed(4)}`);
            console.log(`  Val MAE: ${logs.val_mae.toFixed(4)}`);
          }
        }
      }
    });

    console.log('Training completed');
  }

  // Evaluar modelo
  async evaluateModel(features, labels) {
    console.log('Evaluating model...');
    
    const evaluation = this.model.evaluate(features, labels);
    const [loss, mae] = await Promise.all([
      evaluation[0].data(),
      evaluation[1].data()
    ]);

    console.log(`Evaluation Results:`);
    console.log(`  Loss: ${loss[0].toFixed(4)}`);
    console.log(`  MAE: ${mae[0].toFixed(4)}`);

    // Limpiar tensores
    evaluation.forEach(tensor => tensor.dispose());

    return { loss: loss[0], mae: mae[0] };
  }

  // Guardar modelo
  async saveModel(path = './saved_model') {
    console.log(`Saving model to ${path}...`);
    await this.model.save(`file://${path}`);
    
    // Guardar historial de entrenamiento
    const historyData = {
      loss: this.trainingHistory.history.loss,
      mae: this.trainingHistory.history.mae,
      val_loss: this.trainingHistory.history.val_loss,
      val_mae: this.trainingHistory.history.val_mae
    };
    
    fs.writeFileSync(`${path}/training_history.json`, JSON.stringify(historyData, null, 2));
    console.log('Model and training history saved');
  }

  // Pipeline completo
  async runPipeline() {
    try {
      // Generar datos
      const { features, labels } = this.generateData(2000);
      
      // Crear modelo
      this.createModel();
      
      // Entrenar
      await this.trainModel(features, labels, 100);
      
      // Evaluar
      await this.evaluateModel(features, labels);
      
      // Guardar
      await this.saveModel('./ml_model');
      
      // Limpiar memoria
      features.dispose();
      labels.dispose();
      
      console.log('Pipeline completed successfully!');
      
    } catch (error) {
      console.error('Pipeline failed:', error);
    }
  }
}

// Ejecutar pipeline
const pipeline = new MLPipeline();
pipeline.runPipeline();
EOF

# Ejecutar pipeline
node train_pipeline.js
```
