
# 🖧 **Configuración SNMP en equipos de red – LinkWich-Monitor**

Este tutorial explica cómo habilitar **SNMP v2c (solo lectura)** en **Cisco IOS/IOS-XE**, **ArubaOS-Switch/HPE ProCurve** y **Allied Telesis AW+**, de modo que LinkWich-Monitor pueda descubrir y monitorear tus equipos.

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
- **Guarda** la configuración para que persista tras reinicio.

---

## 3️⃣ **Comandos por marca**

> Reemplaza los valores entre `<>` por los de tu entorno.

## 🟦 **Cisco IOS / IOS-XE**
```plaintext
enable
configure terminal
 snmp-server community <COMUNIDAD> ro
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
end
write memory
```

---


### 5️⃣ **Probar desde LinkWich-Monitor**

1. Ve a **Agregar Dispositivos → Descubrimiento por SNMP** (o **Agregar manual**).
2. Ingresa:
   - **Versión SNMP:** `v2c`
   - **Comunidad:** la que configuraste (p. ej., `LM-RO`)
3. Ejecuta el **escaneo** o **guarda** el equipo.
4. Verifica en **Dashboard → Disponibilidad** que aparezcan interfaces, CPU, memoria, etc.

---

### 🟦 **Verificación**
```bash
show running-config | include snmp-server
show snmp
```
---


## 🟨 **ArubaOS-Switch / HPE ProCurve**
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
## 🟧 **Aruba Series 6000 (AOS-CX) – SNMP v2c**

> Recomendado: **solo lectura (RO)** para monitoreo.  
> Si realmente necesitas cambios vía SNMP, usa `access-level rw` (no recomendado).

```bash
configure terminal
 snmp-server vrf default
 snmp-server community <COMUNIDAD> access-level ro    ! usa ro (recomendado)
 ! snmp-server community <COMUNIDAD> access-level rw  ! opcional, NO recomendado
 snmp-server contact "<CONTACTO>"
 snmp-server location "<UBICACION>"
exit
write memory
```
---

## 🟩 **Allied Telesis (AW+)**
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
## 🪟 **Windows (Server / Pro) – Habilitar SNMP por PowerShell**

> Ejecuta **PowerShell como Administrador**.

#### 1) Instalar el servicio SNMP
```powershell
# Server 2012 R2 / 2016 (si existe Install-WindowsFeature):
if (Get-Command Install-WindowsFeature -ErrorAction SilentlyContinue) {
  Install-WindowsFeature -Name SNMP-Service -IncludeManagementTools
  Install-WindowsFeature -Name SNMP-WMI-Provider
}
else {
  # Windows 10/11 y Server 2019/2022 (Feature on Demand):
  Add-WindowsCapability -Online -Name 'SNMP.Client~~~~0.0.1.0'
}
```

#### 2) Configurar comunidad RO y restringir managers
```powershell
$Community = 'LM-RO'        # ← cambia si deseas otro nombre
$ManagerIP = '10.100.0.12'  # ← IP de tu servidor LinkWich-Monitor

# Comunidad RO (DWORD: 4=Read-Only, 8=Read-Write)
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'ValidCommunities' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\ValidCommunities' -Name $Community -PropertyType DWord -Value 4 -Force | Out-Null

# Permitir solo a tu servidor (recomendado)
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'PermittedManagers' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\PermittedManagers' -Name '1' -PropertyType String -Value $ManagerIP -Force | Out-Null
```

#### 3) (Opcional) Contacto y ubicación
```powershell
New-Item -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters' -Name 'RFC1156Agent' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\RFC1156Agent' -Name 'sysContact'  -PropertyType String -Value 'NOC LinkWich-IT (+52 624 …)' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\SNMP\Parameters\RFC1156Agent' -Name 'sysLocation' -PropertyType String -Value 'Site Querencia | IDF-A | Rack 2'      -Force | Out-Null
```

#### 4) Abrir firewall (UDP/161) y arrancar el servicio
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

### 4️⃣ **Plantilla rápida (recomendado)**
Valores de referencia:
```bash
<COMUNIDAD> = LM-RO
<UBICACION> = "Site nombre Empresa/Local | IDF-A | Rack 2"
<CONTACTO>  = "NOC LinkWich-IT (+52 624 XXX XXXX)"
```
Aplica los comandos de tu marca con esos valores y guarda la configuración.


## 6️⃣ **Checklist de conectividad**

| ✔️ | Verificación                                     |
|----|--------------------------------------------------|
| ✅ | IP alcanzable (ping)                              |
| ✅ | **UDP/161** abierto (SNMP)                        |
| ✅ | Comunidad **RO** correcta                         |
| ✅ | Sin ACL que bloquee al servidor de LinkWich-Monitor |
| ✅ | Fecha/hora del equipo correctas                   |


## 7️⃣ **Resolución de problemas**

| **Síntoma**                | **Causa probable**            | **Acción sugerida**                               |
|---------------------------|-------------------------------|---------------------------------------------------|
| Tiempo de espera agotado  | Firewall o ruta bloqueada     | Permite **UDP/161**; revisa VLAN y rutas          |
| No autorizado             | Comunidad incorrecta          | Corrige ortografía/mayúsculas                     |
| Sin métricas/Interfaces   | SNMP incompleto/deshabilitado | Revisa `show snmp` y guarda cambios               |
| Datos en “0” o parciales  | SO muy antiguo / MIB limitada | Actualiza SO o valida compatibilidad              |



