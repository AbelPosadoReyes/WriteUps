# Write Up Pickle Rick

¡Hola! Vamos a realizar la maquina Pickle Rick de Tryhackme.

# Enumeración

Realizamos la enumeración de protocolos de la máquina, para ello utilizamos:

> Nmap -T5 -p- -sV 10.10.139.30

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen1.PNG?raw=true)

# Encontrar Usuario y Contraseña

## Usuario

Podemos visualizar el código fuente de la web y obtenemos el usuario.

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen2.PNG?raw=true)

## Contraseña

Para poder obtener la contraseña, debemos iniciar con el comando dirb y gobuster, estos dos comandos nos ofrecen una lista de webs. Tenemos que entrar en la siguiente web:

> Dirb http://10.10.46.194/

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen3.PNG?raw=true)

> Gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.10.46.194 -x php

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen4.PNG?raw=true)

Y de esta forma, conseguimos la contraseña del usuario.

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen5.PNG?raw=true)

# Acceso

Como hemos realizado el listado de directorios con páginas webs vemos que existe una que se llama login.php, e ingresamos las credenciales.

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen6.PNG?raw=true)

# Preguntas frecuentes

Una vez dentro, debemos hacernos las siguientes preguntas:

- ¿Que permisos tenemos?

- ¿Quién somos?

- ¿Dónde estamos?

Para respondernos a estas cuestiones, debemos poner los siguientes comandos:

> Sudo -l

> Whoami

> Pwd

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen7.PNG?raw=true)

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen8.PNG?raw=true)

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/Imagen9.PNG?raw=true)

# Flags

Debemos investigar mediante los comandos para encontrar las flags.

## Flag 1

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/flag1.PNG?raw=true)

## Flag 2

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/flag2.PNG?raw=true)

## Flag 3

![`enter image description here`](https://github.com/AbelPosadoReyes/WriteUps/blob/main/PickleRick/img/flag3.PNG?raw=true)