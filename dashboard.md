📘 Manual de Usuario – Dashboard de LinkWich-Monitor
El Dashboard es el centro de control de tu sistema. Aquí puedes monitorear en tiempo real el estado de la red, servicios, alertas y métricas clave.

1️⃣ Organización del Dashboard
Tarjetas movibles:
Todas las tarjetas (widgets) del dashboard son arrastrables y reubicables para que las acomodes según tus preferencias o el tamaño de tu monitor.

Esto es ideal si vas a usar el dashboard en una pantalla de monitoreo tipo NOC.

El acomodo se guarda por usuario, así cada persona puede tener su propio diseño.

2️⃣ Componentes principales
📍 Dispositivos Críticos
Muestra los equipos más importantes definidos en el sistema.

El color indica estado:

🟢 Activo

🔴 Inactivo

🟡 Estado desconocido o alerta

Haz clic en un equipo para acceder a sus detalles.

📍 Dispositivos Inactivos
Lista en tiempo real los equipos que han perdido conexión.

Incluye fecha, hora, nombre, IP y estado.

Ideal para detectar caídas recientes y actuar rápidamente.

📍 Alertas Actuales
Agrupa alertas por severidad:

Azul: Informativo

Amarillo: Warning

Rojo: Crítico

Cada alerta incluye el dispositivo afectado, descripción y fecha/hora.

Botón "Marcar alertas como resueltas": Úsalo una vez que hayas confirmado que el incidente fue solucionado para mantener el panel limpio.

📍 Métricas SNMP
Top 10 de interfaces más usadas:

Barras naranjas → tráfico entrante (Mbps)

Barras moradas → tráfico saliente (Mbps)

Ayuda a detectar saturaciones y comportamientos anómalos.

📍 Syslog
Gráfica circular con la distribución de mensajes por severidad.

Ranking de las 3 IPs con más logs en la semana.

Útil para identificar equipos que generan más eventos.

📍 Mapa de Dispositivos
Ubicación geográfica de todos los equipos registrados.

Integración con lista lateral por grupos.

Posibilidad de ocultar/mostrar el mapa.

📍 Disponibilidad y Estado de Interfaces
Gráficos de barras y pastel con:

Porcentaje de equipos conectados/desconectados.

Estado de interfaces monitorizadas por SNMP.

📍 Backups Windows
Resumen de tareas de respaldo en las últimas 24h.

Muestra cantidad de backups correctos y con error.

Lista los últimos respaldos con fecha, servidor, destino y estado.

📍 Dispositivos por Marca
Gráfica de distribución de marcas en la infraestructura.

Útil para inventario rápido y control de diversidad tecnológica.

3️⃣ Uso como panel NOC
Configura el dashboard en una pantalla grande para monitoreo continuo.

Ajusta el acomodo de tarjetas para mostrar las métricas más críticas en la parte visible.

Mantén la sección de Dispositivos Inactivos y Alertas siempre a la vista.

Habilita la opción de auto-refresco (si está disponible en tu configuración) para que los datos se actualicen automáticamente.

4️⃣ Limpieza de alertas
Una vez que el problema haya sido validado y solucionado:

Haz clic en "Marcar alertas como resueltas".

Esto ayuda a mantener el panel libre de incidentes antiguos y enfocado en problemas actuales.

Las alertas resueltas quedan registradas en el historial para auditoría.
