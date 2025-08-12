# 👥 **Manual de Gestión de Usuarios y Roles – LinkWich-Monitor**

En **LinkWich-Monitor** puedes crear usuarios con distintos niveles de permisos para controlar el acceso y las acciones dentro del sistema.  
Esto permite mantener la seguridad y evitar cambios no autorizados.

---

## 1️⃣ **Acceder a la Gestión de Usuarios**

1. Desde el **menú lateral**, selecciona **Configuración de Usuarios**.  
2. Se abrirá la lista de usuarios existentes, mostrando:
   - **Nombre de usuario**
   - **Correo electrónico** (si aplica)
   - **Rol asignado**
   - **Estado** (activo/inactivo)
   - **Fecha de creación**

---

## 2️⃣ **Agregar un nuevo usuario**

1. Pulsa el botón **➕ Agregar Usuario**.  
2. Completa el formulario:
   - **Nombre de usuario** → Identificador único para iniciar sesión.  
   - **Correo electrónico** (opcional) → Usado para notificaciones y recuperación.  
   - **Contraseña** → Se recomienda una contraseña segura.  
   - **Rol** → Selecciona el tipo de acceso (ver siguiente sección).  
   - **Estado** → Activo (puede iniciar sesión) o Inactivo (acceso bloqueado).  
   - **Fecha de vigencia** (opcional) → Fecha límite para que la cuenta pueda iniciar sesión.  
3. Haz clic en **Guardar** para crear el usuario.

💡 **Tip:** Si el sistema tiene habilitado **2FA**, podrás activarlo desde la edición del usuario una vez creado.

---

## 3️⃣ **Tipos de Roles y Permisos**

En **LinkWich-Monitor** existen tres roles principales:

### 🔍 **Visitante**
- **Acceso:** Solo puede visualizar información.  
- **Restricciones:**
  - No puede agregar, modificar o eliminar dispositivos, alertas ni configuraciones.
  - No puede acceder a la configuración del sistema.
- **Uso típico:** Personal de consulta, clientes que solo requieren ver el estado de su red.

### ⚙️ **Administrador**
- **Acceso:** Puede agregar, modificar y eliminar datos.  
- **Permisos:**
  - Gestión completa de dispositivos, alertas, backups, mapas y reportes.
  - Puede agregar o eliminar usuarios, pero solo con rol **Visitante** o **Administrador**.
- **Restricciones:**
  - No puede modificar ni eliminar usuarios con rol **Super Admin**.
  - No puede acceder a configuraciones críticas reservadas al **Super Admin**.
- **Uso típico:** Personal de TI encargado de la operación y mantenimiento del sistema.

### 🛡 **Super Admin**
- **Acceso total:** Puede realizar cualquier acción sin restricciones.  
- **Permisos:**
  - Gestión total de usuarios, incluyendo otros **Super Admin**.
  - Acceso a configuraciones críticas del sistema.
  - Control completo sobre dispositivos, alertas, roles y permisos.
- **Uso típico:** Propietario del sistema o responsable máximo de seguridad.

---

## 4️⃣ **Editar o eliminar usuarios**

- **Editar:** Pulsa el botón ✏️ junto al usuario, realiza los cambios necesarios y guarda.  
- **Eliminar:** Pulsa el icono 🗑 y confirma la eliminación.  

⚠️ **Nota:** No se puede eliminar al usuario con el que estás actualmente conectado si es el único **Super Admin**.

---

## 5️⃣ **Buenas prácticas de gestión de usuarios**

- Usa roles mínimos necesarios para cada usuario.  
- Mantén inactivos los usuarios que no se usen temporalmente en lugar de eliminarlos.  
- Cambia contraseñas periódicamente.  
- Habilita **2FA** en cuentas con permisos de administrador y superiores.  
- Mantén un registro de auditoría para rastrear acciones críticas.  

---

# 🔐 **Manual de Configuración de 2FA (Autenticación en Dos Pasos) – LinkWich-Monitor**

La autenticación en dos pasos (**2FA**) añade una capa extra de seguridad a tu cuenta.  
Con **2FA**, para iniciar sesión necesitarás tu usuario y contraseña **más un código temporal** generado en una app autenticadora como *Google Authenticator*, *Authy* o *Microsoft Authenticator*.

---

## 1️⃣ **Activar 2FA por primera vez**

1. Ingresa a **Configuración de Usuarios** desde el menú lateral.  
2. Edita el usuario al que deseas habilitarle **2FA**.  
3. Activa la opción **Habilitar 2FA**.  
4. Guarda los cambios.  
5. Se mostrará un **código QR** en pantalla.  
6. Escanea el código con tu app de autenticación:
   - Abre *Google Authenticator* o similar.
   - Pulsa **Agregar cuenta → Escanear código QR**.
   - Una vez agregado, tu app mostrará **códigos de 6 dígitos** que cambian cada 30 segundos.
7. En el próximo inicio de sesión, además de usuario y contraseña, se pedirá el **código 2FA**.

---

## 2️⃣ **Regeneración automática del código QR**

En algunas situaciones, el sistema invalida el código **2FA** anterior y genera uno nuevo por seguridad.  
Esto ocurre si:

- Cambias la contraseña del usuario.
- Modificas el estado de **Activo/Inactivo**.
- Cambias o expira la fecha de vigencia de la cuenta.
- Desactivas y vuelves a activar la opción **2FA**.

Cuando cualquiera de estas acciones se realice:

- El sistema creará un **nuevo código secreto**.
- Se generará un **nuevo QR** para escanear.
- Si hay un correo configurado, el QR se enviará al email del usuario.
- Si no hay correo configurado, el QR se mostrará en pantalla para agregarlo nuevamente.

---

## 3️⃣ **Desactivar 2FA**

1. Ve a **Configuración de Usuarios**.  
2. Edita el usuario y desactiva la opción **2FA**.  
3. Guarda los cambios.  

⚠️ **Advertencia:** Desactivar **2FA** reduce la seguridad de la cuenta, úsalo solo si es estrictamente necesario.

---

## 4️⃣ **Buenas prácticas de seguridad**

- Mantén siempre actualizada tu app de autenticación.
- Haz una copia de seguridad del código secreto o QR al momento de configurarlo.
- Si pierdes acceso a tu app de autenticación, contacta al administrador para regenerar el QR.
- No compartas tu código **2FA** con nadie.
