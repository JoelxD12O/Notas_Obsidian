## 🧠 Hacking Bootcamp S1 — _What’s a JPEG?_

### 📄 Resumen (páginas 1–40)

---

## 1️⃣ Introducción y objetivos

- El bootcamp trata sobre **archivos**, **formatos**, y cómo pueden ser **interpretados, manipulados y abusados**.
    
- Temas principales:
    
    - Comandos básicos de archivos
        
    - Formatos de archivo
        
    - Magic bytes
        
    - Metadatos
        
    - Archivos embebidos
        
    - Esteganografía (básica)
        
    - Sistemas de archivos y discos
        

---

## 2️⃣ Comandos básicos de archivos (Linux)

### 📁 `touch`

- Crea archivos vacíos.
    
- Modifica timestamps (fecha/hora).
    

### 📁 `cp`

- Copia archivos.
    
- `cp SRC DST`
    
- `cp SRC DIR/`
    
- `cp -r` → copia directorios de forma recursiva.
    

### 📁 `mv`

- Mueve o renombra archivos.
    
- `mv SRC DST`
    
- También sirve para mover a directorios.
    

### ❌ `rm`

- Elimina archivos.
    
- `rm -r` → elimina directorios completos.
    

---

## 3️⃣ Descarga y visualización de archivos

### 🌐 `curl`

- Descarga o consulta URLs.
    
- `curl URL`
    
- `curl -O URL` → guarda el archivo.
    

### 🌐 `wget`

- Similar a `curl -O`, más común para descargas.
    

### 👀 `less`

- Visualiza archivos página por página.
    

### 🧾 `history`

- Muestra el historial de comandos.
    

### 🧹 `clear`

- Limpia la terminal.
    

---

## 4️⃣ ¿Qué es “Hacking”?

- Idea clave: **todo son bytes**.
    
- El significado depende **de quién y cómo los interprete**.
    
- No existe un “tipo real” de archivo, solo **interpretaciones**.
    

---

## 5️⃣ Un mismo archivo, varios lenguajes

- Un mismo archivo puede ser:
    
    - C
        
    - C++
        
    - Python
        
    - Perl
        
    - Ruby
        
- Todo depende del **intérprete/compilador** que lo lea.
    
- Paralelo directo con los formatos de archivo.
    

---

## 6️⃣ ¿Qué es un formato de archivo?

- Define:
    
    - Qué datos contiene
        
    - Cómo están codificados
        
    - Qué significan
        
- Las aplicaciones **leen bytes** y deciden qué hacer con ellos.
    

---

## 7️⃣ Estructura común de los formatos

La mayoría de formatos tienen:

### 🧱 Header

- Información para interpretar el archivo.
    
- Ej: tamaño, tipo de imagen, metadata.
    

### 📦 Data / Payload

- Contenido principal (imagen, audio, etc.).
    

### 🧾 Footer / Trailer

- Información final o de integridad.
    

---

## 8️⃣ Magic Bytes (Firmas)

- Bytes iniciales que identifican el formato.
    
- Ejemplos:
    
    - PNG → `89 50 4E 47`
        
    - JPG → `FF D8 FF`
        
    - PDF → `%PDF`
        
    - ZIP → `PK`
        
- Se pueden ver con `xxd`.
    

👉 **El sistema reconoce archivos por magic bytes, no por extensión.**

---

## 9️⃣ Metadatos

- Información adicional en header/footer.
    
- Ejemplos:
    
    - Resolución
        
    - Fecha
        
    - Autor
        
    - Geolocalización
        
- Pueden modificarse **sin romper el archivo**.
    

### 🔧 Herramientas

- `exiftool` → lectura/escritura de metadatos.
    
- `mediainfo` → info técnica de archivos multimedia.
    

---

## 🔟 Extensiones de archivo

- Son **solo parte del nombre**.
    
- Cambiar `.png` a `.jpg` **NO cambia el formato real**.
    
- Algunos sistemas (Windows) usan la extensión para decidir qué programa abrir.
    

---

## 1️⃣1️⃣ PNG como ejemplo real

- Formato bien documentado (W3C).
    
- Estructura basada en _chunks_:
    
    - `IHDR`, `IDAT`, `IEND`, etc.
        
- Puede contener datos **después del `IEND`** sin romper la imagen.
    

---

## 1️⃣2️⃣ El programa que abre el archivo manda

- Un visor de imágenes → muestra la imagen.
    
- `exiftool` → muestra metadata.
    
- Editor de texto → interpreta bytes como texto (resultado raro).
    

👉 El archivo **no tiene tipo propio**, solo **validez para un propósito**.

---

## 1️⃣3️⃣ Ocultación de datos en archivos

- Algunos formatos permiten agregar datos extra.
    
- PNG permite agregar información después del final oficial.
    

### 🧪 Ejemplo

- Concatenar:
    
    `cat imagen.png secreto.pdf > imagen-final.png`
    
- Sigue siendo un PNG válido.
    

---

## 1️⃣4️⃣ `binwalk`

- Detecta archivos embebidos dentro de otros.
    
- `binwalk FILE`
    
- `binwalk -e FILE` → extrae contenido oculto.


--------------------------------------------------------------------------

**sxiv (Simple X Image Viewer)**:  
Visor de imágenes ligero y rápido para Linux, diseñado para ser minimalista. Permite ver imágenes desde la terminal de forma eficiente y sin consumir muchos recursos. Soporta navegación por carpetas, presentación de diapositivas, zoom y rotación. Ideal para usuarios que prefieren herramientas simples y rápidas.

--------------------------------------------------------------------------


identificar base64 es cuando usualmente termina en == y una  característica tambien es que es mayuscula y minuscula  

Para **decodificar** una cadena en **Base64** en Linux, puedes usar el comando `base64` con la opción `-d` (para decodificar). Aquí te dejo algunos ejemplos:

### 1. **Decodificar desde la terminal**:

Si tienes una cadena Base64 y quieres decodificarla directamente en la terminal, usa el siguiente comando:

`echo "cadena_base64" | base64 -d`

### 2. **Decodificar desde un archivo**:

Si tienes un archivo que contiene datos en Base64 y quieres decodificarlo, puedes hacer lo siguiente:

`base64 -d archivo_base64.txt > archivo_decodificado`

Este comando tomará el contenido de `archivo_base64.txt`, lo decodificará y lo guardará en `archivo_decodificado`.

### 3. **Guardar el resultado en un archivo**:

También puedes redirigir la salida decodificada a un archivo, si lo prefieres:

`echo "cadena_base64" | base64 -d > archivo_salida`

### Notas:

- **`base64 -d`**: Se utiliza para decodificar datos en Base64.
- base64: codifica datos en base64
    
- Si la cadena Base64 está en un archivo, puedes usar la opción `-d` directamente con el archivo, como mostré en el segundo ejemplo.

--------------------------------------------------------------------------
#### **Notas en Obsidian**:

**Título**: _Extraer Información de Archivos SVG con Ripgrep_  
**Contenido**:

``### Objetivo Extraer texto relevante (por ejemplo, una flag) de un archivo SVG que contiene el texto dentro de etiquetas `<tspan>`.  ### Pasos  1. **Buscar el contenido dentro de las etiquetas `<tspan>`**:    ```bash    rg 'id="tspan\d+">(.+)</tspan>' -or '$1' archivo.svg``

2. **Filtrar solo caracteres alfanuméricos y símbolos de la flag**:
    

- `rg 'id="tspan\d+">(.+)</tspan>' -or '$1' archivo.svg | tr -cd 'a-zA-Z0-9}{_'`
    
- **Resultado final**:  
    La flag extraída fue:
    

2. `picoCTF{3nh4nc3d_24374675}`
    

### Comandos Importantes

- **`rg`**: Herramienta rápida de búsqueda en archivos.
    
- **`tr`**: Herramienta de transformación de texto, útil para eliminar caracteres no deseados.
-------------------------------------------------------------------
### **Ocultación de Archivos (Hiding Files)**

#### **Archivos PNG + Cualquier Formato (PNG + ANY)**

Los archivos PNG pueden contener datos después del bloque `IEND`, por lo que podemos concatenar cualquier dato a un archivo PNG y este permanecerá allí sin que el archivo deje de ser válido. Esto permite ocultar datos dentro de un archivo PNG sin que sea fácilmente detectable.

Ejemplo:

`$ cat imagen.png archivo.pdf > imagen-archivo.png 
$ file imagen-archivo.png imagen-archivo.png: PNG image data, 1663 x 2057, 8-bit/color RGBA, non-interlaced 
$ binwalk imagen-archivo.png`

**Salida de `binwalk`**:

`DECIMAL HEXADECIMAL DESCRIPTION ---------------------------------------------------------------- 0       0x0     PNG image, total size: 2856846 bytes 2856846 0x2B978E PDF document, version 1.7`

---

#### **Uso de `binwalk` para Identificar y Extraer Archivos Embebidos**

**`binwalk`** es una herramienta que permite identificar y extraer archivos ocultos dentro de otros archivos, como imágenes o documentos.

- **Comando básico para identificar archivos embebidos**:
    

- `binwalk archivo`
    
- **Comando para extraer los archivos encontrados**:
    

- `binwalk -e archivo`
    

Ejemplo:

`$ cat imagen.png archivo.pdf > imagen-archivo.png 
$ binwalk imagen-archivo.png`

---

#### **Combinaciones de Archivos Polígrafos (Polyglots)**

Algunos formatos de archivo pueden combinarse de tal forma que puedan ser leídos como múltiples tipos de archivo válidos al mismo tiempo. Un ejemplo común es la combinación de archivos PNG y ZIP.

- **PNG + ZIP**: Los archivos ZIP son leídos de manera inversa (de atrás hacia adelante), mientras que los archivos PNG se leen de manera secuencial. Esto permite concatenar un archivo PNG con un archivo ZIP para que ambos funcionen correctamente.
    

Ejemplo:

`$ cat imagen.png archivo.zip > imagen-archivo.zip $ file imagen-archivo.zip imagen-archivo.zip: PNG image data, 1663 x 2057, 8-bit/color RGBA, non-interlaced $ unzip imagen-archivo.zip Archive: imagen-archivo.zip warning [imagen-archivo.zip]: 2856846 extra bytes at beginning or within zipfile (attempting to process anyway) extracting: archivo.txt $ cat archivo.txt Hola, mundo`

---

### **Herramientas Útiles (Some Tools)**

1. **`file`**: Determina el tipo de archivo mediante su firma.
    

- `file archivo`
    
- **`xxd`**: Muestra un volcado hexadecimal de un archivo o lo revierte.
    

- `xxd archivo`
    
- **`strings`**: Busca y muestra los caracteres imprimibles dentro de un archivo.  
    **Consejo**: Siempre usa `strings` para buscar cadenas de texto en archivos binarios.
    

1. `strings archivo`
    

---

### **`pngcheck`** – Verificación de Archivos PNG

**`pngcheck`** es una herramienta para verificar la integridad de los archivos PNG y mostrar detalles sobre los mismos.

- **Comando básico para comprobar un archivo PNG**:
    

- `pngcheck -v archivo.png`
    
- Ejemplo de salida:
    

`$ pngcheck -v archivo.png File: archivo.png (13114 bytes) chunk IHDR at offset 0x0000c, length 13 1642 x 1095 image, 24-bit RGB, non-interlaced chunk sRGB at offset 0x00025, length 1 rendering intent = perceptual chunk gAMA at offset 0x00032, length 4: 0.45455 chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi) chunk IDAT at offset 0x00057, length 13007 zlib: deflated, 32K window, fast compression chunk IEND at offset 0x03332, length 0 No errors detected in archivo.png (6 chunks, 99.8% compression).`

---

### **`ImHex`** – Editor Hexadecimal

**`ImHex`** es un editor hexadecimal diseñado para ingenieros inversos y programadores. Permite leer y editar los bytes de un archivo, útil para análisis y modificaciones a nivel bajo.

---

### **Esteganografía (Stego)**

La esteganografía es la práctica de ocultar información dentro de otros archivos, de forma que el archivo resultante siga siendo funcional y no detecte la presencia de los datos ocultos.

#### **Uso de LSB (Least Significant Bit) en Imágenes**

La esteganografía de LSB es una técnica donde los bits menos significativos de los valores de color de los píxeles de una imagen se modifican para almacenar datos. Esta técnica permite ocultar mensajes sin alterar perceptiblemente la imagen.

- **Ejemplo**:  
    Supongamos que queremos ocultar la palabra "hello" (en binario: `0b110100001100101011011000110110001101111`) en una imagen.
    
    Si tenemos una imagen roja (255, 0, 0), cambiaríamos el último bit del valor RGB de cada píxel con los bits de nuestro mensaje. Este proceso se repite con cada píxel hasta que todo el mensaje esté oculto en la imagen.
    

#### **Herramientas de Esteganografía**

1. **`zsteg`**: Detecta esteganografía en imágenes utilizando la técnica de LSB y otras.
    

- `zsteg imagen`
    
- **`stegsolve.jar`**: Permite visualizar diferentes planos de una imagen al aislar partes de los valores RGB, útil para la detección de esteganografía.
    

1. `java -jar stegsolve.jar`
    

---

### **Resumen y Notas**

- **Binwalk**: Herramienta potente para identificar y extraer archivos embebidos dentro de otros, especialmente útil en archivos como imágenes o documentos comprimidos.
    
- **Archivos Polígrafos (Polyglots)**: Al combinar formatos de archivo como PNG y ZIP, es posible crear archivos que puedan ser leídos como ambos formatos válidos sin perder funcionalidad.
    
- **Esteganografía LSB**: Técnica de ocultación de datos usando los bits menos significativos de los valores RGB de los píxeles en imágenes, ideal para ocultar mensajes de forma casi imperceptible.