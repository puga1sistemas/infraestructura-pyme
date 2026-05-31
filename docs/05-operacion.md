# Guía de Operación – Mantenimiento Diario

## 1. Introducción
Este documento describe las tareas de operación y mantenimiento diario necesarias para garantizar la estabilidad, seguridad y disponibilidad del sistema.  
El objetivo es establecer un procedimiento claro y repetible para el equipo de operaciones.

---

## 2. Comprobaciones diarias del sistema

### 2.1 Estado de servicios críticos
```
systemctl status apache2
systemctl status mysql
systemctl status ssh
```

### 2.2 Uso de recursos
```
top
df -h
free -m
```

### 2.3 Logs del sistema
```
journalctl -p 3 -xb
tail -n 50 /var/log/syslog
```

---

## 3. Verificación de seguridad

### 3.1 Intentos de acceso fallidos
```
grep "Failed password" /var/log/auth.log
```

### 3.2 Estado de Fail2ban
```
sudo fail2ban-client status sshd
```

### 3.3 Reglas del firewall
```
sudo ufw status verbose
```

---

## 4. Comprobación de servicios web

### 4.1 Disponibilidad HTTP/HTTPS
```
curl -I http://empresa.local
curl -I https://empresa.local
```

### 4.2 Estado de certificados SSL
```
sudo certbot certificates
```

---

## 5. Copias de seguridad

### 5.1 Verificar que se han generado correctamente
```
ls -lh /var/backups/
```

### 5.2 Probar restauración en entorno controlado
```
mysql -u plataforma -p plataforma < /var/backups/backup.sql
```

---

## 6. Tareas semanales recomendadas

- Revisión de actualizaciones del sistema.
- Limpieza de logs antiguos.
- Verificación de espacio en disco.
- Comprobación de integridad de backups.

---

## 7. Conclusión
Este documento establece las tareas de operación necesarias para mantener el sistema en funcionamiento óptimo.  
Debe revisarse y actualizarse periódicamente según evolucione la infraestructura.

## 8. Operación y mantenimiento del balanceador HAProxy

La incorporación de HAProxy en la infraestructura requiere añadir tareas específicas de operación para garantizar la disponibilidad del servicio web y la correcta distribución del tráfico.

### 8.1 Estado del servicio HAProxy
```
systemctl status haproxy
systemctl enable haproxy
systemctl restart haproxy
```

### 8.2 Comprobación de salud de los backends
Verificar que el servidor Apache responde correctamente a través del balanceador:

```
curl -I http://balanceador.local
```

Consultar el estado interno de HAProxy (si está habilitada la página de estadísticas):

```
http://balanceador.local:8404
```

### 8.3 Revisión de logs del balanceador
```
tail -n 50 /var/log/haproxy.log
journalctl -u haproxy -n 50
```

### 8.4 Validación de reglas y configuración
Comprobar que la configuración no contiene errores:

```
haproxy -c -f /etc/haproxy/haproxy.cfg
```

### 8.5 Tareas semanales específicas de HAProxy
- Revisar el estado de los servidores backend.
- Verificar que no existan tiempos de respuesta anómalos.
- Comprobar la rotación de logs del balanceador.
- Validar que los certificados