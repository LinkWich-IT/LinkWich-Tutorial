# 📘 **Manual de Usuario – Dashboard de LinkWich-Monitor**

El **Dashboard** es el **centro de control** de tu sistema.  
Aquí puedes **monitorear en tiempo real** el estado de la red, servicios, alertas y métricas clave.

---

## 1️⃣ **Organización del Dashboard**

### 🖱 **Tarjetas movibles**
- Todas las tarjetas (**widgets**) del dashboard son **arrastrables y reubicables**.
- Puedes acomodarlas según tus preferencias o el tamaño de tu monitor.
- Ideal para usar el dashboard en una **pantalla de monitoreo tipo NOC**.
- El acomodo **se guarda por usuario**, permitiendo que cada persona tenga su propio diseño.

---

## 2️⃣ **Componentes principales**

### 📍 **Dispositivos Críticos**
- Muestra los **equipos más importantes** definidos en el sistema.
- Colores de estado:
  - 🟢 **Activo**
  - 🔴 **Inactivo**
  - 🟡 **Estado desconocido o con alerta**
- Haz clic en un equipo para acceder a sus **detalles**.

---

### 📍 **Dispositivos Inactivos**
- Lista **en tiempo real** de equipos que han perdido conexión.
- Incluye **fecha, hora, nombre, IP y estado**.
- Ideal para detectar **caídas recientes** y actuar rápidamente.

---

### 📍 **Alertas Actuales**
- Agrupa alertas por severidad:
  - 🔵 **Informativo**
  - 🟡 **Warning**
  - 🔴 **Crítico**
- Cada alerta incluye:
  - **Dispositivo afectado**
  - **Descripción**
  - **Fecha y hora**
- Botón **"Marcar alertas como resueltas"** → Úsalo una vez confirmada la solución para mantener el panel limpio.

---

### 📍 **Métricas SNMP**
- **Top 10 de interfaces más usadas**:
  - 🟧 Barras naranjas → **Tráfico entrante (Mbps)**
  - 🟪 Barras moradas → **Tráfico saliente (Mbps)**
- Útil para detectar **saturaciones** o **comportamientos anómalos**.

---

### 📍 **Syslog**
- Gráfica **circular** con la distribución de mensajes por severidad.
- Ranking de las **3 IPs con más logs** en la semana.
- Ayuda a identificar **equipos con más eventos**.

---

### 📍 **Mapa de Dispositivos**
- Muestra la **ubicación geográfica** de todos los equipos registrados.
- Lista lateral por **grupos de dispositivos**.
- Posibilidad de **ocultar o mostrar** el mapa.

---

### 📍 **Disponibilidad y Estado de Interfaces**
- Gráficos de **barras** y **pastel** que muestran:
  - Porcentaje de equipos **conectados/desconectados**.
  - Estado de **interfaces SNMP**.

---

### 📍 **Backups Windows**
- Resumen de tareas de respaldo de las últimas **24 horas**.
- Indica:
  - ✅ **Cantidad de backups correctos**
  - ❌ **Cantidad de backups con error**
- Lista con **fecha, servidor, destino y estado**.

---

### 📍 **Dispositivos por Marca**
- Gráfica que muestra la **distribución de marcas** en la infraestructura.
- Útil para **inventario rápido** y control de **diversidad tecnológica**.

---

## 3️⃣ **Uso como panel NOC**
- Configura el dashboard en una **pantalla grande** para monitoreo continuo.
- Ajusta el acomodo de tarjetas para mostrar siempre **métricas críticas**.
- Mantén **Dispositivos Inactivos** y **Alertas** siempre visibles.
- Habilita **auto-refresco** (si está disponible) para datos actualizados sin intervención manual.

---

## 4️⃣ **Limpieza de alertas**
- Una vez validada la solución de un problema:
  - Pulsa **"Marcar alertas como resueltas"**.
- Mantiene el panel libre de **alertas antiguas** y enfocado en incidentes actuales.
- Las alertas resueltas se guardan en el **historial** para auditoría.

---
