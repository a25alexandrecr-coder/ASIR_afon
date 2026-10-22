# Instalación de MySQL en Windows y Ubuntu

Guía breve para instalar **MySQL Server** en dos sistemas operativos y comprobar que funciona. Está pensada para alumnos que empiezan en *Xestión de Bases de Datos*.

## Índice

- [Instalación de MySQL en Windows y Ubuntu](#instalación-de-mysql-en-windows-y-ubuntu)
  - [Índice](#índice)
  - [1. Introducción](#1-introducción)
  - [2. Requisitos previos](#2-requisitos-previos)
  - [3. Procedimiento](#3-procedimiento)
    - [3.1 Instalación en Windows](#31-instalación-en-windows)
    - [3.2 Instalación en Ubuntu](#32-instalación-en-ubuntu)
  - [4. Comprobación](#4-comprobación)
  - [5. Resolución de problemas](#5-resolución-de-problemas)
  - [6. Referencias](#6-referencias)

---

## 1. Introducción

**MySQL** es un sistema gestor de bases de datos relacionales de código abierto. Se utiliza con el lenguaje *SQL* y es muy habitual en servidores web y aplicaciones.

![Logotipo de MySQL](imagenes/captura1.png)

> :bulb: **Consejo:** antes de instalar, comprueba qué versión necesitas. En clase usaremos **MySQL 8.0** o superior.

## 2. Requisitos previos

- Equipo con permisos de administrador.
- Conexión a Internet.
- Al menos 2 GB de RAM y 1 GB de disco libre.

| Sistema   | Método de instalación  | Servicio por defecto |
|-----------|------------------------|----------------------|
| Windows   | MySQL Installer (.msi) | `MySQL80`           |
| Ubuntu    | Paquete `apt`          | `mysql`             |

---

## 3. Procedimiento

### 3.1 Instalación en Windows

1. Descarga **MySQL Installer** desde la [web oficial de MySQL](https://dev.mysql.com/downloads/installer/).
2. Ejecuta el instalador y elige el tipo de instalación *Server only*.
3. Pulsa **Execute** para instalar los componentes.
4. En *Accounts and Roles*, define la contraseña del usuario `root`.
5. Deja marcada la opción de iniciar MySQL como servicio de Windows y finaliza el asistente.

### 3.2 Instalación en Ubuntu

1. Actualiza la lista de paquetes e instala el servidor:

   ```bash
   sudo apt update
   sudo apt install mysql-server -y
   ```

2. Asegura la instalación con el script de configuración inicial:

   ```bash
   sudo mysql_secure_installation
   ```

3. Comprueba que el servicio está activo con `systemctl status mysql`.

---

## 4. Comprobación

Conéctate al servidor desde la terminal (o desde *MySQL Command Line Client* en Windows) y ejecuta:

```sql
SELECT VERSION();
SHOW DATABASES;
```

Si se muestra la versión y la lista de bases de datos, la instalación es correcta. :white_check_mark:

> :warning: **Aviso:** si aparece el error `Access denied for user 'root'`, revisa la contraseña definida durante la instalación.

## 5. Resolución de problemas

| Problema | Causa probable | Solución |
|----------|----------------|----------|
| `Access denied for user 'root'` | Contraseña incorrecta | Revisa la contraseña definida en la instalación |
| `Can't connect to local MySQL server` | El servicio está parado | En Ubuntu: `sudo systemctl start mysql`. En Windows: inicia `MySQL80` desde *Servicios* |
| `mysql: command not found` | MySQL no está en el PATH | Añade la carpeta `bin` de MySQL a las variables de entorno |

> :bulb: **Consejo:** para ver por qué falla el servicio en Ubuntu, usa `sudo journalctl -u mysql`.

---

## 6. Referencias

- [Documentación oficial de MySQL](https://dev.mysql.com/doc/)
- [Guía de Ubuntu Server](https://ubuntu.com/server/docs)
