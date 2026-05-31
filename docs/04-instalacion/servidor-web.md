# Servidor Web – Apache 2.4.60

## 1. Introducción
El servidor web es el componente encargado de publicar la aplicación y servir contenido HTTP/HTTPS a los usuarios internos de la organización.  
En esta infraestructura se utiliza **Apache 2.4.60**, una versión estable y ampliamente soportada en entornos Linux.

Este documento describe el proceso de instalación, configuración y validación del servicio.

---

## 2. Requisitos previos
- Servidor Linux actualizado (Debian/Ubuntu).
- Acceso con privilegios de administrador.
- Puerto 80 y 443 disponibles.
- Certbot instalado para la gestión de certificados SSL/TLS.

---

## 3. Instalación de Apache 2.4.60

### 3.1 Actualización del sistema
```
sudo apt update
sudo apt upgrade -y
```

### 3.2 Instalación del servidor web
```
sudo apt install apache2 -y
```

### 3.3 Verificación del servicio
```
systemctl status apache2
systemctl enable apache2
systemctl start apache2
```

El servidor debe mostrar el estado **active (running)**.

---

## 4. Estructura de directorios recomendada

| Ruta | Descripción |
|------|-------------|
| /var/www/ | Raíz de los sitios web |
| /etc/apache2/ | Configuración principal |
| /etc/apache2/sites-available/ | VirtualHosts disponibles |
| /etc/apache2/sites-enabled/ | VirtualHosts activos |
| /var/log/apache2/ | Logs de acceso y error |

---

## 5. Configuración del sitio web

### 5.1 Creación del directorio del sitio
```
sudo mkdir -p /var/www/empresa.local
sudo chown -R www-data:www-data /var/www/empresa.local
```

### 5.2 VirtualHost básico
Crear el archivo:

```
sudo nano /etc/apache2/sites-available/empresa.local.conf
```

Contenido recomendado:

```
<VirtualHost *:80>
    ServerName empresa.local
    DocumentRoot /var/www/empresa.local

    ErrorLog ${APACHE_LOG_DIR}/empresa_error.log
    CustomLog ${APACHE_LOG_DIR}/empresa_access.log combined
</VirtualHost>
```

### 5.3 Activación del sitio
```
sudo a2ensite empresa.local.conf
sudo systemctl reload apache2
```

---

## 6. Habilitar HTTPS con Certbot

### 6.1 Instalación de Certbot (si no está instalado)
```
sudo apt install certbot python3-certbot-apache -y
```

### 6.2 Obtención del certificado
```
sudo certbot --apache -d empresa.local
```

Certbot configurará automáticamente el VirtualHost HTTPS.

---

## 7. Pruebas de funcionamiento

1. Acceder desde un navegador a:  
   `http://empresa.local`
2. Verificar que el sitio responde correctamente.
3. Si se ha configurado HTTPS, comprobar:  
   `https://empresa.local`
4. Revisar logs en caso de error:
   ```
   tail -f /var/log/apache2/empresa_error.log
   ```

---

## 8. Conclusión
El servidor web Apache 2.4.60 queda instalado, configurado y preparado para servir contenido de forma segura mediante HTTPS.  
Este documento forma parte de la infraestructura base de la plataforma.

## 9. Integración con el balanceador HAProxy

El servidor web Apache no recibe tráfico directamente desde los clientes, sino a través del balanceador de carga HAProxy. La integración se realiza de la siguiente forma:

### 9.1. Arquitectura de acceso
- Los clientes acceden a HAProxy mediante HTTP/HTTPS.
- HAProxy actúa como frontal y distribuye las peticiones al servidor Apache.
- Apache solo debe aceptar tráfico desde la IP del balanceador.

### 9.2. Configuración recomendada en Apache
En el VirtualHost se recomienda añadir:

```
RemoteIPHeader X-Forwarded-For
RemoteIPTrustedProxy 192.168.1.10   # IP del balanceador HAProxy
```

Esto permite que Apache registre correctamente la IP real del cliente.

### 9.3. Backend en HAProxy
El servidor Apache debe estar definido como backend en HAProxy, por ejemplo:

```
backend apache_backend
    server apache1 192.168.1.20:80 check
```

### 9.4. Consideraciones de seguridad
- Apache debe estar accesible **solo** desde HAProxy.
- El firewall debe bloquear accesos directos al puerto 80/443 desde redes externas.
- Los certificados SSL se gestionan en HAProxy (terminación TLS en el frontal).

### 9.5. Pruebas de integración
1. Acceder a la IP o dominio del balanceador.
2. Verificar que Apache responde correctamente a través de HAProxy.
3. Revisar los logs de Apache para comprobar que la IP del cliente aparece correctamente:
   ```
   tail -f /var/log/apache2/empresa_access.log
   ```
