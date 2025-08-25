
# 🧾 **Configuración de Syslog en equipos – LinkWich-Monitor**

Guía para enviar registros (syslog) desde tus dispositivos y servidores hacia **LinkWich-Monitor**.

---

## 1️⃣ **Antes de empezar**

- **Servidor syslog:** define la IP de tu servidor (ejemplo: `<SYSLOG_SERVER> = 10.100.0.12`).
- **Puerto:** UDP **514** (predeterminado).  
- **Firewall:** permite tráfico **saliente** UDP/514 desde los equipos y **entrante** UDP/514 en el servidor.
- **Hora/NTP:** ajusta la hora correcta (mejora análisis de eventos).

> 🧠 **Tip:** si tu red usa VLANs de gestión, define una **interfaz de origen** (cuando el equipo lo permita) para que los logs salgan por esa VLAN.

---

## 2️⃣ **Cisco IOS / IOS-XE**

> Reemplaza `\<SYSLOG_SERVER>` por tu IP de servidor (p. ej., `10.100.0.12`).  
> Ajusta `VlanX` si quieres fijar interfaz origen (opcional).

```bash
enable
configure terminal
 service timestamps log datetime msec
 service timestamps debug datetime msec
 logging host <SYSLOG_SERVER>
 logging trap informational
 ! opcional (si aplica):
 ! logging source-interface VlanX
 logging on
end
write memory
```

### **Verificación**
```bash
show running-config | include logging
show logging
```

---

## 3️⃣ **ArubaOS-Switch / HPE ProCurve**
En muchos modelos basta con `logging <SYSLOG_SERVER>`. Algunos soportan severidad explícita.
```bash
configure terminal
 logging <SYSLOG_SERVER>
 ! opcional (solo si tu versión lo soporta):
 ! logging severity info
 ! logging facility local7
exit
write memory
```

**Verificación**
```bash
show running-config | include logging
show logging
```

---

## 4️⃣ **Allied Telesis (AlliedWare Plus / AW+)**
```bash
enable
configure terminal
 logging host <SYSLOG_SERVER>
 logging trap informational
 ! opcional:
 ! logging source-interface vlan <ID>
exit
write
```

**Verificación**
```bash
show running-config | include logging
show logging
```

---

## 5️⃣ **Linux (rsyslog)**
**Crea un archivo de configuración:**
```bash
sudo tee /etc/rsyslog.d/99-linkwich.conf >/dev/null <<'EOF'
*.* @<SYSLOG_SERVER>:514
EOF
```

**Reinicia el servicio:**
```bash
sudo systemctl restart rsyslog
```

**Prueba rápida:**
```bash
logger -p local0.info "Prueba syslog desde Linux hacia <SYSLOG_SERVER>"
```
## 6️⃣ **Windows (agente NXLog – ejemplo mínimo)**

Windows no envía syslog de forma nativa. Usa un agente como **NXLog** (o Syslog-NG/RSyslog para Windows).

**Fragmento `nxlog.conf` (básico):**
```conf
define SYSLOG_SERVER <SYSLOG_SERVER>

<Input in>
    Module  im_msvistalog
</Input>

<Output out>
    Module  om_udp
    Host    %SYSLOG_SERVER%
    Port    514
</Output>

<Route r>
    Path    in => out
</Route>
```

> Reinicia el servicio **nxlog** tras aplicar cambios.

---

## 7️⃣ **Niveles de severidad (syslog)**

| **Número** | **Nombre**     | **Uso típico**            |
|-----------:|----------------|---------------------------|
| 0          | emergency      | Caída total               |
| 1          | alert          | Acción inmediata          |
| 2          | critical       | Error crítico             |
| 3          | error          | Errores                   |
| 4          | warning        | Advertencias              |
| 5          | notice         | Notas importantes         |
| 6          | informational  | Información general       |
| 7          | debug          | Diagnóstico detallado     |

> 🎯 **Recomendado:** `informational` (o **info**) para operación normal; usa **debug** solo temporalmente.

---

## 8️⃣ **Comprobación en LinkWich-Monitor**

- En el módulo **Syslog**, valida que aparezcan entradas desde las IPs de tus equipos.  
- Filtra por **IP/hostname** y verifica **timestamps** correctos.  
- Si no ves tráfico, revisa **firewall**, **ruta** y **severidad** configurada.

---

## 9️⃣ **Troubleshooting rápido**

| **Síntoma**             | **Causa probable**           | **Acción sugerida**                                  |
|-------------------------|------------------------------|------------------------------------------------------|
| No llegan logs          | Firewall / ruta bloqueada    | Permite **UDP/514**, revisa rutas/VLAN               |
| Logs con desfase de hora| NTP no configurado           | Configura **NTP** en equipos y servidor              |
| Muy pocos eventos       | Severidad muy restrictiva    | Sube a `informational` temporalmente                 |
| Demasiado volumen       | Severidad muy alta (debug)   | Baja a `notice` o `informational`                    |
| Logs con IP inesperada  | Interfaz origen sin fijar    | Usa `source-interface` (si el equipo lo soporta)     |

---

### 🔚 **Resumen**

- Usa `<SYSLOG_SERVER> = 10.100.0.12` (o tu IP real).  
- Habilita **UDP/514** y **NTP**.  
- Ajusta severidad a **informational** para operación normal.  
- Verifica desde el equipo (`show logging`) y desde el servidor (módulo **Syslog** en **LinkWich-Monitor**).
