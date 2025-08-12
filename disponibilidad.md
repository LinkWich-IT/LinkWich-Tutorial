# 📊 **Manual de Métricas de Disponibilidad – LinkWich-Monitor**

El módulo de **Métricas de Disponibilidad** te permite visualizar el **tiempo de actividad**, **latencia** y **pérdida de paquetes** de los dispositivos monitoreados.  
Es clave para el **diagnóstico** y el **seguimiento del rendimiento** de la red.

---

## 1️⃣ **Acceder a las Métricas de Disponibilidad**

1. Desde el **menú lateral**, entra a **`Métricas → Disponibilidad`**.
2. Verás la **lista de dispositivos monitoreados** con columnas de:
   - **Nombre**
   - **IP**
   - **Disponibilidad (%)**
   - **Prom. de respuesta (ms)**
   - **Pico de respuesta (ms)**
   - **Fecha del pico**
   - **Acción** (**Detalles**)

💡 **Tip:** Usa **Buscar** (por nombre o IP), **Rango** (**Hoy, Semana, Mes, Año, Todo**) y **Elementos/página** para ajustar tu vista.

---

## 2️⃣ **Lista de dispositivos monitoreados (vista general)**

- **Rango:** elige el período a analizar (**Hoy / Semana / Mes / Año / Todo**).  
- **Disponibilidad (%):** porcentaje de tiempo que el equipo estuvo **en línea** en el rango elegido.  
- **Prom. Resp. (ms):** promedio de **latencia** medida.  
- **Pico Resp. (ms):** **máxima latencia** registrada y su **fecha/hora**.  
- **Detalles:** abre la **vista individual** del dispositivo.

---

## 3️⃣ **Detalle de un dispositivo (vista individual)**

### 🧾 **Información general**
- **Nombre, IP, Ubicación, Grupo y Estado** *(En línea / Fuera de línea)*.

### 🧭 **Indicadores principales**
- **Tiempo medio de respuesta (ms):** latencia promedio en el rango.  
- **Pérdida media de paquetes (%):** porcentaje de paquetes no entregados.

### 🔎 **Filtros por fecha**
- Usa **Desde / Hasta** para un rango **personalizado** y pulsa **Filtrar**.

### 📈 **Gráfica de disponibilidad**
- **Línea azul:** **Tiempo de respuesta**.  
- **Línea verde:** **Pérdida de paquetes**.  
- Permite localizar **picos** de latencia o **eventos** de pérdida.

### 📋 **Tabla de eventos**
- Registra **Fecha/Hora**, **Tiempo Resp. (ms)** y **Pérdida Paq. (%)** para análisis fino.

---

## 4️⃣ **Vista comparativa por dispositivo (gráfica global)**

- Filtra por **Mes** y **Año** *(y Día, opcional)* y pulsa **Consultar**.  
- La gráfica **“Disponibilidad por Dispositivo”** compara el **% de uptime** de **todos** los equipos.  
- **Barras azules** → alta disponibilidad. **Segmentos rojos** → caídas.

💡 **Tip:** Útil para **auditorías**, **SLA** y **reportes mensuales**.

---

## 5️⃣ **Interpretación rápida de métricas**

- **Disponibilidad (%)**
  - `100%` → sin interrupciones en el período.
  - `< 100%` → hubo caídas o pérdida de conectividad.
- **Prom. Resp. (ms)**
  - **Bajo** → red estable/rápida.
  - **Alto** → congestión, saturación o problemas de ruta.
- **Pérdida de paquetes (%)**
  - `0%` → comunicación óptima.
  - `> 0%` → revisar enlaces, colas, errores físicos o QoS.

---

## 6️⃣ **Casos de uso recomendados**

- **Incidentes en curso:** filtra por **Hoy** y revisa **picos** y **tabla** para correlación.  
- **Tendencias semanales:** usa **Semana** y compara **Prom. Resp.** vs **Fecha Pico**.  
- **SLA mensual:** usa **Mes** y la **gráfica comparativa** para detectar outliers.  
- **Capacidad:** observa equipos con **Prom. Resp.** creciente para planear upgrades.

---

## 7️⃣ **Buenas prácticas de monitoreo**

- Revisa **semanalmente** equipos con **pérdida > 0%** o **picos** fuera de lo normal.  
- Mantén **alertas** configuradas para latencia y pérdida de paquetes.  
- Documenta **patrones repetitivos** (días/horas) para encontrar **causas raíz**.  
- Cruza datos con **Syslog** y **Mapa de Dispositivos** para un diagnóstico completo.

---
