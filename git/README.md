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

### Renombrar rama actual 
    git branch -M newNameBranch

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

### eliminar archivo de git
    git rm fileName

# Remoto

### Agregar repositorio remoto
    git remote add origin http://github.com/yourUrl

### Empujar por primera vez una rama al repositorio remoto
    git push -u origin yourNameBranch

`-u` se usa para indicar que ésta será la rama por defecto, de tal modo que posteriormente pueda hacerce 
únicamente `git push` para actualizar esta rama.

### Traer cambios del repositorio remoto 
    git pull