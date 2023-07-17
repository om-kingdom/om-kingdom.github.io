---
layout: post
title:  "vault-door-training PicoCTF"
date:   2023-07-09 12:32:45 +0100
categories:
---


# vault-door-training
#picoCTF2019 #ReversEngineering
# Objetivo
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: VaultDoorTraining.java
# Solucion
Se decarga mediante wget el archivo. Es un archivo con codigo fuente de Java sin compilar.
El codigo fuente presenta un corroborador de contraseñas, si se entrega la contraseña correcta (la bandera) se otorga acceso al usuario.
La contraseña real (bandera) esta colocada dentro del codigo fuente sin compilar.

```Java
  15   │    }
  16   │ 
  17   │     // The password is below. Is it safe to put the
       │  password in the source code?
  18   │     // What if somebody stole our source code? Then
       │  they would know what our
  19   │     // password is. Hmm... I will think of some way
       │ s to improve the security
  20   │     // on the other doors.
  21   │     //
  22   │     // -Minion #9567
  23   │     public boolean checkPassword(String password) {
  24   │         return password.equals("w4rm1ng_Up_w1tH_jAv
       │ 4_3808d338b46");
  25   │     }
```

```bash
❯ cat VaultDoorTraining.java | grep password 
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_3808d338b46");
```
picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46}

# Notas Adicionales
# Referencias
