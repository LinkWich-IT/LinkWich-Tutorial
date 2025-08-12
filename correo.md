# 📧 **Manual de Configuración de Correo en LinkWich-Monitor**

El sistema **LinkWich-Monitor** permite **enviar notificaciones y alertas por correo electrónico** de forma automática.  
Para que esta función funcione correctamente, es necesario **configurar un servidor SMTP**.

---

## 1️⃣ **Acceder a la Configuración de Correo**

1. En el menú lateral, ve a:  
   **`Configuración del sistema → Correo de Envío`**  
2. Se abrirá el formulario donde podrás ingresar los datos de tu servidor de correo.

---

## 2️⃣ **Ejemplo de configuración con Gmail**

### 🔹 **Paso 1 – Activar la verificación en dos pasos**
- Ingresa a tu cuenta de **Google**.
- Habilita la **verificación en dos pasos**.  
  *(Es necesaria para poder generar una contraseña de aplicación).*

---

### 🔹 **Paso 2 – Generar una contraseña de aplicación**
1. En tu cuenta de Google, ve a:  
   **`Seguridad → Contraseñas de aplicación`**  
2. Selecciona:
   - **Aplicación:** Correo
   - **Dispositivo:** Otro *(escribe “LinkWich-Monitor”)*
3. Google generará una **contraseña especial de 16 caracteres**.

---

### 🔹 **Paso 3 – Llenar los campos en LinkWich-Monitor**
Completa el formulario con la siguiente información:

| **Campo**                           | **Valor ejemplo**                                       |
|--------------------------------------|---------------------------------------------------------|
| **Correo Remitente**                | `app.manager.network@gmail.com` *(tu correo de Gmail)*  |
| **Contraseña**                      | La **contraseña de aplicación** generada en Google      |
| **Servidor SMTP**                   | `smtp.gmail.com`                                        |
| **Puerto SMTP**                     | `587` *(TLS)* o `465` *(SSL)*                           |
| **Correo de Destino para Prueba**   | *(Opcional)* Cualquier correo válido para probar el envío |

---

### 🔹 **Paso 4 – Guardar y probar**
- Pulsa **"Guardar Configuración"**.
- Luego presiona **"Probar Envío de Correo"** para verificar que todo funciona correctamente.

---

## 3️⃣ **Configuración con otros proveedores**

Si usas otro proveedor de correo, solicita los **datos SMTP** a tu servicio.  
Algunos ejemplos comunes:

| **Proveedor**          | **Servidor SMTP**         | **Puerto** | **Seguridad** |
|------------------------|---------------------------|------------|---------------|
| Outlook / Office 365   | `smtp.office365.com`      | 587        | TLS           |
| Yahoo Mail             | `smtp.mail.yahoo.com`     | 465        | SSL           |
| Zoho Mail              | `smtp.zoho.com`           | 587        | TLS           |
| Servidor propio        | `mail.midominio.com`      | 465/587    | SSL/TLS       |

**Importante:**  
Si usas un servidor propio:
- Asegúrate de que el **puerto SMTP** esté abierto.
- Configura correctamente los registros **SPF/DKIM/DMARC** de tu dominio para evitar bloqueos.

---

## 4️⃣ **Gestión de destinatarios**

1. En el menú lateral, ve a **`Destinatarios de Correo`**.
2. Agrega las direcciones que recibirán las notificaciones.
3. Usa el interruptor para **activar o desactivar** la recepción.
4. **Botón "Asignar a todos"** → Todos los dispositivos enviarán alertas a ese destinatario.  
   *(O asigna de forma individual a cada dispositivo).*

---

## 5️⃣ **Recomendaciones de uso**

💡 **Buenas prácticas:**
- 📉 Limita el número de destinatarios para evitar bloqueos por envío masivo.
- 🔒 Usa **contraseñas de aplicación**, nunca la contraseña principal.
- ✅ Realiza **pruebas periódicas** para confirmar que el envío funciona.
- 📬 Si notas que no llegan los correos, revisa la **carpeta de spam** o los registros SMTP.

---
