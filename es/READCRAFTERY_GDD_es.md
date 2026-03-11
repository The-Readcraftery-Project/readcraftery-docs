# READCRAFTERY — Documento de Diseño del Juego
**Versión:** 1.2  
**Fecha:** marzo de 2026  
**Estado:** Especificación de preproducción  
**Autor:** Andrés Reyes. El Programador Pobre  
**Documentos complementarios:** Architecture Contract v1.1 · Build Guide v1.3  

---

> **Nota para lectores técnicos:** Este documento describe la visión y el diseño del juego.
> Es intencionalmente aspiracional: incluye funciones como Teacher Dashboard,
> karaoke-style highlighting y soporte RTL que todavía no tienen contrato técnico cerrado.
> Para saber qué está especificado y construible hoy, ver el **Architecture Contract**.
> Para el orden de construcción y la guía de implementación, ver el **Build Guide**.

---

## Tabla de Contenidos

1. [Visión general del juego](#1-visión-general-del-juego)
2. [Visión y pilares](#2-visión-y-pilares)
3. [Público objetivo](#3-público-objetivo)
4. [Bucle principal de juego](#4-bucle-principal-de-juego)
5. [Mecánicas de puzzles](#5-mecánicas-de-puzzles)
6. [Sistema de integración literaria](#6-sistema-de-integración-literaria)
7. [Progresión y recompensas](#7-progresión-y-recompensas)
8. [Efectos visuales y feedback](#8-efectos-visuales-y-feedback)
9. [Diseño UI/UX](#9-diseño-uiux)
10. [Diseño de audio](#10-diseño-de-audio)
11. [Accesibilidad y localización](#11-accesibilidad-y-localización)
12. [Herramientas para docentes y familias](#12-herramientas-para-docentes-y-familias)
13. [Sistema de modding](#13-sistema-de-modding)
14. [Estrategia de monetización](#14-estrategia-de-monetización)
15. [Estrategia de plataformas](#15-estrategia-de-plataformas)
16. [Recomendación de stack tecnológico](#16-recomendación-de-stack-tecnológico)
17. [Arquitectura técnica](#17-arquitectura-técnica)
18. [Descripciones de concept art](#18-descripciones-de-concept-art)
19. [Hoja de ruta de lanzamiento](#19-hoja-de-ruta-de-lanzamiento)
20. [Preguntas abiertas y riesgos](#20-preguntas-abiertas-y-riesgos)
21. [Apéndice A — Glosario](#apéndice-a--glosario)
22. [Apéndice B — Panorama competitivo](#apéndice-b--panorama-competitivo)

---

## 1. Visión general del juego

| Campo | Detalle |
|---|---|
| **Título** | READCRAFTERY |
| **Eslogan** | *"Every word is an adventure."* |
| **Género** | Juego educativo de palabras / aventura literaria |
| **Plataforma principal** | PC (Windows/Mac/Linux), Web (HTML5), Android e iOS |
| **Edad objetivo** | 4–9 años (núcleo); 6–12 con uso escolar/docente |
| **Idiomas de lanzamiento** | Inglés, español (+ la API de modding admite cualquier idioma) |
| **Monetización** | Pago único (itch.io / Steam) — pagas una vez, tuyo para siempre |

### Elevator pitch
READCRAFTERY es un juego de descubrimiento de palabras que envuelve contenido literario apropiado para cada edad dentro de mecánicas de puzzle divertidas y coloridas. Los jugadores exploran una biblioteca mágica, eligen libros y luego se sumergen en el texto: buscan palabras ocultas, reordenan letras y conectan significado con historia. Cada palabra encontrada se anima, brilla y recompensa al jugador con progreso narrativo, personajes desbloqueables y celebraciones visuales. Los docentes pueden asignar libros específicos y seguir el progreso. Todo el juego —desde los libros hasta los temas visuales— es moddable por la comunidad.

---

## 2. Visión y pilares

### Pilares de diseño

| Pilar | Descripción |
|---|---|
| 🔤 **La lectura primero** | Toda mecánica debe reforzar habilidades lectoras, nunca reemplazarlas. El texto siempre está presente y en el centro. |
| 🎉 **Recompensa alegre** | Los niños deben sentirse celebrados con frecuencia. El feedback visual y sonoro debe ser inmediato, cálido y emocionante. |
| 📚 **Respeto por lo literario** | Los libros no son simples bancos de palabras: la historia importa. El jugador debe salir habiendo absorbido contenido. |
| 🔧 **Abierto por diseño** | El modding no es un añadido tardío; el sistema de contenido ES el juego. Los libros son mods. Los themes son mods. |
| 👩‍🏫 **Docente empoderado** | El juego también funciona como herramienta de aula. Los docentes necesitan control sin tener que ser desarrolladores. |

---

## 3. Público objetivo

### Primario: niños de 4 a 9 años

**Subsegmentos:**
- **4–6 años (prelectores / fonética inicial):** foco en reconocimiento de letras, palabras simples de 2–3 letras y vocabulario con apoyo visual. Necesitan mucho soporte visual, tipografías grandes y lectura en voz alta de todo el texto.
- **6–9 años (lectores iniciales):** pueden manejar palabras de 4–6 letras, oraciones básicas y pasajes cortos. Se benefician de pistas contextuales y preguntas de comprensión.

### Perfiles de lector — segmentación interna

El rango 4–9 cubre etapas de desarrollo lector muy distintas.
El juego reconoce tres perfiles internos:

**Perfil A — Prelector (4–5 años)**
No decodifica todavía. Reconoce letras y su nombre.
El juego ofrece exposición al lenguaje escrito y conciencia fonológica.
Los book packs marcados `early_emergent` están diseñados para este perfil.
WordGlow en modo simplificado (TTS lee cada palabra al tocarla, sin expectativa de lectura autónoma).

**Perfil B — Lector emergente (6–7 años)**
Está aprendiendo a decodificar. Lee sílaba por sílaba.
Necesita palabras fonéticamente regulares, repetición, y feedback sin frustración.
Es el perfil primario de diseño de Readcraftery.

**Perfil C — Lector en desarrollo con dificultades (7–9 años)**
Puede leer con esfuerzo. Puede tener dislexia, TDAH, o menor exposición previa.
Necesita textos con vocabulario controlado, fuentes apropiadas, y ritmo sin exposición negativa.
El modo `dyslexia_font` y `reduce_motion` están diseñados principalmente para este perfil.

> **Nota de diseño:** El Perfil B es el centro de gravedad del juego.
> Las decisiones de diseño que entren en conflicto entre perfiles
> se resuelven a favor del Perfil B.


### Secundario: educadores y familias
- Docentes de primaria que buscan herramientas de alfabetización
- Padres y madres que buscan tiempo de pantalla con valor de aprendizaje
- Familias homeschool

### Terciario: comunidad de modding
- Desarrolladores indie que quieran subir libros de dominio público
- Docentes que quieran crear sus propios book packs
- Personas aficionadas a los puzzles de palabras (10+) atraídas por el contenido de la comunidad

### Ejemplos de persona

**“Sofía, 6 años”** — aprende a leer en español e inglés en casa. Le encantan los colores vivos y los animales. Se frustra rápido si los puzzles son demasiado difíciles. Necesita soporte de audio y refuerzo positivo constante.

**“Ms. Rivera, docente de 2.º grado”** — quiere asignar el mismo libro a su clase y seguir qué estudiantes encontraron todas las palabras. Necesita un panel docente, una configuración simple y acceso gratuito o de bajo costo.

**“Carlos, desarrollador indie”** — quiere subir un libro de dominio público y crear un puzzle pack para compartir en itch.io. Necesita documentación JSON clara y una herramienta de previsualización para mods.

---

## 4. Bucle principal de juego

```text
┌─────────────────────────────────────────────────────────────┐
│                  EL BUCLE DE READCRAFTERY                  │
│                                                             │
│  [BIBLIOTECA] → [ELEGIR LIBRO] → [LEER PASAJE]             │
│                                         ↓                   │
│  [CELEBRAR] ← [ENCONTRAR PALABRAS] ← [DESAFÍO DE PUZZLE]   │
│       ↓                                                     │
│  [DESBLOQUEAR: siguiente pasaje / sticker / theme]          │
│       ↓                                                     │
│  [VOLVER A LA BIBLIOTECA o CONTINUAR LIBRO]                 │
└─────────────────────────────────────────────────────────────┘
```

### Flujo paso a paso

1. **La Gran Biblioteca** — El menú principal es una biblioteca acogedora y mágica. Las estanterías cubren las paredes. Los libros brillan suavemente para invitar a interactuar. El búho compañero del jugador descansa cerca.

2. **Selección de libro** — El jugador escoge un libro. Cada libro muestra portada, título, una valoración de dificultad de 1–3 estrellas y una insignia de conteo de palabras. Los libros nuevos se bloquean hasta reunir suficientes estrellas.

3. **Momento de lectura (Passage View)** — Se muestra un pasaje del libro. Fuente grande y amigable. Ilustración al lado si el pack la incluye. El búho lector lee el pasaje en voz alta (TTS o audio pregrabado). El jugador puede repetir la lectura en cualquier momento.

4. **Desafío de puzzle** — Debajo o junto al pasaje aparece un puzzle. El tipo depende del nivel de dificultad y del perfil de edad del jugador.

5. **Descubrimiento de palabras** — El jugador interactúa con letras o palabras. Cada acierto dispara celebración visual inmediata.

6. **Pasaje completado** — Una pantalla de “capítulo completado” muestra estrellas ganadas, palabras aprendidas y una breve pregunta o resumen para reforzar comprensión.

7. **Desbloqueo y progreso** — Se desbloquea el siguiente pasaje o un bonus (sticker, elemento visual, mini-historia). El jugador vuelve a la biblioteca o continúa.

---

## 5. Mecánicas de puzzles

### Puzzle tipo 1: Word Glow (4–6 años, dificultad ★☆☆)
**Mecánica principal:** el pasaje completo se muestra en pantalla. Una palabra objetivo aparece en el banco de palabras inferior. El jugador debe tocar esa misma palabra cuando la detecta en el pasaje.

- Las palabras del pasaje se iluminan sutilmente al pasar por encima.
- La palabra objetivo se muestra con un icono o imagen de apoyo.
- El audio lee la palabra objetivo en voz alta.
- Sin límite de tiempo. Sin estado de fracaso: solo guía y ánimo.
- Al acertar, la palabra “vuela” desde el pasaje hasta su hueco del word bank con chispas.

**Habilidad reforzada:** reconocimiento visual de palabras, sight words, escaneo de izquierda a derecha.

### Puzzle tipo 2: Letter Scramble (5–7 años, dificultad ★★☆)
**Mecánica principal:** una palabra del pasaje aparece desordenada bajo el texto. El jugador reordena fichas de letras para escribirla correctamente.

- Las letras mezcladas se apoyan sobre una pequeña “mesa de trabajo”.
- Hay una pista visual opcional (tocar al búho para recibir ayuda, con usos limitados).
- La palabra correspondiente en el pasaje está difuminada u oculta hasta resolverla.
- Al acertar, la palabra del pasaje “se desenfoca” con un pequeño pop satisfactorio.

**Habilidad reforzada:** orden de letras, patrones ortográficos, fonética.

### Puzzle tipo 3: Word Hunt Grid (6–9 años, dificultad ★★☆ a ★★★)
**Mecánica principal:** se genera una sopa de letras con letras del pasaje. El jugador encuentra entre 5 y 10 palabras ocultas.

- Para perfiles jóvenes, las palabras van solo de izquierda a derecha y de arriba abajo; las diagonales se desbloquean en dificultad 3.
- Al encontrar una palabra en la cuadrícula, también se resalta en el pasaje, conectando puzzle y contexto literario.
- La lista de palabras aparece con pequeños iconos.

**Habilidad reforzada:** ortografía, vocabulario, reconocimiento de patrones.

### Puzzle tipo 4: Fill the Passage (7–9 años, dificultad ★★★)
**Mecánica principal:** una oración del pasaje aparece con 1–3 huecos. Se ofrecen varias fichas con palabras y el jugador arrastra la correcta a cada hueco.

- Los intentos incorrectos tiemblan y vuelven a su sitio; no hay sonido de castigo.
- La colocación correcta hace que toda la oración “se ilumine”.
- Los distractores son plausibles pero incorrectos.

**Habilidad reforzada:** comprensión lectora, vocabulario en contexto, conciencia gramatical.

### Puzzle tipo 5: Rhyme Finder (4–7 años, dificultad ★★☆)
**Mecánica principal:** se destaca una palabra del pasaje. El jugador debe encontrar otra palabra que rime con ella, ya sea dentro del pasaje o en un set de opciones.

- Las parejas de rima se definen durante la autoría del book pack.
- El soporte de audio lee ambas palabras para compararlas.

**Habilidad reforzada:** conciencia fonémica, reconocimiento de rimas.

### Escalado de dificultad

| Perfil de edad | Puzzles por defecto | Longitud de palabra | Tiempo límite | Pistas |
|---|---|---|---|---|
| 4–5 años | Word Glow, Rhyme Finder | 2–4 letras | Ninguno | Ilimitadas |
| 5–6 años | Word Glow, Letter Scramble | 3–5 letras | Ninguno | 3 por puzzle |
| 6–7 años | Scramble, Word Hunt | 3–6 letras | Opcional | 2 por puzzle |
| 7–9 años | Word Hunt, Fill Passage | 4–8 letras | Opcional | 1 por puzzle |

El perfil se define durante el onboarding y puede cambiarse por padre/madre o docente en cualquier momento.

---

## 6. Sistema de integración literaria

### Estructura de un libro

```text
Book Pack
├── metadata.json
├── cover.png
├── passages/
│   ├── passage_01.json
│   ├── passage_02.json
│   └── ...
├── audio/
│   ├── passage_01_en.ogg
│   └── passage_01_es.ogg
└── illustrations/
    └── passage_01.png
```

### Formato JSON de un pasaje (ejemplo)

```json
{
  "id": "passage_01",
  "title": "The Brave Little Seed",
  "text": "Once upon a time, a tiny seed fell from a great oak tree. The wind carried it far across the green meadow.",
  "language": "en",
  "difficulty": 1,
  "illustration": "passage_01.png",
  "audio": "passage_01_en.ogg",
  "puzzles": [
    {
      "type": "word_glow",
      "targets": ["seed", "wind", "tree", "green"]
    },
    {
      "type": "word_hunt",
      "targets": "auto",
      "auto_config": {
        "word_count": 6,
        "min_length": 3,
        "max_length": 7,
        "pos_filter": ["noun", "verb"]
      }
    },
    {
      "type": "scramble",
      "targets": ["meadow", "carried"]
    }
  ],
  "comprehension_question": {
    "text": "Where did the wind carry the seed?",
    "options": ["A forest", "A green meadow", "A big city"],
    "correct": 1
  }
}
```

> **Regla de autogeneración:** cuando `targets` es la cadena `"auto"`, `PuzzleGenerator` corre al cargar el pack y completa el array de objetivos antes de que cualquier escena `IPuzzle` reciba la `PuzzleDefinition`. El puzzle nunca distingue entre objetivos escritos a mano y objetivos generados automáticamente. Las estrellas otorgadas son idénticas.

> **Algoritmo de autogeneración (v1 — basado en reglas, sin dependencia NLP):**
> 1. Tokenizar el texto del pasaje
> 2. Pasar a minúsculas y quitar puntuación
> 3. Eliminar stopwords
> 4. Filtrar por `min_length` / `max_length`
> 5. Eliminar duplicados
> 6. Ordenar por frecuencia general del corpus (las palabras más raras se priorizan)
> 7. Tomar las primeras `word_count`
> 8. *(M1)* Filtrar palabras con mayúscula para reducir nombres propios
> 9. *(M1)* Filtrar tokens con apóstrofes o guiones
> 10. *(M2)* Ratio opcional de sight words, configurable por docente

> **Bundle de stopwords (formato categorizado):**
```json
{
  "always_exclude": ["a", "an", "the", "of", "in", "on", "at"],
  "exclude_age_4_6": ["because", "although", "nevertheless", "through"],
  "exclude_age_6_9": [],
  "pedagogical_override": ["the", "and", "is"]
}
```

Las palabras de `pedagogical_override` se excluyen por defecto, pero pueden reintroducirse con `"include_pedagogical_overrides": true`. Los listados `stopwords_en.json` y `stopwords_es.json` van embebidos en el motor y versionados en el repo. Los packs pueden añadir overrides por pack vía `metadata.json`.

> **Flag interno:** los puzzles generados automáticamente registran `"auto_generated": true` en el save del puzzle. Esto nunca se muestra al jugador, pero sí permite depurar la calidad del generador en reportes docentes o parentales.

### Biblioteca built-in de lanzamiento

| Libro | Rango de edad | Idioma | Fuente |
|---|---|---|---|
| *The Little Seed* (original) | 4–6 | EN, ES | Contenido original |
| *Adventures of Pip the Puppy* (original) | 5–7 | EN, ES | Contenido original |
| *Aesop's Fables — Selections* | 6–9 | EN, ES | Dominio público |
| *Simple Science Stories* (original) | 6–8 | EN, ES | Contenido original |
| *Fairy Tales for Early Readers* | 5–8 | EN, ES | Texto PD reescrito |

> **Política de licencias de contenido:** “adaptaciones de dominio público” es una categoría de riesgo y no debe aparecer en contenido publicado sin trazabilidad. Las opciones seguras son: (a) texto original del autor, (b) texto PD usado literalmente desde una edición verificada anterior a 1928, o (c) texto fuente PD completamente reescrito. Traducciones pos-1928 e ilustraciones de terceros se presumen protegidas. Debe existir un `CONTENT_LICENSING.md` antes de cualquier distribución pública.

---

## 7. Progresión y recompensas

### Sistema de estrellas
Cada puzzle otorga 1–3 estrellas:
- ⭐ — completado usando 2 o más pistas
- ⭐⭐ — completado con 1 pista
- ⭐⭐⭐ — completado sin pistas

Las estrellas desbloquean nuevos libros en la biblioteca.

### El búho lector
El compañero del jugador (nombrado al inicio) crece y cambia con el progreso:
- Gana accesorios: sombreros, bufandas, gafas, alas, etc.
- Reacciona emocionalmente al rendimiento
- Puede renombrarse y cambiar de aspecto mediante themes desbloqueables

### Protocolo de feedback del Owl — ✅ CERRADO

El Owl es la pieza pedagógica más importante del juego.
Su comportamiento ante el error determina si el niño sigue intentando
o desarrolla una identidad negativa como lector.

**Regla fundamental: el Owl nunca evalúa — modela.**

#### Cuando el niño no interactúa por más de 8 segundos:
- El Owl entra en estado `thinking`
- Después de 5 segundos adicionales: el Owl lee la palabra target en voz alta
  y la silabea lentamente (TTS con pausa entre sílabas)
- El hint se ofrece sin que el niño tenga que pedirlo
- No se registra como "hint usado" si fue automático por inactividad

#### Cuando el niño selecciona una palabra incorrecta:
- Sin X roja. Sin sonido de error.
- El Owl dice la palabra seleccionada en voz alta (TTS)
- Pausa de 1 segundo
- El Owl dice la palabra target en voz alta
- El tile incorrecto regresa a su posición sin animación de fracaso
- El contador de intentos no es visible para el niño

#### Cuando el niño encuentra una palabra correcta:
- Feedback positivo inmediato — el Owl entra en `happy`
- La palabra se destaca en el pasaje
- TTS lee la palabra y la usa en una oración corta (M1)

#### Lo que el Owl nunca hace:
- Mostrar un contador de errores
- Expresar impaciencia o frustración
- Interrumpir al niño mientras está intentando
- Celebrar de forma que exponga al niño frente a otros

#### Hints automáticos vs manuales:
- **Automático** (inactividad > 13 segundos): no se descuenta de `hint_count`
- **Manual** (niño presiona botón hint): se descuenta de `hint_count`
- `hint_count` mínimo: 3 por puzzle, independiente de la dificultad

### Colección de stickers
Cada libro completado añade stickers al “Reading Journal”, un scrapbook persistente del jugador.

### Reading Journal
Registro visual persistente de:
- libros leídos y porcentaje completado
- palabras favoritas guardadas
- total de estrellas por libro
- insignias obtenidas

### Insignias

| Insignia | Disparador |
|---|---|
| First Word! | Encontrar la primera palabra |
| Bookworm | Completar el primer libro |
| No Hints Needed | Completar un puzzle sin pistas |
| Speed Reader | Completar un puzzle por debajo del tiempo objetivo |
| Library Card | Desbloquear 5 libros |
| Word Collector | Guardar 50 palabras en el journal |
| Language Star | Completar un puzzle en un segundo idioma |

---

## 8. Efectos visuales y feedback

### Filosofía de diseño
Para edades 4–9, el feedback debe ser **inmediato (<200ms)**, **visualmente claro** y **emocionalmente cálido**. Evitar cruces rojas duras o castigos visuales. Se usa redirección y ánimo.

### Efectos de éxito
- **Sparkle Burst:** la palabra emite chispas con colores del theme del libro
- **Word Flight:** la palabra se eleva del pasaje y vuela al banco de palabras
- **Letter Pop:** cada letra correcta rebota en secuencia
- **Star Rain:** al completar el puzzle caen entre 1 y 3 estrellas con un chime suave
- **Owl Dance:** el búho salta, bate alas o celebra según el contexto

### Efectos de intento incorrecto
- **Gentle Wobble:** los tiles tiemblan y vuelven a posición
- **Owl Hint Nudge:** el búho inclina la cabeza, curioso
- **Soft Glow Fade:** las letras probadas brillan un instante en ámbar y se desvanecen

### Pantalla de pasaje completado
- Confetti con colores del libro
- Estrellas animadas una a una
- Animación especial del búho
- Nuevo sticker deslizándose hacia el journal

### Sistema de variedad
Para evitar fatiga visual:
- 5 paletas de chispas por libro
- 3 animaciones de celebración del búho
- 4 patrones de confetti
- Intensidad escalable para rachas de aciertos

---

## 9. Diseño UI/UX

### Principios para edades 4–9
- **Tap targets grandes** — mínimo 48x48dp móvil, 60x60px PC
- **Alto contraste** — mínimo WCAG AA
- **Navegación no dependiente de lectura** — iconos + etiquetas sonoras
- **Operación con un dedo** en móvil
- **Botón de volver / home siempre visible**

### Layouts principales

#### Pantalla principal de biblioteca
- Biblioteca pixel art cálida
- Libros disponibles brillando; bloqueados atenuados
- Búho compañero en un rincón
- Barra superior con estrellas, nombre y settings
- CTA clara para jugar/leer

#### Pantalla Passage View
- Izquierda (60%): pasaje grande y legible
- Derecha (40%): área del puzzle
- Parte inferior: word bank, botón de pista, replay de audio
- Parte superior: título, número de pasaje, salida

#### Responsive breakpoints

| Dispositivo | Layout |
|---|---|
| Teléfono vertical | Texto arriba, puzzle abajo; swipe para cambiar |
| Tablet / iPad | Lado a lado |
| PC / Web 1080p | Side-by-side completo con marco decorativo |
| Web 720p | Side-by-side compacto |

### Sistema de themes
La UI se skinnea con **Theme Packs** que pueden sobrescribir:
- tokens de color
- familia tipográfica
- sprite sheet del búho
- backgrounds
- estados de botones y tiles
- colores de partículas

**Themes built-in de lanzamiento:**
| Theme | Descripción |
|---|---|
| Cozy Library | Marrones cálidos y crema |
| Enchanted Forest | Verdes profundos y luciérnagas |
| Ocean Voyage | Azules y teales |
| Space Station | Azul oscuro y neón |
| Classroom Chalk | Alto contraste y simplicidad |

---

## 10. Diseño de audio

### Música
- **Tema de biblioteca:** ambiente suave, piano y cuerdas
- **Tema de puzzle:** más animado pero no distractor
- **Sting de celebración:** melodía breve y triunfante
- Tono siempre infantil, cálido y no competitivo

### Efectos de sonido

| Evento | Sonido |
|---|---|
| Palabra encontrada | Chime suave + whoosh brillante |
| Letra colocada correctamente | Pop amable |
| Intento incorrecto | “bwoop” discreto |
| Pista del búho | Hoot suave |
| Libro desbloqueado | Paso de página + fanfarria breve |
| Sticker ganado | Sonido de papel adhesivo |
| Botón | Click suave |

### Sistema TTS
- Todo texto de pasajes debe poder leerse con TTS o audio grabado
- **Orden de fallback:** audio pregrabado → TTS nativo del sistema → TTS in-engine
- Velocidades: 0.75x, 1x, 1.25x
- Resaltado palabra por palabra sincronizado con la lectura en voz alta

### Accesibilidad de audio
- Volúmenes separados para música, SFX y voz/TTS
- Posibilidad de mutear solo la música
- Subtítulos para cualquier diálogo hablado

---

## 11. Accesibilidad y localización

### Accesibilidad

| Función | Detalle |
|---|---|
| Tamaño de fuente | Small / Medium / Large / XL |
| High contrast mode | Aumenta el contraste general |
| Fuente amigable para dislexia | Opción OpenDyslexic |
| Modos daltonismo | Deuteranopia, Protanopia, Tritanopia |
| TTS para toda la UI | No solo para pasajes |
| Reduced motion | Desactiva confetti y partículas intensas |
| Layout zurdo/diestro | Posibilidad de espejar distribución |

### Arquitectura de localización
- Todas las cadenas en archivos externos `.po` / `.json`
- Formateo de fecha y números según locale
- Fuentes con soporte para latino extendido, cirílico y árabe
- Selector de idioma siempre accesible
- Idiomas de lanzamiento: inglés y español
- La comunidad puede añadir nuevos locales

### Soporte RTL
El motor de layout debe soportar `direction: RTL` para packs en árabe, hebreo o urdu añadidos por modders.

---

## 12. Herramientas para docentes y familias

### Parent Dashboard (in-app)
Accesible por PIN o contraseña definida al primer inicio:
- tiempo de lectura hoy / esta semana
- libros completados
- total de palabras encontradas
- precisión en puzzles
- ajustes de dificultad

### Flujo de subida de libros para docentes (sin JSON)
```text
Paso 1 — pegar o escribir el texto
Paso 2 — elegir rango de edad
Paso 3 — escoger tipos de puzzle
Paso 4 — el sistema genera objetivos automáticamente
Paso 5 — previsualización exacta
Paso 6 — opcional: quitar palabras con un clic
Paso 7 — “Guardar Pack” → pack.zip listo para /mods
```

---

## 13. Sistema de modding

### Visión general
READCRAFTERY se construye sobre el principio **contenido = mods**. Incluso los libros integrados usan el mismo formato que la comunidad.

### Dos capas de modding

#### Capa 1: mods de contenido (libros y puzzles)
Cualquiera puede crear un Book Pack con carpetas JSON + assets.

**Book Pack Validator Tool**
Herramienta standalone/web que:
- previsualiza el pack exactamente como se verá
- valida el schema JSON
- genera un `pack.zip` listo para compartir

**Distribución**
- Packs subidos a itch.io con etiqueta “READCRAFTERY Book Pack”
- Navegador in-game de mods en fase posterior
- Soporte de drop directo en `/mods`

#### Capa 2: mods de theme (UI)
Un Theme Pack contiene:
```text
my_theme/
├── theme.json
├── fonts/
├── sprites/
└── preview.png
```

### Esquema base del modding API

#### Schema de `metadata.json`
- requeridos: `title`, `author`, `language`, `age_min`, `age_max`, `difficulty`, `version`
- opcionales: `description`, `cover_image`, `tags[]`, `license`

#### Schema de `passage_XX.json`
- requeridos: `id`, `text`, `language`, `difficulty`, `puzzles[]`
- opcionales: `title`, `illustration`, `audio`, `comprehension_question`

#### Schema de `theme.json`
- requeridos: `name`, `version`, `author`
- tokens de color: `background`, `surface`, `text_primary`, `text_secondary`, `accent`, `highlight`, `correct`, `incorrect`, `shadow`
- fuentes: `body_font`, `display_font`
- flags: `rtl`, `dark_mode`
- sprites opcionales con fallback al theme default

### Documentación de modding
Habrá una guía completa separada, publicada:
- in-game
- como PDF en itch.io / web
- como wiki pública si las herramientas se abren

---

## 14. Estrategia de monetización

### Modelo: pago único
✅ **CERRADO** — READCRAFTERY es un juego de **pago único, tuyo para siempre**. Sin free-to-play, sin DLC por niveles, sin moneda premium. El jugador paga una vez y obtiene el juego completo con todos los book packs y themes integrados.

**Justificación:** Alineación honesta con la realidad de un desarrollador solo. Maximiza la confianza de los padres. Evita la complejidad de infraestructura de suscripciones o DLC antes de tener ingresos que lo justifiquen. La Teacher Edition con suscripción es un producto separado, posterior, dirigido a un cliente diferente.

READCRAFTERY sigue una política estricta de **sin dark patterns, sin anuncios, sin moneda premium**.

### Fuentes de ingresos

| Fuente | Descripción | Rango |
|---|---|---|
| **Juego base** | Todos los book packs integrados, todos los themes, gameplay completo — un solo pago | $4.99–$7.99 (por definir) |
| **Book Packs comunitarios** | Contenido de terceros en itch.io — precio libre del creador (READCRAFTERY no cobra comisión) | Variable |
| **Steam Release (Fase 2)** | Mismo modelo de pago único en Steam con integración Workshop | Por definir |

### Notas
- Nunca se muestran anuncios a los jugadores.
- No hay contenido de gameplay detrás de un paywall — el juego está completo al comprarlo.
- La comunidad puede distribuir y monetizar sus propios packs libremente.
- Precio exacto por definir según volumen de contenido al lanzamiento e investigación de mercado.

---

## 15. Estrategia de plataformas

### Fase 1: itch.io + Web (meses 1–12)
- HTML5 gratuito en itch.io
- Builds descargables Windows y Mac
- Devlog y comunidad en itch.io
- Comunidad de modding vía tags + Discord

### Fase 2: móvil (meses 9–18)
- Android y iOS
- Adaptaciones UX específicas

### Fase 3: Steam (meses 18–30)
- Release en Steam
- Steam Workshop
- Achievements y trading cards
- Compatibilidad con Steam Deck

### Consideraciones por plataforma

| Plataforma | Consideración clave |
|---|---|
| Web (HTML5) | Cargar en <5 s en una conexión escolar media; base assets <20MB |
| Android | Soporte Android 8.0+ y layouts grandes |
| iOS | Rating 4+ y sin SDKs analíticos de terceros |
| Steam | Todo el juego operable con controller y Steam Deck |

---

## 16. Recomendación de stack tecnológico

### Recomendación principal: Godot 4
**Veredicto:** mejor elección para un desarrollador solo que apunta a PC + Web + móvil.

| Criterio | Evaluación |
|---|---|
| Export multiplataforma | ✅ |
| Rendimiento 2D | ✅ |
| Scripting | ✅ |
| Coste | ✅ 100% libre y open source |
| Soporte para modding | ✅ |
| Comunidad | ✅ |
| Export a itch.io | ✅ |
| Idoneidad para solo dev | ✅ |
| TTS / audio | ✅ |
| Curva de aprendizaje | moderada |

**Módulos de Godot 4 a usar:**
- `FileAccess` + `JSON`
- `AudioStreamPlayer` + `AudioBus`
- `RichTextLabel` con BBCode
- `AnimationPlayer` / `Tween`
- `HTTPClient` para tooling futuro
- `DisplayServer`

### Alternativa 1: web-first con TypeScript + Phaser.js
Muy buena si la prioridad absoluta es web. Menos cómoda para móvil nativo y builds standalone.

### Alternativa 2: Unity
Funciona, pero no es la recomendación para este caso. Demasiado peso y más fricción para un proyecto 2D puro.

### Alternativa 3: C++ con Raylib
No recomendada salvo que el objetivo fuera un proyecto muy de sistemas. Demasiado coste para la complejidad real del juego.

### Alternativa 4: Flutter + Flame
Opción legítima si el foco principal fuera móvil y ya se domina Dart/Flutter.

### Resumen final
```text
Solo dev + PC + Web + móvil + juego infantil + modding
                    ↓
             ✅ GODOT 4 (recomendación principal)
             ✅ Phaser.js (si web-first es prioridad)
             ⚠️ Flutter/Flame (si móvil-first es prioridad)
             ❌ Unity / C++ Raylib
```

---

## 17. Arquitectura técnica

### Arquitectura de alto nivel (Godot 4)

```text
READCRAFTERY
├── /core
│   ├── GameManager.gd
│   ├── AudioManager.gd
│   ├── LocaleManager.gd
│   └── ProgressManager.gd
├── /content
│   ├── ModLoader.gd
│   ├── BookPack.gd
│   ├── Passage.gd
│   ├── PuzzleDefinition.gd
│   └── PuzzleGenerator.gd
├── /scenes
│   ├── Library/
│   ├── PassageView/
│   ├── Puzzles/
│   ├── Celebration/
│   ├── Journal/
│   └── Settings/
├── /themes
│   ├── ThemeLoader.gd
│   └── ThemeTokens.gd
└── /mods
    ├── builtin_books/
    └── [community packs]/
```

### Save System
- Datos en `user://saves/profile_01.json`
- Soporta hasta 4 perfiles
- Incluye progreso, estrellas, journal, ajustes y theme activo
**Schema base del save (M0 desde día 0):**
```json
{
  "save_version": "1.0.0",
  "profile_id": "profile_01",
  "display_name": "Sofia",
  "avatar_id": "owl_default",
  "settings": {
    "language": "es",
    "tts_speed": 1.0,
    "font_size": "large",
    "active_theme": "cozy_library"
  },
  "progress": {
    "total_stars": 42,
    "books": {
      "little_seed": { "passages_completed": 3, "stars": [3, 2, 3] }
    },
    "achievements": ["first_word", "bookworm"]
  },
  "journal": {
    "stickers": ["seed_sticker", "owl_hat"],
    "saved_words": ["meadow", "carried"]
  }
}
```

> **Por qué importa `save_version`:** cualquier cambio futuro del schema necesita migración controlada. Añadirlo desde M0 cuesta una línea; añadirlo tarde pone en riesgo saves ya existentes.

### Flujo de carga de mods
```text
Inicio de la app
  → ModLoader escanea /mods/
  → valida metadata.json de cada carpeta
  → packs válidos se registran
  → packs inválidos se reportan en panel de error (modo dev)
  → la Library consulta el registro
  → el jugador abre un libro
      → se cargan pasajes lazy
      → si targets == "auto", PuzzleGenerator resuelve
      → IPuzzle recibe PuzzleDefinition ya resuelta
```

### Flujo de localización
```text
LocaleManager.set_language("es")
  → carga /locales/es.json
  → actualiza UI translatable
  → actualiza AudioManager.tts_language
  → verifica si el pack tiene pasaje en ese idioma
  → fallback a "en" si no existe
```

### Motor de puzzles
Cada puzzle es una escena autónoma que implementa `IPuzzle`:
```gdscript
class_name IPuzzle extends Control
signal word_found(word: String)
signal puzzle_completed(stars: int)

func initialize(puzzle_def: PuzzleDefinition, passage_text: String) -> void:
    pass

func get_hint() -> void:
    pass
```

Esto permite añadir nuevos tipos de puzzle sin tocar el core.

---

## 18. Descripciones de concept art

Estas descripciones funcionan como briefs para artista o generación de imágenes.

### Escena 1: The Great Library (menú principal)
**Estilo:** 2D cálido, ilustrado, ligera perspectiva isométrica. Biblioteca acogedora de libro infantil. Paleta con ámbar, crema, rojos cálidos y luz dorada suave.

**Contenido:** estanterías hasta el techo, libros con brillo suave, mesa redonda central, búho grande posado sobre una pila de libros, libros bloqueados con polvo y candado, estrellas flotando suavemente.

### Escena 2: Puzzle View — Word Glow
**Estilo:** split-screen limpio. Izquierda: panel tipo pergamino con pasaje grande. Derecha: palabra objetivo y apoyo visual. Abajo: banda amplia de word bank.

**Acento visual:** al tocar correctamente la palabra, se despega de la página, explota en chispas y vuela al banco.

### Escena 3: Celebration Screen
**Estilo:** explosión de color a pantalla completa. Búho celebrando en el centro, lluvia de estrellas, confetti en espiral, sticker nuevo que entra desde la derecha y se pega al scrapbook.

### Escena 4: Ejemplos de themes
- **Enchanted Forest:** bosque crepuscular, luciérnagas, estanterías con enredaderas, búho con plumas verdes y violetas.
- **Space Station:** espacio exterior con la Tierra al fondo, libros flotando, UI neón azul, búho astronauta.
- **Classroom Chalk:** fondo de pizarra, UI con estilo de tiza, simple y de alto contraste.

### Escena 5: Layout móvil vertical
**Estilo:** mitad superior texto sobre pergamino; mitad inferior bandeja de puzzle colorida. Indicador sutil de swipe. El búho aparece como avatar reducido abajo a la derecha.

---

## 19. Hoja de ruta de lanzamiento

### Milestone 0 — Fundación (mes 1–2)
- [ ] Configuración del proyecto Godot 4, estructura de carpetas, arquitectura de escenas
- [ ] **Schema de save con `save_version` implementado** — día 0, sin excepciones
- [ ] ModLoader core con formato de book pack cerrado
- [ ] Passage view con texto + TTS básico
- [ ] Word Glow completamente funcional
- [ ] 1 libro built-in bilingüe EN/ES
- [ ] Progresión básica con estrellas locales
- [ ] **Validar export HTML5 en itch.io** (COOP/COEP, audio en Chrome/Firefox/Safari)
- [ ] **Auditoría de tamaño base del build** — HTML5 < 15MB sin comprimir
- [ ] **Smoke test TTS por plataforma** — web, Android, iOS

### Milestone 1 — Vertical slice (mes 3–4)
- [ ] Los 5 tipos de puzzle implementados
- [ ] Animaciones base del búho (idle, celebrate, hint)
- [ ] Sistema de VFX (chispas, lluvia de estrellas, confetti)
- [ ] 3 book packs integrados
- [ ] Settings (audio, idioma, accesibilidad básica)
- [ ] Export Web y prueba en itch.io
- [ ] **Preview Tool interno** para validar contenido y PuzzleGenerator

### Milestone 2 — Alpha (mes 5–6)
- [ ] Biblioteca built-in completa (5 libros)
- [ ] Reading Journal + stickers
- [ ] Achievement badges
- [ ] Sistema de themes (3 integrados)
- [ ] Parent Dashboard
- [ ] Localización EN + ES
- [ ] Build Android probado

### Milestone 3 — Beta / lanzamiento itch.io (mes 7–8)
- [ ] Documentación de modding publicada
- [ ] **Book Pack Validator Tool público** (versión interna en M1; esta es la versión pulida y distribuible para docentes y la comunidad)
- [ ] **`CONTENT_LICENSING.md` en el repo** ← gate duro antes de cualquier distribución pública
- [ ] **Política de privacidad publicada** (basada en template; cubre juego base sin recolección de datos; no requiere abogado en esta etapa)
- [ ] Build iOS probado
- [ ] User testing con niños de 5–9 años (reclutar via escuela local o comunidad)
- [ ] Sprint de corrección de bugs basado en feedback
- [ ] Soft launch en itch.io (gratis, web)
- [ ] 5 themes comunitarios destacados (curados de la comunidad modding inicial)
- [ ] Sistema base de soporte / feedback

### Milestone 4 — Post-lanzamiento (mes 9–12)
- [ ] Primera colección curada de Book Packs comunitarios
- [ ] Navegador de mods in-game (Phase 2)
- [ ] Primer showcase de mods comunitarios

---

## 20. Preguntas abiertas y riesgos

### Bloqueadores duros

| Tema | Por qué bloquea | Cuándo |
|---|---|---|
| **Versionado de saves** | Sin `save_version`, cualquier cambio rompe saves existentes | M0 día 0 |
| **Headers COOP/COEP HTML5** | Sin headers correctos puede romperse el audio silenciosamente | M0 |
| **Smoke test TTS** | TTS se comporta distinto en Web/Android/iOS | M0 |
| **Baseline de tamaño HTML5** | El build puede crecer demasiado para conexiones escolares | M0 |
| **Licenciamiento de contenido** | No se puede distribuir públicamente sin derechos claros | Antes de M3 |
| **Privacy policy base** | Obligatoria para cualquier producto público | Antes de M3 |

### Mejoras de calidad

| Mejora | Impacto si falta | Hito objetivo |
|---|---|---|
| Filtros de nombres propios y apóstrofes | Menor calidad de targets generados | M1 |
| Stopwords por edad | Menor control pedagógico | M2 |
| `sight_words_ratio` | Menor flexibilidad docente | M2 |
| Test suite de PuzzleGenerator | Más bugs descubiertos por playtesters | M1–M2 |
| Validación de accesibilidad con niños reales | Riesgo de UX mal calibrada | Antes de M3 |

### Preguntas resueltas
| Pregunta | Decisión |
|---|---|
| ¿Mismas estrellas para puzzles auto y manuales? | **Sí** — el jugador nunca distingue; la paridad es correcta |
| ¿Cuándo sale el Preview Tool? | **M1 interno, M3 público** — necesario para validar contenido propio antes de distribuirlo a modders |
| ¿Analytics para el juego base? | **Ninguno** — sin analytics. Cero recolección de datos, punto final. |
| ¿COPPA para el juego base (sin recolección de datos)? | **Trivial** — cero recolección de datos = cumplimiento COPPA automático. No se recopilan datos personales de ningún jugador. |
| ¿TTS pregrabado o en runtime? | **Híbrido** — audio pregrabado para libros built-in oficiales (calidad); TTS nativo del sistema (OS-native) para libros moddados |
| ¿Licencias de fuentes? | **Andika** (SIL OFL) para texto de pasajes · **Nunito** (OFL) para UI. Ambas con licencia OFL. Descargar desde Google Fonts. Commit en `res://fonts/` antes de construir PassageView. |
| ¿Modelo de monetización? | **Pago único** — pagas una vez, tuyo para siempre. Sin free-to-play, sin DLC por niveles, sin moneda premium, sin suscripción. Modelo Stardew Valley: juego completo al comprar, mods de comunidad gratis. Ver §14. |
| ¿Estructura de repositorios? | **Cuatro repos bajo la organización [The-Readcraftery-Project](https://github.com/The-Readcraftery-Project) en GitHub.** Ver tabla más abajo. El engine es comercial de código cerrado; el formato de modding es abierto. |

### Estructura de repositorios

| Repo | Visibilidad | Propósito | URL |
|---|---|---|---|
| `readcraftery` | 🔒 Privado | Engine + contenido oficial. Proyecto Godot completo, book packs built-in, assets de arte oficiales, saves, locales, contenido de producción. | https://github.com/The-Readcraftery-Project/readcraftery |
| `readcraftery-docs` | 🌐 Público | Documentación pública (GitHub Pages eventual). GDD, Art Guide, Asset Contracts, Guía de modding. Audiencia: modders, docentes, prensa, colaboradores. | https://github.com/The-Readcraftery-Project/readcraftery-docs |
| `readcraftery-dev-docs` | 🔒 Privado | Documentación técnica interna. Build Guide, Architecture Contract, notas de diseño y decisiones internas. | https://github.com/The-Readcraftery-Project/readcraftery-dev-docs |
| `readcraftery-SDK` | 🌐 Público | SDK de modding. Schema JSON de book packs, schema JSON de themes, Preview Tool (M3), ejemplos de book packs. Audiencia: modders y creadores de contenido. | https://github.com/The-Readcraftery-Project/readcraftery-SDK |

---

## Apéndice A — Glosario

| Término | Definición |
|---|---|
| Book Pack | Bundle de mod con pasajes, puzzles y assets de un libro |
| Theme Pack | Bundle que reskinnea la UI y el look visual del juego |
| Passage | Un fragmento de texto con puzzles asociados |
| Word Bank | Lista de palabras objetivo del puzzle actual |
| Reading Owl | Personaje compañero animado del jugador |
| Reading Journal | Scrapbook persistente de progreso y stickers |
| IPuzzle | Interfaz / clase abstracta que implementa cada puzzle |
| TTS | Text-to-Speech |
| PuzzleGenerator | Motor basado en reglas que extrae objetivos cuando `targets: "auto"` |
| Puzzle autogenerado | Puzzle cuyos targets fueron generados automáticamente |

---

## Apéndice B — Panorama competitivo

| Juego | Similitud | Diferencia clave |
|---|---|---|
| Endless Reader | Juego infantil de palabras | Sin modding, contenido cerrado |
| Duolingo ABC | App de alfabetización | Solo app, sin contenido comunitario |
| Wordle / NYT Games | Puzzles de palabras | No orientado a infancia, sin contexto literario |
| Epic! | Biblioteca digital infantil | Sin mecánicas de puzzle |
| Khan Academy Kids | App educativa | Enfoque mucho más amplio, sin modding |

**Diferenciador de READCRAFTERY:** un juego de alfabetización y puzzles de palabras con sistema completo de modding para libros y themes, pensado tanto para juego en casa como para uso docente.

---

*Fin del documento — READCRAFTERY GDD v1.2 (versión en español)*  
*Documento siguiente: contrato técnico, guía de construcción, guía de arte y contratos de assets.*
