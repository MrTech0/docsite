---
title: "Como instalar Wordpress en Ubuntu"
summary: Tutorial básico para tener una instancia de WordPress
date: 2023-05-09T17:56:54+02:00
author: "Pol Carmona"
draft: false
---

WordPress es una plataforma de gestión de contenidos muy popular que se utiliza para crear sitios web y blogs. En este tutorial, aprenderás cómo instalar WordPress en Ubuntu.

# Requisitos previos

Antes de comenzar, necesitarás lo siguiente:

- Una instancia de Ubuntu
- Un usuario con permisos de sudo
- Acceso a Internet

## Paso 1: Instalar LAMP

Para instalar WordPress, necesitarás un servidor web y una base de datos. En Ubuntu, puedes instalar ambos utilizando LAMP (Linux, Apache, MySQL, PHP).

Para instalar LAMP, abre una terminal y ejecuta los siguientes comandos:

```bash
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql
```

Durante la instalación, se te pedirá que configures una contraseña para el usuario de root de MySQL. Asegúrate de recordarla, ya que la necesitarás más adelante.

## Paso 2: Descargar WordPress

Una vez que LAMP esté instalado, puedes descargar WordPress. Descarga la última versión de WordPress desde su sitio web oficial:

```bash
cd /tmp
curl -LO https://wordpress.org/latest.tar.gz
```

Después de descargar WordPress, descomprime el archivo:

```bash
tar xzvf latest.tar.gz
```

## Paso 3: Crear la base de datos de WordPress

Antes de continuar con la instalación de WordPress, necesitas configurar la base de datos. En primer lugar, crea una base de datos y un usuario para WordPress:

```bash
mysql -u root -p
```

Luego, en el shell de MySQL, ejecuta los siguientes comandos:

```sql
CREATE DATABASE wordpress;
GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
EXIT;
```

Recuerda reemplazar "password" con una contraseña segura.

## Paso 4: Configurar WordPress

Ahora, mueve el directorio de WordPress descargado a la raíz de tu servidor web:

```bash
sudo mv /tmp/wordpress /var/www/html/
```

Luego, cambia los permisos del directorio para que el servidor web pueda escribir en él:

```bash
sudo chown -R www-data:www-data /var/www/html/wordpress
```

A continuación, renombra el archivo de configuración de WordPress:

```bash
cd /var/www/html/wordpress
cp wp-config-sample.php wp-config.php
```

Abre el archivo wp-config.php en un editor de texto y edita las siguientes líneas:

```php
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'wordpressuser' );
define( 'DB_PASSWORD', 'password' );
```

Recuerda reemplazar "password" con la contraseña que configuraste anteriormente.

## Paso 5: Instalar WordPress

Por último, abre tu navegador web e ingresa la dirección de tu servidor web seguida de "/wordpress". Deberías ver el instalador de WordPress. Elige el idioma que deseas utilizar y sigue las instrucciones en pantalla para completar la instalación.

Una vez que la instalación esté completa, podrás acceder al panel de administración de WordPress ingresando la dirección de tu servidor web seguida de "/wordpress/wp-admin".

¡Felicidades, has instalado WordPress en Ubuntu!