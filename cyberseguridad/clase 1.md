# 🧠 Linux & Hacking Bootcamp — **Listado de Comandos**

---

## 📌 1. `echo`

### 🎯 Objetivo

Mostrar texto por pantalla o enviarlo a otro comando/archivo.

### 🧾 Sintaxis

`echo TEXTO`

### ✅ Ejemplo

`echo "Hello, world"`

### 💡 Usos típicos

- Debug rápido
    
- Enviar texto a archivos
    
- Pipes (`|`) y redirecciones (`>`)
    

---

## 📌 2. `pwd`

### 🎯 Objetivo

Mostrar el **directorio actual** (Current Working Directory).

### 🧾 Sintaxis

`pwd`

### ✅ Ejemplo

`/home/hacker`

---

## 📌 3. `cd`

### 🎯 Objetivo

Cambiar el directorio actual.

### 🧾 Sintaxis

`cd DIRECTORIO`

### ✅ Ejemplos

`cd Desktop cd /etc/systemd cd ..`

### ⚠️ Nota

- **No es un programa**, es un _builtin_ de bash.
    
- Afecta solo a la shell actual.
    

---

## 📌 4. `ls`

### 🎯 Objetivo

Listar archivos y carpetas.

### 🧾 Sintaxis

`ls [DIR]`

### ✅ Ejemplos

`ls ls /etc ls -la`

### 💡 Tip

- `-l` → detalles
    
- `-a` → archivos ocultos
    

---

## 📌 5. `cat`

### 🎯 Objetivo

Mostrar el contenido de archivos (concatenar).

### 🧾 Sintaxis

`cat ARCHIVO`

### ✅ Ejemplos

`cat hello.txt cat a.txt b.txt`

### 🔍 Extra útil

`cat -A archivo`

→ muestra tabs, saltos de línea, etc.

---

## 📌 6. `ssh`

### 🎯 Objetivo

Conectarse a una máquina remota vía SSH.

### 🧾 Sintaxis

`ssh usuario@host`

### ✅ Ejemplos

`ssh hacker@dojo.pwn.college ssh hacker@host id`

### 💡 Usos

- Acceso remoto
    
- Ejecutar comandos sin entrar al shell
    

---

## 📌 7. `nc` (netcat)

### 🎯 Objetivo

Crear conexiones TCP/UDP (cliente o servidor).

### 🧾 Sintaxis

`nc HOST PUERTO`

### ✅ Ejemplo

`nc 127.0.0.1 31337`

### 🧠 Muy usado en:

- CTFs
    
- Reverse shells
    
- Servicios simples
    

---

## 📌 8. Redirección `>`

### 🎯 Objetivo

Enviar la salida de un comando a un archivo.

### 🧾 Sintaxis

`COMANDO > archivo`

### ✅ Ejemplo

`echo "Hola" > saludo.txt`

⚠️ Sobrescribe el archivo.

---

## 📌 9. Pipe `|`

### 🎯 Objetivo

Enviar la salida de un comando como entrada a otro.

### 🧾 Sintaxis

`COMANDO1 | COMANDO2`

### ✅ Ejemplo

`echo "Hello" | rev`

---

## 📌 10. `man`

### 🎯 Objetivo

Mostrar el **manual completo** de un comando.

### 🧾 Sintaxis

`man comando`

### ✅ Ejemplo

`man cat`

📖 Sale con `q`.

---

## 📌 11. `--help`

### 🎯 Objetivo

Mostrar ayuda rápida de un comando.

### 🧾 Sintaxis

`comando --help`

### ✅ Ejemplo

`cat --help`

---

## 📌 12. `info`

### 🎯 Objetivo

Documentación más detallada (GNU).

### 🧾 Sintaxis

`info comando`

### ✅ Ejemplo

`info cat`

---

## 📌 13. `tldr`

### 🎯 Objetivo

Ejemplos simples y prácticos de comandos.

### 🧾 Sintaxis

`tldr comando`

### ✅ Ejemplo

`tldr grep`

🌐 [https://tldr.inbrowser.app/](https://tldr.inbrowser.app/)

---

## 📌 14. `file`

### 🎯 Objetivo

Detectar el **tipo real** de un archivo (por magic bytes).

### 🧾 Sintaxis

`file ARCHIVO`

### ✅ Ejemplo

`file imagen.png`

🧠 CLAVE en forense y hacking.

---

## 📌 15. `find`

### 🎯 Objetivo

Buscar archivos en el sistema.

### 🧾 Sintaxis

`find RUTA -name NOMBRE`

### ✅ Ejemplo

`find . -name secret.txt`

---

## 📌 16. `grep`

### 🎯 Objetivo

Buscar texto dentro de archivos.

### 🧾 Sintaxis

`grep PATRON ARCHIVO`

### ✅ Ejemplos

`grep flag dump.txt grep -i flag dump.txt`

### 🔥 Muy usado con pipes

`cat archivo | grep flag`

---

## 📌 17. `strings`

### 🎯 Objetivo

Extraer texto legible desde archivos binarios.

### 🧾 Sintaxis

`strings ARCHIVO`

### ✅ Ejemplo

`strings programa.out`

🚨 **Siempre usar primero en CTFs**.

---

## 📌 18. `base64`

### 🎯 Objetivo

Codificar o decodificar base64.

### 🧾 Sintaxis

`base64 ARCHIVO base64 -d ARCHIVO`

### ✅ Ejemplo

`echo "Hello" | base64 echo "SGVsbG8=" | base64 -d`

---

## 📌 19. `xxd`

### 🎯 Objetivo

Ver archivos en hexadecimal (binario).

### 🧾 Sintaxis

`xxd ARCHIVO`

### ✅ Ejemplo

`xxd imagen.png`

### 🔁 Reverso

`xxd | xxd -r`

---

## 📌 20. `nano`

### 🎯 Objetivo

Editar archivos de texto en terminal.

### 🧾 Sintaxis

`nano ARCHIVO`

### ⌨️ Atajos

- `CTRL+X` salir
    
- `CTRL+O` guardar
    

---

## 🧠 RESUMEN RÁPIDO (para Obsidian)

`Comandos clave: 
- echo → imprimir texto 
- pwd → ver directorio actual 
- cd → cambiar directorio 
- ls → listar archivos 
- cat → ver archivos 
- ssh → conexión remota 
- nc → conexiones TCP/UDP 
- file → tipo real de archivo 
- find → buscar archivos 
- grep → buscar texto 
- strings → texto en binarios 
- base64 → codificar/decodificar 
- xxd → ver binario 
- nano → editar texto`