# 📄 **Gestión de Syslog – LinkWich-Monitor**

El módulo **Syslog** permite **centralizar, visualizar, filtrar y gestionar** mensajes de log enviados por tus dispositivos de red.  
Además, puedes configurar **reglas** para generar alertas automáticas y definir **qué niveles de severidad** se aceptan por dispositivo.

---

## ✅ Requisitos previos (importante)

Antes de configurar dispositivos, define lo siguiente:

- **IP del servidor Syslog (LinkWich-Monitor):** `\<SYSLOG_SERVER_IP\>`
- **Puerto Syslog:** normalmente **UDP/514** (si tu instalación usa otro puerto, usa ese).
- **Firewall / red:**
  - Permitir desde los dispositivos hacia LinkWich-Monitor:
    - **UDP/514** (Syslog) ✅ recomendado
    - *(Opcional)* **TCP/514** si tu dispositivo/escenario lo requiere
- **Hora/fecha (recomendado):**
  - Habilita **NTP** en tus equipos para que los logs tengan timestamps confiables.

---

## 1️⃣ **Panel de Visión General**

En **Syslog → Logs por dispositivos** verás un resumen de mensajes recibidos, clasificados por severidad:

- 🚨 **Emergency / Alert** – Eventos críticos inmediatos (si aplica).
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
- **Palabra clave** (ej. `error`, `link-down`, `STP`, `authentication failed`).
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

💡 **Recomendación:** En equipos sensibles o con muchos mensajes, habilita solo niveles críticos (Emergency/Alert/Critical/Error) para evitar sobrecarga.

Pulsa **Guardar configuración** para aplicar los cambios.

---

## 5️⃣ **Eliminar Logs**

En **Syslog → Eliminar**, puedes borrar registros por:

- **Todos los registros**.
- **Filtrar por IP de Origen**.

⚠️ Esta acción es irreversible.

---

## 6️⃣ **Cómo activar Syslog por marca (paso a paso)**

> En todos los ejemplos reemplaza:
- `\<SYSLOG_SERVER_IP\>` por la IP del servidor donde corre LinkWich-Monitor
- `\<SYSLOG_PORT\>` por el puerto (si usas el estándar, es `514`)
- Si tu red tiene VLANs/ACL, valida que el dispositivo **sí pueda llegar** a la IP del servidor por **UDP/514**

---

### 🟩 Allied Telesis (AlliedWare Plus / AW+)

#### A) Configuración básica (1 servidor)
```plaintext
enable
configure terminal
 log host <SYSLOG_SERVER_IP>
 log host <SYSLOG_SERVER_IP> level notices
 log host <SYSLOG_SERVER_IP> level warnings
 log host <SYSLOG_SERVER_IP> level errors
 log host <SYSLOG_SERVER_IP> level critical
 log host <SYSLOG_SERVER_IP> level emergencies
exit
write
```

#### B) Ejemplo completo (2 servidores + exclusión por texto)
> Útil cuando quieres enviar logs a dos destinos y excluir mensajes repetitivos.
```plaintext
enable
configure terminal
 log host 10.100.0.202
 log host 10.100.0.202 level notices
 log host 10.100.0.202 level warnings
 log host 10.100.0.202 level errors
 log host 10.100.0.202 level critical
 log host 10.100.0.202 level emergencies
 log host 10.100.0.202 exclude msgtext MLD-EVENTS

 log host 10.100.0.203
 log host 10.100.0.203 level notices
 log host 10.100.0.203 level warnings
 log host 10.100.0.203 level errors
 log host 10.100.0.203 level critical
 log host 10.100.0.203 level emergencies
 log host 10.100.0.203 exclude msgtext MLD-EVENTS
exit
write
```

✅ **Verificación**
```plaintext
show log config
show log
```

---

### 🟦 Cisco IOS / IOS-XE (Switch/Router)

#### 1) Configurar servidor Syslog + severidad
```plaintext
enable
configure terminal
 service timestamps log datetime msec localtime show-timezone
 logging host <SYSLOG_SERVER_IP>
 logging trap warnings
 logging origin-id hostname
end
write memory
```

> `logging trap warnings` envía **warnings y más críticos** (warning, error, critical, alert, emergency).  
> Si deseas más detalle, usa `logging trap informational` (más mensajes).

#### 2) (Opcional) Forzar la interfaz origen (recomendado en redes con múltiples rutas)
```plaintext
configure terminal
 logging source-interface VlanX
end
write memory
```

✅ **Verificación**
```plaintext
show logging
show running-config | include logging
```

---

### 🟨 ArubaOS-Switch / HPE ProCurve (AOS-S)

#### 1) Agregar servidor Syslog
```plaintext
configure terminal
 logging <SYSLOG_SERVER_IP>
```

#### 2) Definir severidad (ejemplo: warning y más críticos)
```plaintext
 logging severity warning
```

#### 3) Guardar cambios
```plaintext
write memory
```

✅ **Verificación**
```plaintext
show debug
show running-config | include logging
```

---

### 🟧 Aruba AOS-CX (CX 6xxx/8xxx/9xxx/10xxx)

#### 1) Configurar Syslog hacia LinkWich-Monitor (UDP/514 por defecto)
```plaintext
configure terminal
 logging <SYSLOG_SERVER_IP> udp 514 severity warning
end
write memory
```

> Puedes ajustar severidad: `info`, `notice`, `warning`, `err`, `crit`, `alert`, `emerg`, `debug`.

#### 2) (Opcional) Usar VRF de management (si aplica)
```plaintext
configure terminal
 logging <SYSLOG_SERVER_IP> udp 514 severity warning vrf mgmt
end
write memory
```

✅ **Verificación**
```plaintext
show running-config | include logging
show logging
```

---

### 🟥 Ruckus ICX (FastIron)

#### 1) Asegurar Syslog habilitado y agregar servidor
```plaintext
enable
configure terminal
 logging on
 logging host <SYSLOG_SERVER_IP>
end
write memory
```

#### 2) Ajustar el “nivel” (si quieres reducir ruido)
En FastIron, una forma común de controlar nivel es **deshabilitando** los niveles que no deseas en el buffer (y eso afecta el envío al servidor).  
Ejemplo: dejar **notifications y superiores** (deshabilita informational + debugging):
```plaintext
configure terminal
 no logging buffered debugging
 no logging buffered informational
end
write memory
```

#### 3) (Opcional) Cambiar facility
```plaintext
configure terminal
 logging facility local0
end
write memory
```

✅ **Verificación**
```plaintext
show logging
show running-config | include logging
```

---

### 🪟 Windows (Windows Server / Windows 10 / Windows 11)

Windows **no envía Syslog nativamente** desde el Event Viewer. Para enviar eventos de Windows a LinkWich-Monitor como Syslog, se usa un **agente**.  
Recomendación común: **NXLog Community Edition**.

> Descarga (ejemplo): `https://nxlog.co/products/nxlog-community-edition`

#### A) Instalar NXLog (paso a paso)
1. Descarga e instala **NXLog Community Edition** en el equipo Windows.
2. Abre el archivo de configuración:
   - Ruta típica: `C:\Program Files\nxlog\conf\nxlog.conf`
3. Edita `nxlog.conf` con un ejemplo como este (envío por TCP/514 o UDP/514).

#### B) Ejemplo de configuración (Windows Event Log → Syslog)
> Este ejemplo lee eventos de Windows y los envía al servidor Syslog.

**Opción 1: TCP/514 (más confiable que UDP)**
```conf
<Extension _syslog>
    Module  xm_syslog
</Extension>

<Input eventlog>
    Module  im_msvistalog
</Input>

<Output out>
    Module  om_tcp
    Host    <SYSLOG_SERVER_IP>
    Port    514
    Exec    to_syslog_bsd();
</Output>

<Route r>
    Path    eventlog => out
</Route>
```

**Opción 2: UDP/514 (syslog clásico)**
```conf
<Extension _syslog>
    Module  xm_syslog
</Extension>

<Input eventlog>
    Module  im_msvistalog
</Input>

<Output out>
    Module  om_udp
    Host    <SYSLOG_SERVER_IP>
    Port    514
    Exec    to_syslog_bsd();
</Output>

<Route r>
    Path    eventlog => out
</Route>
```

#### C) Reiniciar servicio NXLog
En PowerShell como Administrador:
```powershell
Restart-Service nxlog
Get-Service nxlog
```

#### D) Firewall (Windows)
Asegura salida desde Windows al servidor:
- **TCP/514** si usas TCP
- **UDP/514** si usas UDP

Ejemplo (salida UDP/514):
```powershell
New-NetFirewallRule -DisplayName "SYSLOG Out UDP 514" -Direction Outbound -Protocol UDP -RemotePort 514 -Action Allow -Profile Any -ErrorAction SilentlyContinue | Out-Null
```

✅ **Verificación**
- Genera un evento (ej. iniciar sesión / apagar servicio) y revisa si aparece en **Syslog → Base de Datos** en LinkWich-Monitor.

---

## 💡 Buenas Prácticas

- Revisa periódicamente los **logs críticos y de error**.
- Crea **reglas** para notificar por correo o WhatsApp eventos importantes.
- Usa **palabras clave** específicas para reducir falsos positivos.
- Restringe severidades por equipo para **evitar saturación**.
- Respalda la base de datos de logs si necesitas histórico para auditorías.
- Asegura NTP/fecha/hora en equipos para que la línea de tiempo sea confiable.

---
