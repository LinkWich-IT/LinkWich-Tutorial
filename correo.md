📧 Manual de Configuración de Correo en LinkWich-Monitor
El sistema LinkWich-Monitor permite enviar notificaciones y alertas por correo electrónico de forma automática.
Para que esta función funcione correctamente, es necesario configurar un servidor SMTP.

1️⃣ Acceder a la Configuración de Correo
Ve al menú lateral y selecciona:

css
Copiar
Editar
Configuración del sistema → Correo de Envío
Se abrirá el formulario donde podrás ingresar los datos de tu servidor de correo.

2️⃣ Ejemplo de configuración con Gmail
Para usar Gmail como servidor de envío, sigue estos pasos:

Paso 1 – Activar la verificación en dos pasos en tu cuenta de Google
Ingresa a tu cuenta de Google y habilita la verificación en dos pasos.

Esto es necesario para generar una contraseña de aplicación.

Paso 2 – Generar una contraseña de aplicación
En tu cuenta de Google, ve a:

csharp
Copiar
Editar
Seguridad → Contraseñas de aplicación
Selecciona Aplicación: Correo y Dispositivo: Otro (escribe “LinkWich-Monitor”).

Google generará una contraseña especial de 16 caracteres.

Paso 3 – Llenar los campos en LinkWich-Monitor
En el formulario, ingresa:

Campo	Valor ejemplo
Correo Remitente	app.manager.network@gmail.com (tu correo de Gmail)
Contraseña	La contraseña de aplicación generada en Google
Servidor SMTP	smtp.gmail.com
Puerto SMTP	587 (TLS) o 465 (SSL)
Correo de Destino para Prueba (opcional)	Un correo válido para probar el envío (puede ser el mismo remitente)

Paso 4 – Guardar y probar
Haz clic en Guardar Configuración.

Luego presiona Probar Envío de Correo para verificar que todo funciona.

3️⃣ Configuración con otros proveedores
Si usas otro proveedor de correo, debes obtener los datos SMTP que te proporcione tu servicio (pueden variar según el dominio y configuración).

Ejemplos comunes:

Proveedor	Servidor SMTP	Puerto	Seguridad
Outlook / Office 365	smtp.office365.com	587	TLS
Yahoo Mail	smtp.mail.yahoo.com	465	SSL
Zoho Mail	smtp.zoho.com	587	TLS
Servidor propio	mail.midominio.com	465/587	SSL/TLS

Importante: Si usas un servidor propio, asegúrate de que:

El puerto SMTP esté abierto.

Tu dominio tenga registros SPF/DKIM/DMARC configurados para evitar bloqueos.

4️⃣ Gestión de destinatarios
Una vez configurado el correo:

Ve a Destinatarios de Correo en el menú.

Agrega las direcciones que recibirán las notificaciones.

Activa o desactiva la recepción con el interruptor de estado.

Usa el botón Asignar a todos para que todos los dispositivos envíen alertas a ese destinatario, o asigna individualmente.

5️⃣ Recomendaciones de uso
Limita el número de destinatarios para evitar que el proveedor bloquee el envío masivo.

Usa siempre contraseñas de aplicación en lugar de la contraseña principal.

Realiza pruebas periódicas para asegurar que las notificaciones siguen funcionando.
