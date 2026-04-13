---
name: brand-setup
description: |
  Brand onboarding skill that creates a single brand-voice.md shared across ALL skills (email, ads, organic content).
  ALWAYS trigger this skill when the user says: "setup de marca", "configurar marca", "onboarding de marca",
  "crear brand voice", "quiero empezar con una marca nueva", "configurar [nombre de marca]",
  "setup brand", "armar el perfil de la marca", "la marca todavía no está configurada",
  "no tenemos brand-voice", "necesito que aprendas sobre mi marca", or anything similar.
  Also trigger when ANY other skill (email, ads, organic) starts and there is no brand-voice.md for the brand.
  Input: website URL + Instagram handle + brand folder. Output: brand-voice.md at [Marca]/brand-voice.md.
---

## Qué hace esta skill

Crea (o actualiza) el archivo `brand-voice.md` combinando dos fuentes:

1. **Datos objetivos** que Claude extrae solo: sitio web, Instagram, archivos en la carpeta
2. **Datos subjetivos** que solo el dueño de la marca puede dar: historia real, valores, forma de tratar al cliente, visión

El resultado cubre los **6 pilares que construyen una marca** (framework Conversion UX):
Brand Story · Fonts & Colors · Tone of Voice · How You Treat Your Customers · Your Product Quality · Vision / Mission / Impact

---

## PASO 1: Bienvenida — pedir los tres inputs

> "Vamos a armar el perfil completo de [Marca] — el documento que va a usar cada skill para comunicar como vos, sin tener que preguntar todo de nuevo cada vez.
>
> Es una entrevista de ~10 minutos. Necesito tres cosas para arrancar:
>
> 1. **URL del sitio web** (o "no tengo web todavía")
> 2. **Usuario de Instagram** (o el que uses más — TikTok, etc.)
> 3. **Ruta de la carpeta** de la marca en tu computadora
>
> Con eso primero reviso lo que ya existe, y después te hago las preguntas que solo vos podés responder."

Esperar los tres inputs antes de continuar.

---

## PASO 2: Escaneo silencioso (sin interrumpir al usuario)

Hacer todo esto en paralelo **sin ir y venir con preguntas**. El usuario no tiene que esperar ni responder nada durante este paso.

### 2a. Sitio web

Usar `WebFetch` para visitar:
- Homepage (`/`) — headline, propuesta de valor, tono
- About / Nosotros (`/about`, `/nosotros`, `/historia`) — historia, fundador, misión
- Productos / Shop (`/productos`, `/shop`, `/collections/all`) — catálogo completo con precios
- Blog (si existe) — tono en formato largo
- FAQ / Contacto — cómo habla con los clientes, políticas

Extraer: lenguaje, registro, frases textuales, productos con precios, colores de UI, historia del fundador.

### 2b. Instagram

Intentar `WebFetch` en `https://www.instagram.com/[handle]/`. Si Instagram bloquea el fetch:
> "No pude acceder a Instagram directamente. Pegame 3-5 captions recientes (cualquier post tuyo) para capturar cómo escribís en redes."

Si hay acceso: extraer captions, hashtags, tono, frecuencia de emojis, tipo de contenido.

### 2c. Carpeta de la marca

Buscar y leer archivos de contenido existente: emails, copies de ads, posts guardados, brand guidelines, catálogos. Si hay poco o nada, anotarlo y seguir.

### 2d. Presentar lo que encontró

Antes de arrancar la entrevista, mostrar un resumen rápido de lo que ya capturó:

> "Listo, revisé el sitio y lo que hay en la carpeta. Esto es lo que ya tengo:
>
> ✅ Productos con precios: [lista rápida]
> ✅ Tono detectado: [coloquial/formal, tuteo/voseo]
> ✅ Frases propias encontradas: "[frase 1]", "[frase 2]"
> ⚠️ Esto no pude encontrar: historia completa del fundador, colores exactos, cómo manejás los reclamos
>
> Ahora necesito lo que solo vos podés contarme. Son 6 bloques de preguntas, 2-3 por vez."

---

## PASO 3: Entrevista — los 6 pilares

**Regla de oro:** Hacer 2-3 preguntas por bloque. Esperar respuesta completa. Recién ahí pasar al siguiente bloque. No mezclar pilares.

Si el usuario ya respondió algo de un pilar en el escaneo o en mensajes anteriores, saltarlo o solo pedir confirmación.

---

### Bloque 1 — BRAND STORY

> "Empecemos por la historia de [Marca].
>
> 1. ¿Cómo nació esto? Contame con tus palabras — qué te pasó a vos que te llevó a crear la marca. No el texto del sitio, la historia real.
> 2. ¿Contra qué está peleando tu marca? ¿Qué está mal en tu industria o mercado que vos querés cambiar?"

*(Escuchar. Si la respuesta es corta, preguntar: "¿Hay algo más detrás que no está en el sitio?")*

---

### Bloque 2 — TONE OF VOICE

> "Ahora quiero escuchar cómo escribís.
>
> 3. Pegame 2-3 textos que hayas escrito vos para la marca — un caption, un DM a un cliente, una descripción de producto, lo que tengas. Cualquier cosa.
> 4. ¿Hay palabras o frases que definitivamente NUNCA usarías para hablar de tu marca? ¿Qué te suena raro o falso?"

*(Con los textos, analizar: ritmo, puntuación, emojis, registro, si usa vos/tú/usted, cómo cierra.)*

---

### Bloque 3 — PRODUCT QUALITY

> "Hablemos del producto.
>
> 5. ¿Qué hace que [producto] sea mejor que lo que ya existe? Específicamente — no lo que dice el marketing, lo que vos sabés que es verdad.
> 6. ¿Qué no usás, no hacés o no tolerás que tu competencia sí hace? Eso es tu diferenciador real."

*(Buscar el argumento honesto de calidad — no el slogan. Eso es lo que convierte en copy.)*

---

### Bloque 4 — HOW YOU TREAT YOUR CUSTOMERS

> "¿Cómo es la relación con tus clientes?
>
> 7. Cuando hay un problema — un pedido que llegó mal, un cliente enojado — ¿cómo lo manejás? ¿Tenés una política de cambios o devoluciones?
> 8. ¿Con qué nombre firmás cuando les escribís? ¿Hay algo que hacés por tus clientes que la mayoría de marcas no hace?"

*(El trato al cliente es parte de la marca. Si Franco firma como "Franco" no como "el equipo de atención", eso va en el perfil.)*

---

### Bloque 5 — VISION / MISSION / IMPACT

> "Mirando más largo plazo.
>
> 9. ¿A dónde querés llevar [Marca] en 3-5 años? No en ventas — en impacto. ¿Qué querés que cambie gracias a tu marca?
> 10. ¿Hay algo más grande detrás de lo que hacés? Una causa, algo que querés demostrar, una forma de entender el mundo que está en el ADN de la marca."

---

### Bloque 6 — FONTS, COLORS & VISUAL IDENTITY

> "Último bloque — identidad visual.
>
> 11. ¿Cuáles son los colores de la marca? (hex si los tenés, o describílos — "verde oscuro y blanco crudo")
> 12. ¿Tenés logo en algún formato digital? ¿Dónde está guardado?
> 13. ¿Hay alguna marca o estética visual que te inspire o con la que quieras que te comparen? (No tiene que ser del mismo rubro)"

---

## PASO 4: Confirmación antes de generar

Antes de crear el archivo, mostrar un resumen de todo lo capturado:

> "Perfecto. Con esto tengo todo lo que necesito. Te confirmo lo que voy a documentar:
>
> **Brand Story:** [2 líneas del origen real]
> **Tono:** [coloquial/formal, tuteo, frases características detectadas]
> **Producto:** [diferenciador principal]
> **Trato al cliente:** [cómo maneja problemas, cómo firma]
> **Visión:** [hacia dónde va]
> **Visual:** [colores confirmados]
>
> ¿Algo que quieras corregir o agregar antes de que genere el brand-voice.md?"

Esperar confirmación o ajustes. Recién ahí generar el archivo.

---

## PASO 5: Generar el brand-voice.md

Con toda la información recopilada, crear el archivo siguiendo el template en `references/brand-voice-template.md`.

**Principios al escribir:**
- Ser específico: no "tono cálido", sino "usa tuteo, frases cortas, cierra con 'Franco / [Marca]'"
- Frases textuales: copiar literalmente del sitio, Instagram o respuestas del usuario
- Palabras prohibidas: las que el usuario dijo + las que detectaste que nunca aparecen en su contenido
- Por canal: aunque el CORE sea igual, cada canal tiene su matiz — documentarlo

Guardar en: `[Marca]/brand-voice.md`

Si ya existía un brand-voice.md: leerlo, comparar con la nueva info, hacer merge inteligente. Agregar `## ACTUALIZACIÓN [fecha]` al final con lo que cambió.

---

## PASO 6: Crear estructura de carpetas

Verificar y crear si no existe:

```bash
mkdir -p "[Marca]/REFERENCIAS/productos"
mkdir -p "[Marca]/REFERENCIAS/estilos"
mkdir -p "[Marca]/Marketing/EMAILS"
mkdir -p "[Marca]/Marketing/ADS"
mkdir -p "[Marca]/Marketing/ORGANICO"
```

Si la carpeta ya tiene una estructura numerada (01-Investigacion, 03-Marketing, etc.), respetar esa estructura y crear las subcarpetas dentro del directorio de marketing correspondiente.

---

## PASO 7: Confirmación final

> "✅ Perfil de [Marca] guardado en `[ruta]/brand-voice.md`
>
> **Cubrimos los 6 pilares:**
> ✅ Brand Story — historia real del fundador
> ✅ Fonts & Colors — [colores documentados]
> ✅ Tone of Voice — [registro, frases, palabras prohibidas]
> ✅ How You Treat Your Customers — [filosofía de atención]
> ✅ Product Quality — [diferenciadores reales]
> ✅ Vision / Mission / Impact — [hacia dónde va la marca]
>
> Ahora podés usar las skills de email, ads y orgánico — todas van a leer este perfil sin preguntarte nada de nuevo.
>
> Para actualizar el perfil en el futuro, solo decime 'actualizá el brand-voice de [Marca]'."

---

## Cuándo actualizar brand-voice.md

- La marca lanzó productos nuevos
- Cambió la paleta o identidad visual
- Empezó a comunicar en un canal nuevo
- El usuario dice "el tono cambió" o "ahora somos más X"
- Han pasado más de 6 meses desde la última actualización

Al actualizar: leer el archivo actual, identificar qué cambió, hacer merge y agregar la sección de actualización con fecha.
