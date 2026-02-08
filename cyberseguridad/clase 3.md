# Web Hacking & Recon – Resumen General (CTF / Bootcamp)

## 1. Mentalidad general
- En web hacking **el cliente NO es confiable**:
  - HTML
  - JavaScript
  - Cookies
  - Headers
- Todo lo que llega desde el navegador **puede ser visto y modificado** por el usuario.
- La mayoría de retos web se resuelven con:
  - observación
  - lectura de código
  - comprensión de errores de diseño

---

## 2. Reconocimiento Web (Recon)
Recon = recolectar información antes de atacar.

### Archivos y rutas comunes
- `/robots.txt`
- `/sitemap.xml`
- archivos `.js`
- comentarios HTML
- endpoints ocultos (`/admin`, `/debug`, `/flag`, etc.)

### robots.txt
- Sirve para **bots**, no para seguridad.
- Puede filtrar rutas “ocultas”.
- Error común: usarlo para esconder contenido sensible.

---

## 3. HTTP básico
Toda aplicación web funciona con **requests** y **responses**.

### Request
- Método: GET / POST
- Headers
- Body (opcional)

### Response
- Status code (200, 401, 403, etc.)
- Headers
- Body (HTML, JSON, texto)

---

## 4. Headers
Headers = metadata enviada en una request.

### Headers vistos
- `User-Agent`
- `Cookie`
- `Set-Cookie`
- `Authorization`
- headers personalizados (`X-Dev-Access`, etc.)

### Lección clave
- Los headers **NO son seguridad**.
- El usuario puede:
  - modificarlos
  - falsificarlos
  - inventarlos

---

## 5. Cookies
- Son **visibles y editables**.
- No deben contener:
  - flags
  - secretos
  - decisiones de autorización

### Técnicas usadas
- Inspección con DevTools
- Identificación de Base64
- Decodificación manual

---

## 6. Encodings comunes (Base64)
Muy frecuente en CTFs.

### Señales típicas
- cadenas largas
- terminan en `==`
- caracteres A–Z a–z 0–9 + /

### Decodificar en Linux
```bash
echo "cadena" | base64 -d
```

---

## 7. DevTools (navegador)
Herramienta clave para web hacking.

### Tabs importantes
- **Elements**: HTML, comentarios ocultos
- **Network**:
  - requests reales
  - endpoints
  - parámetros
  - responses
- **Console**:
  - ejecutar JavaScript
  - usar fetch
- **Application / Storage**:
  - cookies
  - localStorage

---

## 8. JavaScript del lado del cliente
- El JS del frontend **no protege nada**.
- Validaciones en JS = solo estética.

### Técnicas vistas
- Leer JS ofuscado
- Ignorar ruido
- Buscar:
  - strings
  - arrays
  - substring, split
- Reconstruir lógica manualmente

---

## 9. Bookmarklets
- JavaScript ejecutado en el contexto del navegador.
- Usados para:
  - ofuscación simple
  - retos educativos
- Se pueden:
  - copiar
  - pegar en consola
  - analizar sin ejecutar

---

## 10. ROT13 y ofuscación simple
- Común en comentarios HTML.
- No es cifrado real, solo ocultamiento.

### ROT13 en Linux
```bash
echo "texto" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

## 11. User-Agent
- Es solo un string.
- Muchos servidores confían erróneamente en él.

### Ejemplo
```
User-Agent: picobrowser
```

### Lección
- Comparaciones sensibles a mayúsculas/minúsculas rompen seguridad.

---

## 12. Herramientas usadas

### HTTPie
Cliente HTTP amigable.

```bash
http URL
http URL Header:Value
http -v URL
```

**Ejemplo:**
```bash
http http://example.com User-Agent:picobrowser
```

Más tolerante, casi siempre disponible.

```bash
curl -H "Header: Value" URL
```

### grep
Buscar texto en archivos.

```bash
grep "picoCTF" archivo
grep -Rni "picoCTF" .
```

**Con binarios:**
```bash
strings archivo | grep picoCTF
```

---

## 13. fetch (desde el navegador)
Permite enviar requests manuales.

```javascript
fetch("URL", {
  method: "POST",
  headers: {
    "Header": "Value"
  },
  body: JSON.stringify(data)
})
.then(r => r.text())
.then(t => console.log(t));
```

---

## 14. Errores de seguridad comunes
- Confiar en `robots.txt`
- Guardar secretos en cookies
- Validar solo en frontend
- Confiar en headers
- Dejar bypasses de desarrollo
- Comparar strings incorrectamente

---

## 15. Regla de oro
> **Si el usuario puede verlo, el usuario puede modificarlo.**

La seguridad **nunca** debe depender del cliente.