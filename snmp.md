
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

### 🟦 **Cisco IOS / IOS-XE**
```plaintext
enable
configure terminal
 snmp-server community <COMUNIDAD> ro
 snmp-server location "<UBICACION>"
 snmp-server contact "<CONTACTO>"
end
write memory


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

### 4️⃣ **Plantilla rápida (recomendado)**
Valores de referencia:
```bash
<COMUNIDAD> = LM-RO
<UBICACION> = "Site nombre Empresa/Local | IDF-A | Rack 2"
<CONTACTO>  = "NOC LinkWich-IT (+52 624 XXX XXXX)"
```
Aplica los comandos de tu marca con esos valores y guarda la configuración.


### 6️⃣ **Checklist de conectividad**

| ✔️ | Verificación                                     |
|----|--------------------------------------------------|
| ✅ | IP alcanzable (ping)                              |
| ✅ | **UDP/161** abierto (SNMP)                        |
| ✅ | Comunidad **RO** correcta                         |
| ✅ | Sin ACL que bloquee al servidor de LinkWich-Monitor |
| ✅ | Fecha/hora del equipo correctas                   |


### 7️⃣ **Resolución de problemas**

| **Síntoma**                | **Causa probable**            | **Acción sugerida**                               |
|---------------------------|-------------------------------|---------------------------------------------------|
| Tiempo de espera agotado  | Firewall o ruta bloqueada     | Permite **UDP/161**; revisa VLAN y rutas          |
| No autorizado             | Comunidad incorrecta          | Corrige ortografía/mayúsculas                     |
| Sin métricas/Interfaces   | SNMP incompleto/deshabilitado | Revisa `show snmp` y guarda cambios               |
| Datos en “0” o parciales  | SO muy antiguo / MIB limitada | Actualiza SO o valida compatibilidad              |



