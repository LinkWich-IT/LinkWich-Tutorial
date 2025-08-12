## **🔁 Respaldos de Dispositivos – LinkWich-Monitor**
Esta sección permite **respaldar la configuración** de tus equipos (switches/routers), **descargar** los archivos generados y **programar** copias automáticas.  
También puedes **subirlos a Google Drive** de forma segura.

---

## **1️⃣ Respaldos manuales**
### ▶️ **Respaldar todos**
En **Respaldos → Opciones de Respaldo**, haz clic en **Respaldar Todos**.

El sistema ejecutará el backup de **cada dispositivo** registrado con **SSH/Telnet habilitado**.

En la tabla verás el **resultado** por equipo:
- ✅ **Éxito**: archivo generado y ruta donde quedó guardado.
- ❌ **Error**: se mostrará el motivo (credenciales, protocolo, etc.).

### ✅ **Respaldar seleccionados**
- Marca la casilla de los dispositivos a respaldar.
- Pulsa **Respaldar Seleccionados**.
- Revisa la columna **Detalle del Respaldo** para confirmar el resultado.

💡 **Tip:** Usa el buscador (arriba a la derecha) para filtrar por **nombre o IP**.

---

## **2️⃣ Descargar y revisar respaldos**
### ⬇️ **Descargar**
En **Respaldos → Descargar**, verás la lista de archivos con:
- **Nombre**
- **Fecha**
- **Tamaño**
- **Acciones**

Acciones disponibles:
- 👁 **Vista previa**: abre el archivo en pantalla.
- ☁ **Descargar**: baja el respaldo en formato `.txt`.
- 🗜 **Descargar Todos en ZIP**: empaqueta todo lo listado.

### 👀 **Vista previa**
Útil para validar rápidamente que el archivo contenga la **configuración completa** (hostnames, interfaces, SNMP, rutas, etc.).

---

## **3️⃣ Programar rutinas de respaldo**
### 🗓 **Nueva programación**
En **Respaldos → Ver Programaciones**, pulsa **Nueva Programación**.

Completa:
- **Descripción** (ej. *Respaldos diarios 02:00*).
- **Frecuencia**: *Diaria / Semanal / Mensual*.
- **Hora**: define la hora de ejecución.
- **¿Qué switches respaldar?**: selecciona equipos (si no marcas ninguno, respalda **todos**).
- (Opcional) **Enviar correo al finalizar**.

Guarda la programación.

### 🛠 **Editar programación**
Desde la lista, edita para ajustar **frecuencia**, **hora**, **día del mes** (si es mensual) y los **equipos** incluidos.

💡 **Recomendación:** Programa los respaldos **fuera del horario laboral** para evitar saturación.

---

## **4️⃣ Subida automática a Google Drive**
### ☁ **Configurar Drive**
1. Abre **Respaldos → Ajustes Drive**.
2. Activa **Subida automática a Drive**.
3. En **Folder ID** pega el ID de la carpeta de tu Google Drive  
   (lo obtienes de la URL del folder: `https://drive.google.com/drive/folders/<ESTE_ID>`).
4. Sube el **client_secret.json** de tu proyecto (Google Cloud → **OAuth 2.0 Client IDs**, tipo **Desktop App**).
5. Pulsa **Guardar cambios**.

### 🔐 **Autorizar cuenta**
1. Haz clic en **Autorizar cuenta**.
2. Presiona **Abrir Google Auth**, inicia sesión y **permite los accesos**.
3. Copia el **código** (o URL completa) que te da Google y pégalo en el campo.
4. Pulsa **Validar**.
5. Usa **Verificar estado** para confirmar que el **token** quedó guardado.

💡 **Importante:**  
En Google Cloud, configura el consentimiento y **publica la app** (para quitar la caducidad de 7 días).  
Crea la credencial como **“Desktop App”** y solicita el token con acceso **offline**.

---

## **5️⃣ Qué significan algunos mensajes**
- **“Error al subir a Drive: No refresh_token found. Please set access_type of OAuth to offline.”**  
  ➜ Repite la autorización asegurando que el flujo OAuth pida **access_type=offline** (credencial **Desktop App**, app **publicada**).

- **“telnet” o error de conexión**  
  ➜ Verifica que el dispositivo tenga **SSH/Telnet habilitado**, IP alcanzable, **credenciales correctas** y que en el alta del equipo esté marcada la opción **Usar SSH**.

- **No se genera archivo**  
  ➜ Confirma que el **driver/marca** del equipo sea el correcto y que el usuario tenga permisos para **mostrar la configuración**.

---

## **6️⃣ Buenas prácticas**
- Realiza al menos **un respaldo completo semanal** y **uno diario** de equipos críticos.  
- Habilita **notificación por correo** en las rutinas programadas.  
- Mantén una **copia externa** (Drive) y descarga periódicamente un **ZIP** como respaldo adicional.  
- Comprueba al azar algunos archivos con **Vista previa** para validar que estén **completos**.  
- Cambios importantes en la red → **Respaldar Ahora**.

---

## **7️⃣ Resumen rápido (checklist)**
- [ ] ¿SSH/Telnet habilitado en los equipos?  
- [ ] ¿Credenciales correctas en el inventario?  
- [ ] ¿Programación creada (frecuencia y hora)?  
- [ ] ¿Google Drive configurado y autorizado (token válido)?  
- [ ] ¿Respaldo descargable/visualizable en “Descargar”?  

---
