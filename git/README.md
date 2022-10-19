# GIT
Es un sistema de control de versiones distribuido como mercurial o bazzar | no es un sistema de compias de seguridad.

<img src="./img/gitGraphic.png" alt="no img"/>

# Local

### configuración
usar `--global` o `--system` o `--local` según se necesite. 

listar configuracion

    git config --list --environment

modificar configuración

    git config --environment user.name "new value"

guardar cambios de configuración local

    git commit -a

### iniciar repositorio
    git init .

### agregar cambios al staging
```
git add directrory 
```

```
git add *.extensionFile
```

```
git add . 
```
### comprometer cambios
    git commit -am "your message"

### Renombrar rama actual 
    git branch -M newNameBranch

### ver cambios en mi repositorio con respecto al remoto
    git diff

### agregar etiquetas
usar `-a` para etiquetas complejas
si no se especifica el código de confirmación se aplica al último commit

    git tag tagName(ej : v1.0) condeCommitConfimation

### subir etiqueta al remoto
    git push origin tagName

### cambiar a rama o etiqueta
    git checkout tagOrBranchName

### revertir cambios a nivel de commit
se crea un nuevo coomit con los cambios de un commit anterior, obviando los que estan en medio.

    git revert codeCommitConfirmation 

 
<img src="./img/revert.png" alt="no img"/>

### regresar a un commit quitando del historial los de enmedio
con `--soft` se quita el historial de los commits pero no se eliminan archivos

    git reset --soft HEAD~numReversePosition

con `--hard` se quita el historial de los commits y se eliminan archivos

    git reset --hard HEAD~numReversePosition

<img src="./img/reset.webp" alt="no img">

### eliminar archivo de git
    git rm fileName

### indicar el commit en que se rompió el proyecto
    git bisect bad  commtCode

e indicar hasta que commit funcionaba

    git bisect good commitCode

### ver quién modifica qué
    git blame fileName


# Ramas

### listar las ramas
    git branch

### crear rama 
    git branch nameNewBranch

crearla desde un commit específico

    git branch nameNewBranch codeOldCommit

### moverse entre ramas
usar `-b` en caso de que no exista la rama para crearla

    git checkout nameBranch

### traer cambios de una rama a la actual
si no se han presentado cambios en la rama actual se hace merge por `Fast-forward`<br/>
si se han hecho cambios en la rama actual se crea un nuevo commit en la rama actual con los cambios

    git merge nameOtherBranch

si se quieren traer los commit de una forma plana como si nunca hubiese existido la otra rama(recomendado sólo en local)

    git rebase nameOtherBranch

### guardar algo para luego continuarlo sin hacer commit
    git stash save "name"

para recuperarlo 

    git stash apply
    git stash clear

para recuperar y limpiar

    git stash pop

para listar los stash 

    git stash list


### fucionar commits concretos

    git cherry-pick commitCode

para fucionar un intervalo cerrado

    git cherry-pick commitCode^..commitCode

para fucionar un intervalo abierto

    git cherry-pick commitCode..commitCode





# Remoto

### Agregar repositorio remoto
    git remote add origin http://github.com/yourUrl

### Empujar por primera vez una rama al repositorio remoto
    git push -u origin yourNameBranch

`-u` se usa para indicar que ésta será la rama por defecto, de tal modo que posteriormente pueda hacerce 
únicamente `git push` para actualizar esta rama.

### Traer cambios del repositorio remoto 
    git pull