---
layout: post
title:  "crackme-py PicoCTF"
date:   2023-07-04 12:32:45 +0100
categories: "Reverse Engineering" 
---


# crackme-py
#picoCTF2021 #ReverseEngineering
# Objetivo
Se nos otorga un archivo de extension py con el nombre 'crackme-py'.
# Solucion
La funcion del archivo es recibir dos numeros e indicar cual es el numero mas grande entre ambos.
```bash
❯ file crackme.py
crackme.py: Python script, ASCII text executable
❯ python crackme.py
What's your first number? 0
What's your second number? 0
The number with largest positive magnitude is 0

```

Al examinar el codigo fuente proporcionado nos encontramos con que existe una cadena de caracteres cifrado en tipo ROT. Junto con un alfabeto especifico y una funcion de desencripcion que utiliza dicho alfabeto. Se indica que aparentemente el cifrado ROT es ROT47 pero como se utiliza un alfabeto particular no se puede desencriptar mediante cyberchef.

```python
bezos_cc_secret = "A:4@r%uL`M-^M0c0AbcM-MFE0g4dd`_cgN"
# Reference alphabet
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
             "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"
```

La funcion para desencriptar es la siguiente:

  21   │     # Storage for decoded secret
  22   │     decoded = ""
  23   │ 
  24   │     # decode loop
  25   │     for c in secret:
  26   │         index = alphabet.find(c)
  27   │         original_index = (index + rotate_const) % l
       │ en(alphabet)
  28   │         decoded = decoded + alphabet[original_index
       │ ]
  29   │ 
  30   │     print(decoded) 

  La solucion optima es cambiar la invocacion de la funcion normal que pide dos numeros, por una invocacion a la funcion que devuelve la cadena descifrada.

  y de esta manera obtenemos la bandera.

  ```bash
  ❯ python crackme.py
picoCTF{1|\/|_4_p34|\|ut_8c551048}
  ```
# Notas adicionales
# Referencias
