# 📄 **Gestión de Syslog – LinkWich-Monitor**

El módulo **Syslog** permite centralizar, visualizar, filtrar y gestionar mensajes de log enviados por los dispositivos de red.  
Además, puedes configurar reglas para generar alertas automáticas y definir qué niveles de severidad se aceptan.

---

## 1️⃣ **Panel de Visión General**

En **Syslog → Logs por dispositivos** verás un resumen de mensajes recibidos, clasificados por severidad:

- 🚨 **Critical** – Eventos críticos del sistema.
- ❌ **Error** – Errores detectados en el dispositivo.
- ⚠️ **Warning** – Advertencias importantes.
- ℹ️ **Notice** – Notificaciones generales.
- 🔍 **Info** – Información adicional.
- 🐞 **Debug** – Mensajes de depuración.

Debajo, se muestra la tabla **Dispositivos que han enviado mensajes de Syslog** con:

- **IP** y **Nombre** del dispositivo.
- **Marca** y **Ubicación**.
- **Total de logs** recibidos.
- **Acciones** (ver detalles).
- Estado **¿Registrado?** (Sí / No).

---

## 2️⃣ **Base de Datos Syslog**

En **Syslog → Base de Datos**, puedes buscar y filtrar mensajes con:

- **Fecha/hora inicio y fin**.
- **IP de origen**.
- **Palabra clave** (ej. *error link-down*).
- **Severidad**.

La tabla mostrará:

- **ID**, fecha, switch, IP origen.
- Nivel de **severidad**.
- Contenido del **mensaje**.
- Botones de **Explicar con IA** y **Crear Alerta**.

---

## 3️⃣ **Crear y Gestionar Reglas Syslog**

En **Syslog → Reglas**:

1. Selecciona el **Dispositivo**.
2. Ingresa **Palabra Clave** para filtrar.
3. Define **IP(s) de origen** (puedes incluir o excluir).  
   - **Ejemplo inclusión:** `192.168.1.10` (solo se aceptan logs de esta IP).  
   - **Ejemplo exclusión:** `!192.168.1.10` (se ignoran logs de esta IP).  
   - **Ejemplo múltiple:** `192.168.1.10,192.168.1.11,!192.168.1.100` (incluye las dos primeras y excluye la última).
4. Escoge **Severidad** y **Nivel de Alerta**.
5. Activa o desactiva el envío de **Correo** o **WhatsApp**.
6. Guarda con **Crear Regla**.

En la parte inferior verás las **Reglas Existentes** con opciones para **editar** ✏️ o **eliminar** 🗑.

---

## 4️⃣ **Configuración de Permisos por Dispositivo**

En **Syslog → Permisos**, define qué niveles de severidad acepta cada equipo:

- **Emergency** 🚨
- **Alert** 🔔
- **Critical** ❌
- **Error** 🛑
- **Warning** ⚠️
- **Notice** ℹ️
- **Info** 🔍
- **Debug** 🐞

💡 **Recomendación:** Solo habilitar niveles críticos (Emergency, Alert, Error) en equipos sensibles para evitar sobrecarga de logs.

Pulsa **Guardar configuración** para aplicar los cambios.

---

## 5️⃣ **Eliminar Logs**

En **Syslog → Eliminar**, puedes borrar registros por:

- **Todos los registros**.
- **Filtrar por IP de Origen**.

⚠️ Esta acción es irreversible.

---

## 💡 Buenas Prácticas

- Revisa periódicamente los **logs críticos y de error**.
- Crea **reglas** para notificar por correo o WhatsApp eventos importantes.
- Usa **palabras clave** específicas para reducir falsos positivos.
- Respalda la base de datos de logs si necesitas histórico para auditorías.
- Configura permisos para evitar saturación por mensajes innecesarios.

---
