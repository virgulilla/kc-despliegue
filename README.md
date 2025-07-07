# Módulo de Bootcamp Keepcoding: Despliegue de Servidores en Producción

## Descripción general

En este módulo se ha desplegado en producción dos aplicaciones:

- Una **aplicación web frontend** desarrollada con **React**
- Una **aplicación backend** con **Node.js + Express**, que renderiza vistas con **EJS**

Ambas están accesibles públicamente mediante HTTPS, desplegadas en un servidor Ubuntu en AWS, gestionadas con Nginx y protegidas con certificados SSL.

---

## Tecnologías utilizadas

- **Servidor**: Ubuntu (AWS EC2)
- **Frontend**: React (CRA)
- **Backend**: Node.js + Express + EJS
- **Base de datos**: MongoDB (instalada localmente)
- **Servidor web**: Nginx
- **Gestor de procesos**: Supervisor
- **Certificados SSL**: Let's Encrypt + Certbot

---

## URLs de acceso

- 🔗 **Aplicación React (SPA)**: [https://kcreact.duckdns.org/](https://kcreact.duckdns.org/)
- 🔗 **Aplicación Node.js + EJS**: [https://kcexpress.duckdns.org/](https://kcexpress.duckdns.org/)

---

## Características clave del despliegue

### ✅ 1. Despliegue en AWS EC2

Se ha levantado una instancia EC2 en AWS, configurando:

- Acceso SSH con clave pública
- Apertura de puertos **80 (HTTP)** y **443 (HTTPS)** en el firewall (Security Groups)

---

### ✅ 2. MongoDB instalado localmente

- MongoDB se instaló en la misma instancia.
- Solo es utilizada por la app de Node.js (la app de React no está conectada a ninguna API).
- Conexión local sin exponer el puerto públicamente.

---

### ✅ 3. Aplicaciones independientes

- La aplicación en React es una SPA que no interactúa con la app de Node.
- La aplicación en Node.js renderiza vistas directamente con EJS y gestiona su lógica de forma autónoma.

---

### ✅ 4. Nginx como proxy inverso y servidor estático

- Nginx se configuró como proxy inverso para la aplicación Node.js (evitando exponer el puerto 3000).
- También sirve los archivos estáticos (CSS, JS, imágenes) de la app de Node directamente, mejorando el rendimiento.
- Para la app React, Nginx sirve directamente los archivos compilados (`build/`).

---

### ✅ 5. HTTPS con Certbot

- Se generaron certificados SSL con Let's Encrypt para ambos dominios.
- Nginx ha sido configurado automáticamente por Certbot para servir las apps de forma segura (HTTPS) y renovar los certificados automáticamente.

---

### ✅ 6. Gestión del backend con Supervisor

- Se configuró Supervisor para mantener el backend Node.js en ejecución.
- Permite reinicios automáticos ante fallos o reinicios del servidor.

---

## Lecciones aprendidas

- Configuración segura de un servidor Ubuntu en AWS
- Despliegue separado de frontend y backend independientes
- Uso de Nginx como proxy inverso y servidor de archivos estáticos
- Gestión de procesos en segundo plano con Supervisor
- Configuración de HTTPS con Certbot y Let's Encrypt
