# Acceso Seguro SSH y Configuración de Firewall

## 1. Introducción
Este documento describe las medidas de seguridad aplicadas al acceso remoto mediante SSH y la configuración del firewall del servidor.  
El objetivo es reducir la superficie de ataque y garantizar que únicamente usuarios autorizados puedan acceder al sistema.

---

## 2. Requisitos previos
- Servidor Linux actualizado (Debian/Ubuntu).
- Acceso con privilegios de administrador.
- Paquetes `openssh-server` y `ufw` instalados.

---

## 3. Configuración segura de SSH

### 3.1 Verificar instalación del servicio SSH
```
sudo systemctl status ssh
```

### 3.2 Archivo de configuración principal
Ruta:

```
/etc/ssh/sshd_config
```

Parámetros recomendados:

```
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
X11Forwarding no
AllowTcpForwarding no
```

Tras modificar:

```
sudo systemctl restart ssh
```

---

## 4. Gestión de claves SSH

### 4.1 Generación de clave en el cliente
```
ssh-keygen -t ed25519 -C "usuario@empresa"
```

### 4.2 Copia de clave pública al servidor
```
ssh-copy-id usuario@IP_DEL_SERVIDOR
```

### 4.3 Permisos correctos
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## 5. Configuración del firewall (UFW)

### 5.1 Activar UFW
```
sudo ufw enable
```

### 5.2 Permitir únicamente SSH y servicios necesarios
```
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### 5.3 Denegar todo lo demás
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### 5.4 Ver estado del firewall
```
sudo ufw status verbose
```

---

## 6. Protección adicional con Fail2ban

### 6.1 Instalación
```
sudo apt install fail2ban -y
```

### 6.2 Activación del jail SSH
Archivo:

```
/etc/fail2ban/jail.local
```

Contenido recomendado:

```
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 10m
```

Reiniciar:

```
sudo systemctl restart fail2ban
```

---

## 7. Pruebas de seguridad

1. Intentar acceso SSH con clave correcta.  
2. Intentar acceso con contraseña (debe fallar).  
3. Revisar logs:
   ```
   tail -f /var/log/auth.log
   ```
4. Verificar que Fail2ban registra intentos fallidos:
   ```
   sudo fail2ban-client status sshd
   ```

---

## 8. Conclusión
El servidor queda protegido mediante:
- Acceso SSH restringido y basado en claves.
- Firewall UFW con reglas estrictas.
- Fail2ban para mitigar ataques de fuerza bruta.

Este documento completa la configuración de seguridad de la plataforma.

## Reglas UFW
- Permitir SSH solo desde IP de la oficina: `ufw allow from 192.168.1.0/24 to any port 22`
- Permitir tráfico web: `ufw allow 80/tcp` y `ufw allow 443/tcp`
