# Plan de Recuperación ante Desastres

## 1. Introducción
Este documento define el procedimiento de recuperación ante fallos críticos del sistema.  
El objetivo es garantizar la continuidad del servicio y minimizar el tiempo de inactividad en caso de incidentes graves.

---

## 2. Tipos de incidentes contemplados

### 2.1 Fallo del servidor web
- Apache no arranca.
- Configuración corrupta.
- Certificados SSL caducados.

### 2.2 Fallo de la base de datos
- Servicio MySQL detenido.
- Corrupción de tablas.
- Pérdida de datos.

### 2.3 Fallo de red o firewall
- Reglas UFW incorrectas.
- SSH inaccesible.
- Bloqueo de puertos críticos.

### 2.4 Fallo de hardware
- Disco dañado.
- Memoria defectuosa.
- Pérdida total del servidor.

---

## 3. Procedimiento general de recuperación

### 3.1 Verificación inicial
```
systemctl status apache2
systemctl status mysql
systemctl status ssh
df -h
journalctl -xe
```

### 3.2 Identificación del origen del fallo
- Revisar logs del sistema.
- Revisar cambios recientes.
- Comprobar estado del firewall.

---

## 4. Recuperación del servidor web

### 4.1 Restaurar configuración
```
sudo cp /etc/apache2/apache2.conf.bak /etc/apache2/apache2.conf
sudo systemctl restart apache2
```

### 4.2 Regenerar certificados SSL
```
sudo certbot renew --force-renewal
```

---

## 5. Recuperación de la base de datos

### 5.1 Reiniciar servicio
```
sudo systemctl restart mysql
```

### 5.2 Restaurar backup
```
mysql -u plataforma -p plataforma < /var/backups/backup.sql
```

### 5.3 Verificar integridad
```
mysqlcheck --all-databases
```

---

## 6. Recuperación del acceso SSH

### 6.1 Restaurar configuración segura
```
sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config
sudo systemctl restart ssh
```

### 6.2 Revisar reglas del firewall
```
sudo ufw status
sudo ufw allow OpenSSH
sudo ufw reload
```

---

## 7. Recuperación ante fallo total del servidor

### 7.1 Reinstalación del sistema
- Instalar SO limpio.
- Instalar Apache, MySQL, SSH, UFW, Fail2ban.

### 7.2 Restauración completa
```
mysql < /var/backups/backup.sql
sudo cp -r /var/www/empresa.local /var/www/
sudo certbot --apache
```

---

## 8. Validación final

1. Comprobar acceso web.  
2. Comprobar acceso SSH.  
3. Verificar logs.  
4. Validar integridad de la base de datos.  
5. Confirmar que los servicios están activos.

---

## 9. Conclusión
Este plan permite recuperar el sistema ante fallos críticos y restablecer la operatividad en el menor tiempo posible.  
Debe revisarse periódicamente y actualizarse según evolucione la infraestructura.
