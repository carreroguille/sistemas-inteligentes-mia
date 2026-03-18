# Proyecto 5: Sistemas inteligentes y sus aplicaciones en la actualidad

## Índice

- [Introducción](#introducción)
- [Características de un sistema inteligente](#características-de-un-sistema-inteligente)
- [Aplicación 1: Enoch — IA para datar manuscritos antiguos](#aplicación-1-enoch--ia-para-datar-manuscritos-antiguos)
- [Aplicación 2: Neuralink BCI — Interfaces cerebro-computador con IA](#aplicación-2-neuralink-bci--interfaces-cerebro-computador-con-ia)
- [Aplicación 3: SpeciesNet y WildDrone — IA para conservación de fauna](#aplicación-3-speciesnet-y-wilddrone--ia-para-conservación-de-fauna)
- [Tabla comparativa](#tabla-comparativa)
- [Conclusiones](#conclusiones)
- [Fuentes](#fuentes)

---

## Introducción

Este proyecto investiga tres aplicaciones actuales de la Inteligencia Artificial en campos muy diferentes: la arqueología, la neurotecnología médica y la conservación de la biodiversidad. Para cada una, se identifican y justifican qué características de un sistema inteligente se cumplen y cuáles no, según la definición de la [Wikipedia](https://es.wikipedia.org/wiki/Sistema_inteligente).

---

## Características de un sistema inteligente

Según la Wikipedia, un sistema inteligente completo debe incluir las siguientes capacidades:

| # | Característica | Descripción |
|---|----------------|-------------|
| 1 | **Inteligencia** | Nivel del sistema en lograr sus objetivos |
| 2 | **Sistematización** | Las partes del sistema están interrelacionadas y tienen correlaciones más fuertes entre sí que con el exterior |
| 3 | **Objetivo** | Situación concreta que el sistema quiere lograr, pudiendo haber subobjetivos |
| 4 | **Capacidad sensorial** | Puede recibir información del entorno para actuar de forma interactiva |
| 5 | **Conceptualización** | Capacidad de generar conceptos, almacenarlos y desarrollar niveles de abstracción |
| 6 | **Reglas de actuación** | Relaciona situaciones con consecuencias de acción, derivadas de la experiencia o la memoria |
| 7 | **Memoria** | Almacenaje físico de conceptos, reglas de actuación y experiencia |
| 8 | **Aprendizaje** | Capacidad de mejorar su rendimiento a partir de la experiencia, detectar patrones y crear conceptos abstractos |

---

## Aplicación 1: Enoch — IA para datar manuscritos antiguos

### Campo: Arqueología / Paleografía digital

### Descripción

Enoch es un modelo de inteligencia artificial desarrollado por un equipo internacional liderado por la Universidad de Groningen (Países Bajos), publicado en la revista PLOS One en junio de 2025. Su propósito es datar manuscritos antiguos, concretamente los Manuscritos del Mar Muerto, combinando datación por carbono-14 con análisis de estilos de escritura mediante aprendizaje automático.

El nombre "Enoch" proviene del personaje bíblico del Libro de Enoc, uno de los propios Manuscritos del Mar Muerto.

### ¿Cómo funciona internamente?

1. **Entrenamiento:** Se dataron con carbono-14 fragmentos de 24 manuscritos del Mar Muerto. Se tomaron imágenes de alta resolución de cada uno.
2. **Extracción de características:** Una red neuronal llamada BiNet analiza los trazos de tinta de las letras, extrayendo vectores de características angulares y alográficas (forma, curvatura, proporciones de cada carácter hebreo o arameo).
3. **Modelo predictivo:** Mediante regresión bayesiana de crestas (*Bayesian Ridge Regression*), Enoch aprende la relación entre estilos de escritura y fechas conocidas. Genera una distribución de probabilidad temporal para cada manuscrito, indicando qué fechas son más probables.
4. **Predicción:** Se le muestran imágenes de manuscritos sin datar y Enoch genera una estimación de edad con un margen de error medio de unos 27-30 años.

### Datos clave

- Entrenado con 24 manuscritos datados por carbono-14.
- Margen de error medio de ~30 años, más preciso que el carbono-14 aislado para este periodo.
- Acertó la edad de los manuscritos un 85% de las veces en pruebas de validación.
- Analizó 135 manuscritos sin fecha, obteniendo resultados considerados "realistas" por los expertos en un 79% de los casos.
- No destruye material: solo necesita imágenes digitales, a diferencia del carbono-14 que requiere cortar un fragmento del manuscrito.
- Reveló que muchos manuscritos son entre 50 y 150 años más antiguos de lo que se creía, alterando la cronología aceptada del judaísmo antiguo.

### Análisis de características de sistema inteligente

| Característica | ¿Se cumple? | Justificación |
|----------------|:-----------:|---------------|
| **Inteligencia** | ✅ Sí | Logra su objetivo principal: datar manuscritos con un 85% de acierto y un margen de ~30 años, superando en precisión a la paleografía humana tradicional en muchos casos. |
| **Sistematización** | ✅ Sí | Sus componentes (BiNet para extracción de características, regresión bayesiana para predicción, base de datos de C-14) están fuertemente interrelacionados. La salida de cada módulo alimenta al siguiente. |
| **Objetivo** | ✅ Sí | Tiene un objetivo claro y definido: predecir la fecha de creación de un manuscrito antiguo a partir de su escritura. |
| **Capacidad sensorial** | ✅ Parcial | Recibe información del entorno a través de imágenes digitalizadas de manuscritos, pero no de forma autónoma: depende de que un humano le proporcione las imágenes. No tiene sensores propios. |
| **Conceptualización** | ✅ Sí | Genera conceptos abstractos a partir de datos concretos: transforma trazos de tinta en vectores numéricos que representan "estilos de escritura" como conceptos. Desarrolla niveles de abstracción al agrupar formas de letras en patrones temporales. |
| **Reglas de actuación** | ✅ Sí | A través del entrenamiento, ha aprendido reglas que relacionan estilos de escritura (situación) con rangos de fechas (consecuencia). La regresión bayesiana codifica estas relaciones. |
| **Memoria** | ✅ Sí | Almacena los pesos del modelo entrenado, que representan toda la "experiencia" acumulada a partir de los 24 manuscritos de referencia. Esta memoria es persistente y reutilizable. |
| **Aprendizaje** | ✅ Parcial | Aprendió durante su fase de entrenamiento, pero actualmente no sigue aprendiendo de forma autónoma con cada nuevo manuscrito que analiza. Los autores señalan que se pueden añadir nuevos datos de C-14 para reentrenarlo y mejorar su precisión, pero esto requiere intervención humana. |

---

## Aplicación 2: Neuralink BCI — Interfaces cerebro-computador con IA

### Campo: Neurotecnología / Medicina

### Descripción

Neuralink es una empresa fundada por Elon Musk en 2016 que desarrolla interfaces cerebro-computador (BCI, *Brain-Computer Interface*) implantables. Su dispositivo, del tamaño de una moneda, se inserta en el cráneo y conecta miles de microelectrodos ultrafinos al córtex cerebral. Mediante algoritmos de IA, decodifica la actividad neuronal en tiempo real para que personas con parálisis puedan controlar dispositivos digitales, brazos robóticos o restaurar el habla, todo usando solo el pensamiento.

A junio de 2025, cinco personas con parálisis severa utilizan Neuralink en su vida diaria. En mayo de 2025, la FDA le otorgó la designación de "Breakthrough Device" para restauración del habla.

### ¿Cómo funciona internamente?

1. **Implantación:** Un robot quirúrgico especializado (R1) implanta hilos de polímero flexibles de 5 micrómetros de diámetro, cada uno con electrodos CMOS personalizados, en el córtex motor y/o áreas del lenguaje. Evita automáticamente los vasos sanguíneos.
2. **Registro neuronal:** Los electrodos registran la actividad eléctrica de miles de neuronas individuales (*spikes* y potenciales de campo local). El implante es inalámbrico y se recarga de forma remota.
3. **Decodificación por IA:** Algoritmos de aprendizaje automático procesan las señales neuronales en tiempo real. Para control del cursor: traducen patrones de activación neuronal en coordenadas de movimiento. Para habla: decodifican la intención de pronunciar palabras y las convierten en texto o en voz sintética.
4. **Retroalimentación:** Se está desarrollando un sistema de "bucle cerrado" donde el cerebro no solo envía órdenes sino que recibe información de vuelta (sensación de tacto o presión), imitando el movimiento natural.

### Datos clave

- Cinco participantes con parálisis usan el dispositivo, algunos más de 100 horas semanales.
- El dispositivo Telepathy permite controlar cursores, jugar videojuegos, mover brazos robóticos.
- Un modelo de IA entrenado con grabaciones de voz previas a la ELA de un paciente logró restaurar su voz natural (no una voz robótica genérica).
- Neuralink ha recaudado más de 650 millones de dólares (Serie C, junio 2025).
- Ensayos clínicos activos en EE.UU., Reino Unido, Canadá y Emiratos Árabes.
- Competidores como Paradromics (200+ bps vs 10 bps de Neuralink) y Synchron (BCI menos invasivo a través de vena yugular) están también en ensayos humanos.

### Dilemas éticos

- **Responsabilidad:** Si la IA media entre el cerebro y una acción, ¿quién es responsable si algo sale mal?
- **Privacidad neuronal:** ¿Quién tiene acceso a los datos de actividad cerebral? ¿Son "tus pensamientos" o datos de la empresa?
- **Equidad:** Dispositivos de alto coste que podrían crear una brecha entre quienes pueden y no pueden acceder a la tecnología.
- **Autonomía:** En un sistema de bucle cerrado, ¿hasta qué punto las decisiones son del usuario o del algoritmo?

### Análisis de características de sistema inteligente

| Característica | ¿Se cumple? | Justificación |
|----------------|:-----------:|---------------|
| **Inteligencia** | ✅ Sí | Logra sus objetivos: permite a personas con parálisis total controlar dispositivos, comunicarse e incluso recuperar el habla. Los participantes lo usan de forma independiente en su vida diaria. |
| **Sistematización** | ✅ Sí | Es un sistema altamente integrado: electrodos, implante inalámbrico, robot quirúrgico, algoritmos de decodificación, software de interfaz. Todos los componentes están fuertemente interrelacionados y son interdependientes. |
| **Objetivo** | ✅ Sí | Tiene objetivos claros y jerarquizados: objetivo principal (restaurar funciones perdidas), subobjetivos (decodificar intención motora, traducir señales a acciones, adaptarse al usuario). |
| **Capacidad sensorial** | ✅ Sí | Tiene una capacidad sensorial directa y en tiempo real: miles de electrodos captan la actividad eléctrica de neuronas individuales, registrando el "entorno" cerebral de forma continua. Es el sistema de los tres con la capacidad sensorial más autónoma. |
| **Conceptualización** | ✅ Sí | Los algoritmos de decodificación generan representaciones abstractas: transforman patrones de actividad neuronal bruta en "conceptos" como "intención de mover el cursor a la derecha" o "intención de decir la palabra 'hola'". Estos conceptos son de alto nivel de abstracción. |
| **Reglas de actuación** | ✅ Sí | El sistema tiene reglas claras que relacionan patrones neuronales (situación) con acciones específicas (movimiento del cursor, generación de voz). Estas reglas se calibran para cada usuario individual. |
| **Memoria** | ✅ Sí | Almacena los modelos de decodificación calibrados para cada usuario, los perfiles neuronales individuales y, en el caso de la restauración de voz, grabaciones de la voz original del paciente. |
| **Aprendizaje** | ✅ Sí | Es el sistema con la capacidad de aprendizaje más robusta de los tres: se calibra y mejora continuamente con cada sesión de uso. Los algoritmos se adaptan a cambios en los patrones neuronales del usuario (por ejemplo, si electrodos se desplazan ligeramente). Además, los usuarios también "aprenden" a generar patrones más claros para el sistema, creando un bucle de aprendizaje mutuo. |

---

## Aplicación 3: SpeciesNet y WildDrone — IA para conservación de fauna

### Campo: Ecología / Conservación de la biodiversidad

### Descripción

SpeciesNet es un modelo de IA open source desarrollado por WWF en colaboración con Google y otras organizaciones de conservación, integrado en la plataforma Wildlife Insights. Identifica automáticamente especies animales en millones de fotografías de cámaras trampa desplegadas en ecosistemas de todo el mundo. Complementariamente, WildDrone es un proyecto financiado por la UE que utiliza drones autónomos equipados con IA para monitorizar fauna de forma no invasiva, y FLIR es un sistema de cámaras térmicas con IA usado para detectar furtivos en reservas de Kenia.

### ¿Cómo funciona internamente?

**SpeciesNet:**
1. **Captura:** Miles de cámaras trampa con sensores infrarrojos de movimiento fotografían animales automáticamente en su hábitat natural.
2. **Detección:** Una primera red neuronal determina si en la imagen hay un animal, un humano, un vehículo o nada (precisión: 99.4% para animales).
3. **Clasificación:** Una segunda red neuronal identifica la especie del animal detectado (precisión: 94.5% a nivel de especie). Ha sido entrenada con más de 65 millones de imágenes.
4. **Análisis:** Los datos se agregan en la plataforma Wildlife Insights para analizar tendencias poblacionales, cambios de hábitat y amenazas.

**WildDrone:**
1. Drones autónomos equipados con cámaras de alta resolución e infrarrojas sobrevuelan zonas protegidas.
2. Algoritmos de visión por computador identifican no solo la especie, sino individuos concretos por sus marcas, tamaño y peso estimado.
3. Los datos se transmiten en tiempo real a los conservacionistas.

**FLIR anti-furtivismo:**
1. Cámaras térmicas con visión nocturna detectan movimientos de humanos, vehículos o animales.
2. La IA distingue entre fauna legítima y posibles furtivos.
3. Envía alertas en tiempo real a los rangers de la reserva.

### Datos clave

- SpeciesNet detecta animales en el 99.4% de las imágenes y acierta la especie el 94.5% de las veces.
- Entrenado con más de 65 millones de imágenes de cámaras trampa.
- Desde marzo de 2025 es open source, disponible en GitHub para cualquier investigador.
- 11 reservas de rinocerontes en Kenia usan cámaras FLIR con IA, reduciendo drásticamente la caza furtiva.
- WildDrone (proyecto europeo, Universidad de Dinamarca del Sur) identifica individuos concretos, no solo especies.
- Conservation AI procesa más de 1.5 millones de imágenes semanales para más de 900 proyectos activos en todo el mundo.

### Análisis de características de sistema inteligente

| Característica | ¿Se cumple? | Justificación |
|----------------|:-----------:|---------------|
| **Inteligencia** | ✅ Sí | Logra sus objetivos con alta eficacia: identifica especies con un 94.5% de precisión, detecta furtivos en tiempo real y ha contribuido a reducir significativamente la caza furtiva en las zonas donde se ha desplegado. |
| **Sistematización** | ✅ Sí | Integra múltiples subsistemas interrelacionados: cámaras trampa, drones, cámaras térmicas, redes neuronales de detección y clasificación, plataforma de análisis Wildlife Insights, y sistema de alertas para rangers. Todos trabajan coordinados. |
| **Objetivo** | ✅ Sí | Objetivos claramente definidos: identificar especies (SpeciesNet), monitorizar poblaciones (WildDrone), detectar y prevenir furtivismo (FLIR). |
| **Capacidad sensorial** | ✅ Sí | Es el sistema con la capacidad sensorial más diversa: cámaras trampa con infrarrojos, cámaras térmicas nocturnas, drones con visión aérea. Recibe información del entorno de forma autónoma y continua (24/7 sin intervención humana). |
| **Conceptualización** | ✅ Sí | Genera conceptos abstractos a partir de datos sensoriales: transforma píxeles en "especie: jaguar", "amenaza: presencia humana nocturna", "individuo: rinoceronte #47 por patrón de cuerno". Son niveles de abstracción crecientes. |
| **Reglas de actuación** | ✅ Parcial | Tiene reglas para clasificar y alertar (si detecta humano nocturno → alerta a ranger), pero las decisiones finales de actuación las toman los humanos. El sistema por sí solo no actúa sobre el entorno, solo informa. |
| **Memoria** | ✅ Sí | Almacena los modelos entrenados y la base de datos de Wildlife Insights con millones de registros. Además, la plataforma mantiene un historial acumulativo que permite analizar tendencias a lo largo de los años. |
| **Aprendizaje** | ✅ Sí | SpeciesNet se ha reentrenado sucesivamente con conjuntos de datos cada vez mayores (de miles a 65 millones de imágenes), mejorando su precisión. Al ser open source, la comunidad puede contribuir con nuevos datos y mejoras. Sin embargo, el reentrenamiento no es automático: requiere intervención humana para incorporar nuevas imágenes etiquetadas. |

---

## Tabla comparativa

| Característica | Enoch (Arqueología) | Neuralink BCI (Neurotecnología) | SpeciesNet/WildDrone (Conservación) |
|----------------|:-------------------:|:-------------------------------:|:-----------------------------------:|
| Inteligencia | ✅ | ✅ | ✅ |
| Sistematización | ✅ | ✅ | ✅ |
| Objetivo | ✅ | ✅ | ✅ |
| Capacidad sensorial | ⚠️ Parcial | ✅ | ✅ |
| Conceptualización | ✅ | ✅ | ✅ |
| Reglas de actuación | ✅ | ✅ | ⚠️ Parcial |
| Memoria | ✅ | ✅ | ✅ |
| Aprendizaje | ⚠️ Parcial | ✅ | ✅ |

**Observaciones:**
- **Neuralink** es el sistema que más se acerca a un sistema inteligente "completo" según la definición de Wikipedia: tiene capacidad sensorial autónoma, aprendizaje continuo y un bucle de retroalimentación con su entorno (el cerebro del usuario).
- **Enoch** tiene limitaciones en capacidad sensorial (depende de que le proporcionen imágenes) y aprendizaje (no aprende de forma continua tras el entrenamiento).
- **SpeciesNet/WildDrone** tiene una capacidad sensorial muy autónoma (cámaras 24/7, drones), pero sus reglas de actuación están limitadas a clasificar e informar: no actúa directamente sobre el entorno.

---

## Conclusiones

Las tres aplicaciones demuestran el enorme potencial de la IA en campos muy diferentes. Sin embargo, ninguna constituye un sistema inteligente "completo" en el sentido estricto de la definición: todas dependen, en mayor o menor medida, de la intervención humana para funcionar.

Neuralink es el caso más cercano a un sistema inteligente completo, ya que opera en tiempo real, tiene sensores propios, aprende de forma continua y actúa directamente sobre su entorno. Sin embargo, también es el que plantea los dilemas éticos más profundos: la frontera entre las decisiones del usuario y las del algoritmo se difumina cuando la IA media directamente entre el cerebro y las acciones del cuerpo.

Estas aplicaciones reflejan una tendencia clara: la IA no está reemplazando a los expertos humanos, sino amplificando sus capacidades. Enoch no sustituye a los paleógrafos, SpeciesNet no reemplaza a los biólogos de campo, y Neuralink no prescinde de los neurocirujanos. En los tres casos, la combinación de inteligencia humana y artificial produce resultados que ninguna de las dos lograría por separado.

---

## Fuentes

### Enoch (Arqueología)
- Popović, M. et al. (2025). *Dating ancient manuscripts using radiocarbon and AI-based writing style analysis*. PLOS One. [Enlace](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0323185)
- Biblical Archaeology Society (2025). *Can AI Date the Dead Sea Scrolls?* [Enlace](https://www.biblicalarchaeology.org/daily/biblical-artifacts/dead-sea-scrolls/can-ai-date-the-dead-sea-scrolls/)
- CNN (2025). *AI analysis of ancient handwriting gives new age estimates for Dead Sea Scrolls*. [Enlace](https://www.cnn.com/2025/06/07/science/dead-sea-scrolls-older-ai-carbon-dating)
- European Research Council (2025). *Unlocking the timecode of the Dead Sea Scrolls*. [Enlace](https://erc.europa.eu/news-events/news/unlocking-timecode-dead-sea-scrolls)

### Neuralink BCI (Neurotecnología)
- Neuralink (2025). Actualización pública del programa PRIME. [Enlace](https://neuralink.com)
- Nature (2025). *A brain implant that could rival Neuralink's enters clinical trials*. [Enlace](https://www.nature.com/articles/d41586-025-03849-0)
- MassDevice (2025). *Neuralink wins FDA breakthrough nod for speech impairment BCI*. [Enlace](https://www.massdevice.com/neuralink-fda-breakthrough-nod-speech-impairment/)
- TechLifeSci (2026). *2025 Neurotech Review: BCIs, Brain Delivery, Organoids & Neuro-AI Move Closer to Clinic*. [Enlace](https://www.techlifesci.com/p/2025-neurotech-review)
- Contrary Research (2025). *Neuralink Business Breakdown*. [Enlace](https://research.contrary.com/company/neuralink)

### SpeciesNet / WildDrone (Conservación)
- WWF (2025). *Using the power of AI to identify and track species*. [Enlace](https://www.worldwildlife.org/news/stories/using-the-power-of-ai-to-identify-and-track-species/)
- WWF (2025). *Artificial Intelligence and Conservation*. [Enlace](https://www.worldwildlife.org/our-work/science/artificial-intelligence-and-conservation/)
- World Economic Forum (2025). *How innovation is driving conservation efforts in Kenya*. [Enlace](https://www.weforum.org/stories/2025/03/biologists-technologists-conservation-wildlife-kenya/)
- MDPI (2024). *Harnessing Artificial Intelligence for Wildlife Conservation*. [Enlace](https://www.mdpi.com/2673-7159/4/4/41)

### Referencia general
- Wikipedia. *Sistema inteligente*. [Enlace](https://es.wikipedia.org/wiki/Sistema_inteligente)
