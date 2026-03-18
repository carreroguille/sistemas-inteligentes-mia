# Neuralink BCI: La Inteligencia Artificial detrás de la interfaz cerebro-computador

## Informe técnico — Asignatura: Modelos de Inteligencia Artificial

---

## 1. Contexto: ¿Qué problema resuelve?

Millones de personas con parálisis severa (ELA, lesión medular, ictus) no pueden mover su cuerpo ni hablar, aunque su cerebro funcione con normalidad. Las interfaces cerebro-computador (BCI) buscan crear un puente directo entre la actividad cerebral y dispositivos externos. El reto técnico fundamental es un problema de inteligencia artificial: **traducir señales eléctricas ruidosas y caóticas del cerebro en intenciones claras y accionables, en tiempo real.**

Neuralink (fundada 2016, primer implante humano enero 2024, cinco participantes a junio 2025) es una de las empresas que lidera esta carrera. Pero lo que la hace funcionar no es solo el hardware: es el pipeline de IA que convierte la actividad de miles de neuronas en acciones.

---

## 2. Las señales del cerebro: ¿qué se captura exactamente?

Antes de hablar de los modelos de IA, es imprescindible entender qué datos recibe el sistema.

### 2.1. Potenciales de acción (spikes)

Cuando una neurona "dispara", genera un impulso eléctrico breve llamado **potencial de acción** o **spike**. Dura aproximadamente 1 milisegundo y tiene una amplitud de menos de 10 microvoltios (µV). Los electrodos de Neuralink (1.024 por implante) detectan estos spikes de neuronas individuales o pequeños grupos de neuronas.

Los spikes son la unidad fundamental de comunicación del cerebro. Cada electrodo muestrea a **20.000 muestras por segundo** con una resolución de 10 bits, generando más de **200 megabits por segundo de datos neuronales por canal**. Con 1.024 canales, el volumen bruto de datos es enorme.

### 2.2. Potenciales de campo local (LFP)

Además de los spikes individuales, los electrodos captan señales más lentas llamadas **potenciales de campo local** (LFP, *Local Field Potentials*). Los LFP representan la actividad promedio de poblaciones de neuronas cercanas. Son más estables que los spikes a lo largo del tiempo y más fáciles de registrar, aunque contienen menos información por canal.

### 2.3. Características extraídas de las señales

De estas señales brutas, los algoritmos extraen **features** (características) que alimentan a los modelos de ML:

| Característica | Descripción | Utilidad |
|---------------|-------------|----------|
| **Tasa de disparo** (*firing rate*) | Número de spikes por segundo de cada neurona | Indicador básico de activación neuronal |
| **Intervalo entre spikes** (*inter-spike interval*) | Tiempo entre disparos consecutivos | Patrón temporal de activación |
| **Correlación espacial** | Relación de activación entre electrodos vecinos | Identifica poblaciones neuronales que trabajan juntas |
| **Forma del spike** (*waveform shape*) | Perfil de voltaje del potencial de acción | Permite distinguir neuronas diferentes en el mismo electrodo |
| **Bandas de frecuencia de LFP** | Descomposición en bandas (theta, alpha, beta, gamma) | Estado cerebral, atención, intención motora |

---

## 3. El pipeline de IA: del cerebro a la acción

El proceso completo de decodificación neuronal es un pipeline de múltiples etapas, cada una con sus propios algoritmos:

### Etapa 1: Adquisición y filtrado de señal

Las señales brutas contienen tanto señal útil como ruido eléctrico (artefactos musculares, interferencia electromagnética, ruido térmico del circuito). Algoritmos de filtrado digital eliminan las frecuencias fuera de banda y aíslan la actividad neuronal relevante. Esto se ejecuta directamente en el chip ASIC personalizado de Neuralink dentro del implante.

### Etapa 2: Detección y clasificación de spikes (Spike Sorting)

Un algoritmo llamado **BOSS** (*Buffer Online Spike Sorter*), propietario de Neuralink, se ejecuta directamente en el implante:

1. **Detección:** Identifica cuándo se produce un spike distinguiéndolo del ruido de fondo. Establece un umbral de voltaje; cuando la señal lo supera, se marca como evento.
2. **Clasificación:** Caracteriza la forma del spike para determinar de qué neurona proviene (diferentes neuronas producen formas de onda distintas).
3. **Compresión:** En lugar de transmitir toda la señal bruta (lo que excedería los límites térmicos y de potencia del implante), solo envía resúmenes compactos que indican **cuándo y dónde** ocurren los spikes. Esto comprime los datos más de **200 veces**. El cálculo tarda menos de **900 nanosegundos** por spike.

Esta compresión es crucial: permite que todo se transmita por Bluetooth al dispositivo externo sin saturar el ancho de banda.

### Etapa 3: Extracción de características

Las señales preprocesadas se convierten en vectores de características (*feature vectors*). Se calcula la tasa de disparo por canal, los intervalos entre spikes, las correlaciones espaciales y las bandas de frecuencia de los LFP. Estos vectores son la entrada real de los modelos de aprendizaje automático.

### Etapa 4: Decodificación (el modelo de IA central)

Aquí es donde actúan los modelos de aprendizaje automático. Neuralink no ha publicado su código fuente ni sus arquitecturas exactas (no hay repositorio open source), pero a partir de patentes, publicaciones académicas y demostraciones, se sabe que utiliza una combinación de:

#### a) Modelos lineales: Filtro de Kalman

El enfoque base clásico en BCI. El **filtro de Kalman** modela la relación entre la actividad neuronal y el movimiento como un sistema dinámico lineal. Predice la velocidad y posición del cursor a partir de las tasas de disparo.

- **Ventaja:** Bajo coste computacional, funciona en tiempo real con facilidad.
- **Limitación:** Asume una relación lineal entre señales neuronales e intención, lo que no siempre es cierto.
- Neuralink usa una versión mejorada llamada **ReFIT** (*Recalibrated Feedback Intention-Trained*), un filtro de Kalman de dos etapas que se recalibra con los datos del propio usuario en bucle cerrado.

#### b) Redes neuronales convolucionales (CNN)

Se aplican a la señal bruta o a los espectrogramas de los LFP para **extraer automáticamente características espaciales y temporales**. Las CNN aprenden filtros convolucionales que detectan patrones en las señales neuronales que un diseño manual de features no captaría.

- Múltiples capas de filtros convolucionales aprenden características cada vez más abstractas.
- Útiles especialmente para identificar patrones espaciales (qué combinación de electrodos se activa).

#### c) Redes neuronales recurrentes (RNN) y LSTM

Son los modelos más relevantes para la **decodificación del habla**. Las RNN procesan secuencias temporales, lo que las hace ideales para señales neuronales (que son series temporales por naturaleza).

- **LSTM** (*Long Short-Term Memory*): variante de RNN que resuelve el problema del gradiente desvaneciente y captura dependencias a largo plazo. Se usa extensamente en BCI para decodificar habla y movimiento continuo.
- El estudio de referencia de Stanford/BrainGate (agosto 2025) usa una **RNN de 5 capas** que convierte la actividad cerebral en **probabilidades de fonemas** (los sonidos mínimos del habla). Emite una distribución de probabilidad sobre 39 fonemas + un token de silencio cada 80 milisegundos.
- Estas probabilidades se combinan con un **modelo de lenguaje** (un modelo n-grama de 125.000 palabras) que determina la secuencia de palabras más probable dada tanto las probabilidades de fonemas como la estadística del idioma.
- **Resultado:** Decodificación de habla imaginada con un vocabulario de 125.000 palabras, con hasta un 74% de precisión.

#### d) Arquitecturas tipo Transformer

En la frontera de la investigación se están explorando **Transformers** para el reconocimiento de patrones neuronales de alta dimensionalidad. Su mecanismo de atención permite ponderar qué canales y momentos temporales son más relevantes para cada predicción, sin la limitación secuencial de las RNN.

### Etapa 5: Generación de salida

La salida decodificada se convierte en la acción final:

| Aplicación | Entrada del modelo | Salida | Modelo principal |
|-----------|-------------------|--------|-----------------|
| Control de cursor | Tasas de disparo del córtex motor | Velocidad y dirección del cursor (x, y) | Filtro de Kalman / ReFIT |
| Escritura manual | Patrones de intento de escribir letras | Trayectoria de la mano → clasificador de caracteres (tipo MNIST) | RNN + clasificador supervisado |
| Habla | Actividad del córtex motor del habla | Probabilidades de fonemas → palabras → voz | RNN/LSTM de 5 capas + modelo de lenguaje n-grama |
| Brazo robótico | Patrones de intención motora | Coordenadas 3D, fuerza, apertura de mano | CNN + filtro de Kalman |

### Etapa 6: Aprendizaje adaptativo

Este es uno de los aspectos más interesantes desde el punto de vista de modelos de IA:

- **El problema de la variabilidad:** Las señales neuronales no son estables día a día. La tasa de disparo promedio de las neuronas puede cambiar significativamente de un día a otro, causando un sesgo en la salida del modelo (por ejemplo, el cursor tiende a moverse en una dirección incorrecta).
- **Solución: calibración y aprendizaje continuo.** El sistema se recalibra periódicamente. El usuario realiza tareas de calibración (intentar mover en distintas direcciones) y el modelo actualiza sus pesos.
- **Aprendizaje de transferencia:** Se investigan métodos de adaptación de dominio (como PCA-based Domain Adaptation) que usan datos de múltiples sesiones anteriores para calibrar el modelo con pocos datos nuevos, reduciendo el tiempo de calibración.
- **Neuroplasticidad del usuario:** Con la práctica, el cerebro del usuario se adapta y genera patrones neuronales más consistentes y diferenciables. Este "co-aprendizaje" entre IA y cerebro humano es un fenómeno único de los BCI que no existe en otros campos de la IA.

---

## 4. Restauración del habla: el caso más avanzado de decodificación con IA

### 4.1. Pipeline completo

```
Córtex motor del habla
        ↓
[Microelectrodos registran actividad neuronal
 mientras el usuario INTENTA hablar]
        ↓
[Spike sorting + extracción de features]
        ↓
[RNN de 5 capas procesa secuencia temporal]
        ↓
[Salida: probabilidad de 39 fonemas cada 80ms]
        ↓
[Modelo de lenguaje (n-grama, 125.000 palabras)
 determina la secuencia de palabras más probable]
        ↓
[Texto generado]
        ↓
[Vocoder / TTS convierte texto en voz sintética]
        ↓
[Voz personalizada: modelo entrenado con
 grabaciones previas a la enfermedad del paciente]
```

### 4.2. Avance clave: decodificación de habla interna (inner speech)

El estudio de Stanford/BrainGate (publicado en Cell, agosto 2025) demostró algo sin precedentes: no es necesario que el paciente intente hablar físicamente. La IA puede decodificar el **habla interna** (pensar en decir algo sin intentar moverlo). Descubrieron que:

- La representación neuronal del habla imaginada está **altamente correlacionada** con la del habla intentada.
- Existe una dimensión neuronal de "intención motora" que diferencia ambas.
- Se puede proteger la privacidad: un sistema de "contraseña mental" impide que el BCI decodifique accidentalmente pensamientos internos. El usuario debe imaginar una frase clave para "desbloquear" el sistema (98.75% de precisión en la detección).

### 4.3. El caso Brad (Neuralink)

Un participante con ELA que perdió el habla. Neuralink entrenó un modelo de IA personalizado con grabaciones de su voz antes de la enfermedad. El resultado: la voz sintética generada por el sistema suena como su propia voz, no como un sintetizador genérico. Jugó a Mario Kart con sus hijos usando el BCI.

---

## 5. Comparativa de modelos de IA en BCI

| Modelo | Tipo | Uso en BCI | Ventajas | Limitaciones |
|--------|------|-----------|----------|--------------|
| **Filtro de Kalman** | Modelo lineal de espacio de estados | Control de cursor, movimiento | Bajo coste computacional, tiempo real | Asume linealidad; sensible a cambios diarios |
| **SVM** | Clasificador supervisado | Clasificación de movimientos discretos | Robusto con pocas muestras | Solo clasificación binaria/multiclase; no genera secuencias |
| **CNN** | Red convolucional profunda | Extracción de features espaciales de señales neuronales | Aprende features automáticamente; detecta patrones espaciales | Necesita muchos datos de entrenamiento |
| **RNN / LSTM** | Red recurrente | Decodificación de habla, movimiento continuo | Captura dependencias temporales; ideal para secuencias | Entrenamiento lento; difícil paralelizar |
| **Transformer** | Atención multi-cabeza | Reconocimiento de patrones de alta dimensionalidad (experimental) | Paralelizable; pondera relevancia por canal y tiempo | Alto coste computacional; aún en fase experimental en BCI |
| **Filtro de Kalman ReFIT** | Kalman de 2 etapas con recalibración | Control de cursor mejorado | Se recalibra en bucle cerrado; más preciso que Kalman estándar | Requiere sesiones de calibración periódicas |

---

## 6. Retos abiertos de la IA en BCI

### 6.1. Variabilidad de las señales
La tasa de disparo de las neuronas cambia de un día a otro. Un modelo entrenado hoy puede funcionar peor mañana. Los métodos de adaptación de dominio y transferencia de aprendizaje buscan resolver esto, pero aún no hay una solución definitiva.

### 6.2. Generalización entre usuarios
Cada cerebro es único. Los modelos actuales se entrenan desde cero para cada usuario. ¿Se podrá algún día entrenar un modelo "universal" de decodificación neuronal y adaptarlo a cada persona con pocos datos (fine-tuning)? Es un problema abierto similar al de los modelos de lenguaje pre-entrenados.

### 6.3. Tiempo real con recursos limitados
El implante tiene restricciones severas de potencia y temperatura (está dentro del cráneo). Los algoritmos deben ser extremadamente eficientes. El algoritmo BOSS de Neuralink comprime datos 200x en 900 nanosegundos, pero modelos más complejos (como RNN profundas o Transformers) se ejecutan en el dispositivo externo.

### 6.4. Habla interna vs. intentada
Decodificar lo que alguien piensa (habla interna) abre posibilidades enormes pero también riesgos de privacidad sin precedentes. La investigación en "contraseñas mentales" y decodificadores que ignoran el habla interna es tan importante como la propia decodificación.

---

## 7. Preguntas éticas (sin posicionamiento)

- Si la IA decodifica una acción que el usuario no pretendía, ¿quién es responsable?
- ¿Deben los datos neuronales tener protección legal especial, como los datos genéticos?
- Si en el futuro estos sistemas se usan para mejora cognitiva (no solo restauración médica), ¿qué límites se establecen?
- ¿Es posible garantizar que un BCI nunca decodifique pensamientos que el usuario no quiere compartir?
- ¿Debería ser obligatorio que las arquitecturas de decodificación sean open source para poder auditarlas?

---

## 8. Fuentes

1. Neuralink white paper original (2019). *An Integrated Brain-Machine Interface Platform With Thousands of Channels*. PMC6914248. https://pmc.ncbi.nlm.nih.gov/articles/PMC6914248/
2. Willett, F. et al. (2025). *Inner speech in motor cortex and implications for speech neuroprostheses*. Cell. https://www.cell.com/cell/fulltext/S0092-8674(25)00681-6
3. Contrary Research (2025). *Neuralink Business Breakdown*. https://research.contrary.com/company/neuralink
4. Neural Decoding for Intracortical BCIs (2023). Cyborg and Bionic Systems. https://spj.science.org/doi/10.34133/cbsystems.0044
5. Stanford Medicine (2025). *Study of promising speech-enabling interface*. https://med.stanford.edu/news/all-news/2025/08/brain-computer-interface.html
6. PMC (2025). *Emerging Brain-to-Content Technologies from Generative AI and Deep Representation Learning*. https://pmc.ncbi.nlm.nih.gov/articles/PMC12333864/
7. TechLifeSci (2026). *2025 Neurotech Review*. https://www.techlifesci.com/p/2025-neurotech-review
8. Nature (2025). *A brain implant that could rival Neuralink's*. https://www.nature.com/articles/d41586-025-03849-0
9. MassDevice (2025). *Neuralink wins FDA breakthrough nod*. https://www.massdevice.com/neuralink-fda-breakthrough-nod-speech-impairment/
10. AllHealthTech (2025). *Neuralink's latest updates*. https://allhealthtech.com/neuralink-update/
