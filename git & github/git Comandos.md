### **Comandos básicos de Git**

| **Comando**                                            | **Descripción**                                       |
| ------------------------------------------------------ | ----------------------------------------------------- |
| `git --version`                                        | Muestra la versión de Git instalada.                  |
| `git config --global user.name "Tu Nombre"`            | Configura tu nombre de usuario global.                |
| `git config --global user.email "tuemail@example.com"` | Configura tu correo global.                           |
| `git config --list`                                    | comando para comprobar que los cambios han funcionado |
| `git status`                                           | mostrar el estado del árbol de trabajo:               |
****
### **Iniciar y gestionar un repositorio**

| **Comando**                 | **Descripción**                                                                             |
| :-------------------------- | ------------------------------------------------------------------------------------------- |
| `git init`                  | Inicializa un repositorio Git en la carpeta actual.                                         |
| `git clone URL`             | Clona un repositorio remoto en tu máquina local.                                            |
| `git remote add origin URL` | Conecta el repositorio local con uno remoto.                                                |
| `git remote -v`             | Muestra los repositorios remotos vinculados.                                                |
| `git init -b main`          |  inicialice el nuevo repositorio y establezca el nombre de la rama predeterminada en `main` |
****
### **Control de cambios (Commits)**

|**Comando**|**Descripción**|
|---|---|
|`git status`|Muestra el estado de los archivos en el repositorio.|
|`git add archivo.txt`|Agrega un archivo específico al área de preparación.|
|`git add .`|Agrega todos los archivos al área de preparación.|
|`git commit -m "Mensaje"`|Guarda los cambios en el historial de Git con un mensaje descriptivo.|
|`git commit --amend -m "Nuevo mensaje"`|Modifica el último commit.|
****
### **Ver historial y cambios**

| **Comando**          | **Descripción**                                    |
| -------------------- | -------------------------------------------------- |
| `git log`            | Muestra el historial de commits.                   |
| `git log --oneline`  | Muestra el historial en una sola línea por commit. |
| `git diff`           | Muestra los cambios no confirmados.                |
| `git show ID_COMMIT` | Muestra los detalles de un commit específico.      |
****
### **Ramas (Branches)**

|**Comando**|**Descripción**|
|---|---|
|`git branch`|Lista todas las ramas en el repositorio.|
|`git branch nombre-rama`|Crea una nueva rama.|
|`git checkout nombre-rama`|Cambia a una rama específica.|
|`git switch nombre-rama`|Alternativa moderna a `git checkout nombre-rama`.|
|`git merge nombre-rama`|Fusiona una rama con la actual.|
|`git branch -d nombre-rama`|Elimina una rama local.|
****
### **Trabajar con GitHub (Repositorio remoto)**

|**Comando**|**Descripción**|
|---|---|
|`git push origin main`|Sube cambios al repositorio remoto en la rama `main`.|
|`git push -u origin main`|Sube cambios y establece la rama remota predeterminada.|
|`git pull origin main`|Descarga cambios desde el repositorio remoto.|
|`git fetch`|Obtiene los cambios remotos sin fusionarlos.|
****
### **Deshacer cambios**

|**Comando**|**Descripción**|
|---|---|
|`git reset archivo.txt`|Quita un archivo del área de preparación.|
|`git reset --hard ID_COMMIT`|Revierte el proyecto a un commit específico (¡Irreversible!).|
|`git revert ID_COMMIT`|Crea un commit que deshace los cambios del commit especificado.|
****
### **Otras Utilidades**

|**Comando**|**Descripción**|
|---|---|
|`git stash`|Guarda temporalmente cambios sin confirmarlos.|
|`git stash pop`|Restaura los cambios guardados en `stash`.|
|`git clean -f`|Elimina archivos no rastreados del directorio.|