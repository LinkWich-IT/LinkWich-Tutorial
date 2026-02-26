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

## 4️⃣ Subida automática a Google Drive (paso a paso, sin pierde)

> Objetivo: que LinkWich-Monitor pueda **subir automáticamente** tus respaldos a una carpeta específica de Drive.  
> Esto se logra creando un **Proyecto en Google Cloud**, habilitando **Google Drive API** y generando un **OAuth Client (Desktop app)**.

---

### 4.1 Crear/seleccionar tu Proyecto en Google Cloud
1. Abre la consola de Google Cloud: `https://console.cloud.google.com/`
2. En la parte superior, selecciona tu **Proyecto** (o crea uno nuevo).

> 💡 Recomendación: usa un proyecto dedicado, por ejemplo: **LinkWich-Monitor-Drive**.

---

### 4.2 Habilitar **Google Drive API**
1. En la consola, ve al menú: **APIs & Services → Library**  
2. En el buscador escribe: **Google Drive API**  
3. Entra a **Google Drive API** y pulsa **Enable**.

✅ Listo: tu proyecto ya puede usar Drive vía API.

---

### 4.3 Configurar la pantalla de consentimiento (Google Auth platform)
Google ha agrupado la configuración OAuth en **Google Auth platform**.

1. En Google Cloud Console ve a: **Google Auth platform → Branding**
   - **App name**: escribe un nombre (ej. *LinkWich-Monitor Backups*)
   - **User support email**: selecciona tu correo
   - (Opcional) agrega logo y datos de soporte si aplica

2. Luego ve a: **Google Auth platform → Audience**
   - Selecciona el tipo de audiencia:
     - **Internal** (si usas Google Workspace y todos son de tu dominio), o
     - **External** (si autorizas con cuentas Gmail normales)
   - Si está en modo de prueba, agrega tu correo en **Test users**

3. Después ve a: **Google Auth platform → Data Access**
   - Agrega el acceso requerido para Drive (scopes).  
   - Si tu asistente/soporte te dio un scope específico, usa ese.  
   - Para respaldo a Drive normalmente se usa alcance de **Google Drive**.

4. Finalmente, deja la app en **Producción** cuando ya esté lista.  
   - Esto evita comportamientos limitados del modo “Testing” en algunos casos.

---

### 4.4 Crear credenciales OAuth (Desktop App) y descargar `client_secret.json`
1. Ve a: **Google Auth platform → Clients**
2. Pulsa **Create Client**
3. En **Application type** elige: **Desktop app**
4. Asigna un nombre (ej. *LinkWich-Monitor Desktop OAuth*)
5. Pulsa **Create**
6. Descarga el **JSON** del cliente (archivo tipo `client_secret_XXXX.json`) y guárdalo.

📌 Ese archivo es el que vas a subir en LinkWich-Monitor como **`client_secret.json`**.

> Nota: si tu consola aún muestra el menú clásico, puede aparecer como: **APIs & Services → Credentials → Create Credentials → OAuth client ID → Desktop app**.

---

### 4.5 Configurar Drive dentro de LinkWich-Monitor
1. Abre **Respaldos → Ajustes Drive**
2. Activa **Subida automática a Drive**
3. En **Folder ID** pega el ID de la carpeta destino.

   - Abre tu carpeta en Drive y copia el ID de la URL:  
     `https://drive.google.com/drive/folders/<ESTE_ID>`

4. Sube el archivo **`client_secret.json`** (tu credencial OAuth descargada).
5. Pulsa **Guardar cambios**.

---

### 4.6 Autorizar la cuenta (vincular Drive)
1. Haz clic en **Autorizar cuenta**
2. Presiona **Abrir Google Auth**
3. Se abrirá la página de Google para iniciar sesión y autorizar permisos.

✅ **Recomendación para que no haya errores por sesión/cookies**
- Abre el enlace en una **ventana de incógnito**.
- Inicia sesión **solo** con la cuenta de Google que será dueña de la carpeta en Drive.

Si Google te abre una cuenta equivocada o no te pide permisos:
- Opción 1 (más fácil): usa incógnito / otro perfil de navegador.
- Opción 2 (limpieza): borra cookies/sesión de Google y vuelve a intentar.
  - En Chrome puedes ir a: `chrome://settings/siteData`
  - Busca y elimina datos de sitios como `accounts.google.com`, `myaccount.google.com` y `google.com`
  - Cierra y abre el navegador y repite la autorización

4. Acepta permisos en la pantalla de Google.
5. Copia el **código** (o la **URL completa** si eso es lo que te muestra) y pégalo en LinkWich-Monitor.
6. Pulsa **Validar**.
7. Pulsa **Verificar estado** para confirmar que el token quedó guardado correctamente.

---

### 4.7 Probar la subida a Drive
- Pulsa **Respaldar ahora** o espera a la próxima **tarea programada**.
- En la consola/verificador del sistema verás algo como: **✅ Subido a Drive (id=...)**
- El archivo aparecerá dentro de la carpeta configurada.

📌 **Renovación de tokens (cómo funciona)**
- El **access token** se renueva automáticamente.
- El **refresh token** normalmente se mantiene, pero puede dejar de funcionar si:
  - se revoca el acceso manualmente,
  - se cambian políticas/cuenta,
  - o pasan largos periodos sin usarse (por ejemplo > 6 meses sin uso, dependiendo del caso).

---

### 4.8 Verificar estado y cómo recuperar si falla
Pulsa **Verificar estado** para comprobar que el token **puede refrescarse**.

Si falla, aplica esta ruta en orden:

1. Quita el acceso de la app desde tu cuenta Google:
   - Abre: `https://myaccount.google.com/permissions`
   - Busca tu app (ej. *LinkWich-Monitor Backups*) y pulsa **Quitar acceso**

2. Regresa a Google Cloud y confirma:
   - Que **Google Drive API** está habilitada (ver **4.2**)
   - Que la app está en **Producción** (ver **4.3**)
   - Que el cliente OAuth es **Desktop app** (ver **4.4**)

3. Regresa a LinkWich-Monitor y repite:
   - **Autorizar cuenta** → **Abrir Google Auth**
   - Asegúrate de aceptar permisos (en ocasiones se fuerza un consentimiento nuevo con `prompt=consent`)

✅ Al final, usa **Verificar estado** nuevamente hasta que confirme OK.

---

## 5️⃣ Qué significan algunos mensajes

### “Error al subir a Drive: No refresh_token found. Please set access_type of OAuth to offline.”
➜ Repite la autorización asegurando que el flujo OAuth solicite acceso **offline** (credencial **Desktop App** y consentimiento completo).

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
- [ ] ¿Google Drive API habilitada?
- [ ] ¿OAuth configurado (Branding/Audience/Data Access/Clients)?
- [ ] ¿Drive configurado y autorizado (token válido)?
- [ ] ¿Respaldo descargable/visualizable en “Descargar”?

---

