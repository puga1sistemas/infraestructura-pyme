# Base de Datos – MySQL 8.0

## 1. Introducción
El sistema de base de datos es un componente crítico para el almacenamiento persistente de la información de la plataforma.  
En esta infraestructura se utiliza **MySQL 8.0**, una versión moderna, estable y con soporte para transacciones ACID.

Este documento describe la instalación, configuración inicial y validación del servicio.

---

## 2. Requisitos previos
- Servidor Linux actualizado (Debian/Ubuntu).
- Acceso con privilegios de administrador.
- Espacio en disco suficiente para datos y logs.
- Firewall configurado para permitir acceso local o remoto según la política de seguridad.

---

## 3. Instalación de MySQL 8.0

### 3.1 Actualización del sistema
```
sudo apt update
sudo apt upgrade -y
```

### 3.2 Instalación del servidor MySQL
```
sudo apt install mysql-server -y
```

### 3.3 Verificación del servicio
```
systemctl status mysql
systemctl enable mysql
systemctl start mysql
```

El servicio debe aparecer como **active (running)**.

---

## 4. Configuración inicial

### 4.1 Ejecución del script de seguridad
```
sudo mysql_secure_installation
```

Recomendaciones:
- Habilitar validación de contraseñas.
- Eliminar usuarios anónimos.
- Deshabilitar acceso root remoto.
- Eliminar base de datos de pruebas.

### 4.2 Acceso al cliente MySQL
```
sudo mysql
```

### 4.3 Creación de usuario y base de datos
```
CREATE DATABASE plataforma;
CREATE USER 'plataforma'@'localhost' IDENTIFIED BY 'cambiar123';
GRANT ALL PRIVILEGES ON plataforma.* TO 'plataforma'@'localhost';
FLUSH PRIVILEGES;
```

---

## 5. Configuración del servicio

### 5.1 Archivo de configuración principal
Ruta habitual:

```
/etc/mysql/mysql.conf.d/mysqld.cnf
```

Parámetros recomendados:

```
bind-address = 127.0.0.1
sql_mode = STRICT_TRANS_TABLES
max_connections = 150
```

Tras modificar:

```
sudo systemctl restart mysql
```

---

## 6. Copias de seguridad

### 6.1 Backup manual
```
mysqldump -u plataforma -p plataforma > backup.sql
```

### 6.2 Restauración
```
mysql -u plataforma -p plataforma < backup.sql
```

---

## 7. Pruebas de funcionamiento

1. Conexión local:
   ```
   mysql -u plataforma -p
   ```
2. Crear tabla de prueba:
   ```
   CREATE TABLE test (id INT PRIMARY KEY, nombre VARCHAR(50));
   ```
3. Insertar datos:
   ```
   INSERT INTO test VALUES (1, 'OK');
   ```
4. Consultar:
   ```
   SELECT * FROM test;
   ```

---

## 8. Conclusión
MySQL 8.0 queda instalado, asegurado y configurado para su uso por la plataforma.  
Este documento forma parte de la infraestructura base del sistema.
