# 👥 Manual de Gestión de Usuarios, Roles y Permisos – LinkWich‑Monitor

En **LinkWich‑Monitor** puedes crear usuarios con distintos niveles de acceso para controlar **qué pueden ver** y **qué acciones pueden ejecutar** dentro del sistema.  
Esto mejora la seguridad, reduce errores operativos y evita cambios no autorizados.

A partir de la actualización de **Roles y Permisos**, el acceso ya no depende solo del “rol clásico”, sino de **permisos granulares por módulo** (RBAC).

---

## 1️⃣ Conceptos (rápido y claro)

### 👤 Usuario
Es la cuenta con la que alguien inicia sesión. Un usuario tiene:
- **Nombre de usuario**
- **Contraseña**
- (Opcional) **Correo**
- **Rol asignado**
- **Estado** (activo/inactivo)
- (Opcional) **Fecha de vigencia**
- (Opcional) **2FA**

### 🧩 Rol
Un rol es un “paquete” de permisos. Ejemplos:
- `visitante (sistema)`
- `admin (sistema)`
- `super_admin (sistema)`
- roles personalizados (ej. `supervisor`, `noc`, `auditor`, etc.)

### 🔐 Permiso (perm_key)
Es una autorización específica, por ejemplo:
- `devices_view` → puede ver dispositivos
- `devices_add` → puede agregar dispositivos
- `Roles_y_Permisos_edit` → puede editar roles y permisos

> ✅ Regla general: **si un usuario NO tiene el permiso**, LinkWich‑Monitor **bloquea** el acceso a esa vista/acción.

---

## 2️⃣ Acceder a la Gestión de Usuarios

1. Desde el **menú lateral**, entra a **Usuarios** (o **Configuración de Usuarios**).
2. Se abrirá la lista de usuarios existentes, mostrando normalmente:
   - **Nombre de usuario**
   - **Correo electrónico** (si aplica)
   - **Rol asignado**
   - **Estado** (activo/inactivo)
   - **Fecha de creación / actualización** (según tu vista)

---

## 3️⃣ Agregar un nuevo usuario

1. Pulsa **➕ Agregar Usuario**.
2. Completa el formulario:
   - **Nombre de usuario** → Identificador único para iniciar sesión.
   - **Correo electrónico** (opcional) → Para notificaciones/recuperación.
   - **Contraseña** → Se recomienda segura.
   - **Rol** → Selecciona el rol que definirá permisos (ver sección 4).
   - **Estado** → Activo (puede iniciar sesión) / Inactivo (acceso bloqueado).
   - **Fecha de vigencia** (opcional) → Fecha límite de acceso.
3. Pulsa **Guardar**.

💡 Tip: Si usas 2FA, normalmente se activa desde la **edición del usuario** una vez creado.

---

## 4️⃣ Gestión de Roles y Permisos (nuevo módulo)

En esta actualización, existe un módulo/modal para administrar roles y sus permisos:

📌 Ruta típica:
- **Usuarios → Roles y permisos** (o botón/modal dentro del módulo de Usuarios)

Dentro del modal verás 2 áreas principales:

### 4.1 Panel izquierdo: Roles
- Selector **“Selecciona un rol”**
- Botón **➕ Crear** para crear un rol nuevo
- Campos de **Nombre** y **Descripción**
- Botones:
  - **Guardar rol**
  - **Eliminar** (si el rol es eliminable)

📝 Nota: Los roles marcados como **(sistema)** normalmente **no se pueden eliminar**.

---

### 4.2 Panel derecho: Permisos del rol
- Buscador: **“Buscar permiso (ej: snmp, syslog, hypermap…)”**
- Botones:
  - **Seleccionar todo**
  - **Limpiar**
  - **Guardar permisos**
- Lista tipo tarjetas con:
  - **Nombre del permiso**
  - **Descripción**
  - Check para activar/desactivar

✅ Recomendación operativa:
- Usa el buscador para asignar por módulo, por ejemplo:
  - `syslog` → permisos del módulo Syslog
  - `devices` / `inventario` → inventario/dispositivos/switches
  - `backup` / `respaldo` → respaldos (equipos, DB, Windows)
  - `Roles_y_Permisos` → administración de roles
  - `terminal` → accesos a terminal SSH/Telnet/WebUI
  - `reports` → reportes y exportaciones

---

## 5️⃣ Crear un rol nuevo (paso a paso)

1. Abre **Roles y permisos**.
2. Pulsa **➕ Crear**.
3. Captura:
   - **Nombre del rol** (ej. `supervisor`, `noc`, `auditor`)
   - **Descripción** (opcional)
4. Pulsa **Guardar rol**.
5. En “Permisos del rol”:
   - Busca y marca los permisos necesarios.
   - Pulsa **Guardar permisos**.

✅ Listo: ya puedes asignar ese rol a usuarios.

---

## 6️⃣ Editar permisos de un rol existente

1. Abre **Roles y permisos**.
2. Selecciona el rol.
3. En “Permisos del rol”:
   - Activa/desactiva checks
4. Pulsa **Guardar permisos**.

💡 Tip: Si el usuario ya estaba logueado, puede requerir **cerrar sesión y volver a entrar** para reflejar cambios de permisos en navegación/menús (según tu implementación).

---

## 7️⃣ Eliminar roles

1. Abre **Roles y permisos**
2. Selecciona el rol
3. Pulsa **Eliminar** y confirma

⚠️ Notas:
- Roles **(sistema)** normalmente no se eliminan.
- Si un rol está asignado a usuarios, se recomienda reasignar usuarios antes de eliminar.

---

## 8️⃣ Editar o eliminar usuarios

- **Editar:** botón ✏️ → ajusta rol, correo, estado, vigencia y/o 2FA → **Guardar**
- **Eliminar:** botón 🗑 → confirma

⚠️ No se recomienda eliminar cuentas críticas. Mejor:
- dejar **Inactivo** si el usuario ya no debe entrar.

---

# 🔐 Manual de 2FA (Autenticación en Dos Pasos)

La autenticación en dos pasos (**2FA**) añade una capa extra de seguridad.  
Con **2FA**, para iniciar sesión necesitarás tu usuario y contraseña **más un código temporal** (6 dígitos) generado por una app como:
- Google Authenticator
- Microsoft Authenticator
- Authy

---

## 1️⃣ Activar 2FA por primera vez

1. Entra a **Usuarios**
2. Edita el usuario deseado
3. Activa **Habilitar 2FA**
4. Guarda
5. Se mostrará un **QR** (o se enviará por correo si tu flujo lo incluye)
6. Escanea el QR en tu app:
   - “Agregar cuenta” → “Escanear QR”
7. En el siguiente login, se pedirá el **código 2FA**

---

## 2️⃣ Regeneración del QR (cuando aplica)

El sistema puede regenerar el QR/secret por seguridad cuando:
- Cambias contraseña
- Cambias estado (Activo/Inactivo)
- Cambias/expira vigencia
- Desactivas y reactivas 2FA

Cuando ocurra:
- Se genera un **nuevo QR**
- Debe escanearse nuevamente en la app

---

## 3️⃣ Desactivar 2FA

1. Usuarios → Editar usuario
2. Desactivar **2FA**
3. Guardar

⚠️ Desactivar 2FA reduce la seguridad. Úsalo solo si es necesario.

---

## 4️⃣ Buenas prácticas de seguridad

- Usa **roles mínimos necesarios** por persona.
- Mantén usuarios no vigentes como **Inactivos**.
- Activa 2FA en cuentas con permisos altos.
- No compartas códigos 2FA.
- Revisa Auditoría (si la tienes habilitada) para rastrear acciones críticas.

---

# 📚 Apéndice – Catálogo completo de permisos (perm_key)

> Este listado corresponde a tu tabla `permisos` (118 permisos).  
> Puedes usarlo para documentar “qué hace cada permiso” y asignarlos por módulo.

| # | perm_key | Descripción |
|---:|---|---|
| 1 | devices_view | Puede ver template de dispositivos |
| 2 | devices_add | Puede agregar dispositivos |
| 3 | devices_edit | Puede editar dispositivos |
| 4 | devices_delete | Puede Eliminar dispositivos |
| 5 | inventario_device_view | Puede ver template de switches |
| 6 | inventory_ver_config | Puede ver configuracion automática en ver config interfaces y poe etc |
| 7 | programar_interfaces_view | Puede ver la lista de programación de interfaces down y up |
| 8 | programar_interfaces_add | Puede agregar la lista de programación de interfaces down y up |
| 9 | programar_interfaces_edit | Puede editar la lista de programación de interfaces down y up |
| 10 | programar_interfaces_delete | Puede eliminar la lista de programación de interfaces down y up |
| 11 | programar_anchobanda_view | Puede ver la lista de programación de ancho de banda villas |
| 12 | programar_anchobanda_edit | Puede editar el ancho de banda de villas |
| 13 | snmp_view | Puede ver SNMP |
| 14 | snmp_devices_view | Puede ver SNMP por dispositivo |
| 15 | metrica_view | Puede ver el template de metricas |
| 16 | dashboard_interfaces_actual_view | Puede ver el template de dashboard de interfaces actual |
| 17 | Historico_interfaces_view | Puede ver el template de Historico de interfaces |
| 18 | Historico_cortes_view | Puede ver el template de Historico de cortes de dispositivos |
| 19 | Historico_cortes_nota | Puede ver el template de Historico de cortes para editar nota |
| 20 | Historico_resumen_general_view | Puede ver el template de Historico de Resumen general |
| 21 | Monitoreo_puertos_view | Puede ver el template de monitorear puertos TCP/UDP |
| 22 | Monitoreo_puertos_add | Puede agregar puertos y servicios http |
| 23 | Monitoreo_puertos_edit | Puede editar puertos y servicios http |
| 24 | Monitoreo_puertos_delete | Puede eliminar puertos y servicios http |
| 25 | Monitoreo_snmp_view | Puede ver el template de monitorear snmp |
| 26 | Monitoreo_snmp_add | Puede agregar snmp servicios y programar CPU,Interfaces,RAM etc |
| 27 | Monitoreo_snmp_edit | Puede editar snmp servicios y programar CPU,Interfaces,RAM etc |
| 28 | Monitoreo_snmp_delete | Puede eliminar snmp servicios y programar CPU,Interfaces,RAM etc |
| 29 | Monitoreo_tarea_view | Puede ver el template de Programar Tarea |
| 30 | Monitoreo_tarea_add | Puede agregar y programar alguna tarea como ping hacia un destino de un dispositivo |
| 31 | Monitoreo_tarea_edit | Puede editar programar alguna tarea como ping hacia un destino de un dispositivo |
| 32 | Monitoreo_tarea_delete | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 33 | upgrade_view | Puede ver el template de Actualizaciones de Firmware |
| 34 | Respaldo_view | Puede ver el template de Programar Tarea |
| 35 | Respaldo_1x1 | Puede agregar y programar alguna tarea como ping hacia un destino de un dispositivo |
| 36 | Respaldo_1xall | Puede editar programar alguna tarea como ping hacia un destino de un dispositivo |
| 37 | Respaldo_drive | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 38 | Respaldo_descargar | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 39 | Respaldo_ver_preview | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 40 | Respaldo_programaciones_view | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 41 | Respaldo_programaciones_add | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 42 | Respaldo_programaciones_edit | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 43 | Respaldo_programaciones_delete | Puede eliminar programar alguna tarea como ping hacia un destino de un dispositivo |
| 44 | Syslog_view | Puede ver el template de Syslog |
| 45 | Syslog_config_view | Puede ver el template de Syslog configuraciones |
| 46 | Syslog_config_edit | Puede ver el template de Syslog configuraciones editar |
| 47 | Syslog_config_add | Puede ver el template de Syslog configuraciones agregar |
| 48 | Syslog_config_delete | Puede ver el template de Syslog configuraciones eliminar |
| 49 | Syslog_permisos_view | Puede ver el template de Syslog permisos para aceptar el log al server |
| 50 | mapa_flujo_view | Puede ver el template de Mapa de flujo |
| 51 | mapa_flujo_edit | Puede ver el template de Mapa de flujo editar |
| 52 | mapa_flujo_add | Puede ver el template de Mapa de flujos agregar |
| 53 | mapa_flujo_delete | Puede ver el template de Mapa de flujo eliminar |
| 54 | hypermap_view | Puede ver el template de Hypermap |
| 55 | hypermap_edit_icono | Puede ver el template de Hypermap editar |
| 56 | hypermap_guardar_map | Puede ver el template de Hypermap Guardar mapa |
| 57 | hypermap_reset_contadores | Puede ver el template de Hypermap eliminar contadores |
| 58 | NetPath_view | Puede ver el template de NetPath |
| 59 | NetPath_edit | Puede ver el template de NetPath editar |
| 60 | NetPath_add | Puede ver el template de NetPath agregar |
| 61 | NetPath_delete | Puede ver el template de NetPath eliminar |
| 62 | root_Hypermap_view | Puede ver el template de root_hypermap |
| 63 | Auditoria_view | Puede ver el template de Auditoria |
| 64 | Auditoria_general_table | Puede ver el template de Auditoria general tabla |
| 65 | Auditoria_terminal_table | Puede ver el template de Auditoria terminal tabla |
| 66 | Auditoria_delete | Puede ver el template de Auditoria eliminar registros |
| 67 | Usuarios_view | Puede ver el template de Usuarios |
| 68 | Usuarios_edit | Puede ver el template de Usuarios editar |
| 69 | Usuarios_add | Puede ver el template de Usuarios agregar |
| 70 | Usuarios_delete | Puede ver el template de Usuarios eliminar |
| 71 | correo_view | Puede ver el template de Correos |
| 72 | correo_edit | Puede ver el template de Correos editar |
| 73 | correo_add | Puede ver el template de Correos agregar |
| 74 | correo_delete | Puede ver el template de Correos eliminar |
| 75 | correo_alertas_global | Puede ver el template de Correos para enviar alerta global |
| 76 | correo_destinatarios | Puede ver el template de Correos para enviar por destinatario |
| 77 | correo_remitente_view | Puede ver el template de Correos Remitente config |
| 78 | whatsapp_view | Puede ver el template de whatsapp |
| 79 | whatsapp_edit | Puede ver el template de whatsapp editar |
| 80 | whatsapp_add | Puede ver el template de whatsapp agregar |
| 81 | whatsapp_delete | Puede ver el template de whatsapp eliminar |
| 82 | Nodos_criticos_view | Puede ver el template de Nodos Criticos |
| 83 | Nodos_criticos_edit | Puede ver el template de Nodos_criticos editar |
| 84 | Nodos_criticos_add | Puede ver el template de Nodos_criticos agregar |
| 85 | Nodos_criticos_delete | Puede ver el template de Nodos_criticos eliminar |
| 86 | Nodos_criticos_version | Puede ver el template de Nodos_criticos seleccionar la versión 1 o 2 |
| 87 | GruposyZonas_view | Puede ver el template de  GruposyZonas |
| 88 | GruposyZonas_edit | Puede ver el template de GruposyZonas editar |
| 89 | GruposyZonas_add | Puede ver el template de GruposyZonas agregar |
| 90 | GruposyZonas_delete | Puede ver el template de GruposyZonas eliminar |
| 91 | backup_bd_view | Puede ver el template de backup base de datos |
| 92 | backup_bd_crear | Puede ver el template de backup base de datos crear |
| 93 | backup_bd_cargar | Puede ver el template de backup base de datos cargar |
| 94 | gptall_view | Puede ver el template de gptall |
| 95 | Utileria_view | Puede ver el template de Utileria |
| 96 | Sniffer_view | Puede ver el template de Sniffer |
| 97 | Ping_view | Puede ver el template de Ping |
| 98 | Backup_Windows_view | Puede ver el template de Backup_Windows |
| 99 | Backup_Windows_Tabla_view | Puede ver el template de Backup_Windows Tabla |
| 100 | terminal_ssh_access | Puede abrir terminal SSH |
| 101 | terminal_telnet_access | Puede abrir terminal Telnet |
| 102 | terminal_webui_access | Puede abrir WebUI |
| 103 | reports_view | Puede ver template de reportes |
| 104 | reports_export | Puede exportar reportes |
| 105 | reports_excel_export | Puede exportar reportes en excel |
| 106 | mapa_geo_view | Puede ver el template de  mapa_geo |
| 107 | mapa_geo_edit | Puede ver el template de mapa_geo editar |
| 108 | mapa_geo_add | Puede ver el template de mapa_geo agregar |
| 109 | mapa_geo_delete | Puede ver el template de mapa_geo eliminar |
| 110 | licencia_view | Puede ver el template de  Licencia |
| 111 | mapa_flujo_ver_diagrama | Puede ver el diagrama del Mapa de Flujo |
| 112 | Syslog_Depurar_view | Puede ver el módulo de depuración de Syslog (filtros y pruebas) |
| 113 | Roles_y_Permisos_view | Puede ver el módulo/Modal de Roles y Permisos |
| 114 | Roles_y_Permisos_edit | Puede editar roles y permisos desde el Modal |
| 115 | Roles_y_Permisos_add | Puede agregar nuevos roles o asignaciones desde el Modal |
| 116 | Roles_y_Permisos_delete | Puede eliminar roles o asignaciones desde el Modal |
| 117 | Tarjeta_Criticos_Editar | Puede editar la imagen y el título de la tarjeta de críticos |
| 118 | Alertas_Marcar_resueltas | Puede marcar alertas como resueltas desde el dashboard |
