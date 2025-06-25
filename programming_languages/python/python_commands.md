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
