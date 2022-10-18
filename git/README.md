# GIT
Es un sistema de control de versiones distribuido como mercurial o bazzar | no es un sistema de compias de seguridad.

## Local

### Renombrar rama actual 
    git branch -M newNameBranch

## Remoto

### Agregar repositorio remoto
    git remote add origin http://github.com/yourUrl

### Empujar por primera vez una rama al repositorio remoto
    git push -u origin yourNameBranch

`-u` se usa para indicar que ésta será la rama por defecto, de tal modo que posteriormente pueda hacerce 
únicamente `git push` para actualizar esta rama.