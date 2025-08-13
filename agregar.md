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

1️⃣ Descargar la plantilla
Haz clic en “Descargar Plantilla de Ejemplo”.

Se guarda como Excel (.xlsx) con las columnas requeridas.

2️⃣ Completar datos en Excel
Llena cada fila con un dispositivo. Respeta nombres de columnas y formatos.

📑 Campos de la plantilla
Columna	¿Requerido?	Formato / Valores válidos	Ejemplo	Notas
marca	Sí	Valor del controlador (ver catálogo más abajo)	allied_telesis_awplus	Debe coincidir exactamente con los valores de marca soportados.
nombre	Sí	Texto (1–80)	SW-NOMBRE 1	Nombre único descriptivo.
ip	Sí	IPv4 en formato A.B.C.D	10.200.0.1	No repitas IP.
status	No	Online / Offline (o deja el valor del ejemplo)	Offline	El sistema actualizará el estado real automáticamente.
usuario	Sí	Texto (usuario de SSH/Telnet)	admin	Para respaldos, comandos y consultas.
password	Sí	Texto (contraseña del usuario anterior)	admin#	Evita caracteres no imprimibles.
ubicacion	No	Texto libre	Cuarto Telecom	Dónde se encuentra físicamente.
grupo_id	Sí	Número entero	26	ID del grupo en tu sistema (Gestión → Grupos).
snmp_version	Sí	1 / 2c / 3	2c	Usa 2c salvo que tengas SNMPv3 configurado.
snmp_community	Sí	Texto (para SNMPv1/v2c)	public	Para v3, deja community y configura credenciales v3 después (si aplica).
snmp	Sí	SI / NO	SI	Si el equipo será consultado por SNMP.
recibe_alertas	Sí	1 (sí) / 0 (no)	1	Si el dispositivo participa en reglas/alertas.
latitud	No	Decimal en formato decimal punto	25.6866	Útil para mapas. Deja NULL si no aplica.
longitud	No	Decimal en formato decimal punto	-100.3161	Útil para mapas. Deja NULL si no aplica.

🔎 Dónde ver el grupo_id: entra a Gestión → Grupos y revisa la columna ID del grupo que usarás.

3️⃣ Catálogo de marcas (controladores)
Usa exactamente estos valores en la columna marca del Excel:

Valor en Excel (marca)	Dispositivo / Familia
allied_telesis_awplus	Allied Telesis
cisco_ios	Cisco IOS
aruba_procurve	Aruba / HP ProCurve
aruba_os	Aruba Series 6100
fortinet	Fortinet Switch
generic	Genérico / Planet
windows	Windows (servidor/host)
ruckus_fastiron	Ruckus ICX
ruijie_os	Ruijie
sophos_sfos	Sophos (dispositivos compatibles)
tplink_jetstream	TP-Link JetStream
mikrotik_routeros	MikroTik RouterOS
mikrotik_switchos	MikroTik SwOS
ubiquiti_edge	Ubiquiti Edge
ubiquiti_edgerouter	Ubiquiti EdgeRouter
ubiquiti_edgeswitch	Ubiquiti EdgeSwitch
ubiquiti_unifiswitch	Ubiquiti UniFi Switch
huawei	Huawei
ups	CyberPower-UPS

⚠️ Importante: escribe el valor exacto en minúsculas, sin espacios.
Si tu equipo no está en la lista, usa generic como fallback (funcionalidad básica).

4️⃣ Ejemplo de filas válidas
csv
Copiar
Editar
marca,nombre,ip,status,usuario,password,ubicacion,grupo_id,snmp_version,snmp_community,snmp,recibe_alertas,latitud,longitud
allied_telesis_awplus,SW-NOMBRE 1,10.200.0.1,Offline,admin,admin#,ubicación,26,2c,public,SI,1,NULL,NULL
ruckus_fastiron,SW-NOMBRE 3,10.200.0.3,Offline,admin,admin#,ubicación,26,2c,public,SI,1,NULL,NULL
fortinet,SW-NOMBRE 4,10.200.0.4,Offline,admin,admin#,ubicación,26,2c,public,NO,1,NULL,NULL
tplink_jetstream,SW-NOMBRE 10,10.200.0.10,Offline,admin,admin#,ubicación,26,2c,public,NO,1,NULL,NULL
5️⃣ Subir el Excel
En la pantalla de carga, pulsa “Examinar…” y elige tu archivo.

Haz clic en “Cargar Excel”.

Revisa el resultado: el sistema confirmará los equipos creados o te indicará errores por fila.

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
