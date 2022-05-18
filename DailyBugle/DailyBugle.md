# Write Up Pickle Rick

¡Hola! Vamos a realizar la maquina Daily-Bugle de Tryhackme.

# Enumeración

Realizamos la enumeración de protocolos de la máquina, para ello utilizamos:

> Nmap -T5 -p- -sV 10.10.209.197

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen1.PNG?raw=true)

# Respuestas
## who robbed the bank

Entramos en la web y nos dice la respuesta.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen2.PNG?raw=true

## Versión

Hemos utilizado joomscan para obtener información sobre el sistema.

> Joomscan -u http://10.10.209.197/

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen3.PNG?raw=true)

## Contraseña

Hemos descargado el script de joomblah para la obtención del hash del usuario, luego lo pasaremos a john the ripper con el diccionario rockyou para saber la contraseña.

> Python script.py http://10.10.209.197/

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen4.PNG?raw=true)

> John --wordlist=worckyou.txt hash.txt

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen5.PNG?raw=true)

Una vez tenemos la contraseña y el usuario, entramos en la aplicación Joomla. 

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen6.PNG?raw=true)

## Shell Reverse
Una vez estamos dentro de joomla, vamos a insertar una shell reversa para poder entrar en el sistema.
Para ello descargamos el archivo de php-reverse-shell de pentestmonkey.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen7.PNG?raw=true)

Una vez hemos adquirido la shell reversa, la vamos a copiar dentro de index.php para disimular un poco y sea un poco mas complicado de localizarla.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen8.PNG?raw=true)

Y modificamos los siguientes parámetros por nuestra dirección.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen9.PNG?raw=true)

En este momento necesitamos poner nuestro equipo en escucha desde el puerto cambiado en la web.
Para este paso debemos poner en la terminal lo siguiente;

> nc -lvpn 4444

A continuación entramos en la siguiente URL para que la se complete la shell reverse.

> http://{IP}/templates/index.php

Y para finalizar debemos entrar en la terminal que dejamos en escucha.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen10.PNG?raw=true)

Una vez estamos dentro vamos a listar el directorio home para saber los usuarios que existen.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen11.PNG?raw=true)

Una vez tenemos el usuario, lo siguiente que vamos ha realizar la lectura del fichero para saber la contraseña:

> cat /var/www/html/configuration.php

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen12.PNG?raw=true)

## Flag Usuario

Una vez allí accedemos como el usuario y entramos en nuestro directorio home y vemos la flag.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen13.PNG?raw=true)

## Flag Root
Entramos por ssh en el equipo mediante el usuario anterior. Luego realizamos le comando sudo -l para saber que permisos tenemos, y vemos que esta habilitado el comando yum. 
Hemos encontrado en gtfobins un script para ser sudo.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen14.PNG?raw=true)

Una vez lo ejecutamos somos root y vemos la flag.

![enter image description here](https://github.com/AbelPosadoReyes/WriteUps/blob/main/DailyBugle/img/Imagen15.PNG?raw=true)