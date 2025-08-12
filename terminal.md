## 📡 **Gestión de Dispositivos – LinkWich-Monitor**
El módulo **Gestión de Dispositivos** permite el control avanzado de **switches** en la red, mostrando información de **configuración**, **estado** y permitiendo ejecutar **comandos remotos**.

> ⚠️ **Importante:** Asegúrate de que el **puerto 5002** esté abierto en el firewall y que el servidor sea accesible en:
- https://IP:5002/terminal/10.100.0.23?name=SW-NAME


---

## 1️⃣ **Acceder al Panel de Dispositivos**
En **Gestión de Datos → Gestión de Dispositivos** podrás:
- 📋 Ver el listado de **switches** con **IP**, **Nombre**, **Ubicación**, **Marca**, **Estado** y **Grupo**.
- ⚡ Acceder a herramientas rápidas: **Ver Interfaces**, **Info Sys**, **SSH** y **Web UI**.

---

## 2️⃣ **Conexión SSH al Dispositivo**
- 🔑 Haz clic en el botón **SSH** del equipo deseado.  
- 📝 Aparecerá una ventana solicitando **usuario** y **contraseña**.  
- ✅ Ingresa las credenciales y presiona **Conectar**.  
- 🌐 Si el **puerto 5002** está abierto y el equipo es alcanzable, se establecerá la **sesión remota** para administración.

---

## 3️⃣ **Visualización de Interfaces**
Una vez conectado por **SSH**, ejecuta:

- show interfaces status

Verás:
- 📶 **Estado** de cada puerto (*Conectado, Apagado, Desconectado*).
- 🏷 **VLAN** asignada.
- ⚡ **Velocidad** y **Dúplex**.
- 🔌 **Tipo** de interfaz.

---

## 4️⃣ **Herramientas de Gestión en Detalles del Switch**
En **Detalles del Switch** puedes usar:
- 🛠 **Ver Config (Manual):** Introduce un puerto o rango (ej. `port1.0.1, 1`) para ver su configuración.  
- 📡 **Test TDR (Manual):** Diagnóstico físico del puerto *(puede causar microcortes)*.  
- 🔍 **Buscar MAC (Manual):** Localiza direcciones MAC (formato `aaaa.bbbb.cccc`).  
- 🌍 **LLDP (Manual):** Descubre dispositivos vecinos conectados.  
- 💻 **Ejecutar Comando:** Ejemplos: `show version`, `show vlan brief`.

---

## 5️⃣ **Estado de Puertos**
La tabla **Estado de Puertos** muestra:
- 🔢 **Puerto** y **Nombre** asignado.  
- 🟢 **Conectado**, 🟡 **Apagado**, 🔴 **Desconectado**.  
- 🏷 **VLAN**, ⚡ **Dúplex**, 📊 **Velocidad** y **Tipo**.  
- ⚡ **Acciones rápidas:** **Config**, **TDR**, **MAC**, **LLDP**.

---

## 6️⃣ **Recomendaciones de Uso**
- ✅ Verifica que el **puerto 5002** esté accesible para conexiones remotas.  
- 🔍 Usa **Ver Interfaces** para diagnósticos rápidos.  
- 🕒 Ejecuta **Test TDR** fuera de horarios críticos.  
- 🗒 Mantén un **registro de cambios** para auditoría.

---
