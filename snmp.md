# 🖧 **Configuración SNMP en equipos de red – LinkWich-Monitor**

Este tutorial explica cómo habilitar **SNMP v2c (solo lectura)** en **Cisco IOS/IOS-XE**, **ArubaOS-Switch/HPE ProCurve**, **Aruba AOS-CX**, **Allied Telesis AW+** y **Ruckus ICX**, además de **Windows Server / Windows 10 / Windows 11** para que LinkWich-Monitor pueda descubrir y monitorear tus equipos.

---

## 1️⃣ **Antes de empezar**

- Define una **comunidad SNMP de solo lectura (RO)**, por ejemplo: `LM-RO`.  
  > 🔒 **Seguridad:** evita usar `public`. Usa un valor propio.
- Ten a la mano:
  - **`<COMUNIDAD>`** (RO)
  - **`<UBICACION>`** (ej.: _“Site nombre Empresa/Local | IDF-A | Rack 2”_)
  - **`<CONTACTO>`** (ej.: _“NOC LinkWich-IT +52 624…”_)
- Asegura conectividad y firewall para **UDP/161** entre LinkWich-Monitor y el equipo.

---

## 2️⃣ **Buenas prácticas**

- Usa **RO** (read-only). Evita RW salvo casos justificados.
- Documenta **location** y **contact** (facilita soporte).
- **Restringe** (cuando aplique) qué IPs pueden consultar SNMP (Permitted Managers / ACL).
- **Guarda** la configuración para que persista tras reinicio.

---

## 3️⃣ **Comandos por marca**

> Reemplaza los valores entre `<>` por los de tu entorno.

### 🟦 **Cisco IOS / IOS-XE**
```plaintext
enable
configure terminal
 snmp-server community <COMUNIDAD> ro
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
end
write memory
```

**Verificación**
```plaintext
show running-config | include snmp-server
show snmp
```

---

### 🟨 **ArubaOS-Switch / HPE ProCurve**
```bash
configure terminal
 snmp-server community "<COMUNIDAD>" operator
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
exit
write memory
```

**Nota:** `operator` = lectura (RO). `manager` = lectura/escritura (RW).

**Verificación**
```bash
show snmp-server
show running-config | include snmp-server
```

---

### 🟧 **Aruba Series 6000 (AOS-CX) – SNMP v2c**
> Recomendado: **solo lectura (RO)** para monitoreo.

```bash
configure terminal
 snmp-server vrf default
 snmp-server community <COMUNIDAD> access-level ro
 snmp-server contact "<CONTACTO>"
 snmp-server location "<UBICACION>"
exit
write memory
```

**Verificación**
```bash
show running-config | include snmp-server
show snmp-server
```

---

### 🟩 **Allied Telesis (AW+)**
```bash
enable
configure terminal
 snmp-server community <COMUNIDAD> ro
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
exit
write
```

**Verificación**
```bash
show running-config | include snmp-server
show snmp
```

---

### 🟥 **Ruckus ICX (ICX FastIron) – SNMP v2c**
> Compatible con la mayoría de ICX (ej. 6450/7250/7450/7750).  
> En algunos modelos/firmware el guardado puede ser `write memory` o `copy running-config startup-config`.

```plaintext
enable
configure terminal
 snmp-server community <COMUNIDAD> ro
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
end
write memory
```

**Verificación**
```plaintext
show running-config | include snmp-server
show snmp
```

---

## 4️⃣ **Windows – Habilitar y configurar SNMP (PowerShell)**

> ✅ Ejecuta **PowerShell como Administrador**.  
> SNMP en Windows es un **componente opcional** y la forma de instalarlo cambia según versión.

---

### 🪟 A) Windows Server 2016 (instalación por Feature)

#### 1) Instalar SNMP Service + Provider
```powershell
Install-WindowsFeature -Name SNMP-Service -IncludeManagementTools
Install-WindowsFeature -Name SNMP-WMI-Provider
```

#### 2) Configurar comunidad RO y Permitted Managers
```powershell
$Community = 'LM-RO'        # Comunidad RO
$ManagerIP = '10.100.0.12'  # IP del servidor LinkWich-Monitor

# Comunidad RO (DWORD: 4=Read-Only, 8=Read-Write)
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'ValidCommunities' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\ValidCommunities' -Name $Community -PropertyType DWord -Value 4 -Force | Out-Null

# Permitir solo a tu servidor (recomendado)
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'PermittedManagers' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\PermittedManagers' -Name '1' -PropertyType String -Value $ManagerIP -Force | Out-Null
```

#### 3) (Opcional) Contacto y ubicación (sysContact/sysLocation)
```powershell
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'RFC1156Agent' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\RFC1156Agent' -Name 'sysContact'  -PropertyType String -Value 'NOC LinkWich-IT (+52 624 …)' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\RFC1156Agent' -Name 'sysLocation' -PropertyType String -Value 'Site | IDF-A | Rack 2' -Force | Out-Null
```

#### 4) Abrir firewall y arrancar servicio
```powershell
New-NetFirewallRule -DisplayName 'SNMP-In (UDP 161)' -Direction Inbound -Protocol UDP -LocalPort 161 -Action Allow -Profile Any -ErrorAction SilentlyContinue | Out-Null

Set-Service -Name 'SNMP' -StartupType Automatic
Restart-Service -Name 'SNMP'
```

#### 5) Verificación
```powershell
Get-Service SNMP
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\ValidCommunities'
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\PermittedManagers'
```

---

### 🪟 B) Windows Server 2019 / 2022 / 2025 (instalación por Feature on Demand)

> En estas versiones, SNMP suele instalarse como **Windows Capability**.

#### 1) Instalar SNMP (Client) y opcionales
```powershell
# Instala el componente SNMP (Feature on Demand)
Add-WindowsCapability -Online -Name 'SNMP.Client~~~~0.0.1.0'

# (Opcional) Herramientas de administración si aplica en tu build
# Add-WindowsCapability -Online -Name 'Rsat.Snmp.Tools~~~~0.0.1.0'
```

#### 2) Confirmar instalación
```powershell
Get-WindowsCapability -Online | Where-Object Name -like 'SNMP*'
```

#### 3) Configurar comunidad RO + permitted managers + contacto/ubicación
> Usa exactamente los mismos bloques de configuración por Registry del apartado **Server 2016**:
- **“Configurar comunidad RO y Permitted Managers”**
- **“Contacto y ubicación”**
- **“Firewall y servicio”**

---

### 🪟 C) Windows 10 y Windows 11 (instalación por Optional Feature)

> SNMP es **opcional**. En algunas ediciones/builds aparece como Capability.

#### 1) Instalar SNMP
```powershell
# Intento 1 (común en Windows 10/11):
Add-WindowsCapability -Online -Name 'SNMP.Client~~~~0.0.1.0'
```

#### 2) Si el comando anterior no encuentra el componente (fallback)
```powershell
# Lista capacidades disponibles relacionadas con SNMP
Get-WindowsCapability -Online | Where-Object Name -like '*SNMP*'
```

#### 3) Configurar comunidad RO + permitted managers + contacto/ubicación
> Usa los mismos bloques del apartado **Server 2016** (Registry + firewall + servicio).

---

## 5️⃣ **Probar desde LinkWich-Monitor**

1. Ve a **Agregar Dispositivos → Descubrimiento por SNMP** (o **Agregar manual**).
2. Ingresa:
   - **Versión SNMP:** `v2c`
   - **Comunidad:** la que configuraste (p. ej., `LM-RO`)
3. Ejecuta el **escaneo** o **guarda** el equipo.
4. Verifica en **Dashboard → Disponibilidad** que aparezcan interfaces, CPU, memoria, etc.

---

## 6️⃣ **Plantilla rápida (recomendado)**

Valores de referencia:
```bash
<COMUNIDAD> = LM-RO
<UBICACION> = "Site nombre Empresa/Local | IDF-A | Rack 2"
<CONTACTO>  = "NOC LinkWich-IT (+52 624 XXX XXXX)"
```

Aplica los comandos de tu marca con esos valores y guarda la configuración.

---

## 7️⃣ **Checklist de conectividad**

| ✔️ | Verificación |
|---|---|
| ✅ | IP alcanzable (ping) |
| ✅ | **UDP/161** abierto (SNMP) |
| ✅ | Comunidad **RO** correcta |
| ✅ | Sin ACL/Permitted Managers bloqueando al servidor de LinkWich-Monitor |
| ✅ | Fecha/hora del equipo correctas |

---

## 8️⃣ **Resolución de problemas**

| **Síntoma** | **Causa probable** | **Acción sugerida** |
|---|---|---|
| Tiempo de espera agotado | Firewall o ruta bloqueada | Permite **UDP/161**; revisa VLAN/rutas |
| No autorizado | Comunidad incorrecta | Corrige ortografía/mayúsculas |
| No aparecen métricas/interfaces | SNMP incompleto o filtrado | Verifica configuración SNMP y restricciones (ACL/Permitted Managers) |
| Datos en “0” o parciales | Limitación del equipo/MIB | Validar soporte del modelo/firmware y ajustar alcance |

---

