
# 🪟💾 Tutorial – Consultas de Backups Windows (WbAdmin) en LinkWich‑Monitor

Este tutorial explica cómo configurar en **LinkWich‑Monitor** las **consultas automáticas** del estado de respaldos en **Windows Server/Windows** usando **WbAdmin**, y cómo habilitar **SSH (OpenSSH Server)** para permitir que LinkWich‑Monitor ejecute comandos remotos de forma segura.

> ✅ **Importante:** Este módulo realiza **consultas (lecturas)** del estado del backup.  
> No ejecuta el backup por sí mismo; consulta lo que ya se haya ejecutado en el servidor (por ejemplo, por una tarea programada de Windows Server Backup o tu software de respaldos).

---

## 1️⃣ Requisitos previos 

Antes de configurar LinkWich‑Monitor, asegúrate de que:

- El servidor Windows tiene **Windows Server Backup** instalado (si aplica) y genera respaldos.
- En el servidor existe historial consultable vía **WbAdmin**.
- LinkWich‑Monitor puede conectarse al servidor por red:
  - ✅ **TCP/22 (SSH)** desde LinkWich‑Monitor hacia el servidor Windows
- Tienes credenciales válidas de Windows (usuario y contraseña) con permisos suficientes para consultar WbAdmin.
- La hora del servidor y la del sistema de monitoreo son correctas (recomendado NTP).

---

## 2️⃣ Concepto clave: “Consulta” vs “Ejecución del backup”

LinkWich‑Monitor hace **consultas periódicas** (por ejemplo, 1 vez al día) para verificar:

- Última fecha de backup
- Destino (disco/carpeta/target)
- Versión / información disponible
- Estado (OK / Error)
- Mensaje o error reportado por WbAdmin

📌 **Ejemplo importante (horario):**  
Si programas la consulta a las **02:00 AM**, pero tu backup realmente termina a las **04:00 AM**, entonces a las 02:00 la consulta **aún no verá el backup finalizado** y puede parecer como si “no se hizo”.  
✅ Solución: programa la consulta **después** de la hora habitual de finalización del backup (o deja margen de 1–2 horas).

---

## 3️⃣ Habilitar SSH en Windows (OpenSSH Server)

Para que LinkWich‑Monitor pueda ejecutar comandos remotos (ej. consultas con `wbadmin`) debes habilitar SSH.

> Ejecuta **PowerShell como Administrador** en el servidor Windows.

### 3.1 Instalar OpenSSH Client
```powershell
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```

### 3.2 Instalar OpenSSH Server
```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

### 3.3 Iniciar el servicio SSH
```powershell
Start-Service sshd
```

### 3.4 Configurar arranque automático
```powershell
Set-Service -Name sshd -StartupType Automatic
```

### 3.5 Abrir el puerto 22 en el firewall
```powershell
New-NetFirewallRule -Name sshd `
  -DisplayName "OpenSSH SSH Server" `
  -Enabled True -Direction Inbound `
  -Protocol TCP -Action Allow -LocalPort 22
```

### 3.6 Verificar que esté corriendo
```powershell
Get-Service sshd
```

✅ Debe aparecer como **Running**.

---

## 4️⃣ Probar conectividad SSH (recomendado)

Desde el servidor donde está LinkWich‑Monitor (o desde una PC de pruebas), valida:

- El servidor responde por puerto **22**
- Las credenciales son correctas

Ejemplo (si tienes cliente SSH):
```bash
ssh usuario@10.0.10.63
```

> Si falla la conexión, revisa firewall, rutas, VLAN/ACL y credenciales.

---

## 5️⃣ Configurar “Consultas de Backups Windows” en LinkWich‑Monitor

### 5.1 Crear una programación de consulta
En LinkWich‑Monitor entra al módulo de **Backups Windows** y crea una nueva programación con estos campos:

- **Descripción:** p.ej. `Backup diario 22 h`
- **Servidor Windows:** selecciona el servidor, por ejemplo:  
  `SERVER-MILESTON-CCTV-1 (10.17.0.63)`
- **Frecuencia:** `Diaria`
- **Hora:** define la hora de la **consulta**
- **Destinatarios (Ctrl + clic):** por ejemplo:
  - `soporte@linkwich.com`

📌 **Recomendación de horario:**  
Pon la consulta **después** de la ventana real del backup.  
Ejemplo: si el backup normalmente termina entre 03:00–04:00, programa la consulta a las **05:00**.

Guarda la programación.

---

### 5.2 Credenciales SSH (muy importante)
Para que LinkWich‑Monitor consulte correctamente, las **credenciales SSH deben ser correctas**:

- Usuario Windows válido (local o dominio)
- Contraseña correcta
- Permisos suficientes para ejecutar `wbadmin`

✅ Si las credenciales fallan, el sistema mostrará **Error de conexión/autenticación** y no podrá obtener el estado.

---

## 6️⃣ ¿Qué consulta LinkWich‑Monitor? (WbAdmin)

El sistema realiza una consulta remota con comandos de lectura de WbAdmin para identificar el estado del respaldo.

Ejemplos de comandos comunes (referencia):
- Ver versiones disponibles:
  - `wbadmin get versions`
- Ver estado/resumen:
  - `wbadmin get status` *(según edición/versión puede variar)*

> Nota: LinkWich‑Monitor adapta el comando según el método de consulta configurado.  
> Lo importante es que el servidor tenga historial disponible y el usuario tenga permisos.

---

## 7️⃣ Histórico y validación en tiempo real

### 7.1 Ver historial
En la sección:
**Histórico Backups Windows → Histórico Backups**

Verás una tabla con columnas como:

- **Servidor (IP)**
- **Fecha Backup**
- **Destino**
- **Versión**
- **P. recuperar** (punto de recuperación)
- **Estado**
- **Mensaje / Error**
- **Registrado / Actualizado**
- **Eventos**

Si aún no hay registros, verás:
> “Ningún dato disponible en esta tabla”

✅ Esto significa que todavía no se ha ejecutado la primera consulta (o falló por conexión/credenciales).

---

### 7.2 Validación “en tiempo real”
Cuando ejecutes una consulta manual o se dispare una programación, puedes:

1. Refrescar la vista de historial
2. Ver si aparece un nuevo registro o si se actualiza la columna **Actualizado**
3. Revisar **Mensaje / Error** para diagnosticar

---

## 8️⃣ Errores comunes y soluciones

### ❌ “No conecta por SSH”
- Verifica **TCP/22** abierto del servidor
- Revisa firewall/ACL de la red
- Confirma que el servicio **sshd** esté **Running**
- Confirma IP y DNS

### ❌ “Credenciales inválidas / Access denied”
- Usuario/contraseña incorrectos
- Usuario sin permisos para consultar WbAdmin
- Si es dominio, valida formato de usuario (según tu estándar):  
  `DOMINIO\usuario` o `usuario@dominio.local`

### ❌ “No aparece el backup (parece que no corrió)”
- La consulta fue ejecutada **antes** de que terminara el backup
- Solución: mueve la hora de consulta a después de la ventana real de backup

### ❌ “No hay historial / no hay versiones”
- Aún no se ha generado un backup que deje versiones consultables
- O Windows Server Backup no está instalado/configurado

---

## 9️⃣ Buenas prácticas

- Programa consultas 1 vez al día (o según criticidad).
- Deja margen de tiempo después del backup para que el resultado ya exista.
- Mantén un correo de notificación por cada servidor o grupo.
- Asegura NTP/hora correcta para reportes confiables.
- Restringe SSH por IP (solo permitir la IP del servidor LinkWich‑Monitor) si tu red lo permite.

---
