# **🌐 NetPath – Monitores y Trazas de Red**

## **📌 ¿Qué es un Monitor NetPath?**
Un **Monitor NetPath** realiza **trazas periódicas** desde un dispositivo origen hacia un destino (**IP o FQDN**), registrando:
- Cada **salto intermedio** (*hop*).
- **Latencia promedio**.
- **Pérdida de paquetes**.

Esto permite **detectar problemas de conectividad** y **cambios en la topología de red**.

> **💡 Recomendación:** No utilices intervalos menores a **120 segundos**. Se sugiere un rango de **300 a 500 segundos** para que la traza pueda completarse hasta el destino sin sobrecargar la base de datos.

---

## **📋 Vista de Monitores**
En esta sección podrás ver todos los monitores configurados.  
La tabla incluye:
- **Origen** → Dispositivo que ejecuta la traza.
- **Destino** → IP o dominio.
- **Puerto** → Puerto de destino.
- **Intervalo (s)** → Frecuencia de ejecución.
- **Activo** → Estado del monitor.
- **Acciones** → Botones para editar, ver traza o eliminar.

**Ejemplo:**
![Monitores NetPath](monitores_netpath.png)

---

## **🖥 Vista de Traza**
Aquí se representa **gráficamente** la topología de red resultante de los traceroutes periódicos guardados en la base de datos.

Puedes:
- **Seleccionar rango** de fecha/hora y número de ejecuciones a mostrar.
- **Cambiar la orientación** del grafo.
- **Guardar o restablecer** el layout.
- **Ver detalles** de cada nodo o enlace con doble clic.

**Leyenda de colores:**
- 🟩 **Verde** → Latencia baja y sin pérdidas.
- 🟨 **Amarillo** → Latencia moderada.
- 🟥 **Rojo** → Latencia alta o pérdida de paquetes.

**Ejemplo:**
![Vista de Traza](vista_traza_netpath.png)

---

## **📊 Métricas de Latencia**
Debajo del grafo se muestra un gráfico de la **latencia promedio** en el tiempo, según las ejecuciones registradas.

Opciones:
- Filtrar por **últimos N registros** o por **rango de fechas**.
- Deslizar en la barra de tiempo para **acotar el periodo mostrado**.

**Ejemplo:**
![Gráfica de Latencia](grafica_latencia_netpath.png)

---

## **✅ Recomendaciones Finales**
- Utiliza intervalos amplios para no saturar la base de datos.
- Configura monitores hacia destinos **críticos** de tu infraestructura.
- Analiza cambios en la ruta para detectar problemas de conectividad.
