---
layout: post
title: "Linuxología Parte II: Alias en GNU/Linux"
date: 2023-09-09 17:28:43 +0100
categories: "Utilidades"
---


# Creando nuestros propios comandos con alias
En esta ocasión crearemos un comando para nuestro propio uso con el comando _alias_. Pero antes de comenzar es necesario que conozcamos un sencillo truco respecto a la linea de comandos en GNU/Linux. Es posible colocar más de un comando en una sola linea separando cada comando con un caracter de punto y coma. De la siguiente manera:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ cd /usr; ls; pwd
   1   │ bin      lib    lib64  sbin   src
   2   │ include  lib32  local  share
   3   │ /usr
───────┴───────────────────────────────────────────────────────────────────────────────
```

Lo que hicimos en el ejemplo anterior fue ejecutar tres comandos distintos en una sola linea
- Nos movimos al directorio __usr__ alojado en la raíz.
- Listamos los archivos y directorios existentes dentro de __usr__.
- Mostramos el directorio en el cual nos encontramos.

Es momento de construir nuestro propio comando personalizado. Para fines prácticos elegiré dar solución a un pequeño problema que me molesta desde hace un tiempo. Yo utilizo la aplicacion Obsidian para tomar notas en formato markdown, sin embargo mi sistema Linux no reconoce la aplicación y por lo tanto para ejecutar la aplicación debo utilizar la AppImage de la aplicación.

Normalmente el procedimiento es el siguiente:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ cd ~/Descargas
   1   │ ❯ ./Obsidian-1.3.5.AppImage& disown
───────┴───────────────────────────────────────────────────────────────────────────────
```

Como podemos observar se ejecutan dos comandos distintos, el primero nos coloca en el directorio de _Descargas_ que es donde tengo almacenado el AppImage de la aplicación, segundo, se ejecuta dicho AppImage.
Por lo tanto podemos acortar estas dos lineas de comandos a una sola:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ cd ~/Descargas; ./Obsidian-1.3.5.AppImage& disown:
───────┴───────────────────────────────────────────────────────────────────────────────
```

Antes de crear nuestro comando personalizado mediante alias debemos pensar en un nombre adecuado para este nuevo comando. Probaremos con _test_. Pero antes de hacer esto, sería una buena idea averiguar si el nombre _test_ se encuentra disponible. Para determinar esto, usaremos el comando _type_:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ type test
   1   │ test is a shell builtin
───────┴───────────────────────────────────────────────────────────────────────────────
```

El nombre "test" ya se encuentra en uso. Probemos con "obsidian":

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ type obsidian
   1   │ obsidian not found
───────┴───────────────────────────────────────────────────────────────────────────────
```

Excelente, "obsidian" no se encuentra en uso. Ahora sí, creemos nuestro alias:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ alias obsidian='cd ~/Descargas; ./Obsidian-1.3.5.AppImage& disown'
───────┴───────────────────────────────────────────────────────────────────────────────
```

Notemos la estructura del comando:

```
alias nombre='cadena'
```

Después del comando _alias_ le damos un nombre seguido inmediatamente (sin espacios en blanco) de un signo de igual, seguido inmediatamente de una cadena entre comillas que contiene el significado asignado al nombre. Después de definir nuestro alias, este puede ser usado en cualquier lugar donde el shell pueda recibir comandos. Probemos:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ obsidian
   1   │ [1] 26087
───────┴───────────────────────────────────────────────────────────────────────────────
```

El número mostrado en la linea número uno es el ID del proceso que se acaba de ejecutar en segundo plano, es decir, efectivamente se ejecutó nuestro comando y abrió correctamente la aplicación Obsidian, se le otorga un ID de proceso para poder monitorearlo o administrarlo si es necesario.
Además podemos corroborar que nuestro alias existe utilizando una vez más el comando _type_.

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ type obsidian
   1   │ obsidian is an alias for cd ~/Descargas; ./Obsidian-1.3.5.AppImage& disown
───────┴───────────────────────────────────────────────────────────────────────────────
```

Para eliminar un alias, el comando _unalias_ es utilizado de esta manera:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ unalias obsidian
   1   │ ❯ type obsidian
   2   │ obsidian not found
───────┴───────────────────────────────────────────────────────────────────────────────
```

Es importante evitar nombrar los alias con nombres que ya están siendo utilizados. Para observar todos los alias existentes podemos usar el comando _alias_ sin parametros:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ alias
   1   │ cat=bat
   2   │ edit-in-kitty='kitten edit-in-kitty'
   3   │ l='lsd --group-dirs=first'
   4   │ la='lsd -a --group-dirs=first'
   5   │ ll='lsd -lh --group-dirs=first'
   6   │ lla='lsd -lha --group-dirs=first'
   7   │ ls='lsd --group-dirs=first'
   8   │ run-help=man
   9   │ which-command=whence
───────┴───────────────────────────────────────────────────────────────────────────────
```

El único detalle con definir alias en la linea de comandos es que desaparecen cuando la sesión del shell se cierra. En otro articulo veremos como agregar nuestros propios alias a los archivos que establece el entorno cada vez que accedemos a nuestro usuario, pero por ahora disfrutemos nuestro primer paso dentro de la programación en shell :).
