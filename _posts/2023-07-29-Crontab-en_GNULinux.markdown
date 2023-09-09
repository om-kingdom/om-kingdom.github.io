---
layout: post
title: "Linuxología Parte I: Crontab en GNU/Linux"
date: 2023-07-29 22:28:50 +0100
categories: "Utilidades"
---

# Linuxología Parte I: Crontab en GNU/Linux
## ¿Qué es el sistema crontab?
En el contexto de GNU/Linux (Linux para abreviar), existe un sistema llamado _cron_ que permite programar y ejecutar tareas de forma periódica, el intervalo de tiempo es definido por el usuario y puede abarcar lapsos de tiempo como miutos, horas, dias, semanas, etc.

El sistema cron es ampliamente utilizado para automatizar tareas repetitivas en sistemas basados en Unix, incluyendo Linux. Como ejemplo podemos hablar de muchas tareas de administración para un servidor, actualizar logs o la propia base de datos interna usando ciertos comandos que requieren ser ejecutados de forma regular por el sistema para trabajar de forma apropiada. Por esta razón es muy importante que el propio sistema operativo ofrezca herramientas que permitan configurar esas ejecuciones regulares.
El sistema cron utiliza dos archivos principales para configurar las tareas programadas:
- __crontab__: 
1. Es el archivo que contiene las entradas de las tareas programadas para un usuario especifico. Cada usuario puede tener su propio archivo crontab, y solo el usuario y el superusuario (root) tienen permisos para modificarlo. Para editar el crontab de un usuario se utiliza el comando crontab -e.
2. __/etc/crontab/__: Este es el archivo de crontab del sistema y contiene tareas programadas para todos los usuarios. Solo el superusuario (root) puede modificar este archivo. Además, en algunos sistemas, hay directorios adicionales `__/etc__` donde se pueden ubicar archivos crontab adicionales para ejecutar tareas en diferentes carpetas o contextos.

## Sintaxis de una entrada cron
La sintaxis de una entrada cron (una tarea programada para repetirse de forma periodica) consiste en cinco campos que espespecifican cuando y con qué frecuencia se debe eejcutar la tarea. Los campos son los siguientes:
1. __Minuto (0-59)__: El minuto específico en el que se ejecutará la tarea.
2. __Hora (0-23)__: La hora del día en la que se ejecutará la tarea.
3. __Día del mes (1-31)__: El día del mes en el que se ejecutará la tarea.
4. __Mes (1-12)__: El mes en el que se ejecutará la tarea.
5. __Día de la semana (0-7)__: El día de la semana en el que se ejecutará la tarea. Donde 0 y 7 representan el domingo.

Usando estos campos, se puede programar la tarea para que se ejecute en intervalos especifícos, diariamente, semanalmente, mensualmente, etc. Además se pueden utilizar caracteres especiales como el asterísco (\*) para indicar "cualquier valor" y la barra (/) para definir intervalos.

## Ejemplos

Por ejemplo, en mi caso utilizo Arch Linux, recordemos que es una distribucion Rolling Release (si no sabes que significa Rolling Release revisa la sección de Notas ubicada al final de este psot) por lo que debo actualizar de forma constante el software de mi equipo. Y esto lo hago mediante el superusuario (root) siguiente comando:

``` bash
    /home/insoportable  󰚌  pacman -Syu
:: Sincronizando las bases de datos de los paquetes...
 core está actualizado
 extra                                            8.3 MiB  2.58 MiB/s 00:03 [###########################################] 100%
 multilib está actualizado
 blackarch está actualizado
:: Iniciando actualización completa del sistema...
resolviendo dependencias...
buscando conflictos entre paquetes...

Paquetes (1) rubberband-3.3.0-1

Tamaño total de la descarga:     1.42 MiB
Tamaño total de la instalación:  5.25 MiB
Tamaño neto tras actualizar:     3.99 MiB

:: ¿Continuar con la instalación? [S/n] S
:: Obteniendo los paquetes...
 rubberband-3.3.0-1-x86_64                     1454.6 KiB  3.06 MiB/s 00:00 [###########################################] 100%
(1/1) comprobando las claves del depósito                                   [###########################################] 100%
(1/1) verificando la integridad de los paquetes                             [###########################################] 100%
(1/1) cargando los archivos de los paquetes                                 [###########################################] 100%
(1/1) comprobando conflictos entre archivos                                 [###########################################] 100%
(1/1) comprobando el espacio disponible en el disco                         [###########################################] 100%
:: Procesando los cambios de los paquetes...
(1/1) actualizando rubberband                                               [###########################################] 100%
:: Ejecutando los «hooks» de posinstalación...
(1/1) Arming ConditionNeedsUpdate...

```

El comando utilizado se explica en la sección de __Notas__ de este post.
Por lo tanto, si deseo automatizar esta tarea para que se ejecute periodicamente deberé crear una emtrada para el superusario (root) en el archivo crontab. Esta entrada se realiza para el superusuario pues es el único usuario con permisos de utilizar el administrador de paquetes.

Para crear o editar una entrada en el crontab de root, debemos tener permisos de superusario o utilizar el comando "sudo". Yo optaré por utilizar el comando "sudo":

1. Abrimos una terminal o una consola de comandos.
2. Ingresamos el siguiente comando para corroborar que tenemos el sistema crontab instalado en el equipo:
    ```bash
        ~  crontab
    zsh: command not found: crontab
    ```
    Como podemos observar yo no tengo el sistema crontab instalado, pero esto se soluciona acudiendo al manejador de paquetes para realizar la instalación.
3. __OPCIONAL__: Realiza este paso si no posees el sistema crontab instalado. En mi caso yo utilizo el manejador de paquetes `pacman` para Arch Linux.

```bash
    ~  sudo pacman -S cronie
resolviendo dependencias...
buscando conflictos entre paquetes...

Paquetes (2) run-parts-5.5-1  cronie-1.6.1-1

```

Tras la instalación podemos ver que ejecutar el comando crontab sin parametros nos muestra ya el manual del comando:

```bash
    ~  crontab
crontab: usage error: file name or - (for stdin) must be specified
Usage:
 crontab [options] file
 crontab [options]
 crontab -n [hostname]

Options:
 -u <user>  define user
 -e         edit user's crontab
 -l         list user's crontab
 -r         delete user's crontab
 -i         prompt before deleting
 -n <host>  set host in cluster to run users' crontabs
 -c         get host in cluster to run users' crontabs
 -T <file>  test a crontab file syntax
 -V         print version and exit
 -x <mask>  enable debugging

Default operation is replace, per 1003.2
```
Además, podemos observar que en el directorio `/var/spool` ya contamos con las carpetas "anacron" y "cron":

```bash
    /var/spool  ls -la
drwxr-xr-x root root 4.0 KB Sat Jul 29 21:27:08 2023  .
drwxr-xr-x root root 4.0 KB Sat Jul 29 19:00:01 2023  ..
drwxr-xr-x root root 4.0 KB Mon Apr 25 07:53:00 2022  anacron
drwxr-xr-x root root 4.0 KB Mon Apr 25 07:53:00 2022  cron
drwxrwxrwt root root 4.0 KB Tue Jan 31 14:51:21 2023  mail
```
4. Una vez tenemos instalado el paquete "cronie" podemos continuar:

```bash
    ~   1m 2s  sudo crontab -e 
```

5. A continuación se abre el archivo crontab de root en el editor de texto por defecto (en mi caso es vi). Y esto nos permitira editar el archivo crontab para agregar una entrada.
6. Agregamos la entrada cron para realizar una actualizacion automatica los días lunes a las 08:00 am cada semana:

```bash
# Ejecutar el comando de actualizacion del sistema todos los lunes a las 08:00 AM
0 8 * * 1 pacman -Syu
```

Podemos corroborar que efectivamente se modifico el archivo cron de root si revisamos el directorio cron de nuestro equipo:

```bash
❯ pwd
/var/spool/cron
❯ ls
 root
❯ sudo cat root
[sudo] contraseña para insoportable: 
# Ejecutar el comando de actualizacion del sistema todos los lunes a las 08:00 AM
0 8 * * 1 pacman -Syu

    /var/s/cron   3s 
```

## Notas
- Habitualmente los archivos cron se almacenan en el directorio __/etc/crontab__.
- En Arch Linux los archivos cron de los usuarios se almacenan en el directorio __/var/spool/cron/nombre_de_usuario__ 
- Un "Rolling Release" (lanzamiento continuo o actualización continua) es un modelo de desarrollo y distribución de software que se utiliza en algunas distribuciones de Linux. En este modelo, en lugar de lanzar versiones de software con fechas de lanzamiento fijas, se realizan actualizaciones continuas y frecuentes para proporcionar a los usuarios las últimas características, mejoras y correcciones de errores sin tener que esperar a una nueva versión mayor.
- El comando utilizado en este post para actualizar Arch Linux se compone de los siguientes parametros:
    - __pacman__: Es el administrador de paquetes utilizado en Arch Linux para instalar, actualizar y administrar software. Se utiliza para interactuar con los repositorios de software de Arch Linux y administrar los paquetes instalados en el sistema.
    - __S__: Significa "sync" o "synchronize" y se utiliza para sincronizar la base de datos de paquetes locales con la base de datos de paquetes en los repositorios oficiales. Esto asegura que el sistema tenga la información más actualizada sobre los paquetes disponibles.
    - __y__: Significa "refresh" o "refresh the package list" y se utiliza para forzar una actualización de la base de datos de paquetes, descargando la información más reciente de los repositorios, incluso si la base de datos local ya está actualizada. Es una buena práctica utilizar esta opción antes de realizar una actualización para asegurarse de tener la información más reciente.
    - __u__: Significa "upgrade" y se utiliza para actualizar todos los paquetes instalados en el sistema a sus versiones más recientes disponibles en los repositorios oficiales. Esto implica descargar e instalar las últimas versiones de los paquetes.
