# 📡 **Diagrama de Red Automático (Mapa LLDP)**

El módulo **Mapa de Red LLDP** te permite visualizar de manera **automática** la topología de tu red detectada mediante el protocolo **LLDP (Link Layer Discovery Protocol)**.  
Esta función es ideal para identificar conexiones físicas entre dispositivos y conocer el estado de uso de cada enlace en tiempo real.

---

## 🎯 **Objetivo**
Proporcionar una vista gráfica e interactiva de la red que te permita:
- **Identificar** rápidamente la ubicación y conexiones de cada dispositivo.
- **Visualizar** el uso de ancho de banda en enlaces críticos.
- **Detectar** problemas como bucles físicos o saturación de interfaces.

---

## 🖥️ **Vista General del Módulo**
En la parte superior encontrarás un panel de **filtros y controles** que te permiten ajustar la vista del mapa según tus necesidades.

### 🔍 **Filtros Disponibles**
- **Buscar nodo** 🔎: Ingresa **IP, nombre o ubicación** del dispositivo para centrar la vista en él.
- **Excluir grupo** 🚫: Oculta dispositivos pertenecientes a un grupo específico.
- **Incluir grupo** 📂: Filtra para mostrar solo los dispositivos de un grupo.
- **Mostrar VLAN en mapa** 🏷️: Resalta los nodos y enlaces asociados a una VLAN específica.
- **Tipo de topología** 🌐:
  - **Libre (auto)**: Organización automática del mapa.
  - **Jerárquico**: Disposición por niveles (core, distribución, acceso).
  - **Estrella**: Todos los nodos conectados visualmente a un centro.

---

## 🎨 **Simbología de Colores**
Cada color representa un estado o condición del enlace:
- 🔵 **Azul**: Dispositivo sin match para cálculo de uso de datos.
- 🟢 **Verde**: Match realizado, cálculo de uso actual disponible.
- 🟡 **Amarillo**: Uso moderado de datos.
- 🔴 **Rojo**: Uso excesivo o al límite de capacidad de la interfaz.
- 🟠 **Anaranjado**: Posible loop físico detectado.
- 🟣 **Morado**: VLAN seleccionada resaltada.

---

## ⚙️ **Controles Rápidos**
- **Mostrar/Ocultar Dispositivos** 👁️: Alterna visibilidad de nodos.
- **Guardar** 💾: Guarda posiciones y visibilidad de los nodos.
- **Desbloquear** 🔓: Permite mover libremente los nodos.
- **Bloquear** 🔒: Fija los nodos en su posición.
- **Cambiar icono** 🖼️: Personaliza el icono de un dispositivo.
- **Resetear contadores** 🔄: Reinicia métricas de uso en los enlaces.
- **Pantalla completa** 🖥️: Expande el mapa para mayor visibilidad.

---

## 📊 **Visualización Interactiva**
- **Líneas y flechas** indican la dirección de la conexión detectada vía LLDP.
- **Tooltips** al pasar el cursor muestran:
  - Puerto local y puerto remoto.
  - Uso porcentual del enlace.
  - Tráfico actual (en Mbps).
  - Capacidad total del enlace.

---

## 🚀 **Buenas Prácticas**
- Guarda los cambios de posiciones **después** de organizar el mapa.
- Utiliza el modo **jerárquico** para redes con múltiples capas de switches.
- Resalta VLANs críticas para detectar enlaces no deseados.

---

📌 **Nota:** El mapa LLDP se actualiza automáticamente según la información SNMP recopilada en cada ciclo de sondeo.  
Para obtener la información más reciente, asegúrate de que los dispositivos tengan **LLDP habilitado** y accesible por SNMP.

---
