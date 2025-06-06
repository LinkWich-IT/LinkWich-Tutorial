<p align="center">
  <img src="assets/LOGO-SIN-CIRCULO-AZUL.png" alt="LinkWich-Monitor Logo" width="220"/>
</p>

<h1 align="center">LinkWich-Monitor</h1>
<p align="center">
  <strong>Tu plataforma integral de monitoreo de redes</strong>
</p>

<p align="center">
  <a href="https://github.com/LinkWich-IT/LinkWich-Tutorial/stargazers">
    <img src="https://img.shields.io/github/stars/LinkWich-IT/LinkWich-Tutorial?style=social" alt="GitHub stars"/>
  </a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT"/>
  </a>
  <a href="https://linkwich-it.github.io/LinkWich-Tutorial/">
    <img src="https://img.shields.io/badge/Docs-Online-blue" alt="Docs Online"/>
  </a>
  <a href="https://github.com/LinkWich-IT/LinkWich-Tutorial/issues">
    <img src="https://img.shields.io/github/issues/LinkWich-IT/LinkWich-Tutorial" alt="Issues"/>
  </a>
</p>

---

## 📖 Introducción

**LinkWich-Monitor** es la solución todo-en-uno diseñada para administradores de red que buscan visibilidad, control y automatización en una misma plataforma. Con un **dashboard interactivo**, **mapas de topología automáticos**, **alertas avanzadas**, **respaldos programados**, **reportes profesionales** y acceso **SSH web**, LinkWich-Monitor te brinda una experiencia ágil y profesional para gestionar cualquier infraestructura de TI.

---

## 📋 Tabla de Contenidos

1. [Características Principales](#-características-principales)  
2. [Capturas de Pantalla](#-capturas-de-pantalla)  
3. [Requisitos](#-requisitos)  
4. [Instalación Rápida](#-instalación-rápida)  
5. [Primeros Pasos](#-primeros-pasos)  
6. [Documentación Completa](#-documentación-completa)  
7. [Colaborar y Contribuir](#-colaborar-y-contribuir)  
8. [Licencia](#-licencia)  

---

## ✨ Características Principales

- 🖥️ **Dashboard Interactivo**  
  Diseño modular con tarjetas movibles; personaliza tu vista y accede rápidamente a métricas clave.  

- 🌐 **Topología Automática (LLDP / CDP)**  
  Mapa dinámico de red con filtros por grupo y dispositivo; guarda y recupera layouts personalizados; información detallada al hacer clic en cada nodo.  

- 🔔 **Alertas Avanzadas**  
  • Monitoreo SNMP para caídas de dispositivos.  
  • Reglas de syslog por nivel de severidad, palabra clave y exclusiones de IP.  
  • Notificaciones por correo electrónico (configurables por grupo/dispositivo).  

- 💾 **Respaldos Automatizados**  
  Programación diaria, semanal o mensual de respaldos de configuración via SSH (TFTP/FTP) en switches y routers compatibles.  

- 📈 **Reportes Profesionales**  
  • Disponibilidad histórica por dispositivo.  
  • Uso de ancho de banda por interfaz.  
  • Historial y resumen de syslog con interpretación básica de IA.  
  • Exportación a PDF o impresión directa.  

- 📡 **Terminal SSH Web Integrada**  
  Consola estilo PuTTY dentro del navegador; múltiples sesiones simultáneas, registro de comandos y auditoría de accesos.  

- 🔄 **NetPath Inteligente**  
  Traceroute avanzado con trazado de múltiples rutas, latencia, pérdida de paquetes y gráficos interactivos.  

---

## 📸 Capturas de Pantalla

<div align="center">
  <img src="assets/dashboard.png" alt="Dashboard" width="45%" style="margin-bottom: 1rem;" />
  <img src="assets/mapa.png" alt="Mapa LLDP" width="45%" style="margin-bottom: 1rem;" />
</div>
<div align="center">
  <img src="assets/alertas.png" alt="Alertas" width="30%" />
  <img src="assets/respaldos.png" alt="Respaldos" width="30%" />
  <img src="assets/terminal.png" alt="Terminal SSH" width="30%" />
</div>

---

## 🎯 Requisitos

- **Sistema Operativo (Servidor):**  
  • Windows Server 2019 en adelante (x64)  
  • Windows 10 / 11 (x64)  

- **Base de Datos:**  
  • MariaDB 10.4+  

- **Dependencias de Python:**  
  • Python 3.9+  
  • Flask  
  • mysql-connector-python  
  • pysnmp  
  • requests  
  • eventlet (para Flask-SocketIO)  

- **Navegador Web (Cliente):**  
  • Chrome, Firefox, Edge o Safari (versión reciente)  

---

## 🚀 Instalación Rápida

> **Nota:** Se asume que MariaDB ya está instalada y accesible.  

1. Clona el repositorio oficial:  
   ```bash
   git clone https://github.com/LinkWich-IT/LinkWich-Tutorial.git
   cd LinkWich-Tutorial
