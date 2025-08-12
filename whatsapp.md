# 📲 **Manual de Configuración de WhatsApp – LinkWich-Monitor**

Esta función permite **enviar alertas y notificaciones** directamente a contactos o grupos de WhatsApp desde **LinkWich-Monitor**.

---

## 1️⃣ **Vinculación del bot con tu cuenta de WhatsApp**

1. Ve a: **`Configuración de Alertas → WhatsApp`**  
2. Si el bot **no está vinculado**:
   - Pulsa **"Mostrar QR"**.
   - Escanea el código QR con la cámara de WhatsApp en tu teléfono:  
     **`WhatsApp → Menú (⋮) → Dispositivos vinculados → Vincular dispositivo`**
   - Una vez vinculado, el QR desaparecerá y verás el estado:  
     **`Vinculado a [número] ([nombre del dispositivo])`**

3. Si el bot **ya está vinculado**:
   - No se mostrará el QR.
   - Para cambiar de cuenta → pulsa **"Cerrar sesión"** y repite el proceso.

---

## 2️⃣ **Agregar destinatarios**

En **`Agregar Destinatarios`** puedes configurar **números individuales o grupos**.

📌 **Para grupos:** El bot debe ser miembro del grupo antes de enviar mensajes.

**Campos a llenar:**
- **Número:** Formato internacional *(Ej: `521XXXXXXXXXX` para México)*.
- **Descripción:** *(Opcional)* para identificarlo en la lista.
- Pulsa **"Agregar"** para guardar.

💡 **Recomendación de uso:**
- Usar **máximo 3 destinatarios** para evitar bloqueos.
- Preferir **un solo grupo** que incluya a todos los contactos.

---

## 3️⃣ **Asignación de alertas**

En la parte inferior encontrarás la lista de dispositivos:

- **WhatsApp activado** *(toggle verde)* → Ese dispositivo enviará alertas al destino configurado.
- **Botón "Asignar a todos"** → Activa WhatsApp para todos los dispositivos.
- **Botón "Quitar a todos"** → Desactiva WhatsApp en masa.

---

## 4️⃣ **Errores comunes y soluciones**

| **Error / Mensaje**           | **Causa probable**                         | **Solución recomendada**                                  |
|--------------------------------|--------------------------------------------|-----------------------------------------------------------|
| QR no disponible               | El bot ya está vinculado                   | Cerrar sesión y volver a vincular                         |
| No se cargan los grupos        | WhatsApp Web no responde rápido            | Esperar unos segundos y refrescar la página               |
| Error `localhost:3000`         | El servicio del bot está detenido          | Reiniciar el servicio del bot en el servidor              |
| Falla de envío a grupo         | El bot no es miembro del grupo             | Agregar el número del bot al grupo y reiniciar sesión     |

---

## 5️⃣ **Políticas y buenas prácticas para evitar baneos**

⚠️ WhatsApp puede **suspender cuentas** si detecta actividad sospechosa.  
Para reducir riesgos:

- 🚫 No envíes mensajes masivos a números desconocidos.
- 🚫 Evita contenido que pueda considerarse **spam**.
- 📉 No envíes mensajes en exceso *(varios por minuto)*.
- 👥 Usa grupos para reducir el número de envíos.
- 📱 No cambies constantemente de dispositivo vinculado.

---

## 6️⃣ **Recomendaciones de mantenimiento**

🔍 **Revisión periódica:**
- Asegúrate de que el estado del bot sea **"Vinculado"**.
- Si cambias de teléfono → Cierra sesión y vincula el nuevo dispositivo.
- Realiza **pruebas mensuales de envío** para confirmar que todo sigue operativo.

---
