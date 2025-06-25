# Comandos Git

Este archivo contiene una lista de comandos comunes de Git para gestionar repositorios y controlar versiones.

## Configuración

### git config

**Descripción:**  
Configura opciones de Git.

**Sintaxis:**
```bash
git config [opciones] [nombre] [valor]
```

**Opciones comunes:**
- `--global`: Aplicar configuración a nivel global (para todos los repositorios del usuario)
- `--local`: Aplicar configuración solo al repositorio actual
- `--system`: Aplicar configuración a nivel de sistema (para todos los usuarios)
- `--list`: Listar todas las configuraciones

**Ejemplos:**
```bash
# Configurar nombre de usuario
git config --global user.name "Tu Nombre"

# Configurar email
git config --global user.email "tu.email@ejemplo.com"

# Ver todas las configuraciones
git config --list

# Configurar editor predeterminado
git config --global core.editor "code --wait"
```

## Crear y Clonar Repositorios

### git init

**Descripción:**  
Inicializa un nuevo repositorio Git.

**Sintaxis:**
```bash
git init [directorio]
```

**Ejemplos:**
```bash
# Inicializar repositorio en el directorio actual
git init

# Inicializar repositorio en un directorio específico
git init mi-proyecto
```

### git clone

**Descripción:**  
Clona un repositorio existente.

**Sintaxis:**
```bash
git clone [url] [directorio]
```

**Opciones comunes:**
- `--depth`: Número de commits a clonar (clon superficial)
- `--branch`, `-b`: Clonar una rama específica

**Ejemplos:**
```bash
# Clonar un repositorio
git clone https://github.com/usuario/repositorio.git

# Clonar un repositorio en un directorio específico
git clone https://github.com/usuario/repositorio.git mi-directorio

# Clonar solo la rama main con historial limitado
git clone --branch main --depth 1 https://github.com/usuario/repositorio.git
```

## Trabajar con Cambios

### git status

**Descripción:**  
Muestra el estado del área de trabajo.

**Sintaxis:**
```bash
git status [opciones]
```

**Opciones comunes:**
- `-s`, `--short`: Formato corto
- `-b`, `--branch`: Mostrar información de la rama

**Ejemplos:**
```bash
# Ver estado completo
git status

# Ver estado en formato corto
git status -s
```

### git add

**Descripción:**  
Añade archivos al área de preparación (staging).

**Sintaxis:**
```bash
git add [opciones] [archivo(s)]
```

**Opciones comunes:**
- `-A`, `--all`: Añadir todos los archivos
- `-p`, `--patch`: Añadir partes específicas de archivos
- `-u`: Añadir solo archivos ya rastreados

**Ejemplos:**
```bash
# Añadir un archivo específico
git add archivo.txt

# Añadir todos los archivos
git add .

# Añadir todos los archivos excepto los nuevos
git add -u

# Añadir interactivamente partes de archivos
git add -p
```

### git commit

**Descripción:**  
Guarda los cambios en el repositorio.

**Sintaxis:**
```bash
git commit [opciones]
```

**Opciones comunes:**
- `-m`: Especificar mensaje de commit
- `-a`: Añadir automáticamente todos los archivos modificados
- `--amend`: Modificar el commit más reciente

**Ejemplos:**
```bash
# Commit con mensaje
git commit -m "Descripción de los cambios"

# Añadir cambios y hacer commit en un solo paso
git commit -am "Descripción de los cambios"

# Modificar el último commit
git commit --amend -m "Nuevo mensaje de commit"
```

## Trabajar con Ramas

### git branch

**Descripción:**  
Lista, crea o elimina ramas.

**Sintaxis:**
```bash
git branch [opciones] [nombre-rama]
```

**Opciones comunes:**
- `-a`: Listar todas las ramas (locales y remotas)
- `-r`: Listar solo ramas remotas
- `-d`, `--delete`: Eliminar rama
- `-D`: Forzar eliminación de rama
- `-v`: Ver último commit en cada rama

**Ejemplos:**
```bash
# Listar ramas locales
git branch

# Crear una nueva rama
git branch nueva-rama

# Eliminar una rama
git branch -d rama-a-eliminar

# Listar todas las ramas
git branch -a
```

### git checkout

**Descripción:**  
Cambia entre ramas o restaura archivos.

**Sintaxis:**
```bash
git checkout [opciones] [rama/commit]
```

**Opciones comunes:**
- `-b`: Crear y cambiar a una nueva rama
- `-B`: Crear/resetear y cambiar a una rama
- `--`: Separar opciones de nombres de archivo

**Ejemplos:**
```bash
# Cambiar a una rama existente
git checkout otra-rama

# Crear y cambiar a una nueva rama
git checkout -b nueva-rama

# Descartar cambios en un archivo
git checkout -- archivo.txt
```

### git switch (Git 2.23+)

**Descripción:**  
Cambia entre ramas (alternativa moderna a `git checkout`).

**Sintaxis:**
```bash
git switch [opciones] [rama]
```

**Opciones comunes:**
- `-c`: Crear y cambiar a una nueva rama
- `-C`: Crear/resetear y cambiar a una rama
- `--detach`: Cambiar a un commit específico (HEAD separado)

**Ejemplos:**
```bash
# Cambiar a una rama existente
git switch otra-rama

# Crear y cambiar a una nueva rama
git switch -c nueva-rama

# Forzar creación de una rama
git switch -C nueva-rama
```

### git merge

**Descripción:**  
Combina dos o más historiales de desarrollo.

**Sintaxis:**
```bash
git merge [opciones] [rama]
```

**Opciones comunes:**
- `--no-ff`: Crear siempre un commit de merge (no fast-forward)
- `--squash`: Combinar todos los commits en uno solo
- `--abort`: Abortar merge en caso de conflictos

**Ejemplos:**
```bash
# Incorporar cambios de otra rama
git merge otra-rama

# Merge sin fast-forward
git merge --no-ff feature-branch

# Abortar un merge con conflictos
git merge --abort
```

### git rebase

**Descripción:**  
Reaplica commits en otra base.

**Sintaxis:**
```bash
git rebase [opciones] [rama-base]
```

**Opciones comunes:**
- `-i`, `--interactive`: Modo interactivo
- `--onto`: Rebase desde un punto específico a otro
- `--abort`: Abortar un rebase en proceso
- `--continue`: Continuar un rebase después de resolver conflictos

**Ejemplos:**
```bash
# Rebase sobre main
git rebase main

# Rebase interactivo sobre los últimos 3 commits
git rebase -i HEAD~3

# Abortar un rebase
git rebase --abort
```

## Sincronización con Remotos

### git remote

**Descripción:**  
Gestiona repositorios remotos.

**Sintaxis:**
```bash
git remote [comando]
```

**Comandos comunes:**
- `add`: Añadir un nuevo remoto
- `remove`: Eliminar un remoto
- `-v`: Ver URLs de remotos
- `show`: Mostrar información de un remoto

**Ejemplos:**
```bash
# Listar remotos
git remote -v

# Añadir un nuevo remoto
git remote add origin https://github.com/usuario/repo.git

# Eliminar un remoto
git remote remove origin

# Ver información detallada de un remoto
git remote show origin
```

### git fetch

**Descripción:**  
Descarga objetos y referencias de un repositorio remoto.

**Sintaxis:**
```bash
git fetch [opciones] [remoto]
```

**Opciones comunes:**
- `--all`: Descargar de todos los remotos
- `-p`, `--prune`: Eliminar referencias remotas que ya no existen
- `--tags`: Descargar todas las tags

**Ejemplos:**
```bash
# Obtener cambios del remoto predeterminado
git fetch

# Obtener cambios de todos los remotos
git fetch --all

# Obtener cambios y eliminar ramas remotas eliminadas
git fetch -p
```

### git pull

**Descripción:**  
Obtiene e integra cambios de un repositorio remoto.

**Sintaxis:**
```bash
git pull [opciones] [remoto] [rama]
```

**Opciones comunes:**
- `--rebase`: Rebasar en lugar de fusionar
- `--no-commit`: No crear automáticamente un commit
- `--ff-only`: Solo permitir fast-forward

**Ejemplos:**
```bash
# Obtener e integrar cambios
git pull

# Obtener cambios y rebasar en lugar de fusionar
git pull --rebase

# Pull desde un remoto y rama específicos
git pull origin main
```

### git push

**Descripción:**  
Envía commits locales a un repositorio remoto.

**Sintaxis:**
```bash
git push [opciones] [remoto] [rama]
```

**Opciones comunes:**
- `-u`, `--set-upstream`: Establecer la rama remota como upstream
- `--force`, `-f`: Forzar push (cuidado, puede sobrescribir trabajo remoto)
- `--tags`: Enviar tags
- `--delete`: Eliminar una rama remota

**Ejemplos:**
```bash
# Push a la rama actual
git push

# Push y establecer upstream
git push -u origin feature-branch

# Eliminar una rama remota
git push origin --delete rama-remota

# Push forzado (usar con precaución)
git push -f
```

## Revisión de Historial

### git log

**Descripción:**  
Muestra el historial de commits.

**Sintaxis:**
```bash
git log [opciones]
```

**Opciones comunes:**
- `--oneline`: Formato corto (una línea por commit)
- `--graph`: Mostrar representación gráfica
- `--decorate`: Mostrar refs (ramas, tags)
- `-p`: Mostrar diferencias introducidas
- `--stat`: Mostrar estadísticas de cambios
- `-n`: Limitar número de commits mostrados

**Ejemplos:**
```bash
# Ver historial completo
git log

# Ver historial en formato resumido
git log --oneline

# Ver historial con gráfico
git log --oneline --graph --decorate

# Ver historial con cambios para un archivo
git log -p archivo.txt
```

### git diff

**Descripción:**  
Muestra cambios entre commits, commit y área de trabajo, etc.

**Sintaxis:**
```bash
git diff [opciones] [commit1] [commit2]
```

**Opciones comunes:**
- `--staged`: Comparar área de staging con último commit
- `--name-only`: Mostrar solo nombres de archivos
- `--word-diff`: Mostrar diferencias a nivel de palabras
- `--color-words`: Colorear palabras para mejor visualización

**Ejemplos:**
```bash
# Ver cambios no preparados (unstaged)
git diff

# Ver cambios preparados (staged)
git diff --staged

# Ver diferencias entre dos commits
git diff abc123..def456

# Ver diferencias en un archivo específico
git diff archivo.txt
```

### git show

**Descripción:**  
Muestra información del objeto Git (commit, tag, etc.).

**Sintaxis:**
```bash
git show [opciones] [objeto]
```

**Ejemplos:**
```bash
# Ver información del último commit
git show

# Ver información de un commit específico
git show abc123

# Ver información de una tag
git show v1.0.0
```

## Deshacer Cambios

### git restore (Git 2.23+)

**Descripción:**  
Restaura archivos en el árbol de trabajo.

**Sintaxis:**
```bash
git restore [opciones] [archivo]
```

**Opciones comunes:**
- `-s`, `--source`: Restaurar desde commit/rama específica
- `-p`, `--patch`: Restaurar interactivamente
- `--staged`: Deshacer cambios en el área de staging

**Ejemplos:**
```bash
# Descartar cambios en un archivo
git restore archivo.txt

# Deshacer cambios en staging (mantener cambios en working dir)
git restore --staged archivo.txt

# Restaurar archivo desde un commit específico
git restore --source=HEAD~1 archivo.txt
```

### git reset

**Descripción:**  
Resetea el HEAD actual a un estado específico.

**Sintaxis:**
```bash
git reset [opciones] [commit]
```

**Opciones comunes:**
- `--soft`: No toca el área de staging ni el árbol de trabajo
- `--mixed`: Resetea el índice pero no el árbol de trabajo (default)
- `--hard`: Resetea índice y árbol de trabajo (descarta cambios)

**Ejemplos:**
```bash
# Deshacer el último commit manteniendo los cambios
git reset --soft HEAD~1

# Deshacer el último commit y quitar cambios del staging
git reset HEAD~1

# Deshacer cambios y descartar todos los cambios
git reset --hard HEAD~1

# Deshacer adición al área de staging
git reset archivo.txt
```

### git revert

**Descripción:**  
Crea un nuevo commit que deshace los cambios de un commit anterior.

**Sintaxis:**
```bash
git revert [opciones] [commit]
```

**Opciones comunes:**
- `--no-commit`, `-n`: Revertir cambios sin crear commit
- `--edit`, `-e`: Editar mensaje de commit
- `--no-edit`: Usar mensaje generado automáticamente

**Ejemplos:**
```bash
# Revertir el último commit
git revert HEAD

# Revertir un commit específico
git revert abc123

# Revertir múltiples commits
git revert abc123..def456

# Revertir cambios sin crear commit
git revert -n HEAD
```

## Guardado Temporal

### git stash

**Descripción:**  
Guarda temporalmente cambios no comprometidos.

**Sintaxis:**
```bash
git stash [comando]
```

**Comandos comunes:**
- `save`: Guarda cambios (opcional desde Git 2.16+)
- `list`: Lista todos los stashes
- `show`: Muestra cambios en un stash
- `pop`: Aplica y elimina el último stash
- `apply`: Aplica un stash (sin eliminarlo)
- `drop`: Elimina un stash
- `clear`: Elimina todos los stashes

**Ejemplos:**
```bash
# Guardar cambios actuales
git stash

# Guardar con un mensaje descriptivo
git stash save "Cambios en progreso para feature X"

# Listar stashes guardados
git stash list

# Aplicar y eliminar el último stash
git stash pop

# Aplicar un stash específico sin eliminarlo
git stash apply stash@{2}

# Eliminar un stash específico
git stash drop stash@{1}

# Eliminar todos los stashes
git stash clear
```

## Etiquetas (Tags)

### git tag

**Descripción:**  
Crea, lista o elimina tags.

**Sintaxis:**
```bash
git tag [opciones] [nombre-tag] [commit]
```

**Opciones comunes:**
- `-a`: Crear tag anotada (con mensaje)
- `-m`: Especificar mensaje
- `-d`: Eliminar tag
- `-l`: Listar tags

**Ejemplos:**
```bash
# Crear tag ligera
git tag v1.0.0

# Crear tag anotada
git tag -a v1.0.0 -m "Versión 1.0.0"

# Crear tag para un commit específico
git tag -a v0.9.0 abc123 -m "Versión beta"

# Listar tags
git tag -l

# Listar tags con patrón
git tag -l "v1.*"

# Eliminar tag
git tag -d v0.9.0

# Publicar tags en remoto
git push origin --tags

# Publicar una tag específica
git push origin v1.0.0
```

## Submodulos

### git submodule

**Descripción:**  
Gestiona submodulos (repositorios dentro de repositorios).

**Sintaxis:**
```bash
git submodule [comando]
```

**Comandos comunes:**
- `add`: Añadir submodulo
- `init`: Inicializar submodulos
- `update`: Actualizar submodulos
- `status`: Mostrar estado de submodulos

**Ejemplos:**
```bash
# Añadir un submodulo
git submodule add https://github.com/usuario/libreria.git libs/libreria

# Inicializar submodulos (después de clonar)
git submodule init

# Actualizar submodulos
git submodule update

# Clonar repositorio con submodulos
git clone --recurse-submodules https://github.com/usuario/proyecto.git

# Actualizar todos los submodulos
git submodule update --remote
```
