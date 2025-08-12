# 📘 **Manual de Usuario – Agregar Dispositivos**

Esta sección te permite añadir dispositivos a tu red de **tres formas diferentes**:

- 🖐 **Manual (uno por uno)**
- 📄 **Carga masiva desde Excel**
- 🌐 **Auto-descubrimiento por SNMP**

---

## 1️⃣ **Agregar un dispositivo manualmente**

### 🏷 **Driver Marca**
Selecciona la marca o fabricante del dispositivo *(Cisco, Mikrotik, Fortinet, etc.)*.  
Esto permite que el sistema utilice el **driver adecuado** para la gestión.

### 💻 **Nombre del equipo**
Escribe un nombre descriptivo para identificar el dispositivo.  
Ejemplo: `CoreSwitch01`.

### 🗂 **Grupo**
Selecciona un grupo existente o crea uno nuevo (**botón ➕**).  
Los grupos permiten **organizar** los dispositivos por ubicación, área o función.

### 📍 **Ubicación**
Describe la ubicación física del dispositivo.  
Ejemplo: `Data Center Principal`.

### 🌐 **IP o DNS**
Ingresa la IP o el nombre de dominio que usa el sistema para conectarse.

---

### ⚙ **Opciones adicionales**
- **Usar SSH**: habilítalo si quieres realizar **respaldos**, ejecutar **comandos** o acceder a la **configuración** del equipo.
- **Usar SNMP**: habilítalo para recopilar **métricas**, **sensores**, **disponibilidad** y datos de red.

---

### 💾 **Guardar dispositivo**
Haz clic en **"Agregar dispositivo"** para registrarlo en el sistema.

💡 **Tip:** Una vez agregado, podrás visualizarlo en el **mapa LLDP** y acceder a sus métricas.

---

## 2️⃣ **Inserción masiva desde plantilla Excel**

### 📥 **Descargar plantilla**
Pulsa en **"Descargar Plantilla de Ejemplo"** para obtener el formato compatible.

### 📝 **Completar datos en Excel**
Llena la hoja con la información de tus dispositivos:  
Marca, nombre, IP, grupo, ubicación, etc.

### 📤 **Cargar archivo**
1. Selecciona tu archivo Excel con **"Examinar…"**.  
2. Pulsa **"Cargar Excel"** para importar **todos los dispositivos** a la vez.

💡 **Tip:** Ideal para **migraciones** o **implementaciones grandes**.

---

## 3️⃣ **Descubrimiento automático por SNMP**

### 🌐 **Rango CIDR**
Indica el rango de IP a escanear.  
Ejemplo: `192.168.1.0/24`.

### 🔑 **Comunidad SNMP**
Escribe la comunidad SNMP configurada en los equipos.  
Ejemplo: `public`.

### 📡 **Versión SNMP**
Selecciona la versión correspondiente *(v1, v2c o v3)* según la configuración de tus dispositivos.

### ⚡ **Escanear red**
Pulsa en **"Escanear red"** para que el sistema detecte y agregue automáticamente los dispositivos que respondan por SNMP.

💡 **Tip:** Perfecto para **detectar equipos** sin registrarlos manualmente.

---

## 🔍 **Visualización y gestión posterior**

Una vez agregados los dispositivos (por cualquier método), podrás:

- 🗺 **Visualizarlos automáticamente** en el **mapa LLDP**.
- 🎯 Usar **filtros** para mostrar solo dispositivos identificados o todos.
- 💾 Guardar tu **layout personalizado** (posiciones, zoom, nodos ocultos).
- ℹ Acceder a un **modal con detalles** (IP, SNMP, disponibilidad, enlace a estadísticas).
- 📊 Abrir un **panel de gráficas y métricas** con doble clic.
- 🔄 Cambiar el acomodo de la red a **jerárquico** o **radial**.

---
