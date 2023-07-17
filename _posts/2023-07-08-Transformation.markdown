---
layout: post
title:  "Transformation PicoCTF"
date:   2023-07-08 12:32:45 +0100
categories:
---


# Transformation
#picoCTF2021 #ReverseEngineering
# Objetivo
I wonder what this really is... enc ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])

# Solucion

```bash
❯ ls
 enc
❯ file enc
enc: Unicode text, UTF-8 text, with no line terminators
❯ cat enc
───────┬────────────────────────────────────────────────────
       │ File: enc
───────┼────────────────────────────────────────────────────
   1   │ 灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸弰摤捤㤷慽
───────┴────────────────────────────────────────────────────

    ~/h/r/Transformation  

```

Se puede obtener el valor hexadecimal de los caracteres mediante python. Obteniendo el valor numerico y despues pasandolo a hexadecimal.

```bash
cat tranformation.py
───────┬───────────────────────────────────────────────────
       │ File: tranformation.py
───────┼───────────────────────────────────────────────────
   1   │ enc = open("enc").read()
   2   │ for c in enc: 
   3   │     print(hex(ord(c)).lstrip("0x"),end='')
   4   │ 
───────┴───────────────────────────────────────────────────
```

obteniendo el siguiente valor hexadecimal:

==7069636f4354467b31365f626974735f696e73743334645f6f665f385f30646463643937617d%==

Al colocarlo en cyberchef obtenemos la bandera.

===picoCTF{16_bits_inst34d_of_8_0ddcd97a}===

# Notas adicionales
# Referencias
https://gchq.github.io/CyberChef/
