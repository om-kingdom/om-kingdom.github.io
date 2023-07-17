---
layout: post
title:  "Keygenme-py PicoCTF"
date:   2023-07-07 12:32:45 +0100
categories:
---

# Keygenme-py
#picoCTF2021 #RevereEngineering
# Objetivo
Se nos otorga unicamente un archivo `py` para descargar.
# Solucion

```bash

❯ ls
 keygenme-trial.py
❯ file keygenme-trial.py
keygenme-trial.py: Python script, ASCII text executable, with very long lines (3876)
```
Tenemos el primer trozo de la bandera haciendo un grep al codigo.

```bash
❯ cat keygenme-trial.py | grep pico
key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
```
Sin embargo el resto de la bandera se encuentra cifrado dentro del programa.
El metodo de extraccion de la bandera que yo encontre es el siguiente:

Dentro del código nos encontramos con un par de variables y una funcion bastante importantes.
- La variable `bUsername_trial = b"MORTON"`. La b en anteposicion al valor de la variable significa que esta variable almacena los bytes de la cadena dada. La variable representa BYTES NO UNA STRING.
- La variable ` key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_` que almacena la primera parte de la bandera.
- La funcion `def check_key(key, username_trial)`. Dentro de el contexto de este programa la llave de licencia es la bandera, pues si el largo de la llave proporcionada por el usuario es distinto al largo de la bandera completa la licencia es invalida. Ademas de que la primera parte de la funcion se dedica a corroborar caracter por caracter que la llave de licencia coincida con la bandera.

Por lo tanto podemos extraer la siguiente linea particular del programa:


`hashlib.sha256(username_trial).hexdigest()[5]`

Es un ejemplo de una serie de comprobaciones que realiza la funcion, la comprobacion courre desde "hexdigest()[1]" hasta "hexdigest()[8]".

Por lo tanto podemos obtener el resto de la bandera si se genera una serie de objetos hash con SHA265 con los bytes de "MORTON" y se muestra la representacion hexadecimal del objeto hash.

El siguiente script en Python resuelve el problema

```python 
❯ python generadorHash.py
   7   │ segundaMitad = segundaMitad + str(hex_digest[4])
   8   │ segundaMitad = segundaMitad + str(hex_digest[5])
   9   │ segundaMitad = segundaMitad + str(hex_digest[3])
  10   │ segundaMitad = segundaMitad + str(hex_digest[6])
  11   │ segundaMitad = segundaMitad + str(hex_digest[2])
  12   │ segundaMitad = segundaMitad + str(hex_digest[7])
  13   │ segundaMitad = segundaMitad + str(hex_digest[1])
  14   │ segundaMitad = segundaMitad + str(hex_digest[8])
  15   │ print (primerMitad+segundaMitad+'}')
  16   │ 
───────┴───────────────────────────────────────────────────
```
```bash
❯ python generadorHash.py
picoCTF{1n_7h3_|<3y_of_75fc1081}
```

===picoCTF{1n_7h3_|<3y_of_75fc1081}===

# Notas adicionales
# Referencias
