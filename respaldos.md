# 🔁 Respaldos de Dispositivos – LinkWich-Monitor

Esta sección te permite **respaldar la configuración** de tus equipos (switches/routers/firewalls compatibles), **descargar los archivos generados** y **programar copias automáticas**.  
Adicionalmente, puedes habilitar la **subida automática a Google Drive** para contar con una copia externa.

---

## ✅ Requisitos previos (recomendado)

Antes de ejecutar respaldos, verifica lo siguiente:

- 🔐 **Acceso remoto habilitado en los equipos**
  - **Preferencia: SSH (puerto 22)** por seguridad.
  - **Telnet (puerto 23)** solo para equipos **legacy** que no soporten SSH (no recomendado, usar únicamente si es necesario).
- 🌐 **Conectividad de red**
  - Desde el servidor de LinkWich-Monitor debe haber acceso hacia los equipos por el protocolo configurado.
- 🧱 **Firewall / reglas de red**
  - Permite el tráfico desde el servidor de LinkWich-Monitor hacia los equipos en:
    - **TCP/22** (SSH) ✅ recomendado
    - **TCP/23** (Telnet) ⚠️ solo legacy
  - Si tu red usa ACLs por VLAN o firewalls internos, valida que **no se bloquee** el acceso de administración.
- 👤 **Credenciales correctas**
  - El usuario debe tener permisos suficientes para ejecutar comandos de lectura de configuración (por ejemplo, `show running-config` o equivalente).

> 💡 Tip: Si la seguridad es prioridad, habilita solo SSH, limita acceso por IP (ACL) y usa usuarios con permisos mínimos necesarios.

---

## 1️⃣ Respaldos manuales

### ▶️ Respaldar todos
En **Respaldos → Opciones de Respaldo**, haz clic en **Respaldar Todos**.

El sistema ejecutará el backup de cada dispositivo registrado con **SSH/Telnet habilitado** y correctamente configurado.

En la tabla verás el resultado por equipo:

- ✅ **Éxito:** archivo generado y ruta donde quedó guardado.
- ❌ **Error:** se mostrará el motivo (credenciales, conectividad, protocolo, permisos, etc.).

---

### ✅ Respaldar seleccionados
1. Marca la casilla de los dispositivos a respaldar.
2. Pulsa **Respaldar Seleccionados**.
3. Revisa la columna **Detalle del Respaldo** para confirmar el resultado.

💡 Tip: Usa el buscador (arriba a la derecha) para filtrar por **nombre** o **IP**.

---

## 2️⃣ Descargar y revisar respaldos

### ⬇️ Descargar
En **Respaldos → Descargar**, verás la lista de archivos con:

- **Nombre**
- **Fecha**
- **Tamaño**
- **Acciones**

Acciones disponibles:

- 👁 **Vista previa:** abre el archivo en pantalla.
- ☁ **Descargar:** baja el respaldo en formato `.txt`.
- 🗜 **Descargar Todos en ZIP:** empaqueta todo lo listado.

---

### 👀 Vista previa
Útil para validar rápidamente que el archivo contenga la configuración completa (hostnames, interfaces, SNMP, rutas, VLANs, reglas, etc.).

---

## 3️⃣ Programar rutinas de respaldo

### 🗓 Nueva programación
En **Respaldos → Ver Programaciones**, pulsa **Nueva Programación**.

Completa:

- **Descripción** (ej. *Respaldos diarios 02:00*).
- **Frecuencia:** Diaria / Semanal / Mensual.
- **Hora:** define la hora de ejecución.
- **¿Qué switches respaldar?:** selecciona equipos (si no marcas ninguno, respalda todos).
- *(Opcional)* **Enviar correo al finalizar.**

Guarda la programación.

---

### 🛠 Editar programación
Desde la lista, edita para ajustar **frecuencia**, **hora**, **día del mes** (si es mensual) y los equipos incluidos.

💡 Recomendación: Programa los respaldos **fuera del horario laboral** para evitar saturación y reducir impacto.

---

## 4️⃣ Subida automática a Google Drive

### ☁ Configurar Drive
1. Abre **Respaldos → Ajustes Drive**.
2. Activa **Subida automática a Drive**.
3. En **Folder ID** pega el ID de la carpeta de tu Google Drive  
   (lo obtienes de la URL del folder: `https://drive.google.com/drive/folders/<ESTE_ID>`).
4. Sube el archivo **`client_secret.json`** de tu proyecto  
   (Google Cloud → OAuth 2.0 Client IDs, tipo **Desktop App**).
5. Pulsa **Guardar cambios**.

---

### 🔐 Autorizar cuenta
1. Haz clic en **Autorizar cuenta**.
2. Presiona **Abrir Google Auth**, inicia sesión y permite los accesos.
3. Copia el código (o URL completa) que te da Google y pégalo en el campo.
4. Pulsa **Validar**.
5. Usa **Verificar estado** para confirmar que el token quedó guardado.

💡 Importante:
- En Google Cloud, configura la pantalla de consentimiento y publica la app (para evitar caducidades innecesarias).
- Crea la credencial como **Desktop App** y solicita el token con acceso **offline**.

---

## 5️⃣ Qué significan algunos mensajes

### “Error al subir a Drive: No refresh_token found. Please set access_type of OAuth to offline.”
➜ Repite la autorización asegurando que el flujo OAuth pida `access_type=offline` (credencial **Desktop App** y app publicada).

---

### “telnet” o error de conexión
➜ Verifica:
- Que el dispositivo tenga **SSH (22) o Telnet (23)** habilitado.
- Que la IP sea alcanzable desde el servidor.
- Que las credenciales sean correctas.
- Que en el alta del equipo esté marcada la opción **Usar SSH** cuando aplique.
- Que el **firewall/ACL** no esté bloqueando el puerto.

---

### No se genera archivo
➜ Confirma:
- Que el driver/marca del equipo sea el correcto.
- Que el usuario tenga permisos para **mostrar** la configuración.
- Que el equipo acepte el comando esperado (según marca/modelo/OS).

---

## 6️⃣ Buenas prácticas

- Realiza al menos **un respaldo completo semanal** y **uno diario** de equipos críticos.
- Habilita **notificación por correo** en las rutinas programadas.
- Mantén una copia externa (Drive) y descarga periódicamente un **ZIP** como respaldo adicional.
- Comprueba al azar algunos archivos con **Vista previa** para validar que estén completos.
- Cambios importantes en la red → **Respaldar Ahora**.
- 🔐 **Seguridad recomendada:** prioriza **SSH**, limita acceso por IP (ACL) y evita Telnet salvo necesidad.

---

## 7️⃣ Resumen rápido (checklist)

- [ ] ¿SSH (22) habilitado en los equipos? *(recomendado)*  
- [ ] ¿Telnet (23) solo si es necesario para legacy?  
- [ ] ¿Firewall/ACL permite el acceso desde LinkWich-Monitor?  
- [ ] ¿Credenciales correctas en el inventario?  
- [ ] ¿Programación creada (frecuencia y hora)?  
- [ ] ¿Google Drive configurado y autorizado (token válido)?  
- [ ] ¿Respaldo descargable/visualizable en “Descargar”?  

---
