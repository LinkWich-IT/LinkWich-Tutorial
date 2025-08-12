
📲 Manual de Configuración de WhatsApp – LinkWich-Monitor
Esta sección permite enviar alertas y notificaciones directamente a contactos o grupos de WhatsApp desde LinkWich-Monitor.

1️⃣ Vinculación del bot con tu cuenta de WhatsApp
Accede a:

Copiar
Editar
Configuración de Alertas → WhatsApp
Si el bot no está vinculado:

Pulsa "Mostrar QR".

Escanea el código QR con la cámara de WhatsApp en tu teléfono:

scss
Copiar
Editar
WhatsApp → Menú (⋮) → Dispositivos vinculados → Vincular dispositivo
Una vez vinculado, el QR dejará de mostrarse y aparecerá el estado:

css
Copiar
Editar
Vinculado a [número] ([nombre del dispositivo])
Si el bot ya está vinculado:

El QR no se mostrará, solo verás el estado actual.

Si quieres cambiar de cuenta, pulsa "Cerrar sesión" y repite el proceso.

2️⃣ Agregar destinatarios
En la sección Agregar Destinatarios:

Elige si vas a agregar un Número individual o un Grupo.

Para grupos, el bot debe estar agregado como miembro del grupo antes de poder enviar mensajes.

Ingresa:

Número (en formato internacional, ej. 521XXXXXXXXXX para México).

Descripción (opcional, para identificarlo en la lista).

Pulsa "Agregar" para guardarlo.

💡 Recomendación:
WhatsApp puede limitar envíos masivos. Se sugiere:

Usar máximo 3 destinatarios.

Preferir un solo grupo que contenga a todos los destinatarios.

3️⃣ Asignación de alertas
En la parte inferior encontrarás la lista de dispositivos:

WhatsApp activado (toggle verde) → ese dispositivo enviará alertas al destino configurado.

Botón "Asignar a todos" para habilitar WhatsApp en todos los dispositivos.

Botón "Quitar a todos" para desactivar en masa.

4️⃣ Errores comunes y soluciones
Error / Mensaje	Causa probable	Solución recomendada
QR no disponible	El bot ya está vinculado.	Cerrar sesión y volver a vincular si es necesario.
No se cargan los grupos	WhatsApp Web no responde rápido.	Esperar unos segundos y refrescar la página.
Error localhost:3000	El servicio de bot está detenido.	Reiniciar el servicio del bot en el servidor.
Falla de envío a grupo	El bot no es miembro del grupo.	Agregar el número del bot al grupo y reiniciar sesión.

5️⃣ Políticas y buenas prácticas para evitar baneos en WhatsApp
No envíes mensajes masivos a números desconocidos.

Evita contenido que pueda ser marcado como spam.

No envíes mensajes excesivamente frecuentes (varios por minuto).

Usa grupos cuando sea posible para reducir el número de envíos.

No cambies constantemente de dispositivo vinculado.

Si WhatsApp detecta actividad sospechosa, puede suspender la cuenta temporal o permanentemente.

6️⃣ Recomendaciones de mantenimiento
Revisa periódicamente que el estado del bot esté "Vinculado".

Si cambias de teléfono, recuerda cerrar sesión en el bot y vincular con el nuevo dispositivo.

Haz pruebas mensuales de envío para confirmar que todo sigue operativo.
