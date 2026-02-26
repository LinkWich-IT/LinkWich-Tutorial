# 📲 **Manual de Configuración de WhatsApp – LinkWich-Monitor**

Esta función permite **enviar alertas y notificaciones** directamente a contactos o grupos de WhatsApp desde **LinkWich-Monitor**.

---

## 1️⃣ **Vinculación del bot con tu cuenta de WhatsApp**

1. Ve a: **`Configuración de Alertas → WhatsApp`**
2. Si el bot **no está vinculado**:
   - Pulsa **"Mostrar QR"**.
   - Escanea el código QR desde tu teléfono:
     **`WhatsApp → Menú (⋮) → Dispositivos vinculados → Vincular dispositivo`**
   - Una vez vinculado, el QR desaparecerá y verás el estado:
     **`Vinculado a [número] ([nombre del dispositivo])`**
3. Si el bot **ya está vinculado**:
   - No se mostrará el QR.
   - Para cambiar de cuenta → pulsa **"Cerrar sesión"** y repite el proceso.

---

## 2️⃣ **Requisitos para que el envío funcione siempre**

Para que LinkWich-Monitor pueda enviar alertas por WhatsApp de forma continua:

- 📱 **El teléfono vinculado** debe estar:
  - **Encendido**
  - Con **internet activo** (Wi-Fi o datos móviles)
- 🌐 El **servidor/equipo** donde está instalado **LinkWich-Monitor** debe tener:
  - **Salida a internet**
  - El servicio de WhatsApp activo (bot en ejecución)

📌 Si el teléfono o el servidor se apagan o pierden internet, **las notificaciones no podrán enviarse en ese momento**.  
Al restablecerse, el sistema retoma su operación normal.

---

## 3️⃣ **Agregar destinatarios**

En **`Agregar Destinatarios`** puedes configurar **números individuales o grupos**.

📌 **Para grupos:** el número vinculado (bot) debe ser **miembro del grupo** antes de enviar mensajes.

**Campos a llenar:**
- **Número:** Formato internacional *(Ej: `521XXXXXXXXXX` para México)*.
- **Descripción:** *(Opcional)* para identificarlo en la lista.
- Pulsa **"Agregar"** para guardar.

💡 **Recomendación de uso (operación clara y ordenada):**
- Preferir **un solo grupo** que incluya a todos los contactos.
- Mantener la lista de destinatarios **simple** para facilitar administración y trazabilidad.

---

## 4️⃣ **Asignación de alertas**

En la parte inferior encontrarás la lista de dispositivos:

- **WhatsApp activado** *(toggle verde)* → Ese dispositivo enviará alertas al destino configurado.
- **Botón "Asignar a todos"** → Activa WhatsApp para todos los dispositivos.
- **Botón "Quitar a todos"** → Desactiva WhatsApp en masa.

---

## 5️⃣ **Errores comunes y soluciones**

| **Error / Mensaje**     | **Causa probable**                       | **Solución recomendada**                              |
|-------------------------|------------------------------------------|-------------------------------------------------------|
| QR no disponible        | El bot ya está vinculado                 | Cerrar sesión y volver a vincular                     |
| No se cargan los grupos | WhatsApp Web tarda en responder          | Esperar unos segundos y refrescar la página           |
| Error `localhost:3000`  | El servicio del bot está detenido        | Reiniciar el servicio del bot en el servidor          |
| Falla de envío a grupo  | El bot no es miembro del grupo           | Agregar el número del bot al grupo y reiniciar sesión |
| No llegan mensajes      | Teléfono/servidor sin internet o apagado | Verificar que ambos estén encendidos y con internet   |

---

## 6️⃣ **Buenas prácticas recomendadas**

Para una experiencia más estable y ordenada:

- ✅ Usar un **número dedicado** para el sistema (solo alertas).
- ✅ Mantener ese teléfono **siempre encendido** y con **Wi-Fi/datos activos**.
- ✅ Evitar estar cambiando frecuentemente el dispositivo vinculado.
- ✅ Centralizar alertas en **un grupo** (cuando aplique), para que todos las reciban.

📌 **Nota:** Si vinculas tu número personal, las alertas **sí llegarán**, pero es más cómodo y claro para operación usar un número dedicado al monitoreo.

---

## 7️⃣ **Actualizaciones y mantenimiento (transparencia del servicio)**

El envío por WhatsApp se realiza mediante un **módulo de integración (WhatsApp Web)**, el cual puede requerir ajustes con el tiempo.

Por ello, cuando existan **actualizaciones de LinkWich-Monitor** o del **módulo de WhatsApp**, en algunos casos puede ser necesario:
- 🔄 **Actualizar el conector** (módulo/código)
- 🔁 **Re-vincular la cuenta** escaneando el QR nuevamente

✅ Esto forma parte del **soporte incluido en la licencia**, y te apoyamos para mantenerlo funcionando correctamente.

---

## 8️⃣ **Aviso importante sobre servicio de terceros**

Las notificaciones por WhatsApp dependen de una **plataforma de terceros** (WhatsApp/WhatsApp Web) y de factores externos como:
- disponibilidad del servicio,
- cambios técnicos en la plataforma,
- conectividad a internet,
- políticas/actualizaciones del proveedor.
- políticas/actualizaciones de WhatsApp.

📌 Por lo anterior, **pueden presentarse interrupciones o fallas sin previo aviso** que estén fuera del control directo de LinkWich-Monitor o del integrador.

✅ En caso de presentarse alguna incidencia, nuestro compromiso es:
- **diagnosticar** la causa,
- **aplicar ajustes/actualizaciones** cuando sea necesario,
- y **restablecer** el servicio a la brevedad posible dentro del alcance de soporte contratado.

💡 **Recomendación:** Para alertas críticas, se sugiere mantener un canal alterno de notificación (por ejemplo, correo electrónico) como respaldo.
