# 🤖 **Configuración de IA Local – GPT4All (LinkWich-Monitor)**

Esta guía muestra cómo **instalar GPT4All**, descargar un **modelo `.gguf`**, y configurarlo en **LinkWich-Monitor** para funciones como explicación de logs, textos, etc.

---

## 1️⃣ Requisitos

- **Windows 10/11** (también funciona en Windows Server).
- **CPU x64** (GPT4All corre en CPU; GPU opcional).
- **Espacio en disco:** 2–10 GB según el modelo.
- **RAM sugerida:** 8 GB mínimo (mejor con 16 GB+).

---

## 2️⃣ Instalar GPT4All (Desktop + CLI tools)

1. Descarga el instalador oficial: **[gpt4all.io](https://gpt4all.io/)** ➜ *Download for Windows*.  
2. Ejecuta el instalador y **marca “CLI tools”** durante la instalación.  
3. Al finalizar, se creará la carpeta (Windows):
> En esa carpeta se guardarán los modelos `.gguf`.


---

## 3️⃣ Descargar un modelo (.gguf)

Tienes dos opciones:

**A) Desde la app GPT4All**
1. Abre **GPT4All**.
2. Ve a **Model Explorer** y busca un modelo “**Instruct**”.
3. Pulsa **Download**.

**B) Descarga directa (avanzado)**
- Descarga el archivo `.gguf` del modelo elegido y colócalo dentro de:
- 
### Modelos recomendados (CPU)
| **Modelo**                                | **Tamaño aprox.** | **Uso típico**                         |
|-------------------------------------------|-------------------|----------------------------------------|
| `Phi-3-mini-4k-instruct.Q4_0.gguf`        | Pequeño           | Rápido, respuestas cortas y utilitarias|
| `Mistral-7B-Instruct.Q4_0.gguf`           | Mediano           | Equilibrio calidad/velocidad           |
| `Llama-3.1-8B-Instruct.Q4_0.gguf`         | Mediano–grande    | Mejor calidad, más RAM requerida       |

> **Nota sobre cuantización (Q2/Q3/Q4/Q5):** valores **más bajos** ⇒ más rápido/ligero, **menos** precisión; **Q4_0** es un buen punto de partida.

---

## 4️⃣ Configurar en LinkWich-Monitor

En **Ajustes → IA GPT4All**:

- **IA habilitada:** activar.  
- **Ruta del modelo:** carpeta donde están los `.gguf`, por ejemplo:

** C:\Users\manager\AppData\Local\nomic.ai\GPT4All

- **Nombre del modelo:** nombre **exacto** del archivo, p. ej.:
** Phi-3-mini-4k-instruct.Q4_0.gguf

- **# Máx tokens:** límite de salida (ej. `100`–`256` para respuestas cortas).

Pulsa **Guardar cambios** y luego **Recargar**.

---

## 5️⃣ Prueba rápida

1. Usa alguna función de IA (p. ej., explicación de logs en Syslog).  
2. Verifica que las respuestas se generen sin errores.  
3. Si falla, revisa que el **archivo** exista en la **ruta** configurada.

---

## 6️⃣ Solución de problemas

| **Problema**                               | **Causa**                                      | **Cómo resolver**                                                                 |
|-------------------------------------------|-----------------------------------------------|-----------------------------------------------------------------------------------|
| “Model file not found”                    | Ruta o nombre incorrectos                      | Copia el **path** desde el Explorador y pega el **nombre exacto** del `.gguf`.   |
| Respuestas muy lentas                     | Modelo grande / poca RAM                       | Prueba un modelo **Q4_0** menor (p. ej. `Phi-3-mini-4k-instruct.Q4_0.gguf`).     |
| Error de permisos al leer el archivo      | Carpeta protegida                              | Usa la ruta del **usuario** (AppData\Local\nomic.ai\GPT4All).                     |
| La app pide `libllmodel.dll` (al empaquetar) | Librería no usada en tu flujo                  | Tu implementación con `gpt4all` **no requiere** esa DLL; puedes **omitirla**.     |
| La app no “ve” el modelo                  | Modelo en carpeta distinta                     | Mueve el `.gguf` a la carpeta configurada o ajusta la ruta en ajustes.           |

---

## 7️⃣ Buenas prácticas

- Mantén **1–2 modelos** estables (evita tener muchos pesados).  
- Sube el **límite de tokens** solo cuando necesites respuestas largas.  
- Actualiza modelos periódicamente desde el **Model Explorer** de GPT4All.  
- Si usas portátiles, conecta a corriente: el CPU se estrangula en modo batería.

---

## 8️⃣ Campos de configuración (resumen)

| **Campo**          | **Ejemplo**                                                      | **Descripción**                                  |
|--------------------|------------------------------------------------------------------|--------------------------------------------------|
| IA habilitada      | Activado                                                         | Enciende la IA local                             |
| Ruta del modelo    | `C:\Users\manager\AppData\Local\nomic.ai\GPT4All`                | Carpeta donde residen los `.gguf`                |
| Nombre del modelo  | `Phi-3-mini-4k-instruct.Q4_0.gguf`                               | Archivo a cargar                                 |
| # Máx tokens       | `100`                                                            | Máximo de tokens de **salida** por respuesta     |

---

## 9️⃣ Referencias útiles

- Sitio oficial: **https://gpt4all.io/**  
- Preguntas frecuentes y modelos: dentro de la app **GPT4All → Model Explorer**.




