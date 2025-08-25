
# 🖧 **Configuración SNMP en equipos de red – LinkWich-Monitor**

Este tutorial explica cómo habilitar **SNMP v2c (solo lectura)** en **Cisco IOS/IOS-XE**, **ArubaOS-Switch/HPE ProCurve** y **Allied Telesis AW+**, de modo que LinkWich-Monitor pueda descubrir y monitorear tus equipos.

---

## 1️⃣ **Antes de empezar**

- Define una **comunidad SNMP de solo lectura (RO)**, por ejemplo: `LM-RO`.  
  > 🔒 **Seguridad:** evita usar `public`. Usa un valor propio.
- Ten a la mano:
  - **`<COMUNIDAD>`** (RO)
  - **`<UBICACION>`** (ej.: _“Site Querencia | IDF-A | Rack 2”_)
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
