# Comandos Básicos de Python

Este documento recoge los principales comandos y sintaxis de Python para uso en la línea de comandos y entornos de desarrollo.

## Intérprete de Python

### python / python3

**Descripción:**  
Ejecuta el intérprete de Python.

**Sintaxis:**
```bash
python [opción] [script [argumentos]]
```

**Opciones comunes:**
- `-V`, `--version`: Muestra la versión de Python
- `-c cmd`: Ejecuta el comando Python proporcionado
- `-m mod`: Ejecuta un módulo como script
- `-i`: Entra en modo interactivo después de ejecutar el script
- `-u`: Modo unbuffered (salida sin búfer)

**Ejemplos:**
```bash
# Ver versión
python --version

# Ejecutar un script
python script.py

# Ejecutar un comando
python -c "print('Hola mundo')"

# Ejecutar un módulo
python -m http.server 8000

# Modo interactivo
python -i script.py

# Pasar argumentos a un script
python script.py arg1 arg2
```

### IDLE

**Descripción:**  
Entorno de desarrollo integrado para Python que viene con la instalación estándar.

**Sintaxis:**
```bash
idle [archivo]
```

**Ejemplos:**
```bash
# Iniciar IDLE
idle

# Abrir un archivo específico
idle script.py
```

## Gestión de Paquetes

### pip

**Descripción:**  
Gestor de paquetes de Python.

**Sintaxis:**
```bash
pip [comando] [opciones]
```

**Comandos comunes:**
- `install`: Instala paquetes
- `uninstall`: Desinstala paquetes
- `list`: Muestra paquetes instalados
- `show`: Muestra información de un paquete
- `search`: Busca paquetes
- `freeze`: Muestra los paquetes instalados en formato de requisitos

**Ejemplos:**
```bash
# Instalar un paquete
pip install requests

# Instalar versión específica
pip install requests==2.25.1

# Instalar con restricción de versión
pip install "requests>=2.20.0,<3.0.0"

# Instalar desde un archivo de requisitos
pip install -r requirements.txt

# Desinstalar un paquete
pip uninstall requests

# Listar paquetes instalados
pip list

# Ver información detallada de un paquete
pip show requests

# Buscar paquetes
pip search "http client"

# Generar archivo de requisitos
pip freeze > requirements.txt
```

### virtualenv

**Descripción:**  
Crea entornos virtuales aislados para Python.

**Sintaxis:**
```bash
virtualenv [opciones] directorio
```

**Opciones comunes:**
- `-p PYTHON`, `--python=PYTHON`: Especifica qué intérprete de Python usar
- `--system-site-packages`: Dar acceso a paquetes globales al entorno virtual
- `--no-pip`: No instalar pip
- `--no-setuptools`: No instalar setuptools

**Ejemplos:**
```bash
# Crear entorno virtual básico
virtualenv entorno

# Especificar versión de Python
virtualenv -p python3.9 entorno

# Crear entorno con acceso a paquetes globales
virtualenv --system-site-packages entorno

# Activar entorno virtual (Linux/Mac)
source entorno/bin/activate

# Activar entorno virtual (Windows)
entorno\Scripts\activate

# Desactivar entorno virtual
deactivate
```

### venv (Python 3.3+)

**Descripción:**  
Módulo integrado en Python 3.3+ para crear entornos virtuales.

**Sintaxis:**
```bash
python -m venv [opciones] directorio
```

**Opciones comunes:**
- `--system-site-packages`: Dar acceso a paquetes globales
- `--without-pip`: No instalar pip

**Ejemplos:**
```bash
# Crear entorno virtual
python -m venv mi_entorno

# Crear entorno con acceso a paquetes globales
python -m venv --system-site-packages mi_entorno

# Activar entorno virtual (Linux/Mac)
source mi_entorno/bin/activate

# Activar entorno virtual (Windows)
mi_entorno\Scripts\activate

# Desactivar entorno virtual
deactivate
```

### conda

**Descripción:**  
Sistema de gestión de paquetes y entornos para cualquier lenguaje (parte de Anaconda).

**Sintaxis:**
```bash
conda [comando] [opciones]
```

**Comandos comunes:**
- `create`: Crea un entorno
- `activate`: Activa un entorno
- `deactivate`: Desactiva el entorno actual
- `install`: Instala paquetes
- `update`: Actualiza paquetes
- `remove`: Elimina paquetes
- `list`: Lista paquetes instalados
- `info`: Muestra información del sistema conda
- `env list`: Lista entornos

**Ejemplos:**
```bash
# Crear un entorno
conda create --name mi_entorno python=3.8

# Crear entorno con paquetes específicos
conda create --name mi_entorno python=3.8 numpy pandas

# Activar entorno
conda activate mi_entorno

# Desactivar entorno
conda deactivate

# Instalar paquete
conda install numpy

# Instalar desde un canal específico
conda install -c conda-forge matplotlib

# Actualizar todos los paquetes
conda update --all

# Eliminar un paquete
conda remove pandas

# Listar entornos
conda env list

# Eliminar un entorno
conda env remove --name mi_entorno
```

## Herramientas de Desarrollo

### pytest

**Descripción:**  
Framework de pruebas para Python.

**Sintaxis:**
```bash
pytest [opciones] [archivo_o_directorio] [...]
```

**Opciones comunes:**
- `-v`, `--verbose`: Modo detallado
- `-q`, `--quiet`: Modo silencioso
- `-xvs`: Detener en primer fallo, modo verboso, no capturar salida
- `-k EXPRESIÓN`: Ejecuta pruebas que coincidan con la expresión
- `--cov`: Mide cobertura de código

**Ejemplos:**
```bash
# Ejecutar todas las pruebas
pytest

# Ejecutar un archivo específico
pytest test_app.py

# Ejecutar en modo detallado
pytest -v

# Detener en primer fallo, modo detallado
pytest -xvs

# Ejecutar pruebas que coincidan con una expresión
pytest -k "test_suma or test_resta"

# Medir cobertura
pytest --cov=mi_modulo
```

### flake8

**Descripción:**  
Herramienta para hacer cumplir el estilo de PEP 8.

**Sintaxis:**
```bash
flake8 [opciones] [archivo_o_directorio] [...]
```

**Opciones comunes:**
- `--max-line-length=N`: Longitud máxima de línea
- `--exclude=PATRONES`: Excluir archivos o directorios
- `--select=ERRORES`: Seleccionar solo ciertos errores
- `--ignore=ERRORES`: Ignorar errores específicos

**Ejemplos:**
```bash
# Analizar directorio actual
flake8 .

# Analizar archivo específico
flake8 mi_script.py

# Personalizar longitud de línea
flake8 --max-line-length=100 .

# Ignorar errores específicos
flake8 --ignore=E501,E303 .

# Excluir directorios
flake8 --exclude=venv,migrations .
```

### black

**Descripción:**  
Formateador de código Python intransigente.

**Sintaxis:**
```bash
black [opciones] [archivo_o_directorio] [...]
```

**Opciones comunes:**
- `-l`, `--line-length`: Longitud máxima de línea
- `-S`, `--skip-string-normalization`: No normalizar strings
- `--check`: No reformatear, solo comprobar
- `--diff`: Mostrar diferencias

**Ejemplos:**
```bash
# Formatear un archivo
black script.py

# Formatear todo el proyecto
black .

# Establecer longitud de línea específica
black -l 100 .

# Comprobar sin modificar
black --check .

# Mostrar diferencias sin modificar
black --diff .
```

### mypy

**Descripción:**  
Verificador de tipos estáticos para Python.

**Sintaxis:**
```bash
mypy [opciones] [archivo_o_módulo] [...]
```

**Opciones comunes:**
- `--strict`: Modo estricto de verificación de tipos
- `--ignore-missing-imports`: Ignorar importaciones faltantes
- `--show-error-codes`: Mostrar códigos de error

**Ejemplos:**
```bash
# Verificar un archivo
mypy script.py

# Modo estricto
mypy --strict script.py

# Ignorar importaciones faltantes
mypy --ignore-missing-imports script.py
```

### pydoc

**Descripción:**  
Generador de documentación y sistema de ayuda en línea.

**Sintaxis:**
```bash
pydoc [opciones] [nombre]
```

**Opciones comunes:**
- `-k palabra_clave`: Buscar palabra clave en documentación
- `-w nombre`: Escribir documentación HTML para el módulo
- `-p puerto`: Iniciar servidor HTTP en el puerto especificado

**Ejemplos:**
```bash
# Ver documentación de un módulo
pydoc math

# Buscar en la documentación
pydoc -k sort

# Generar HTML
pydoc -w os

# Iniciar servidor de documentación
pydoc -p 8080
```

## Perfilado y Depuración

### cProfile

**Descripción:**  
Perfilador de código Python.

**Sintaxis:**
```bash
python -m cProfile [-o archivo_salida] [-s clasificador] script.py [args]
```

**Opciones comunes:**
- `-o`: Guarda estadísticas en un archivo
- `-s`: Ordena estadísticas por columna específica

**Ejemplos:**
```bash
# Perfilar script
python -m cProfile script.py

# Perfilar y ordenar por tiempo
python -m cProfile -s time script.py

# Guardar resultados en archivo
python -m cProfile -o output.prof script.py
```

### pdb

**Descripción:**  
Depurador de Python.

**Sintaxis:**
```bash
python -m pdb script.py [args]
```

**Comandos comunes (dentro de pdb):**
- `h(elp)`: Ayuda
- `n(ext)`: Ejecutar la siguiente línea
- `s(tep)`: Paso a paso (adentrarse en funciones)
- `c(ontinue)`: Continuar hasta el siguiente punto de interrupción
- `b(reak)`: Establecer punto de interrupción
- `p(rint)`: Imprimir expresión
- `l(ist)`: Listar código fuente
- `q(uit)`: Salir del depurador

**Ejemplos:**
```bash
# Iniciar depuración
python -m pdb script.py

# También se puede usar dentro del script
import pdb; pdb.set_trace()  # Punto de interrupción
```

### timeit

**Descripción:**  
Medir el tiempo de ejecución de pequeños fragmentos de código.

**Sintaxis:**
```bash
python -m timeit [-n N] [-r N] [-s SETUP] código_a_medir
```

**Opciones comunes:**
- `-n N`: Número de ejecuciones
- `-r N`: Número de repeticiones
- `-s SETUP`: Código de configuración

**Ejemplos:**
```bash
# Medir tiempo de una expresión simple
python -m timeit "'-'.join(str(n) for n in range(100))"

# Con código de configuración
python -m timeit -s "data = list(range(10000))" "sorted(data)"

# Comparar dos implementaciones
python -m timeit -s "l = list(range(1000))" "l.sort()"
python -m timeit -s "l = list(range(1000))" "sorted(l)"
```

## Herramientas de Distribución

### setuptools

**Descripción:**  
Crear paquetes Python distribuibles.

**Sintaxis:**
```bash
python setup.py [comando]
```

**Comandos comunes:**
- `sdist`: Crear distribución de código fuente
- `bdist_wheel`: Crear distribución wheel
- `install`: Instalar el paquete
- `develop`: Instalar en modo de desarrollo

**Ejemplos:**
```bash
# Crear distribución de código fuente
python setup.py sdist

# Crear wheel
python setup.py bdist_wheel

# Instalar en modo desarrollo
python setup.py develop
```

### twine

**Descripción:**  
Cargar paquetes Python a PyPI.

**Sintaxis:**
```bash
twine [comando] [opciones] [archivos]
```

**Comandos comunes:**
- `check`: Verificar paquete
- `upload`: Subir a PyPI
- `register`: Registrar paquete en PyPI

**Ejemplos:**
```bash
# Verificar distribuciones
twine check dist/*

# Subir a PyPI
twine upload dist/*

# Subir a TestPyPI
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```

## Jupyter Notebook

### jupyter

**Descripción:**  
Interfaz web interactiva para Python y otros lenguajes.

**Sintaxis:**
```bash
jupyter [comando] [opciones]
```

**Comandos comunes:**
- `notebook`: Iniciar Jupyter Notebook
- `lab`: Iniciar JupyterLab
- `console`: Iniciar consola interactiva
- `nbconvert`: Convertir notebooks a otros formatos

**Ejemplos:**
```bash
# Iniciar Jupyter Notebook
jupyter notebook

# Iniciar en puerto específico
jupyter notebook --port=8888

# Iniciar sin navegador
jupyter notebook --no-browser

# Iniciar JupyterLab
jupyter lab

# Convertir notebook a Python
jupyter nbconvert --to python notebook.ipynb

# Convertir notebook a HTML
jupyter nbconvert --to html notebook.ipynb
```

## Interacción con la consola de Python

### help()

**Descripción:**  
Sistema de ayuda integrado.

**Sintaxis:**
```python
help()  # Modo interactivo
help(objeto)  # Ayuda sobre un objeto específico
```

**Ejemplos:**
```python
# Entrar en modo interactivo de ayuda
help()

# Ayuda sobre un módulo
help(os)

# Ayuda sobre una función
help(len)

# Ayuda sobre un método
help(str.split)
```

### dir()

**Descripción:**  
Lista los nombres dentro de un espacio de nombres o atributos de un objeto.

**Sintaxis:**
```python
dir()  # Lista nombres en el espacio actual
dir(objeto)  # Lista atributos del objeto
```

**Ejemplos:**
```python
# Ver nombres en el espacio actual
dir()

# Ver atributos de un módulo
import os
dir(os)

# Ver métodos y atributos de una cadena
dir("hola")
```

### type()

**Descripción:**  
Devuelve el tipo de un objeto.

**Sintaxis:**
```python
type(objeto)
```

**Ejemplos:**
```python
# Ver el tipo de un valor
type(42)  # <class 'int'>
type("hola")  # <class 'str'>
type([1, 2, 3])  # <class 'list'>

# Comprobar tipos
if type(x) is list:
    print("x es una lista")
```

### id()

**Descripción:**  
Devuelve el identificador único de un objeto.

**Sintaxis:**
```python
id(objeto)
```

**Ejemplos:**
```python
# Ver ID de un objeto
a = [1, 2, 3]
id(a)  # Por ejemplo: 140371523195968

# Comparar si dos variables refieren al mismo objeto
b = a
print(id(a) == id(b))  # True

c = [1, 2, 3]
print(id(a) == id(c))  # False
```

### vars()

**Descripción:**  
Devuelve el diccionario `__dict__` de un objeto o del módulo.

**Sintaxis:**
```python
vars()  # Equivalente a locals()
vars(objeto)  # __dict__ del objeto
```

**Ejemplos:**
```python
# Ver variables locales
vars()

# Ver atributos de un objeto
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

p = Persona("Juan", 30)
vars(p)  # {'nombre': 'Juan', 'edad': 30}
```

### locals(), globals()

**Descripción:**  
Devuelven diccionarios con variables locales o globales.

**Sintaxis:**
```python
locals()  # Variables locales
globals()  # Variables globales
```

**Ejemplos:**
```python
# Ver variables globales
globals()

# Ver variables locales
def funcion():
    x = 10
    y = 20
    print(locals())

funcion()  # {'x': 10, 'y': 20}
```

### input()

**Descripción:**  
Lee una línea de la entrada estándar.

**Sintaxis:**
```python
input([prompt])
```

**Ejemplos:**
```python
# Entrada básica
nombre = input("Introduce tu nombre: ")
print(f"Hola, {nombre}")

# Convertir a tipo específico
edad = int(input("Introduce tu edad: "))
altura = float(input("Introduce tu altura en metros: "))
```

### print()

**Descripción:**  
Imprime objetos en la salida estándar.

**Sintaxis:**
```python
print(*objetos, sep=' ', end='\n', file=sys.stdout, flush=False)
```

**Ejemplos:**
```python
# Impresión básica
print("Hola mundo")

# Múltiples argumentos
print("Nombre:", "Juan", "Edad:", 30)

# Cambiar separador
print("a", "b", "c", sep="-")  # "a-b-c"

# Cambiar final de línea
print("Sin salto de línea", end=" ")
print("en la misma línea")

# Escribir a un archivo
with open("salida.txt", "w") as f:
    print("Escrito a un archivo", file=f)

# Forzar vaciado del buffer
print("Mensaje urgente", flush=True)
```

### IPython Magic Commands

**Descripción:**  
Comandos especiales disponibles en IPython y Jupyter.

**Sintaxis:**
```python
%comando  # Line magic
%%comando  # Cell magic
```

**Ejemplos:**
```python
# Medir tiempo de ejecución
%time sorted(range(10000))

# Medir múltiples ejecuciones
%timeit [i**2 for i in range(1000)]

# Ejecutar comandos del sistema
%ls
%cd /ruta/al/directorio

# Depuración
%debug  # Ingresar al depurador

# Cargar extensiones
%load_ext autoreload
%autoreload 2  # Auto-recargar módulos modificados

# Cargar archivo como código
%load script.py

# Ejecutar archivo
%run script.py

# Cell magic para ejecutar código en otro lenguaje
%%bash
ls -la
echo "Ejecutando bash"

# Documentación
%pinfo función  # Equivalente a ?función
%pdoc función  # Mostrar docstring

# Mostrar variables
%who  # Lista de variables definidas
%whos  # Lista detallada de variables

# Guardar entorno
%save mi_sesion.py 1-10  # Guarda celdas 1 a 10
```

## Python AI/ML Commands

### Machine Learning Libraries

#### Scikit-learn
```bash
# Instalar scikit-learn
pip install scikit-learn

# Entrenar modelo desde línea de comandos
python -c "
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
import pickle

# Cargar datos
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Entrenar modelo
model = RandomForestClassifier()
model.fit(X_train, y_train)

# Evaluar
predictions = model.predict(X_test)
accuracy = accuracy_score(y_test, predictions)
print(f'Accuracy: {accuracy:.2f}')

# Guardar modelo
with open('iris_model.pkl', 'wb') as f:
    pickle.dump(model, f)
print('Model saved to iris_model.pkl')
"

# Hacer predicciones con modelo guardado
python -c "
import pickle
import numpy as np

# Cargar modelo
with open('iris_model.pkl', 'rb') as f:
    model = pickle.load(f)

# Hacer predicción
new_data = np.array([[5.1, 3.5, 1.4, 0.2]])
prediction = model.predict(new_data)
print(f'Prediction: {prediction[0]}')
"
```

#### TensorFlow/Keras
```bash
# Instalar TensorFlow
pip install tensorflow

# Entrenar modelo simple de clasificación
python -c "
import tensorflow as tf
from tensorflow.keras import layers, models
import numpy as np

# Datos sintéticos
X = np.random.random((1000, 20))
y = np.random.randint(2, size=(1000, 1))

# Crear modelo
model = models.Sequential([
    layers.Dense(64, activation='relu', input_shape=(20,)),
    layers.Dropout(0.2),
    layers.Dense(32, activation='relu'),
    layers.Dense(1, activation='sigmoid')
])

# Compilar
model.compile(optimizer='adam',
              loss='binary_crossentropy',
              metrics=['accuracy'])

# Entrenar
model.fit(X, y, epochs=10, batch_size=32, validation_split=0.2)

# Guardar modelo
model.save('my_model.h5')
print('Model saved to my_model.h5')
"

# Cargar y usar modelo guardado
python -c "
import tensorflow as tf
import numpy as np

# Cargar modelo
model = tf.keras.models.load_model('my_model.h5')

# Hacer predicción
new_data = np.random.random((1, 20))
prediction = model.predict(new_data)
print(f'Prediction: {prediction[0][0]:.4f}')
"

# Convertir modelo a TensorFlow Lite
python -c "
import tensorflow as tf

# Cargar modelo
model = tf.keras.models.load_model('my_model.h5')

# Convertir a TFLite
converter = tf.lite.TFLiteConverter.from_keras_model(model)
tflite_model = converter.convert()

# Guardar modelo TFLite
with open('model.tflite', 'wb') as f:
    f.write(tflite_model)
print('TFLite model saved to model.tflite')
"
```

#### PyTorch
```bash
# Instalar PyTorch
pip install torch torchvision torchaudio

# Entrenar modelo simple
python -c "
import torch
import torch.nn as nn
import torch.optim as optim
import numpy as np

# Datos sintéticos
X = torch.randn(1000, 10)
y = torch.randint(0, 2, (1000,)).float()

# Definir modelo
class SimpleNet(nn.Module):
    def __init__(self):
        super(SimpleNet, self).__init__()
        self.fc1 = nn.Linear(10, 64)
        self.fc2 = nn.Linear(64, 32)
        self.fc3 = nn.Linear(32, 1)
        self.relu = nn.ReLU()
        self.sigmoid = nn.Sigmoid()
    
    def forward(self, x):
        x = self.relu(self.fc1(x))
        x = self.relu(self.fc2(x))
        x = self.sigmoid(self.fc3(x))
        return x

# Crear modelo y optimizador
model = SimpleNet()
criterion = nn.BCELoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# Entrenar
for epoch in range(100):
    optimizer.zero_grad()
    outputs = model(X)
    loss = criterion(outputs.squeeze(), y)
    loss.backward()
    optimizer.step()
    
    if epoch % 20 == 0:
        print(f'Epoch {epoch}, Loss: {loss.item():.4f}')

# Guardar modelo
torch.save(model.state_dict(), 'pytorch_model.pth')
print('Model saved to pytorch_model.pth')
"
```

#### Pandas para Data Science
```bash
# Análisis de datos desde línea de comandos
python -c "
import pandas as pd
import numpy as np

# Crear datos sintéticos
data = {
    'feature1': np.random.randn(1000),
    'feature2': np.random.randn(1000),
    'target': np.random.choice([0, 1], 1000)
}
df = pd.DataFrame(data)

# Análisis estadístico básico
print('Dataset Info:')
print(df.info())
print('\nStatistical Summary:')
print(df.describe())
print('\nCorrelation Matrix:')
print(df.corr())

# Guardar datos
df.to_csv('dataset.csv', index=False)
print('Dataset saved to dataset.csv')
"

# Procesar CSV desde línea de comandos
python -c "
import pandas as pd

# Leer CSV
df = pd.read_csv('dataset.csv')

# Operaciones básicas
print(f'Dataset shape: {df.shape}')
print(f'Missing values: {df.isnull().sum().sum()}')
print(f'Target distribution:')
print(df['target'].value_counts())

# Filtrar datos
filtered_df = df[df['feature1'] > 0]
print(f'Filtered dataset shape: {filtered_df.shape}')

# Guardar datos procesados
filtered_df.to_csv('processed_dataset.csv', index=False)
"
```

### Computer Vision Libraries

#### OpenCV
```bash
# Instalar OpenCV
pip install opencv-python

# Procesar imagen desde línea de comandos
python -c "
import cv2
import numpy as np

# Leer imagen
img = cv2.imread('input.jpg')
if img is not None:
    # Convertir a escala de grises
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    # Aplicar filtro Gaussiano
    blurred = cv2.GaussianBlur(gray, (15, 15), 0)
    
    # Detectar bordes
    edges = cv2.Canny(blurred, 50, 150)
    
    # Guardar resultados
    cv2.imwrite('gray.jpg', gray)
    cv2.imwrite('blurred.jpg', blurred)
    cv2.imwrite('edges.jpg', edges)
    print('Image processing completed')
else:
    print('Error: Could not load input.jpg')
"

# Detectar caras en imagen
python -c "
import cv2

# Cargar clasificador de caras
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

# Leer imagen
img = cv2.imread('faces.jpg')
if img is not None:
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    # Detectar caras
    faces = face_cascade.detectMultiScale(gray, 1.1, 4)
    
    # Dibujar rectángulos alrededor de las caras
    for (x, y, w, h) in faces:
        cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)
    
    # Guardar imagen con caras detectadas
    cv2.imwrite('faces_detected.jpg', img)
    print(f'Detected {len(faces)} faces')
else:
    print('Error: Could not load faces.jpg')
"
```

#### PIL/Pillow
```bash
# Instalar Pillow
pip install Pillow

# Procesar múltiples imágenes
python -c "
from PIL import Image, ImageFilter, ImageEnhance
import os

# Procesar todas las imágenes JPG en el directorio actual
for filename in os.listdir('.'):
    if filename.lower().endswith('.jpg'):
        try:
            with Image.open(filename) as img:
                # Redimensionar
                resized = img.resize((800, 600))
                
                # Aplicar filtros
                blurred = resized.filter(ImageFilter.BLUR)
                sharpened = resized.filter(ImageFilter.SHARPEN)
                
                # Ajustar brillo
                enhancer = ImageEnhance.Brightness(resized)
                brightened = enhancer.enhance(1.2)
                
                # Guardar versiones procesadas
                base_name = os.path.splitext(filename)[0]
                resized.save(f'{base_name}_resized.jpg')
                blurred.save(f'{base_name}_blurred.jpg')
                sharpened.save(f'{base_name}_sharpened.jpg')
                brightened.save(f'{base_name}_brightened.jpg')
                
                print(f'Processed {filename}')
        except Exception as e:
            print(f'Error processing {filename}: {e}')
"
```

### Natural Language Processing

#### NLTK
```bash
# Instalar NLTK
pip install nltk

# Análisis de texto básico
python -c "
import nltk
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
from collections import Counter

# Descargar recursos necesarios
nltk.download('punkt')
nltk.download('stopwords')

# Texto de ejemplo
text = '''
Natural language processing (NLP) is a subfield of linguistics, 
computer science, and artificial intelligence concerned with the 
interactions between computers and human language.
'''

# Tokenización
sentences = sent_tokenize(text)
words = word_tokenize(text.lower())

# Eliminar stopwords
stop_words = set(stopwords.words('english'))
filtered_words = [w for w in words if w.isalpha() and w not in stop_words]

# Stemming
stemmer = PorterStemmer()
stemmed_words = [stemmer.stem(w) for w in filtered_words]

# Frecuencia de palabras
word_freq = Counter(stemmed_words)

print(f'Sentences: {len(sentences)}')
print(f'Total words: {len(words)}')
print(f'Filtered words: {len(filtered_words)}')
print(f'Most common words: {word_freq.most_common(5)}')
"
```

#### spaCy
```bash
# Instalar spaCy
pip install spacy

# Descargar modelo en inglés
python -m spacy download en_core_web_sm

# Análisis de texto con spaCy
python -c "
import spacy

# Cargar modelo
nlp = spacy.load('en_core_web_sm')

# Texto de ejemplo
text = 'Apple Inc. was founded by Steve Jobs in Cupertino, California.'

# Procesar texto
doc = nlp(text)

# Extraer entidades nombradas
print('Named Entities:')
for ent in doc.ents:
    print(f'{ent.text}: {ent.label_}')

# Análisis de dependencias
print('\nDependency Parsing:')
for token in doc:
    print(f'{token.text}: {token.dep_} -> {token.head.text}')

# POS tagging
print('\nPart-of-Speech Tags:')
for token in doc:
    print(f'{token.text}: {token.pos_}')
"
```

### API Integration for AI Services

#### OpenAI API
```bash
# Instalar OpenAI library
pip install openai

# Usar ChatGPT desde línea de comandos
python -c "
import openai
import os

# Configurar API key (asegúrate de tener OPENAI_API_KEY en variables de entorno)
openai.api_key = os.getenv('OPENAI_API_KEY')

if openai.api_key:
    try:
        response = openai.ChatCompletion.create(
            model='gpt-3.5-turbo',
            messages=[
                {'role': 'user', 'content': 'Explain machine learning in simple terms'}
            ],
            max_tokens=150
        )
        
        print('ChatGPT Response:')
        print(response.choices[0].message.content)
        
    except Exception as e:
        print(f'Error: {e}')
else:
    print('Please set OPENAI_API_KEY environment variable')
"

# Generar imagen con DALL-E
python -c "
import openai
import os

openai.api_key = os.getenv('OPENAI_API_KEY')

if openai.api_key:
    try:
        response = openai.Image.create(
            prompt='A futuristic city with flying cars',
            n=1,
            size='512x512'
        )
        
        image_url = response['data'][0]['url']
        print(f'Generated image URL: {image_url}')
        
    except Exception as e:
        print(f'Error: {e}')
else:
    print('Please set OPENAI_API_KEY environment variable')
"
```

### Jupyter/IPython for AI/ML

#### Jupyter Lab
```bash
# Instalar Jupyter Lab
pip install jupyterlab

# Iniciar Jupyter Lab
jupyter lab

# Iniciar en puerto específico
jupyter lab --port=8888

# Iniciar sin abrir navegador
jupyter lab --no-browser

# Listar kernels disponibles
jupyter kernelspec list

# Instalar kernel de Python
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"

# Convertir notebook a script Python
jupyter nbconvert --to script notebook.ipynb

# Convertir notebook a HTML
jupyter nbconvert --to html notebook.ipynb

# Ejecutar notebook desde línea de comandos
jupyter nbconvert --execute --to notebook notebook.ipynb
```

### Model Deployment

#### Flask API para modelos ML
```bash
# Crear API Flask simple para modelo ML
python -c "
from flask import Flask, request, jsonify
import pickle
import numpy as np

app = Flask(__name__)

# Cargar modelo (asumiendo que existe iris_model.pkl)
try:
    with open('iris_model.pkl', 'rb') as f:
        model = pickle.load(f)
    print('Model loaded successfully')
except FileNotFoundError:
    print('Model file not found. Train a model first.')
    model = None

@app.route('/predict', methods=['POST'])
def predict():
    if model is None:
        return jsonify({'error': 'Model not loaded'}), 500
    
    try:
        data = request.json
        features = np.array(data['features']).reshape(1, -1)
        prediction = model.predict(features)[0]
        probability = model.predict_proba(features)[0].max()
        
        return jsonify({
            'prediction': int(prediction),
            'probability': float(probability)
        })
    except Exception as e:
        return jsonify({'error': str(e)}), 400

@app.route('/health', methods=['GET'])
def health():
    return jsonify({'status': 'healthy'})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
" > ml_api.py

# Ejecutar API
python ml_api.py &

# Probar API
sleep 2
curl -X POST http://localhost:5000/predict \
     -H "Content-Type: application/json" \
     -d '{"features": [5.1, 3.5, 1.4, 0.2]}'
```

### Scripts de Automatización para AI/ML

#### Script de Entrenamiento Automatizado
```bash
#!/bin/bash
# train_models.py
python -c "
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report
import pickle
import json

# Cargar datos
try:
    df = pd.read_csv('dataset.csv')
    print(f'Dataset loaded: {df.shape}')
except FileNotFoundError:
    print('Dataset not found. Creating synthetic data...')
    import numpy as np
    data = {
        'feature1': np.random.randn(1000),
        'feature2': np.random.randn(1000),
        'feature3': np.random.randn(1000),
        'target': np.random.choice([0, 1], 1000)
    }
    df = pd.DataFrame(data)
    df.to_csv('dataset.csv', index=False)

# Preparar datos
X = df.drop('target', axis=1)
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Modelos a entrenar
models = {
    'random_forest': RandomForestClassifier(n_estimators=100, random_state=42),
    'gradient_boosting': GradientBoostingClassifier(random_state=42),
    'logistic_regression': LogisticRegression(random_state=42)
}

results = {}

# Entrenar y evaluar modelos
for name, model in models.items():
    print(f'Training {name}...')
    model.fit(X_train, y_train)
    
    # Predicciones
    train_pred = model.predict(X_train)
    test_pred = model.predict(X_test)
    
    # Métricas
    train_acc = accuracy_score(y_train, train_pred)
    test_acc = accuracy_score(y_test, test_pred)
    
    # Guardar modelo
    with open(f'{name}_model.pkl', 'wb') as f:
        pickle.dump(model, f)
    
    # Guardar resultados
    results[name] = {
        'train_accuracy': train_acc,
        'test_accuracy': test_acc,
        'classification_report': classification_report(y_test, test_pred, output_dict=True)
    }
    
    print(f'{name} - Train Acc: {train_acc:.3f}, Test Acc: {test_acc:.3f}')

# Guardar resultados
with open('model_results.json', 'w') as f:
    json.dump(results, f, indent=2)

print('Training completed. Results saved to model_results.json')
"
```

#### Script de Evaluación de Modelos
```bash
#!/bin/bash
# evaluate_models.py
python -c "
import pickle
import pandas as pd
import numpy as np
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
import json
import glob

# Cargar datos de prueba
df = pd.read_csv('dataset.csv')
X = df.drop('target', axis=1)
y = df['target']

# Encontrar todos los modelos guardados
model_files = glob.glob('*_model.pkl')

evaluation_results = {}

for model_file in model_files:
    model_name = model_file.replace('_model.pkl', '')
    
    try:
        # Cargar modelo
        with open(model_file, 'rb') as f:
            model = pickle.load(f)
        
        # Hacer predicciones
        predictions = model.predict(X)
        probabilities = model.predict_proba(X) if hasattr(model, 'predict_proba') else None
        
        # Calcular métricas
        accuracy = accuracy_score(y, predictions)
        conf_matrix = confusion_matrix(y, predictions).tolist()
        class_report = classification_report(y, predictions, output_dict=True)
        
        evaluation_results[model_name] = {
            'accuracy': accuracy,
            'confusion_matrix': conf_matrix,
            'classification_report': class_report
        }
        
        print(f'{model_name}: Accuracy = {accuracy:.3f}')
        
    except Exception as e:
        print(f'Error evaluating {model_name}: {e}')

# Guardar resultados de evaluación
with open('evaluation_results.json', 'w') as f:
    json.dump(evaluation_results, f, indent=2)

print('Evaluation completed. Results saved to evaluation_results.json')
"
```
