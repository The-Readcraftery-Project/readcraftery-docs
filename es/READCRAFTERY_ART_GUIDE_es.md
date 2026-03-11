# READCRAFTERY — Guía de Estilo Artístico
**Versión:** 1.2  
**Fecha:** marzo de 2026  
**Estado:** Preproducción  
**Documentos complementarios:** GDD v1.2 · Contrato de Arquitectura v1.1 · Guía de Construcción v1.3  

---

> **Cómo leer este documento**
>
> Este documento tiene dos audiencias:
> - **El desarrollador / artista** — dirección visual, personaje, especificaciones técnicas de producción
> - **Los modders** — guía para crear themes y book packs con assets visuales compatibles
>
> Las secciones §1–§5 son para producción interna. La sección §6 es la guía pública para modders.
> El documento usa **pixel art con Estrategia B** como estilo definitivo — sprites a
> 48×48 px escalados a 4× en un viewport de 1920×1080, texto siempre en resolución nativa.
> Esta decisión está cerrada. Las secciones técnicas (§4–§5) reflejan esta elección.

---

## Tabla de Contenidos

1. [Referentes Visuales y Filosofía](#1-referentes-visuales-y-filosofía)
2. [Paleta y Valores de Color](#2-paleta-y-valores-de-color)
3. [El Istari Owl — Diseño del Personaje](#3-el-istari-owl--diseño-del-personaje)
4. [El Default Theme — Biblioteca Acogedora](#4-el-default-theme--cozy-library)
5. [Shape Language & Rendering Rules](#5-shape-language--rendering-rules)
6. [UI Readability Doctrine](#6-ui-readability-doctrine)
7. [Especificaciones Técnicas de Producción](#7-especificaciones-técnicas-de-producción)
8. [Guía para Modders — Crear un Theme](#8-guía-para-modders--crear-un-theme)
9. [Asset Priority for First Playable](#9-asset-priority-for-first-playable)
10. [Acceptance Criteria Visual](#10-acceptance-criteria-visual)
11. [Lo Que Todavía Está Abierto](#11-lo-que-todavía-está-abierto)

---

## 1. Referentes Visuales y Filosofía

### Los dos referentes fundacionales

**Choose Your Own Adventure (1979–1998, Bantam Books)**  
Los libros de aventura interactiva de los 80 tienen una cualidad visual específica que queremos capturar: ilustraciones con *peso narrativo*, mundos que se sienten habitados y ligeramente peligrosos pero fascinantes, composiciones dramáticas con fuerte contraste de luz, y una paleta cálida interrumpida por destellos de color imposible (el portal que brilla, la criatura que luce). Las ilustraciones de interior eran en blanco y negro con gran expresividad de línea — cada escena sugería un mundo más grande fuera del cuadro.

Lo que tomamos: **el sentido de que cada pantalla es una página de un libro real**. El juego debe sentirse como estar *dentro* de una ilustración de esos libros.

Lo que no tomamos: el dramatismo oscuro. READCRAFTERY es para niños de 4–9 — el tono es mágico y acogedor, no tenso.

**Dr. Seuss (Theodor Seuss Geisel, 1937–1991)**  
El universo visual de Seuss tiene reglas muy específicas que lo hacen inmediatamente reconocible y profundamente infantil en el mejor sentido:
- **Nada es perfectamente recto.** Las torres se tuercen, los árboles se curvan, las casas se inclinan. Hay vida orgánica en cada línea.
- **Las texturas son inventadas.** No piel real, no madera real — texturas que solo existen en ese mundo.
- **La paleta es limitada y audaz.** Pocos colores, muy saturados, con fuertes contrastes. El blanco de la página (o el fondo claro) trabaja como color propio.
- **Los personajes tienen expresividad exagerada pero nunca aterradora.** Ojos grandes, posturas teatrales, emociones claras desde lejos.
- **La tipografía y las ilustraciones coexisten como parte del mismo mundo visual.**

Lo que tomamos: **la línea con personalidad, las formas orgánicas, la paleta audaz, la textura inventada**.

Lo que no tomamos: la excentricidad extrema. Queremos que el mundo sea reconocible — una biblioteca es una biblioteca — pero dibujada con esa calidez orgánica.

### La síntesis: Storybook Arcane

El estilo resultante tiene nombre propio en este documento: **Storybook Arcane**.

Es una biblioteca mágica dibujada a mano, donde:
- Los libros en los estantes tienen colores imposibles y brillan suavemente
- El mobiliario se curva levemente, como si hubiera crecido en lugar de haber sido construido
- La magia es ambient, no explosiva — rayos de luz, motas de polvo dorado, runas que parpadean suavemente
- Todo tiene textura táctil — papeles con grano, telas con tejido, madera con veta
- Los colores son ricos y cálidos, con un contrapunto de azul-noche profundo para la magia

### Tres palabras que definen el estilo

**Cálido.** El juego debe sentirse como una tarde de lluvia con una taza de algo caliente y un libro bueno.  
**Vivo.** Nada es perfectamente estático. Las cosas breathe suavemente incluso en reposo.  
**Honesto.** La ilustración tiene la imperfección deliberada de algo hecho a mano, no la frialdad de un vector perfecto.

### Lo que evitar explícitamente

- ❌ **Flat design moderno** — iconos sin textura, gradientes minimalistas, look de app de productividad
- ❌ **Chibi / anime** — proporciones de cabeza grande estilo japonés no encajan con el referente
- ❌ **Ilustración digital lisa** — vectores perfectos, gradientes suaves, sin textura de pixel
- ❌ **Realismo** — proporciones anatómicas correctas, iluminación PBR
- ❌ **Dark fantasy** — calaveras, garras, oscuridad inquietante; incluso el mago es amable

### Pixel art — la decisión cerrada

El estilo visual de READCRAFTERY es **pixel art**, con Estrategia B de escalado (ver §5).

La razón central: el texto es el producto. Un niño de 5 años necesita texto perfectamente nítido en cualquier pantalla. El pixel art con Estrategia B permite texto en resolución nativa 1080p mientras los sprites y backgrounds viven en su resolución natural escalada a 4×. No hay tradeoff entre calidez visual y legibilidad del texto.

El pixel art también es coherente con los referentes: los libros CYOA de los 80 son los primeros libros que muchos de nosotros elegimos leer por voluntad propia — tienen una relación directa con la era del pixel art. Y el Istari Owl en pixel art bien ejecutado tiene más personalidad que en cualquier otro estilo a su nivel de complejidad de producción.

---

## 2. Paleta y Valores de Color

### Paleta principal — Biblioteca Acogedora

Estos son los valores de color del default theme. Los themes de modders pueden usar paletas completamente diferentes, pero deben mantener los mismos **roles funcionales** (ver §6).

```
FONDOS Y SUPERFICIES
────────────────────────────────────────────────────────────
background          #2C1A0E   Marrón noche — el color de la biblioteca oscurecida
surface             #4A2E1A   Marrón caoba — estantes, paneles de madera
surface_light       #6B4226   Marrón cálido — superficies iluminadas
parchment           #F5E6C8   Pergamino — fondo de pasajes de texto
parchment_shadow    #E8D4A8   Pergamino sombra — bordes de papel, separadores

TEXTO
────────────────────────────────────────────────────────────
text_primary        #2C1A0E   Sobre parchment: tinta oscura
text_primary_light  #F5E6C8   Sobre fondos oscuros: pergamino
text_secondary      #8B6914   Marrón dorado — subtítulos, labels, metadata

ACENTO Y MAGIA
────────────────────────────────────────────────────────────
accent              #D4A017   Dorado — highlights, selecciones, estrellas
accent_warm         #E8721A   Ámbar — botones primarios, CTA
magic_glow          #7B4FBE   Púrpura mágico — efectos del Istari Owl, runas
magic_blue          #1E3A5F   Azul noche — profundidad, sombras mágicas

FEEDBACK
────────────────────────────────────────────────────────────
correct             #4CAF50   Verde — palabra encontrada correctamente
incorrect           #E53935   Rojo suave — error, pero nunca agresivo
hint                #FF9800   Naranja — pista disponible, sugerencia
neutral             #9E9E9E   Gris — elementos inactivos o deshabilitados
```

### Reglas de uso de color

**Regla 1 — El dorado es sagrado.**  
`accent` (#D4A017) se reserva para logros, palabras encontradas, estrellas ganadas. Úsarlo en elementos decorativos lo devalúa. Cada vez que el jugador ve dorado, debe sentir que ganó algo.

**Regla 2 — La magia es rara.**  
`magic_glow` (#7B4FBE) aparece solo en elementos directamente asociados con el Istari Owl o con efectos mágicos narrativos. No en UI funcional.

**Regla 3 — El texto sobre parchment siempre en `text_primary`.**  
Nunca texto gris sobre fondo claro para niños de 4–9. Contraste mínimo WCAG AA en todos los textos de lectura.

**Regla 4 — `incorrect` nunca es el rojo agresivo de un error.**  
Es un rojo suave, momentáneo. El juego no castiga — informa. La animación de error dura máximo 500ms y el color vuelve al estado neutro.

### Notas de accesibilidad de color

- Todo el texto de juego pasa WCAG AA mínimo (ratio 4.5:1 para texto pequeño, 3:1 para texto grande)
- Los colores de feedback (`correct`, `incorrect`) nunca son la **única** señal — siempre van acompañados de animación, sonido o icono para usuarios con daltonismo

### Paletas para modos de daltonismo ✅ CERRADO (M1)

**Decisión de arquitectura:** El juego aplica transformaciones de paleta automáticas como primera línea de defensa. Los modders pueden opcionalmente proveer paletas manuales en `theme.json` que reemplazan la transformación automática para su theme. Si no proveen paleta manual, la transformación automática se aplica. Esto da compatibilidad a todos los themes sin trabajo extra del modder.

**Herramienta recomendada para validar:** Color Oracle (gratis, macOS/Windows/Linux) — simula las tres condiciones en tiempo real sobre cualquier pantalla.

**Milestone:** Paletas definidas y testeadas en M1. Integradas en `colorblind_mode` en M2. El Preview Tool valida contraste de paleta desde M1.

```
DEUTERANOPIA (sin cono verde — más común, ~6% hombres)
Problema principal: correct (verde) e incorrect (rojo) son indistinguibles.
────────────────────────────────────────────────────────────────────────
Token           Paleta base     Paleta deuteranopia   Razón del cambio
correct         #4CAF50         #1E88E5 (azul)        Verde invisible
incorrect       #E53935         #E65100 (naranja)     Rojo visible como marrón
accent          #D4A017         #D4A017               Dorado-amarillo: ok
hint            #FF9800         #FF9800               Naranja: ok
magic_glow      #7B4FBE         #0288D1 (cyan)        Púrpura puede confundirse
────────────────────────────────────────────────────────────────────────

PROTANOPIA (sin cono rojo — ~2% hombres)
Problema principal: incorrect (rojo) aparece como gris oscuro.
────────────────────────────────────────────────────────────────────────
Token           Paleta base     Paleta protanopia     Razón del cambio
correct         #4CAF50         #4CAF50               Verde: legiblemente distinto
incorrect       #E53935         #FF6F00 (amber)       Rojo invisible
accent          #D4A017         #D4A017               Dorado: ok
hint            #FF9800         #FF9800               Naranja: ok
magic_glow      #7B4FBE         #7B4FBE               Púrpura: ok
────────────────────────────────────────────────────────────────────────

TRITANOPIA (sin cono azul — <0.1%, ambos sexos)
Problema principal: azules y amarillos se confunden.
────────────────────────────────────────────────────────────────────────
Token           Paleta base     Paleta tritanopia     Razón del cambio
correct         #4CAF50         #4CAF50               Verde: ok
incorrect       #E53935         #E53935               Rojo: ok
accent          #D4A017         #E040FB (magenta)     Dorado confundible con verde
magic_glow      #7B4FBE         #E91E63 (rosa)        Azul-púrpura invisible
magic_blue      #1E3A5F         #1B5E20 (verde oscuro) Azul oscuro invisible
────────────────────────────────────────────────────────────────────────

REGLA COMÚN A LOS TRES MODOS:
  correct e incorrect SIEMPRE acompañados de forma + animación + sonido.
  El color es refuerzo, no señal única. Nunca depender solo del color.
```

---

## 3. El Istari Owl — Diseño del Personaje

### Concepto y personalidad

El Istari Owl es el companion del jugador. Su nombre lo elige el niño al comenzar. En este documento se llama **"el Profesor"** como nombre de trabajo interno.

**Personalidad visual:** Viejo, sabio, amable, ligeramente excéntrico. Piensa en Radagast el Pardo si hubiera dedicado su vida a los libros en lugar de a los animales. O en el Mago de Oz si fuera genuinamente sabio en lugar de charlatán. Hay décadas de historia en cada pluma, pero sus ojos son cálidos y comprensivos — nunca intimidantes.

**La tensión central del diseño:** Es más mago que búho, pero la naturaleza de ave nunca desaparece. La tensión entre los dos es lo que lo hace visualmente interesante.

### Anatomía del personaje

```
PROPORCIONES BASE
────────────────────────────────────────────────────────────
Altura total:       ~8 "cabezas" de alto en pose estándar
Cabeza:             Grande, redonda — característica de búho
Ojos:               El rasgo más expresivo. Grandes, circulares,
                    color ámbar-dorado. Cejas independientes
                    (aunque los búhos no las tienen — es Seuss-style)
Pico:               Pequeño, curvado, casi oculto por la barba
Barba:              Sí. Larga, blanca, ligeramente alborotada.
                    Fluye sobre la túnica. La barba es lo que lo
                    ancla como mago, no como ave.

VESTIMENTA
────────────────────────────────────────────────────────────
Túnica:             Azul noche profundo (#1E3A5F) con detalles
                    en dorado. Mangas largas que ocultan las
                    "manos" (alas anteriores). La tela tiene
                    textura — no es plana.
Cinturón/faja:      Cuero desgastado con fíbula dorada.
Sombrero:           Puntiagudo, levemente torcido (estilo Seuss).
                    Mismo azul que la túnica. Tiene una banda
                    con runas y una pluma (de sí mismo, o de
                    otro pájaro — a definir).
Bastón:             Madera oscura nudosa, aproximadamente de su
                    altura. Tiene un cristal en la punta que
                    emite una luz suave cuando "habla" o ayuda.
                    El cristal es el color magic_glow (#7B4FBE).

NATURALEZA DE AVE — LO QUE SE MANTIENE
────────────────────────────────────────────────────────────
Plumas:             Visibles en el cuello, asomando bajo la
                    túnica en los hombros y brazos. Color base:
                    marrón-gris con rayado sutil (como un Bubo
                    bubo real). Algunas plumas primarias tienen
                    tips dorados.
Garras:             Sus pies son garras de búho. Grandes, curvas,
                    expresivas. A veces sostienen el bastón con
                    ellas. Son lo más visiblemente "ave" del
                    personaje.
Movimiento:         Cuando piensa, gira la cabeza casi 180°
                    (comportamiento real de búho). Cuando está
                    emocionado, las plumas del cuello se erizan
                    levemente. Parpadea lentamente — el parpadeo
                    lento de los búhos es una señal de confianza
                    y afecto en la naturaleza real.
```

### Estados de animación requeridos (M1)

Cada estado es una animación en loop o una animación de un disparo. El sistema usa `AnimationPlayer` de Godot.

| Estado | Tipo | Descripción | Trigger |
|---|---|---|---|
| `idle` | Loop | Respiración suave. Parpadeo ocasional lento. La punta del bastón pulsa con luz suave. | Por defecto |
| `happy` | Loop | Plumas del cuello erizadas suavemente. Ligero balanceo. Ojos entrecerrados (sonrisa de búho). | Palabra encontrada, progreso positivo |
| `thinking` | Loop | Giro lento de cabeza. Una garra rasca el mentón (con bastón en la otra). | Durante puzzle activo, esperando input |
| `excited` | One-shot | Alas ligeramente extendidas. Salto corto. Cristal del bastón destella. | 3 estrellas, primer libro completado |
| `hint` | One-shot | Se inclina hacia adelante. El bastón señala suavemente hacia el área del puzzle. Cristal brillando. | Al dar pista |
| `reading` | Loop | Sostiene un libro abierto. Los ojos se mueven de un lado al otro lentamente. | Durante lectura de pasaje con TTS |
| `celebrate` | One-shot | Extiende completamente las alas (máxima expansión). Motas de magia `magic_glow` emergen. | Completar un libro entero |
| `sleepy` | Loop | Cabeceos lentos. Ojos semicerrados. Para pantallas de descanso o inactividad. | Timeout de inactividad |
| `wave` | One-shot | Levanta una ala en saludo. Para onboarding y regreso del jugador. | Primera vez, regreso a sesión |


#### Mapping animación → protocolo de feedback

| Evento pedagógico | Animación | Duración |
|---|---|---|
| Inactividad > 8s | `thinking` | Loop hasta interacción |
| Inactividad > 13s + TTS automático | `hint` | One-shot |
| Palabra correcta | `happy` | One-shot → vuelve a `idle` |
| Palabra incorrecta | `idle` | Sin cambio — no expresar fracaso |
| Puzzle completado | `celebrate` (M1) / `happy` (M0) | One-shot |
| TTS leyendo pasaje | `reading` (M1) / `idle` (M0) | Mientras dura TTS |

> **Regla de oro:** el Owl nunca expresa frustración, impaciencia,
> ni decepción. Si una animación podría leerse como negativa,
> no se usa en respuesta a errores del niño.

### Accesorios desbloqueables (M2)

Los accesorios son overlays sobre el sprite base. No requieren redibujar el personaje completo — se superponen en el layer de accesorios.

```
Categorías:
  hats/        — Sombreros alternativos, gorros, coronas de flores
  scarves/     — Bufandas, collares, amuletos
  staff_tips/  — Diferentes cristales/ornamentos para la punta del bastón
  badges/      — Medallones en el cinturón, prendedores en la túnica
```

Los accesorios se ganan con estrellas acumuladas. Diseño en v1.1.

### Lo que NO es el Istari Owl

- ❌ No es condescendiente — nunca tiene cara de "debería saber esto"
- ❌ No es perfecto — tiene manchas de tinta en la túnica, plumas levemente despeinadas
- ❌ No es voluminoso o amenazante — aunque es alto, su postura es abierta
- ❌ No flota en el aire — camina (con garras), usa el bastón de apoyo
- ❌ No habla en el juego (solo TTS del texto del libro) — se expresa solo con animaciones

---

## 4. El tema predeterminado — Biblioteca Acogedora

### Composición de la Library Scene (pantalla principal)

```
Vista general:
  Una biblioteca circular o de ábside. Estantes hasta el techo en las paredes.
  Escalera de biblioteca con ruedas (la que se desliza en el riel).
  Mesa de lectura redonda en el centro-frente, con un candelabro.
  Ventana grande al fondo — lluvia suave o noche estrellada, según la hora.
  El Istari Owl en una percha/atril a la derecha, en estado `idle` o `reading`.

Libros en los estantes:
  Bloqueados:     Cubiertos de polvo. Colores apagados. Pequeño candado dorado.
  Disponibles:    Colores saturados. Un sutil shimmer dorado. "Respiran" levemente.
  Completados:    Brillo constante suave. Pequeñas estrellas flotando cerca.
  
Iluminación:
  Fuente principal: candelabros/lámparas de aceite. Luz cálida (#D4A017 tinted).
  Fuente secundaria: los propios libros disponibles. Emiten light suave.
  Fuente mágica: el bastón del Profesor. Pulsa lentamente.
  
Parallax layers (para animación de fondo):
  Layer 1 (más cercano):  Mesa, sillas, objetos de primer plano
  Layer 2:                Estantes centrales, El Profesor
  Layer 3:                Estantes del fondo
  Layer 4 (más lejano):   Ventana, cielo/lluvia
```

### Composición de la PassageView

```
División de pantalla (desktop/tablet landscape):
  60% izquierda:  PassagePanel
    - Fondo: parchment (#F5E6C8) con bordes ligeramente irregulares
    - Textura de papel sutil (grain muy suave)
    - Título del libro: fuente serif, color text_secondary
    - Texto del pasaje: fuente serif legible, color text_primary
    - Ilustración del libro (si existe en el pack): arriba o integrada en texto
    
  40% derecha:    PuzzlePanel
    - Fondo: surface (#4A2E1A) con textura de madera suave
    - El puzzle se instancia aquí
    - Pequeño retrato del Profesor en esquina superior — en estado `thinking`

  Bottom bar:
    - Word bank: fichas de pergamino con borde dorado
    - Hint button: cristal del bastón (icono), counter numérico
    - Exit: puerta pequeña (icono)
```

### El libro como objeto físico

Cada book pack tiene una `cover_image`. El diseño de la Library Scene muestra los libros en el estante como objetos 3D-ish (ilustrados con perspectiva isométrica ligera). El default para packs sin cover_image es un libro genérico con el color del spine generado a partir del `id` del pack (hash → color en paleta limitada).

---

## 5. Lenguaje de formas y reglas de renderizado

✅ **CERRADO** — estas reglas definen cómo debe verse el arte de READCRAFTERY a nivel de pixel. Sin estas reglas, dos artistas distintos producirán assets inconsistentes aunque ambos "sigan el estilo". Son el contrato visual del sistema.

### Filosofía: pixel art orgánico, no pixel art geométrico

El pixel art de READCRAFTERY no es el pixel art frío y geométrico de los juegos retro de acción. Es pixel art con **formas orgánicas deliberadas**: las esquinas de los estantes se curvan suavemente, el sombrero del Profesor se dobla hacia un lado, los libros tienen lomos ligeramente irregulares. La cuadrícula de pixels es el medio, no el mensaje. La calidez de Seuss se puede lograr en pixel art — Stardew Valley y Celeste lo demuestran.

### Reglas de outline

```
OUTLINE OBLIGATORIO en todos los sprites de personaje, objetos y UI tiles.
  Grosor:       1px exacto. Nunca 2px, nunca 0px.
  Color:        NO negro puro (#000000). Usar la variante _shadow del color
                dominante del objeto. Ej: un libro marrón tiene outline #3E1A00,
                no #000000. Outline negro puro aplana y mata la profundidad.
  Excepción:    Backgrounds no tienen outline — son el "mundo", no objetos en él.
                Tiles de terreno tampoco tienen outline exterior.

OUTLINE INTERIOR (inner outline / pillow shading):
  No se usa. Pillow shading hace que los sprites parezcan embossed/3D genérico.
  La forma se define con bloque de sombra, no con outline interior.
```

### Reglas de sombra e iluminación

```
SOMBRAS: bloques planos únicamente.
  Número de colores de sombra:   máximo 2 por elemento (shadow, deep_shadow)
  Gradientes:                    NO. Nunca. Una sombra es un color plano.
  Dirección de luz:              superior izquierda en todos los assets.
                                 Consistencia de dirección > realismo.
  Sombra proyectada:             no se dibuja en el sprite — es un efecto
                                 de escena separado si se necesita.

HIGHLIGHTS: un solo pixel estratégico.
  Número de colores de highlight:  máximo 1 por elemento (light)
  Posición:                        esquina superior izquierda de la forma curva
  Superficies planas/madera:       sin highlight especular — solo sombra suave
```

### Reglas de detalle y densidad

```
DENSIDAD MÁXIMA DE DETALLE:
  Elementos finos (1–2px):    máximo 20% del área del sprite
  El 80% restante:            masas de color plano o con una sola transición

  Razón: a 48×48 dibujado, cada pixel vale. El ojo de un niño de 4 años
  debe poder leer "búho con sombrero" desde la silueta, sin procesar detalle.

SILUETA PRIORITARIA:
  El Istari Owl debe ser reconocible por silueta sola a 48×48 native.
  Test: desaturar el sprite completo y reducir a 12×12 px. Si se reconoce
  como "figura con sombrero y bastón", la silueta es correcta.
  Si no se reconoce, hay demasiado detalle o la silueta es ambigua.

JERARQUÍA DE LECTURA por tipo de asset:
  Personaje:    silueta → expresión facial → vestimenta → detalles
  Libro:        color del lomo → título (si existe) → ornamento
  UI tile:      forma → estado (normal/selected/found) → decoración
  Background:   atmósfera → elementos narrativos → detalles ambientales
```

### Reglas de forma orgánica

```
CURVAS EN PIXEL ART:
  Las curvas se construyen con escalones de pixel decrecientes.
  Curva correcta de 45°:    2px, 1px, 1px, 2px (escalones irregulares = orgánico)
  Curva incorrecta:         1px, 1px, 1px, 1px (escalón uniforme = mecánico)

ESQUINAS:
  Objetos vivos (personaje, criaturas, libros mágicos):  esquinas redondeadas
  Objetos inanimados (madera, piedra, marco de UI):       esquinas rectas permitidas
  Regla práctica: si el objeto podría crecer, tiene curvas. Si fue construido, puede tener ángulos.

DEFORMACIÓN ORGÁNICA PERMITIDA:
  El sombrero del Profesor:   puede inclinarse hasta 10° sobre el eje vertical
  Los lomos de los libros:    pueden ser 1–2px más anchos en el centro
  Las paredes de la biblioteca: pueden tener ligera curvatura (max 3px en 480px de ancho)
  UI funcional (botones, tiles):  NO deformación — deben ser rectangulares precisos
```

### Reglas de anti-alias y dithering

```
ANTI-ALIAS MANUAL: NO se usa.
  No mezclar colores intermedios en los bordes del outline.
  El outline es 1px limpio. El pixel art puro no tiene AA manual.

DITHERING: permitido con restricciones.
  Uso correcto:   transición entre dos colores de la misma familia
                  (surface → surface_light en un área grande)
  Uso incorrecto: simular gradientes, crear un tercer color intermedio
  Máximo:         banda de 2px de dithering entre dos zonas de color
  Patrón:         checkerboard (ajedrezado) — no líneas ni patrones decorativos
```

### Reglas de paleta por sprite

```
COLORES POR SPRITE:
  Personaje (Istari Owl completo):   máximo 20 colores (de la master palette)
  Objeto individual (libro, botón):  máximo 8 colores
  Icono UI:                          máximo 4 colores
  Background (layer completo):       máximo 32 colores

  Todos los colores deben estar en la master palette de §2.
  Un color fuera de la master palette en producción = error, no estilo.
```

---

## 6. Doctrina de legibilidad de UI

✅ **CERRADO** — estas reglas protegen la función pedagógica del juego. Para un niño de 4–9 años aprendiendo a leer, la carga cognitiva visual importa tanto como la mecánica. El arte no solo debe ser encantador; debe hacer que leer sea fácil.

### El principio fundamental

**El texto manda.** En cualquier conflicto entre "verse bonito" y "ser legible", la legibilidad gana sin discusión. La función pedagógica de READCRAFTERY es exactamente: hacer que un niño lea una palabra con éxito. Todo lo que compite con eso es ruido.

### Reglas de PassageView (la pantalla más crítica)

```
FONDO DETRÁS DEL TEXTO:
  El parchment panel es el fondo del texto. Nunca tiene:
  - Textura con contraste > 5% sobre el color base de parchment
  - Animación de ningún tipo mientras el niño lee
  - Gradientes o variaciones de color visibles
  Permitido: grain muy sutil (noise < 3% de intensidad)

DECORACIÓN EN PASSAGEVIEW:
  El puzzle panel puede tener textura de madera.
  El passage panel: sin decoración estructural. Solo el texto y la ilustración del libro.
  Ilustraciones de libro: ocupan máximo 30% del passage panel. Nunca superponen texto.

ANIMACIONES DURANTE LECTURA:
  Estado activo de lectura (TTS playing o el niño leyendo):
    → El Istari Owl entra en estado `reading` (animación mínima, ojos moviéndose)
    → NINGUNA otra animación activa en pantalla
    → Parallax: detenido o reducido a 10% de velocidad normal
  Estado activo de puzzle:
    → El Profesor puede estar en `thinking`
    → Word bank tiles: solo animación de hover en el tile tocado, nunca en otros
```

### Reglas de jerarquía visual en PassageView

```
JERARQUÍA (orden de atención visual, de más a menos):
  1. Palabra target en el pasaje (glow, pulsación suave)
  2. Word bank tiles activos
  3. Texto del pasaje
  4. Título del libro
  5. Controles (hint button, exit)
  6. El Istari Owl (siempre subordinado al contenido)
  7. Decoración del fondo

Si un elemento en posición 5–7 compite visualmente con 1–3, es un bug visual.

DISTANCIA MÍNIMA ENTRE ELEMENTOS INTERACTIVOS:
  Entre tiles del word bank:    8px en pantalla (2px en dibujo)
  Entre tile y borde del panel: 16px en pantalla (4px en dibujo)
  Entre hint button y word bank: 24px en pantalla (6px en dibujo)
  Tap target mínimo para niños: 96×96 px en pantalla (24×24 px en dibujo)
```

### Reglas de feedback visual

```
JERARQUÍA DE FEEDBACK (de más visible a menos):
  1. Correcto: palabra encontrada → glow dorado → vuela al word bank → SFX
  2. Completado: todas las palabras → celebration scene completa
  3. Error: tile rojo suave 500ms máximo → vuelve a estado normal
  4. Pista: el Profesor señala → cristal brilla → highlight sutil en área

REGLA DE DURACIÓN:
  Feedback positivo (correcto, completado): puede durar todo lo necesario
  Feedback negativo (error): máximo 500ms. El juego no castiga — informa.
  Animaciones de celebración: nunca bloquean la siguiente acción del niño

REGLA DE CONTRASTE DE FEEDBACK:
  El estado "found" de un tile debe ser claramente más brillante que "normal"
  El estado "incorrect" es momentáneo — no persiste como estado visual
  Ambos estados van siempre con sonido Y animación, nunca solo color
```

### Reglas de la Library Scene

```
RIQUEZA VISUAL PERMITIDA:
  La Library Scene SÍ puede ser visualmente rica — es la "portada" del juego
  Parallax activo: permitido en idle (sin interacción activa)
  Animaciones ambient: libros brillando, motas de polvo, el Profesor en `idle`
  
LÍMITES DE LA RIQUEZA:
  Los libros interactivos (disponibles) deben destacar sobre los decorativos
  La diferencia entre libro "disponible" y "bloqueado" debe leerse en 1 segundo
  El Profesor nunca tapa libros interactivos en su posición de reposo

DURANTE SELECCIÓN:
  Cuando el cursor/dedo está sobre un libro: todo lo demás reduce brillo al 70%
  Solo el libro seleccionado y el Profesor tienen animación activa
```

### Regla de "cuánto vivo es demasiado"

```
TEST DE DISTRACCIÓN:
  Mostrar la pantalla a un adulto 3 segundos, luego taparla.
  Pregunta: "¿Qué era lo más importante en esa pantalla?"
  
  En PassageView: respuesta correcta = "el texto / las palabras"
  En Library: respuesta correcta = "los libros disponibles"
  
  Si la respuesta es "el búho" o "el fondo" o "las animaciones",
  hay demasiado movimiento o decoración compitiendo con el contenido.
```

---

## 7. Especificaciones Técnicas de Producción

### Estrategia de escalado — Estrategia B (CERRADO)

```
ESTILO:                   Pixel art
ESTRATEGIA:               B — viewport 1920×1080, sprites escalados 4×
FACTOR DE ESCALA:         4× (único factor, sin excepciones)

Godot viewport:           1920 × 1080 px
Stretch mode:             disabled (sin stretch — el viewport ES la resolución)
Aspect ratio:             keep (letterbox si necesario)
Texture filter:           Nearest (TODO — proyecto y por sprite)

  Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  Project Settings → Rendering → 2D → Snap 2D Transforms to Pixel → ON

El texto (pasajes de lectura, UI labels) vive en resolución nativa 1080p.
Los sprites y backgrounds viven en su resolución de dibujo escalada a 4×.
Nunca mezclar filtro Nearest con Bilinear en la misma escena.
```

### Tabla de resoluciones de dibujo → pantalla

```
Asset                   Dibujado en      Se muestra en    Factor
────────────────────────────────────────────────────────────────
Istari Owl (sprite)     48 × 48 px    →  192 × 192 px     4×
Accesorios (overlay)    48 × 48 px    →  192 × 192 px     4×
Iconos UI               16 × 16 px    →   64 ×  64 px     4×
Botones / tiles         16 × 16 px    →   64 ×  64 px     4×   (NineSlice)
Tiles de escena         16 × 16 px    →   64 ×  64 px     4×
Background (layer)     480 × 270 px   → 1920 × 1080 px    4×
Estrellas (pequeña)      8 ×  8 px    →   32 ×  32 px     4×
Estrellas (grande)      16 × 16 px    →   64 ×  64 px     4×
Celebration bg         480 × 270 px   → 1920 × 1080 px    4×
```

Todas las dimensiones de dibujo son **potencia de 2** o múltiplos de 16. Godot acepta cualquier tamaño pero las GPU prefieren POT para atlases.

### Gotchas críticos de pixel art en Godot (leer antes de dibujar el primer sprite)

```
GOTCHA 1 — Filtro de textura (el más común, el más destructivo)
  Godot aplica bilinear por defecto. Destruye el pixel art silenciosamente.
  Fix OBLIGATORIO antes de cualquier import de sprite:
    Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  Y por sprite individualmente si se importa antes del fix:
    Inspector → Texture → Filter → Nearest

GOTCHA 2 — Sub-pixel movement (blur en animaciones)
  Mover un sprite a posición 100.7 px causa blur parcial incluso con Nearest.
  Fix OBLIGATORIO en Project Settings:
    Rendering → 2D → Snap 2D Transforms to Pixel → ON
  Y en código si hay movimiento manual:
    position = position.round()

GOTCHA 3 — Atlas demasiado grande
  Un atlas de 2048×2048 = 16MB en GPU memory, se carga entero aunque no se use.
  Regla: UN ATLAS POR FAMILIA. No mezclar Istari Owl con UI tiles.
    atlas_owl.png        — todos los frames del personaje
    atlas_ui.png         — tiles, botones, iconos
    atlas_fx.png         — efectos (estrellas, partículas mágicas)
  Máximo 2048×2048 px por atlas.

GOTCHA 4 — Master palette rota
  Si cada asset usa colores independientes, el juego se ve inconsistente.
  Solución: definir master palette ANTES de dibujar cualquier asset.
  Ver §2 — Paleta. Todos los sprites sacan colores de ahí, nunca fuera.
  Anti-alias manual (colores intermedios en bordes) NO se usa en pixel art puro.
  El contorno es el color más oscuro de la paleta, sin suavizado.

GOTCHA 5 — Importación en Godot
  Por defecto Godot recomprime las texturas. Para pixel art:
    Inspector del archivo → Import → Compress → Mode → Lossless
    Inspector del archivo → Import → Mipmaps → OFF
  Hacer esto antes del primer sprite, o hacerlo en el preset de import
  para que aplique automáticamente a todos los PNG importados.
```

### Paleta — estructura para pixel art

La paleta Biblioteca Acogedora de §2 son los **tokens funcionales**. La master palette de producción los expande con variantes de luz y sombra necesarias para el pixel art:

```
Por cada color base, se generan 3 valores:
  [base]_shadow   — 25% más oscuro (sombras internas, outlines de profundidad)
  [base]          — el valor definido en §2
  [base]_light    — 25% más claro (highlights especulares)

Ejemplo con parchment (#F5E6C8):
  parchment_shadow:  #C9B898   ← texto secundario, bordes de papel
  parchment:         #F5E6C8   ← fondo principal del texto
  parchment_light:   #FFF5E0   ← highlight en esquinas iluminadas

Total master palette: ~32 colores (16 tokens × 2 variantes + negros y blancos)
Colores fuera de la master palette: no existen.
```

### Sprites y assets del personaje

```
Istari Owl — sprite atlas:
  Resolución por frame:   48 × 48 px
  Frames por estado:      4–8 frames (idle: 4, excited: 8, celebrate: 8)
  Formato de dibujo:      PNG-8 (paleta indexada) o PNG-24 con alpha
  Formato de export:      PNG con alpha transparente
  Atlas destino:          atlas_owl.png — máx 2048 × 2048
  Naming:                 owl_[estado]_[frame_2digits].png
  Punto de anclaje:       centro-base del sprite (pies del personaje)
  
  Organización en atlas (Godot SpriteFrames):
    Cada estado es una Animation en AnimationSprite2D
    FPS por estado:   idle=4, thinking=4, happy=6, hint=8, excited=8,
                      reading=4, celebrate=8, sleepy=3, wave=6

Accesorios (M2):
  Resolución:         48 × 48 px exactos — mismo tamaño que sprite base
  Punto de anclaje:   IDÉNTICO al sprite base — registro pixel-perfect
  Atlas destino:      atlas_accessories.png (separado de atlas_owl.png)
  Transparencia:      100% alpha en áreas sin accesorio
```

### Backgrounds y escenas

```
Library Scene — 4 layers para parallax:
  Resolución de dibujo:   480 × 270 px cada layer
  Se muestra en:          1920 × 1080 px (escala 4×)
  Formato:                PNG con alpha en layers 1–2, PNG sin alpha en 3–4
  Naming:                 bg_library_layer_[1-4].png
  
  Layer 4 (fondo):    Cielo/ventana — sin parallax, estático
  Layer 3:            Estantes del fondo — parallax lento (factor 0.1)
  Layer 2:            Estantes centrales + Profesor — parallax medio (factor 0.3)
  Layer 1 (frente):   Mesa, objetos primer plano — parallax normal (factor 0.6)

PassageView — fondos:
  ParchmentPanel:     tileable 64 × 64 px (se repite a 4× = tile de 256×256)
  WoodPanel:          tileable 64 × 64 px
  Formato:            PNG sin alpha

Celebration scene:
  Fondo animado:      480 × 270 px, 8–12 frames
  Naming:             celebration_[frame_2digits].png
  Formato:            PNG sin alpha
```

### UI elements

```
Word Bank tiles:
  Tamaño de dibujo:   variable × 8 px alto mínimo (NineSlice: 16px ancho, márgenes 4px)
  Se muestra en:      ×4 = altura mínima 32px — pero el contenedor del tile
                      debe tener tap target ≥ 96px alto con padding invisible
  Estados:            normal, hover, selected, found, disabled
  Naming:             tile_word_[estado].png

Botones:
  Tamaño de dibujo:   24 × 24 px mínimo (tap target 96×96 en pantalla)
  Razón:              Apple/Google exigen 44pt mínimo. Para dedos de 4 años
                      con coordinación motriz en desarrollo: 96px en pantalla
                      es el mínimo cómodo. 64px está al límite — no usar.
  NineSlice:          márgenes 4px en dibujo = 16px en pantalla
  Estados:            normal, hover, pressed, disabled

Iconos:
  Tamaño de dibujo:   16 × 16 px
  Se muestra en:      64 × 64 px en pantalla
  Formato:            PNG con alpha
  Naming:             icon_[nombre].png

Estrellas:
  Tamaño de dibujo:   8 × 8 px
  Se muestra en:      32 × 32 px en pantalla
  Estados:            empty, filled, shimmer (4 frames de animación)
  Naming:             star_[estado]_[frame].png
```

### Fuentes — texto en resolución nativa

El texto de pasajes y UI **no es pixel art**. Vive en resolución 1080p nativa para máxima legibilidad. El contraste entre texto nítido y sprites pixelados es intencionado — refuerza que el texto es "real" y el mundo mágico es el juego.

```
Fuente de lectura (pasajes de texto):
  Función:          Máxima legibilidad para niños aprendiendo a leer
  Estilo:           Serif clara con letterforms sin ambigüedad
                    (b/d/p/q claramente distintas — crítico para lectores iniciales)
  ✅ SELECCIONADA:  Andika (SIL) — OFL — diseñada específicamente para literacy
                    letterforms engineered para minimizar confusión b/d/p/q
  Fallback:         OpenDyslexic — para el modo dyslexia_font del settings
  Tamaños:          small=18px, medium=22px, large=28px, xl=34px
  NUNCA menos de 18px para texto de pasaje

Fuente de UI (labels, títulos, botones):
  Estilo:           Redondeada, legible desde 14px, evoca lettering de libro ilustrado
  ✅ SELECCIONADA:  Nunito (Google Fonts) — OFL — redondeada, amigable, legible en tamaños pequeños
  NUNCA cursiva para texto funcional. NUNCA menos de 14px.

Reglas comunes:
  - Licencia OFL obligatoria ✅ (Andika: SIL OFL · Nunito: OFL)
  - Guardadas en res://fonts/ como .ttf
  - Subsetted si > 500KB (usar pyftsubset — instrucciones en Guía de Construcción)
  - Descarga: https://fonts.google.com/specimen/Andika
              https://fonts.google.com/specimen/Nunito
```

### Presupuesto de memoria GPU y build size HTML5

```
MEMORIA GPU — TEXTURAS EN PANTALLA ACTIVA
────────────────────────────────────────────────────────────
Atlas personaje (atlas_owl.png):
  Contenido:     ~72 frames × 48×48 → cabe en 1024×512 px
  En GPU:        1024 × 512 × 4 bytes = 2MB

Atlas UI (atlas_ui.png):
  Contenido:     tiles, botones, iconos, estrellas
  Tamaño atlas:  512 × 512 px
  En GPU:        512 × 512 × 4 bytes = 1MB

Backgrounds (4 layers — ARCHIVOS SEPARADOS, nunca un atlas):
  Cada layer:    480 × 270 × 4 bytes ≈ 500KB
  Total 4 layers: ~2MB
  ⚠️ Si los layers estuvieran en un atlas 1920×1080 = 8MB en un solo texture
     y excedería el límite de 2048×2048 de Chromebooks escolares. No hacer esto.

Total estimado en pantalla activa: ~5MB de texturas en GPU

LÍMITES DE TEXTURA POR PLATAFORMA (HTML5)
────────────────────────────────────────────────────────────
Chrome desktop:            16384×16384  ✅
Chrome Android gama alta:   8192×8192   ✅
Chrome Android gama baja:   4096×4096   ⚠️  Testear
Safari iOS:                16384×16384  ✅
Firefox:                   16384×16384  ✅
Chromebook escolar:         2048×2048   ⚠️  Target crítico — hardware más común en escuelas

Regla derivada: ningún atlas individual supera 2048×2048. Siempre.
Los 4 background layers son archivos PNG separados (480×270 cada uno).
Un atlas de layers combinados en 1920×1080 rompería en Chromebooks.

BUILD SIZE HTML5 — EL PRESUPUESTO REAL
────────────────────────────────────────────────────────────
Cap objetivo:              < 15MB total (definido en Contrato de Arquitectura)
Godot runtime (WASM):      ~10MB (fijo — no se puede reducir)
Presupuesto para contenido: ~5MB para TODOS los assets

Desglose de los 5MB disponibles:
  Texturas (atlas_owl + atlas_ui + 4 bg layers):  ~5MB sin comprimir
  → Con compresión PNG real:                       ~1.5–2MB ✅
  Audio UI (SFX, música ambiente):                 ~1MB
  Fuentes (2 fuentes subsetted):                   ~0.3MB
  Código GDScript compilado:                       ~0.5MB
  Primer book pack builtin (texto + audio):        ~1MB
  Total estimado:                                  ~4–4.5MB ✅ con margen

⚠️ BLOQUEADOR: testear export HTML5 en Chromebook real o con
   Chrome DevTools → More tools → Rendering → Hardware concurrency: 2 cores
   ANTES de fin de M0. Si el WASM pesa más de 10MB en el build, revisar
   opciones de export de Godot (template size, strips debug info).
```

### Formatos y límites

```
Audio (narración):      OGG Vorbis, max 1MB por archivo
Imágenes (sprites):     PNG con alpha, max 2MB por archivo
Imágenes (fondos):      PNG sin alpha, max 2MB por archivo
Fuentes:                TTF/OTF, max 5MB por archivo
Cualquier asset:        max 10MB hard cap

Import settings en Godot (aplicar a todos los PNG de sprites):
  Compress → Mode:      Lossless   (preserva pixels exactos)
  Mipmaps:              OFF        (mipmaps destruyen pixel art)
  Filter:               Nearest    (ya definido en Project Settings, confirmar por asset)
```

---

## 8. Guía para modders — crear un theme

> Esta sección es el contenido de `THEME_CREATION.md` que se distribuirá públicamente.
> Escrita para un audience de teachers, artistas indie y modders sin perfil técnico profundo.

### ¿Qué es un theme?

Un theme es un conjunto de archivos que cambia el aspecto visual del juego sin tocar el código. El contenido (libros, puzzles) y el gameplay no cambian.

### Niveles de override — qué puedes cambiar y cuándo

No todos los overrides son iguales. El sistema tiene tres niveles de apertura:

**Nivel 1 — Safe overrides (disponible desde M1):**
Cambios que no pueden romper el juego ni la accesibilidad si se hacen mal. El juego valida estos automáticamente.
- Tokens de color (`theme.json` → `colors`)
- Backgrounds de la Library Scene (4 layers PNG)
- Preview image del theme
- Sonidos de UI (clicks, hover) — especificados en M2

**Nivel 2 — Advanced overrides (disponible desde M2):**
Cambios que requieren más cuidado. El Preview Tool da advertencias pero no bloquea.
- Fuentes custom (solo OFL — el validador chequea la licencia declarada en metadata)
- Sprites del Profesor (solo estados completos — no frames sueltos)
- UI tiles: word bank, botones, iconos

**Nivel 3 — Restricted (no disponible para modders externos):**
Cambios que tocan layout, accesibilidad sistémica, o features incompletos.
- Paletas de daltonismo (el juego las gestiona automáticamente)
- Celebration scene (schema aún abierto — ver §11)
- Layout RTL visual (Contrato de Arquitectura §7.2 abierto)
- Reemplazos de frames individuales del Profesor (solo atlas completo)
- Cualquier cosa que cambie el tamaño de tap targets

### Estructura de un theme pack

```
mi_theme/
├── metadata.json         ← OBLIGATORIO — descripción del theme
├── theme.json            ← OBLIGATORIO — tokens de color y referencias a assets
├── preview.png           ← Recomendado — captura 640×360 para el selector
├── sprites/
│   ├── owl_idle_01.png   ← Opcional — reemplaza sprites del Profesor
│   └── ...
├── backgrounds/
│   ├── bg_main.png       ← Opcional — fondo de la Library Scene
│   └── ...
├── ui/
│   ├── tile_word_normal.png   ← Opcional — tiles del word bank
│   └── ...
└── fonts/
    └── mi_fuente.ttf     ← Opcional — fuente custom (licencia OFL)
```

### `metadata.json`

```json
{
  "schema_version": "1.0",
  "id": "enchanted_forest",
  "title": "Enchanted Forest",
  "author": "Tu Nombre",
  "version": "1.0.0",
  "description": "Un bosque mágico para leer entre árboles y hongos luminosos.",
  "preview": "preview.png",
  "license": "CC BY 4.0",
  "flags": {
    "dark": false,
    "rtl": false
  }
}
```

### `theme.json`

Define los colores usando los tokens del sistema. **Solo necesitas definir los tokens que quieres cambiar** — los que omitas usan los valores del Biblioteca Acogedora por defecto.

```json
{
  "schema_version": "1.0",
  "colors": {
    "background":       "#0D1F0A",
    "surface":          "#1A3311",
    "surface_light":    "#2A5218",
    "parchment":        "#E8F0D4",
    "parchment_shadow": "#D0E0B0",
    "text_primary":     "#1A0F00",
    "text_primary_light": "#E8F0D4",
    "text_secondary":   "#4A7A2A",
    "accent":           "#8BC34A",
    "accent_warm":      "#FF9800",
    "magic_glow":       "#00BCD4",
    "magic_blue":       "#0A1F15",
    "correct":          "#4CAF50",
    "incorrect":        "#E53935",
    "hint":             "#FF9800",
    "neutral":          "#607D4A"
  },
  "backgrounds": {
    "library_layer_1": "backgrounds/forest_layer_1.png",
    "library_layer_2": "backgrounds/forest_layer_2.png",
    "library_layer_3": "backgrounds/forest_layer_3.png",
    "library_layer_4": "backgrounds/forest_sky.png"
  },
  "sprites": {
    "owl_idle":     "sprites/owl_idle_01.png",
    "owl_happy":    "sprites/owl_happy_01.png"
  },
  "fonts": {
    "reading":  "fonts/mi_fuente_lectura.ttf",
    "ui":       "fonts/mi_fuente_ui.ttf"
  }
}
```

### Tokens de color obligatorios vs opcionales

| Token | Obligatorio | Notas |
|---|---|---|
| `background` | ✅ | Color de fondo principal |
| `surface` | ✅ | Paneles, contenedores |
| `parchment` | ✅ | Fondo del texto de lectura |
| `text_primary` | ✅ | Texto sobre parchment |
| `text_primary_light` | ✅ | Texto sobre fondos oscuros |
| `accent` | ✅ | Estrellas, logros, highlights. **Elige con cuidado: el juego lo usa para recompensar al niño.** Tu `accent` debe destacar fuertemente sobre tu `background` (ratio ≥ 3:1). En un theme cyberpunk, el rosa neón es el nuevo "dorado sagrado" — úsalo solo para victorias. |
| `correct` | ✅ | Feedback positivo |
| `incorrect` | ✅ | Feedback de error |
| `surface_light` | ❌ | Default: `surface` + 20% luminosidad |
| `parchment_shadow` | ❌ | Default: `parchment` - 15% luminosidad |
| `text_secondary` | ❌ | Default: `accent` + 30% oscuridad |
| `accent_warm` | ❌ | Default: `accent` con hue +30° |
| `magic_glow` | ❌ | Default: `#7B4FBE` |
| `magic_blue` | ❌ | Default: `#1E3A5F` |
| `hint` | ❌ | Default: `#FF9800` |
| `neutral` | ❌ | Default: `#9E9E9E` |

### Especificaciones de assets para modders

```
Backgrounds (layers de biblioteca):
  Resolución de dibujo:   480 × 270 px por layer (se escala 4× en juego)
  Formato:      PNG con alpha en layers 1–2, PNG sin alpha en 3–4
  Límite:       2MB por archivo

Sprites del Profesor (opcionales, Nivel 2):
  Resolución:   48 × 48 px exactos — NO escalar antes de exportar
  Formato:      PNG con alpha, Filter → Nearest, Mipmaps → OFF
  Punto de anclaje: centro-base — debe coincidir pixel-perfect con default
  Override:     atlas completo por estado (no frames sueltos)
  Límite:       100KB por sprite

UI tiles (opcionales, Nivel 2):
  Word bank tile: 16 × 8 px (NineSlice, márgenes 4px) — se ve 64×32 en pantalla
  Botones:        24 × 24 px mínimo — se ve 96×96 en pantalla ← tap target para niños
  Formato:        PNG con alpha
```

### ¿Qué es NineSlice y cómo dibujar para él?

NineSlice permite que un botón o tile se estire para contener texto de cualquier largo sin distorsionar las esquinas. Se dibuja así:

```
┌──┬────────────┬──┐   El sprite de 16×16 se divide en 9 zonas
│  │            │  │   con márgenes de 4px en cada lado:
│  │            │  │
├──┼────────────┼──┤   Esquinas (4px×4px): NO se estiran nunca
│  │            │  │   Bordes H (top/bottom): se estiran solo en X
│  │   centro   │  │   Bordes V (left/right): se estiran solo en Y
├──┼────────────┼──┤   Centro: se estira en X e Y
│  │            │  │
└──┴────────────┴──┘
←4→←────────────→←4→
     (se estira)

Práctica: dibuja las 4 esquinas con tu decoración (redondeada, ornamentada,
lo que sea). El centro y los bordes pueden ser color plano o textura simple.
En Godot: NinePatchRect, patch_margin_left/right/top/bottom = 4 (en px del sprite).
```

### Reglas de accesibilidad (validadas automáticamente por el Preview Tool desde M1)

Un theme que viola estas reglas será **bloqueado** por el Preview Tool — no se puede publicar ni usar:

1. **Contraste mínimo:** `text_primary` sobre `parchment` debe tener ratio ≥ 4.5:1 (WCAG AA)
2. **Contraste mínimo:** `text_primary_light` sobre `background` debe tener ratio ≥ 4.5:1
3. **`correct` e `incorrect` no pueden ser el mismo color** ni tener contraste < 3:1 entre sí
4. **`accent` debe ser distinguible de `background` con ratio ≥ 3:1**

El Preview Tool reporta el ratio exacto de cada regla fallida con el valor necesario para corregirlo.

---

## 9. Prioridad de assets para el primer jugable

✅ No producir assets fuera de M0 hasta que los de M0 estén jugables y testeados en HTML5.

### M0 — Primer pasaje jugable (mínimo absoluto)

```
Personaje:
  owl_idle_01..04.png        4 frames — el Profesor existe en pantalla
  owl_thinking_01..04.png    4 frames — durante puzzle activo
  owl_hint_01..04.png        4 frames — al dar pista

Library Scene:
  bg_library_layer_4.png     fondo estático (ventana/cielo) — sin parallax por ahora
  bg_library_layer_3.png     estantes del fondo — sin parallax por ahora
  (layers 1 y 2 pueden ser placeholder de color plano en M0)

PassageView:
  parchment_tile.png         64×64 tileable para fondo de texto
  wood_tile.png              64×64 tileable para panel de puzzle

UI:
  tile_word_normal.png       word bank tile — estado base
  tile_word_selected.png     word bank tile — seleccionado
  tile_word_found.png        word bank tile — encontrado
  btn_hint.png               botón de pista (24×24)
  btn_exit.png               botón de salida (24×24)
  star_empty.png             estrella vacía (8×8)
  star_filled.png            estrella llena (8×8)
  icon_hint.png              cristal del bastón (16×16)

Celebration:
  celebration_stub.png       frame único estático — placeholder hasta M1

Total M0: ~20 archivos. Todos deben testear en HTML5/Chromebook antes de M1.
```

### M1 — Estados completos y parallax

```
Personaje (estados restantes):
  owl_happy_01..06.png       6 frames
  owl_excited_01..08.png     8 frames
  owl_reading_01..04.png     4 frames
  owl_celebrate_01..08.png   8 frames
  owl_sleepy_01..04.png      4 frames
  owl_wave_01..06.png        6 frames

Library Scene:
  bg_library_layer_1.png     objetos primer plano (con alpha)
  bg_library_layer_2.png     estantes centrales + posición del Profesor (con alpha)
  Parallax activo en los 4 layers

UI:
  tile_word_disabled.png     estado deshabilitado
  tile_word_hover.png        estado hover (desktop)
  btn_*_pressed.png          estado pressed para todos los botones
  btn_*_disabled.png         estado disabled para todos los botones
  star_shimmer_01..04.png    animación de shimmer (4 frames)
  icon_star.png, icon_settings.png, icon_home.png (16×16 c/u)

Celebration scene completa (reemplaza stub)
```

### M2+ — Accesorios, themes, polish

```
M2:  Sistema de accesorios del Profesor (atlas_accessories.png)
     Paletas de daltonismo testeadas e integradas
     Primer theme comunitario de referencia

M3+: Celebration scene rica con partículas
     Libros como objetos con perspectiva en estante
     Assets RTL si el contrato de §7.2 se cierra
```

---

## 10. Criterios visuales de aceptación

Antes de considerar un milestone completo desde el punto de vista visual, todos los checks deben pasar. Son tests que puede hacer cualquier persona — no requieren conocimiento técnico.

### Checks de silueta y legibilidad

```
✓ El Istari Owl se reconoce como "figura con sombrero y bastón"
  al ver solo la silueta sin color, a tamaño 48×48 nativo.
  Test: screenshot → desaturar → reducir a 12×12 → identificable.

✓ Los tiles del word bank se leen como "palabras en fichas"
  a 64×32 en pantalla desde 60cm de distancia en tablet.

✓ Un libro disponible se distingue de uno bloqueado en < 1 segundo
  sin instrucción previa. Test con niño de 5 años.

✓ Los botones de acción principal tienen área táctil ≥ 96×96 px en pantalla.
  Test: activar Accessibility → Touch → Show Touches en Android, confirmar zona.
```

### Checks de UI readability

```
✓ Mostrar PassageView 3 segundos a un adulto → tapar → preguntar:
  "¿Qué era lo más importante?"
  Respuesta correcta: "el texto" o "las palabras".
  Si dice "el búho" o "el fondo": hay ruido visual.

✓ Mostrar Library Scene 3 segundos → tapar → preguntar:
  "¿Dónde harías clic para leer?"
  Respuesta correcta: señala libros brillantes.
  Si señala el Profesor o la decoración: los libros no destacan suficiente.

✓ Texto de pasaje a tamaño `small` (18px) legible desde 40cm en pantalla
  de tablet de 7 pulgadas. Test físico.

✓ En modo daltonismo deuteranopia: `correct` e `incorrect` son distinguibles
  sin sonido ni animación. Test con Color Oracle activado.
```

### Checks de consistencia visual

```
✓ Todos los sprites usan colores de la master palette.
  Test: abrir atlas_owl.png en editor → usar cuentagotas en 10 pixels random
  → todos deben estar en la master palette de §2.

✓ El outline del Profesor tiene 1px exacto. Sin zonas de 2px ni 0px.
  Test: zoom 800% en el sprite → inspeccionar borde.

✓ La dirección de luz es superior izquierda en todos los sprites.
  Test: verificar que sombras están en inferior-derecha en todos los assets.

✓ El build HTML5 total es < 15MB (incluyendo WASM).
  Test: `du -sh` en el directorio de export. Bloqueador si > 15MB.

✓ El juego corre a 60fps estables en Chromebook de gama media.
  Test: Chrome DevTools → Performance → 30 segundos de gameplay.
  Si hay drops bajo 45fps: investigar antes de continuar.
```

### Checks de storybook warmth

```
✓ Mostrar 3 screenshots del juego a alguien que no lo conoce.
  Pregunta: "¿Para quién es este juego?"
  Respuesta esperada: niños, escuela, lectura, magic/mágico.
  Si dice "adultos" o "acción" o "genérico": el estilo necesita trabajo.

✓ El juego NO parece una app de productividad o un SaaS de educación.
  Check subjetivo pero importante — si tiene look de Google Classroom,
  algo está mal con la paleta o las formas.
```

---

## 11. Lo que todavía está abierto

⚠️ No producir assets en estas áreas hasta que estén cerradas.

| Tema | Estado | Milestone | Impacto |
|---|---|---|---|
| **Estilo: pixel art, Estrategia B** | ✅ Cerrado | — | — |
| **Paletas daltonismo** | ✅ Cerrado en decisión arquitectónica | Paletas en M1, integración M2 | Testear con Color Oracle antes de M1 |
| **Validador contraste Preview Tool** | ✅ Cerrado — M1 | M1 | — |
| **Fuentes específicas** | ✅ Cerrado — Andika (pasajes) + Nunito (UI) | M0 | Descargar y commit en `res://fonts/` antes de construir PassageView |
| **Tipografía display para títulos** | ✅ Cerrado — Nunito (misma que UI) | M0 | Coherente con decisión de fuente UI |
| **Accesorios del Istari Owl** | ⚠️ Abierto — categorías definidas | M2 | No bloquea M0/M1 |
| **Diseño Celebration Scene completo** | ⚠️ Abierto — stub en M0 | M1 | Stub suficiente para M0 |
| **Libro como objeto con perspectiva** | ⚠️ Abierto | M2+ | Puede ser sprite 2D plano en M0/M1 |
| **RTL layout visual** | 🔴 Bloqueado — Contrato de Arquitectura §7.2 | Post-M3 | No producir assets RTL |
| **Validación visual con mock** | ⚠️ Pendiente | Antes de fin M0 | 1 Library, 1 PassageView, 1 owl sheet, 1 UI set |

---

*Documento: READCRAFTERY Art Style Guide v1.3*  
*Siguiente revisión: mock visual de validación (antes de fin de M0), paletas de daltonismo testeadas (M1).*
