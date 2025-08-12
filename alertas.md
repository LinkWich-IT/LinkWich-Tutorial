# 📡 **Monitoreo de Servicios y Alertas – LinkWich-Monitor**
El módulo de **Servicios y Alertas** te permite **vigilar puertos/hosts**, crear **reglas de notificación** (correo y/o WhatsApp) y **programar tareas** de verificación como **PING**.

---

## 1️⃣ **Registrar un Servicio a Monitorear**
En **`Servicios → Registrar Servicio`** completa:

- **Nombre:** etiqueta del servicio (ej. *Puerto 5000*).
- **Tipo:** elige **Puerto** (o el tipo disponible en tu instalación).
- **URL/IP:** dirección o IP del host (ej. `10.100.0.203`).
- **Protocolo:** **TCP** o **UDP** según el servicio.
- **Puerto:** número del puerto (ej. `5000`, `90`, `514`).
- *(Opcional)* **Generar alerta** → crea una regla automática para este chequeo.
- *(Opcional)* **Enviar correo** → notificará por email si hay falla.

Pulsa **Registrar**.

---

## 🧪 **Ejemplos útiles**
- `10.100.0.203 : TCP : 5000` → **Puerto TCP abierto**
- `10.100.0.6 : TCP : 90` → **Puerto TCP abierto**
- `10.100.0.203 : UDP : 514` → **Sin respuesta** *(posible filtro, pero no rechazado)*

---

## 2️⃣ **Servicios Monitoreados**
En la tabla **Servicios Monitoreados** verás:

- **Nombre / Tipo / URL-IP / Puerto**
- **Alerta** (estado) y **Correo** (si enviará email)
- **Estado** (Activo/Inactivo) y **Última verificación**
- **Protocolo** y **Detalle** del resultado
- **Acciones:** ✏️ **Editar** | 🗑 **Eliminar**

💡 **Tip:** Si activaste **Generar alerta**, el sistema creará la **regla asociada** para avisarte ante fallas.

---

## 3️⃣ **Reglas de Alerta (Resumen y Gestión)**
Ve a **`Alertas → Regla de alertas`** para revisar todas tus reglas:

- Columnas: **Dispositivo**, **Tipo** *(UPS/Servicio/Interfaz/RAM)*, **Detalle**, **Umbral/Severidad/Estado**, **Nivel** *(INFO/WARNING/CRITICAL)*, **Activo**, **Acciones**.
- Usa **Crear Nueva Regla** para añadir una desde cero.
- Botones: **azul** ✏️ para **editar**, **rojo** 🗑 para **eliminar**.

### 🧭 **Ejemplos típicos de reglas**
- **UPS** → `battery_charge < 80` con nivel **CRITICAL**.
- **Servicio** → proceso `CHO.Next.Management.RUA.exe`.
- **Interfaz** → `port5 != 2-NORMAL` *(administrativamente/operacionalmente arriba)*.
- **Almacenamiento/RAM** → `Physical memory > 10` *(umbral informativo/aviso)*.

---

## 4️⃣ **Crear Alerta SNMP (por Tipo/Umbral)**
En **`Alertas → Configuración de tipos de alertas por SNMP`**:

1. **Dispositivo:** selecciona el equipo.  
2. **Tipo de Alerta:**  
   - **Almacenamiento / RAM**  
   - **Interfaz**  
   - **Servicio**  
   - **UPS**  
3. **Nombre del Objetivo:** ej. `battery_charge`, `port5`, `CHO.Next.Proxy…`  
4. **Tipo de Severidad:** **Info / Warning / Critical**.  
5. *(Opcional)* **Enviar notificación por correo**.  
6. *(Opcional)* **Enviar notificación por WhatsApp** *(requiere WhatsApp configurado)*.  
7. Pulsa **Crear Regla**.

### 📌 **Sugerencias de umbral**
- **UPS** → `battery_temp_c > 28` (**CRITICAL**)  
- **UPS** → `battery_charge < 95` (**CRITICAL**)  
- **Interfaz** → estado distinto a **2-NORMAL** (**CRITICAL**)  
- **RAM** → `Physical memory > 10` (**WARNING/INFO** según tu política)

---

## 5️⃣ **Programar Tareas de Verificación (PING, etc.)**
En **`Alertas → Lista de reglas de Alerta`** *(sección **Programar Nueva Tarea**)*:

1. **Dispositivo:** equipo origen del chequeo.  
2. **Tipo:** selecciona **PING**.  
3. **Destino:** host o dominio (ej. `google.com`).  
4. **Intervalo (segundos):** ej. `300`.  
5. **Guardar**.

Se mostrará en **Tareas Activas** con opciones: **Activar / Desactivar / Detener / Eliminar**.  
Abajo verás los **Resultados** *(latencia, pérdida de paquetes, etc.)*.

💡 **Recomendación:** para monitoreo **24/7**, usa **300–600s** de intervalo y activa el **envío por correo** si necesitas evidencias históricas.

---

## 6️⃣ **Buenas Prácticas**
- **Nombra** claramente tus servicios y reglas (ej. *FW: Port 5000 Admin*).  
- Evita **falsos positivos**: elige bien **protocolo** y **puerto** (TCP vs UDP).  
- **Centraliza alertas**: usa reglas **CRITICAL** solo para incidentes reales.  
- Usa **correo/WhatsApp** con moderación para no saturar a tu equipo.  
- **Revisa periódicamente** los resultados y ajusta umbrales según la operación.

---

## 7️⃣ **Checklist rápido**
- [ ] Servicio creado con **IP/host**, **protocolo** y **puerto** correctos.  
- [ ] **Generar alerta** activado *(si aplica)*.  
- [ ] **Regla** de **SNMP/Servicio** con **umbral** y **nivel** adecuados.  
- [ ] **Correo** y/o **WhatsApp** configurados *(si deseas notificaciones)*.  
- [ ] **Tarea PING** programada con **intervalo** razonable.  
- [ ] Validada la **Última Verificación** y el **Detalle** del resultado.

---
