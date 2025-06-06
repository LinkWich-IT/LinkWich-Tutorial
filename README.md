<p align="center">
  <img src="assets/img/LOGO-SIN-CIRCULO-AZUL.png" alt="LinkWich-Monitor Logo" width="220"/>
</p>

<h1 align="center">LinkWich-Monitor</h1>
<p align="center">
  <strong>Tu plataforma integral de monitoreo de redes e infrastructura</strong>
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

**LinkWich-Monitor** es la solución todo-en-uno diseñada para administradores de red que buscan visibilidad, control y automatización en una misma plataforma. Con un **dashboard interactivo**, **mapas de topología automáticos**, **alertas avanzadas**, **respaldos programados**, **reportes profesionales**, **syslog** y acceso **SSH web**, LinkWich-Monitor te brinda una experiencia ágil y profesional para gestionar cualquier infraestructura de TI.

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
  Programación diaria, semanal o mensual de respaldos de configuración via SSH en switches y routers compatibles.  

- 📈 **Reportes Profesionales**  
  • Disponibilidad histórica por dispositivo.  
  • Uso de ancho de banda por interfaz.  
  • Historial y resumen de syslog con interpretación básica de IA.  
  • Exportación a PDF o impresión directa.  

- 📡 **Terminal SSH Web Integrada**  
  Consola estilo PuTTY dentro del navegador; múltiples sesiones simultáneas, registro de comandos y auditoría de accesos.  

- 🔄 **NetPath Inteligente**  
  Traceroute avanzado con trazado de múltiples rutas, latencia, pérdida de paquetes y gráficos interactivos.

-🖱️ **Interacción Visual y Diagnóstico**  
  • **Ver Interfaces:** con un solo clic, muestra en pantalla las estadísticas SNMP de cada interfaz (tráfico, errores, estado).  
  • **Buscar MAC:** botón dedicado para filtrar y localizar direcciones MAC en la tabla de switching, sin escribir comandos.  
  • **Prueba TDR (Time Domain Reflectometry):** ejecuta un test de cableado desde la interfaz web y muestra resultados de reflectometría automáticamente.  
  • **Descubrimiento LLDP:** botón “Mapear Vecinos” que ejecuta la consulta LLDP y despliega automáticamente los vecinos conectados.  
  • **Comandos de Visualización Predefinidos:** menú desplegable con opciones como `show interfaces`, `show mac-address-table`, `show lldp neighbors`, etc., que se ejecutan al presionar y presentan la salida en pantalla.  
  • **Upgrade de Equipo:** acción gráfica para iniciar el proceso de actualización de firmware/configuración vía SSH, todo controlado desde el panel sin ingresar a CLI.  

---

## 📸 Capturas de Pantalla

<div align="center">
  <img src="assets/img/dashboard.png" alt="Dashboard" width="45%" style="margin-bottom: 1rem;" />
  <img src="assets/img/MAP.png" alt="Mapa LLDP" width="45%" style="margin-bottom: 1rem;" />
</div>
<div align="center">
  <img src="assets/img/alertas.png" alt="Alertas" width="30%" />
  <img src="assets/img/respaldos.png" alt="Respaldos" width="30%" />
  <img src="assets/img/terminal.png" alt="Terminal SSH" width="30%" />
</div>

---

A continuación se muestran los requisitos de hardware y software para instalar y ejecutar LinkWich-Monitor de manera óptima.

| Componente                      | Requisito Mínimo                          | Recomendado / Notas                                              |
|---------------------------------|-------------------------------------------|------------------------------------------------------------------|
| **Sistema Operativo (Servidor)**| Windows Server 2019 (x64)                 | Windows Server 2022 (x64)                                        |
|                                 | Windows 10 / 11 (x64)                     | Windows 10 Pro / Windows 11 Pro                                  |
| **Procesador (CPU)**            | 4 cores (x64, 2.0 GHz)                    | 8 cores (x64, 3.0 GHz o superior)                                |
| **Memoria RAM**                 | 8 GB                                      | 16 GB o más                                                      |
| **Almacenamiento (HDD/SSD)**    | 50 GB libres                              | SSD NVMe de 100 GB o más                                         |
| **Base de Datos**               | MariaDB 10.4+                             | MariaDB 10.6+                                                    |
| **Dependencias de Python**      | Python 3.9+                               | Python 3.10+; entrono virtual (venv)                             |
|                                 | Flask                                     | Última versión estable                                           |
|                                 | mysql-connector-python                    | Última versión estable                                           |
|                                 | pysnmp                                    | Última versión estable                                           |
|                                 | requests                                  | Última versión estable                                           |
|                                 | eventlet (para Flask-SocketIO)            | Última versión estable                                           |
| **Tarjeta de Video (GPU)**      | No es obligatoria                         | NVIDIA con soporte CUDA (p. ej. RTX 20/30/40 series) para IA     |
|                                 |                                           | *(Requerida solo si se desea acelerar procesamiento de modelos)* |
| **Navegador Web (Cliente)**     | Chrome, Firefox, Edge o Safari (actualizados) |                                                              |

> **Nota sobre IA y GPU:**  
> Para aprovechar las funcionalidades de análisis de logs basadas en modelos de IA, se recomienda contar con una **tarjeta de video NVIDIA** con soporte CUDA. Sin embargo, LinkWich-Monitor funcionará correctamente sin GPU dedicada; contará con procesamiento en CPU, aunque con menor rendimiento en tareas de inferencia de modelos.

> **Espacio adicional en disco:**  
> - Logs históricos y respaldos automáticos pueden requerir almacenamiento extra (dependiendo del volumen de datos).  
> - Se sugiere reservar al menos **100 GB** en el servidor si se prevé un uso intensivo de reportes, dashboards y archivos de respaldos.  
- **Navegador Web (Cliente):**  
  • Chrome, Firefox, Edge o Safari (versión reciente)  

---

| Cantidad de Dispositivos | CPU (mínimo)                   | RAM (mínimo)                        | Tarjeta de Video                                    | Tarjeta de Red                                     | Notas                                 |
|--------------------------|--------------------------------|-------------------------------------|------------------------------------------------------|----------------------------------------------------|---------------------------------------|
| Hasta 50                 | Intel Core i5 (o equivalente)  | 8 GB DDR4 (o equivalente DDR3)      | No obligatoria (recomendada NVIDIA con CUDA para IA) | 1 Gbps                                             | Hasta 500 sensores                    |
| 51 – 150                 | Intel Core i7 (o equivalente)  | 16 GB                               | No obligatoria (recomendada NVIDIA con CUDA para IA) | 1 Gbps (varias NIC si hay múltiples VLAN/redes)   |                                       |
| Más de 150               | Intel Core i9 (o equivalente)  | 32 GB                               | No obligatoria (recomendada NVIDIA con CUDA para IA) | 1 Gbps (varias NIC si hay múltiples VLAN/redes)   | En Windows Server: soporte para NIC-TEAM |

## 🚀 Instalación Rápida

> **Nota:** Se asume que MariaDB ya está instalada y accesible.  

1. Clona el repositorio oficial:  
   ```bash
   git clone https://github.com/LinkWich-IT/LinkWich-Tutorial.git
   cd LinkWich-Tutorial
