# Git, un Sistema de Control de Versiones

## Configuración de Git

Para usar git es necesario configurarlo con el nombre de usuario y su correo electrónico.

### Git config

Establecer el nombre de usuario:
  
    git config --global user.name "Your-Full-Name"

Establecer el correo del usuario:
    
    git config --global user.email "your-email-address"

Activar el coloreado de la salida:
    
git config --global color.ui auto

Mostrar el estado original en los conflictos:
        
    git config --global merge.conflictstyle diff3

Mostrar la configuración:
    
    git config --list

## Creación de un repositorio nuevo

### Git init
 
Crea un repositorio nuevo con el nombre nombre-repositorio.

Este comando crea crea una nueva carpeta con el nombre del repositorio, que a su vez contiene otra carpeta oculta llamada .git que contiene la base de datos donde se registran los cambios en el repositorio.

    - git init <nombre-repositorio>

## Copia de repositorios

### Git clone

Crea una copia local del repositorio ubicado en la dirección url-repositorio.

A partir de que se hace la copia, los dos repositorios, el original y la copia, son independientes, es decir, cualquier cambio en uno de ellos no se verá reflejado en el otro.

    git clone <url-repositorio>

- Añadir cambios a un repositorio
  
    Con Git, cualquier cambio que hagamos en un proyecto tiene que pasar por tres estados hasta que guarde definitivamente en el repositorio.

    - Directorio de trabajo Es el directorio que contiene una copia de una versión concreta del proyecto en la que se está trabajando. Puede contener ficheros que no pertenecen al repositorio.
      
    - Zona temporal de intercambio (staging area) es una zona donde se guardan los cambios temporalmente desde el directorio de trabajo antes de hacerlos definitivos y registrarlos en el repositorio.
      
    - Repositorio Es donde finalmente se guardan los cambios confirmados desde la zona temporal de intercambio.

### Añadir cambios a la zona de intercambio temporal

Añade los cambios en el fichero fichero del directorio de trabajo a la zona de intercambio temporal.

    git add <fichero>

Añade los cambios en todos los ficheros de la carpeta carpeta del directorio de trabajo a la zona de intercambio temporal.
  
    git add <carpeta>

Añade todos los cambios de todos los ficheros no guardados aún en la zona de intercambio temporal.
            
    git add . 

### Añadir cambios al repositorio

git commit
  
    git commit -m "mensaje" 

confirma todos los cambios de la zona de intercambio temporal añadiéndolos al repositorio y creando una nueva versión del proyecto. "mensaje" es un breve mensaje describiendo los cambios realizados que se asociará a la nueva versión del proyecto.

    git commit -m "mensaje"

git commit --amend -m "mensaje" cambia el mensaje del último commit por el nuevo mensaje "mensaje".

    git commit --amend -m "mensaje"

### Referenciar un commit

Cada commit tiene asociado un código hash de 40 caracteres hexadecimales que lo identifica de manera única. Hay dos formas de referirse a un commit:

    - Nombre absoluto: Se utiliza su código hash (basta indicar los 4 o 5 primeros dígitos).
    - Nombre relativo: Se utiliza la palabra HEAD para referirse siempre al último commit. 
    - Para referirse al penúltimo commit se utiliza HEAD~1, al antepenúltimo HEAD~2, etc.

### Mostrar el estado de un repositorio

git status

    git status 

muestra el estado de los cambios en el repositorio desde la última versión guardada. En particular, muestra los ficheros con cambios en el directorio de trabajo que no se han añadido a la zona de intercambio temporal y los ficheros en la zona de intercambio temporal que no se han añadido al repositorio.

### Mostrar el historial de versiones de un repositorio

git log

    git log 

muestra el historial de commits de un repositorio ordenado cronológicamente. Para cada commit muestra su código hash, el autor, la fecha, la hora y el mensaje asociado.
Este comando es muy versátil y muestra la historia del repositorio en distintos formatos dependiendo de los parámetros que se le den. 

Los más comunes son:

    --oneline muestra cada commit en una línea produciendo una salida más compacta.

    --graph muestra la historia en forma de grafo.

### Mostrar los datos de un commit

    git show
  
git show muestra el usuario, el día, la hora y el mensaje del último commit, así como las diferencias con el anterior.

    git show <commit> 
  
muestra el usuario, el día, la hora y el mensaje del commit indicado, así como las diferencias con el anterior.

### Mostrar el historial de cambios de un fichero

git annotate
  
    git annotate 

muestra el contenido de un fichero anotando cada línea con información del commit en el que se introdujo.
Cada línea de la salida contiene los 8 primeros dígitos del código hash del commit correspondiente al cambio, el autor de los cambio, la fecha, el número de línea del fichero y el contenido de la línea.

### Mostrar las diferencias entre versiones

    git diff

muestra las diferencias entre el directorio de trabajo y la zona de intercambio temporal.

    git diff --cached 
  
muestra las diferencias entre la zona de intercambio temporal y el último commit.

    git diff HEAD 
  
muestra la diferencia entre el directorio de trabajo y el último commit.

 ### Deshacer cambios

Eliminar cambios del directorio de trabajo o volver a una versión anterior

    git checkout
  
Actualiza el fichero file a la versión correspondiente al commit commit.
Suele utilizarse para eliminar los cambios en un fichero que no han sido guardados aún en la zona de intercambio temporal, mediante el comando git checkout HEAD -- file.

    git checkout <commit> -- <file>

Eliminar cambios de la zona de intercambio temporal
  
    git reset

Elimina los cambios del fichero fichero de la zona de intercambio temporal, pero preserva los cambios en el directorio de trabajo.

    git reset <fichero>

Para eliminar por completo los cambios de un fichero que han sido guardados en la zona de intercambio temporal hay que aplicar este comando y después git checkout HEAD -- fichero.

- Eliminar cambios de un commit

git reset elimina todos los cambios desde el commit commit y actualiza el HEAD este commit.

    git reset --hard <commit>

Suele usarse para eliminar todos los cambios en el directorio de trabajo desde el último commit mediante el comando git reset --hard HEAD.

Usar con cuidado este comando pues los cambios posteriores al commit indicado se pierden por completo.
git reset commit actualiza el HEAD al commit commit, es decir, elimina todos los commits posteriores a este commit, pero no elimina los cambios del directorio de trabajo.

### Creación de ramas

git branch

    git branch <rama> 

crea una nueva rama con el nombre rama en el repositorio a partir del último commit, es decir, donde apunte HEAD.
Al crear una rama a partir de un commit, el flujo de commits se bifurca en dos de manera que se pueden desarrollar dos versiones del proyecto en paralelo.

### Listado de ramas

git log

    git branch 

muestra las ramas activas de un repositorio indicando con * la rama activa en ese momento.

    git log --graph --oneline 

muestra la historia del repositorio en forma de grafo (–graph) incluyendo todas las ramas (–all).

### Cambio de ramas

git checkout

    git checkout <rama> 
            
actualiza los ficheros del directorio de trabajo a la última versión del repositorio correspondiente a la rama rama, y la activa, es decir, HEAD pasa a apuntar al último commit de esta rama.

    git checkout -b <rama> 

crea una nueva rama con el nombre rama y la activa, es decir, HEAD pasa a apuntar al último commit de esta rama. Este comando es equivalente aplicar los comandos git branch rama y después git checkout rama.

## Fusión de ramas

git merge

    git merge <rama> 

integra los cambios de la rama rama en la rama actual a la que apunta HEAD.

### Reorganización de ramas

git rebase

    git rebase <rama-1> <rama-2> 

replica los cambios de la rama rama-2 en la rama rama-1 partiendo del ancestro común de ambas ramas. El resultado es el mismo que la fusión de las dos ramas pero la bifurcación de la rama-2 desaparece ya que sus commits pasan a estar en la rama-1.

## Eliminación de ramas

git branch -d

    git branch -d <rama> 

elimina la rama de nombre rama siempre y cuando haya sido fusionada previamente.

    git branch -D <rama></rama> 

elimina la rama de nombre rama incluso si no ha sido fusionada. Si la rama no ha sido fusionada previamente se perderán todos los cambios de esa rama.

# Github

### Añadir un repositorio remoto
git remote add

    git remote add <repositorio-remoto> <url> 

crea un enlace con el nombre repositorio-remoto a un repositorio remoto ubicado en la dirección url.
Cuando se añade un repositorio remoto a un repositorio, Git seguirá también los cambios del repositorio remoto de manera que se pueden descargar los cambios del repositorio remoto al local y se pueden subir los cambios del repositorio local al remoto.

### Lista de repositorios remotos
git remote

    git remote 

muestra un listado con todos los enlaces a repositorios remotos definidos en un repositorio local.

    git remote -v 

muestra además las direcciones url para cada repositorio remoto.

### Descargar cambios desde un repositorio remoto
git pull

    git pull <remoto> <rama> 

descarga los cambios de la rama rama del repositorio remoto remoto y los integra en la última versión del repositorio local, es decir, en el HEAD.

    git fetch <remoto> 

descarga los cambios del repositorio remoto remoto pero no los integra en la última versión del repositorio local.

### Subir cambios a un repositorio remoto

git push

    git push <remoto> <rama> 

sube al repositorio remoto remoto los cambios de la rama rama en el repositorio local.

### Colaboración en repositorios remotos de GitHub

Existen dos formas de colaborar en un repositorio alojado en GitHub:

* Ser colaborador del repositorio.

    * Recibir autorización de colaborador por parte de la persona propietaria del proyecto.
  
    * Clonar el repositorio en local.

    * Hacer cambios en el repositorio local.
  
    * Subir los cambios al repositorio remoto. Primero hacer git pull para integrar los cambios remotos en el repositorio local y luego git push para subir los cambios del repositorio local al remoto.
  
* Replicar el repositorio y solicitar integración de cambios.

    * Replicar el repositorio remoto en nuestra cuenta de GitHub mediante un fork.

    * Hacer cambios en nuestro repositorio remoto.
    
    * Solicitar a la persona propietaria del repositorio original que integre nuestros cambios en su repositorio mediante un pull request.

