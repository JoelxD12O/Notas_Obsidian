## 1️⃣ ¿De qué trata el paper?

- El paper estudia **cómo mejorar el comportamiento de un auto** frente a baches y vibraciones.
    
- Se enfoca en **comodidad del pasajero** y **estabilidad del vehículo**.
    
- Usa **simulación en computadora (MATLAB)**, no experimentos reales.
    

---

## 2️⃣ Modelo usado: _Quarter-Car Model_

- No modelan todo el auto.
    
- Solo modelan **una rueda + la parte del carro encima de esa rueda**.
    
- Es un modelo **simplificado**, pero muy usado en ingeniería.
    

---

## 3️⃣ Grados de libertad (2 DOF)

El sistema tiene **2 movimientos independientes**:

1. 📦 **Movimiento vertical de la carrocería**
    
    - Subir y bajar del cuerpo del auto
        
    - Relacionado con **comodidad**
        
2. 🛞 **Movimiento vertical de la rueda**
    
    - Subir y bajar de la rueda
        
    - Relacionado con **contacto con el suelo**
        

---

## 4️⃣ Problema principal (conflicto)

Hay un conflicto natural:

- Mejor comodidad → rueda puede rebotar
    
- Mejor estabilidad → pasajero siente vibraciones
    

👉 No se pueden optimizar ambos fácilmente con solo suspensión tradicional.

---

## 5️⃣ Tipos de suspensión comparados

El paper compara tres casos:

1. 🚗 **Suspensión pasiva**
    
    - Resortes y amortiguadores normales
        
    - Sin control
        
2. 🚗 **Suspensión activa**
    
    - Aplica fuerzas controladas
        
    - Mejora respecto a la pasiva
        
3. 🚗🪽 **Suspensión activa + aerodinámica activa**
    
    - Suspensión + empuje del aire hacia abajo
        
    - Propuesta del paper
        

---

## 6️⃣ ¿Qué es la aerodinámica activa?

- Usa una **superficie tipo alerón**
    
- El aire empuja el auto **hacia abajo**
    
- Genera una fuerza extra llamada **downforce**
    
- Es _activa_ porque se ajusta automáticamente
    

👉 Ayuda a que la rueda **no pierda contacto con el suelo**

---

## 7️⃣ Objetivos del control

El sistema busca:

- Reducir vibraciones de la carrocería (comodidad)
    
- Mantener la rueda pegada al suelo (estabilidad)
    
- Evitar fuerzas excesivas
    

---

## 8️⃣ Método de control usado

- Usan **control óptimo (LQR)**
    
- El controlador decide qué fuerzas aplicar
    
- Minimiza un “costo” basado en:
    
    - Vibraciones
        
    - Desplazamientos
        
    - Esfuerzo del control
        

---

## 9️⃣ Evaluación del desempeño

- Analizan el sistema en:
    
    - ⏱️ Dominio del tiempo
        
    - 📈 Dominio de la frecuencia
        
- Calculan **índices de desempeño**
    
- Comparan resultados entre los tres sistemas
    

---

## 🔟 Resultado clave

- El sistema propuesto mejora el desempeño total en:
    
    - 📊 **70–80%**
        
- Comparado con **solo suspensión activa**




# 📝 NOTAS – INTRODUCCIÓN DEL PAPER

## 1️⃣ Contexto general

- En los últimos años se investiga mucho cómo **mejorar el desempeño dinámico de la suspensión**.
    
- Dos objetivos principales:
    
    - **Ride comfort** → comodidad del pasajero (menos vibraciones).
        
    - **Road holding** → que la rueda mantenga buen contacto con el suelo.
        
- Estos dos objetivos **normalmente están en conflicto**.
    

---

## 2️⃣ Problema de las vibraciones

- Las irregularidades del camino (baches, pistas malas) causan:
    
    - Incomodidad al pasajero.
        
    - Desgaste mecánico del vehículo.
        
- Por eso se buscan **nuevas estrategias de control**.
    

---

## 3️⃣ Estudios previos (limitaciones)

### Paper [1]

- Usó control predictivo para suavizar la aceleración del carro.
    
- Consideró posición, velocidad y aceleración.
    
- ❌ No consideró **road holding** (contacto de la rueda con el suelo).
    

### Paper [2]

- Usó un **quarter-car model**.
    
- Probó suspensión pasiva, activa y semi-activa.
    
- ❌ Evaluó solo el movimiento del asiento, no el agarre de la rueda.
    

---

## 4️⃣ Otros enfoques alternativos

### Papers [3] y [4]

- Usaron machine learning y control predictivo.
    
- Objetivos:
    
    - Confort
        
    - Ahorro de combustible
        
    - Estilo de conducción
        
- ❌ No analizaron parámetros físicos de la suspensión.
    

### Paper [5]

- Analizó vibraciones en trenes.
    
- Conclusión:
    
    - Irregularidades pequeñas y frecuentes empeoran mucho el confort.
        
- Sirve como **justificación teórica**.
    

---

## 5️⃣ Modelo usado: Quarter-Car

- El vehículo se divide en:
    
    - **Masa suspendida** → carrocería.
        
    - **Masa no suspendida** → rueda + eje.
        
- Movimiento:
    
    - Solo vertical.
        
    - **2 grados de libertad (2 DOF)**.
        
- Es un modelo simplificado pero muy usado.
    

---

## 6️⃣ Definiciones clave

- **Ride comfort**:
    
    - Aislar la carrocería de las vibraciones del camino.
        
- **Road holding**:
    
    - Reducir la variación de la fuerza de la rueda contra el suelo.
        
    - Mejor agarre y seguridad.
        

---

## 7️⃣ Control óptimo

- Un controlador óptimo:
    
    - Usa sensores para anticipar irregularidades del camino.
        
    - Combina:
        
        - **Feedback** (reacción).
            
        - **Feedforward** (anticipación).
            
- Objetivo:
    
    - Reducir vibraciones.
        
    - Mantener contacto con el suelo.
        
- Las perturbaciones del camino se modelan como **señales aleatorias**.
    

---

## 8️⃣ Aerodinámica activa en trabajos previos

- En autos de carrera:
    
    - Alerones activos mejoran estabilidad y seguridad.
        
- Se han usado:
    
    - Spoilers delanteros y traseros.
        
    - Alas móviles.
        
- Beneficio:
    
    - Reducen oscilaciones verticales del carro.
        
- Dificultad:
    
    - Generar fuerza vertical en la parte frontal del vehículo.
        

---

## 9️⃣ Estudios cercanos al presente trabajo

### Paper [12]

- Usó un alerón activo con variación de ángulo a 10 Hz.
    
- Mejoró el confort sin afectar negativamente la rueda.
    

### Paper [13]

- Usó dos superficies aerodinámicas activas:
    
    - Una en la carrocería.
        
    - Una en la rueda.
        
- Resultados:
    
    - Menor aceleración.
        
    - Mejor road holding.
        
- La mejora frente a suspensión activa fue **limitada**.
    

---

## 🔟 Estudios con modelos más complejos

### Papers [14] y [15]

- Usaron modelos de medio auto (half-car).
    
- Aplicaron control predictivo.
    
- Resultados:
    
    - Menos vibraciones.
        
    - Mejor contacto con el suelo.
        

---

## 1️⃣1️⃣ Motivación del paper

- No se ha estudiado suficientemente:
    
    - La **colaboración** entre:
        
        - Suspensión activa.
            
        - Aerodinámica activa.
            
    - En un **quarter-car model**.
        
- Aunque los objetivos están en conflicto, el uso de aerodinámica activa puede ayudar a superarlo.
    

---

## 1️⃣2️⃣ Problema práctico real

- La suspensión activa:
    
    - Mejora el desempeño.
        
    - ❌ Consume mucha energía (actuadores hidráulicos).
        
- La aerodinámica activa:
    
    - Puede ayudar a reducir el esfuerzo de la suspensión.
        
    - Mejora eficiencia global.
        

---

## 1️⃣3️⃣ Propuesta del paper

- Usar:
    
    - Suspensión activa.
        
    - Superficie aerodinámica activa.
        
    - Control óptimo **LQR**.
        
- Objetivo:
    
    - Minimizar las variaciones cuadráticas promedio:
        
        - De la comodidad.
            
        - Del road holding.
            

---

## 1️⃣4️⃣ Objetivos del estudio

1. Analizar solo el efecto aerodinámico del alerón.
    
2. Evaluar el efecto combinado con suspensión activa.
    
3. Comparar con otros sistemas de suspensión.
    

---

## 1️⃣5️⃣ Estructura del paper

- Sección 2 → Modelo matemático.
    
- Sección 3 → Formulación del problema.
    
- Sección 4 → Diseño del controlador.
    
- Sección 5 → Resultados.
    
- Sección 6 → Conclusiones.
    

---

📌 **Tip final para cuando lo repases**  
Si te pierdes:

- Piensa siempre en **fuerzas verticales**
    
- Piensa en **dos masas que suben y bajan**
    
- Piensa en **un controlador que decide fuerzas**

previo a realizar metodologias :
### 1. Definición del Modelo (Quarter-Car)

- **¿Qué es?** Es una simplificación que solo analiza **una rueda** del carro.
    
- **Grados de libertad (DOF):** Tiene **2**, porque hay dos masas que se mueven de forma independiente hacia arriba y hacia abajo ($z_1$ y $z_2$).
    
- **Masa Suspendida ($m_1$):** Chasis/Cuerpo del carro. Su movimiento define el **confort** (qué tanto vibra el pasajero).
    
- **Masa No Suspendida ($m_2$):** Eje/Rueda. Su movimiento define el **agarre** (que la llanta no pierda contacto con el suelo).
    

### 2. Los Componentes (Parámetros)

Anota estas definiciones para cuando hagas la tabla de parámetros en tu trabajo:

- **$k_1$:** Constante del resorte (Rigidez).
    
- **$b_1$:** Coeficiente del amortiguador (Disipación de energía).
    
- **$k_2$:** Rigidez del neumático (Se modela como un resorte que toca el suelo).
    
- **$z_0$:** Entrada del sistema. Es el "perfil del camino" (baches, ondas, piedras).
    

### 3. Las Fuerzas Especiales (Variables de Control)

Este paper no es de un carro normal, tiene dos "ayudas" extra:

- **$u_1$ (Control Activo):** Fuerza que genera un actuador hidráulico o eléctrico entre las dos masas.
    
- **$u_2$ (Aerodinámica):** Fuerza que genera el "alerón" (airfoil). Esta fuerza empuja el carro hacia abajo usando el aire.
    

### 4. ¿Qué vamos a resolver? (El objetivo numérico)

- **Entrada:** Una función matemática que represente el camino ($z_0$). Por ejemplo, una función seno o un escalón.
    
- **Salida:** Los valores de $z_1$ y $z_2$ a través del tiempo.
    
- **Conflicto a resolver:** Si la suspensión es muy suave, hay confort pero el carro es inestable. Si es muy dura, hay estabilidad pero es incómodo. El paper busca el equilibrio perfecto.
    

### 5. Supuestos para tu Metodología (Muy importante para el paper)

Anota estos puntos, porque el profesor evaluará que los menciones:

1. **Movimiento lineal:** Se asume que el carro solo sube y baja perfectamente recto (no se inclina hacia los lados).
    
2. **Amortiguación del neumático despreciable:** Se asume que la llanta no tiene amortiguador propio, solo resorte ($k_2$).
    
3. **Contacto permanente:** Se asume (para el modelo base) que la llanta no despega del suelo.