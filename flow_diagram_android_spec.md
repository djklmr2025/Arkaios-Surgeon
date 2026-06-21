# Flow Diagram Creator — Especificación Técnica para App Android
**Versión:** 1.4-r1 | **Fecha:** 2026-06-01

---

## 1. Arquitectura General del Sistema

El sistema es una **Single Page Application (SPA)** en HTML/JS puro que vive en Vercel. Todo el render ocurre en un `<canvas>` HTML5 usando la API 2D (`CanvasRenderingContext2D`). No hay librería de render de terceros — es canvas puro con transformaciones de cámara propias.

```
Usuario/App Android
      │
      ▼
GET https://flow-diagram-creator.vercel.app/api/project?id=<ID>
      │
      ▼
Vercel Blob Storage → devuelve el JSON del proyecto
      │
      ▼
index.html parseea elements[] y dibuja en canvas 2D
```

---

## 2. Estructura Completa del JSON

### 2.1 Envelope raíz

```json
{
  "name": "NOMBRE DEL PROYECTO",
  "date": "2026-06-01T23:27:11.731Z",
  "elements": [ ...array de objetos... ],
  "camera": {
    "x": 0,
    "y": 0,
    "zoom": 1
  }
}
```

| Campo | Tipo | Descripción |
|---|---|---|
| `name` | string | Nombre del proyecto |
| `date` | string ISO8601 | Fecha de guardado |
| `elements` | array | **Todos los objetos del canvas** |
| `camera` | object | Estado inicial de la cámara (pan + zoom) |

---

### 2.2 Objeto BASE — campos comunes a todos los tipos

Todos los elementos comparten estos campos:

```json
{
  "id": "1772517759336.8704",
  "type": "circle",
  "name": "Nombre del elemento",
  "x": 400.5,
  "y": 300.2,

  "strokeColor": "transparent",
  "fillColor": "transparent",
  "lineWidth": 5,

  "locked": false,
  "active": true,
  "preview": false,

  "connectionStatus": "none",

  "routeRole": true,
  "followRoute": false,
  "routeId": "",
  "routeSpeed": 40,
  "routeDirection": "right",
  "routeProgress": 0,
  "routeMode": "loop",
  "autoConnectRoute": false
}
```

| Campo | Valores posibles | Descripción |
|---|---|---|
| `id` | string timestamp | ID único |
| `type` | `circle`, `rect`, `path`, `line`, `image`, `mover`, `text` | Tipo de elemento |
| `connectionStatus` | `"none"`, `"left"`, `"right"`, `"both"` | Indicador de flujo visual |
| `routeRole` | boolean | Si este elemento ES una ruta (path) |
| `followRoute` | boolean | Si un mover sigue esta ruta |
| `routeDirection` | `"right"`, `"left"` | Dirección de animación |
| `routeMode` | `"loop"`, `"once"` | Tipo de ciclo |
| `active` | boolean | Si está animado activamente |
| `preview` | boolean | Si está en modo preview (fondo 3D) |

---

### 2.3 Tipo: `circle`

```json
{
  "type": "circle",
  "x": 400,
  "y": 300,
  "radius": 25,
  "strokeColor": "#00d4ff",
  "fillColor": "transparent",
  "lineWidth": 2
}
```

**Render:** `ctx.arc(x, y, radius, 0, Math.PI * 2)`

---

### 2.4 Tipo: `rect`

```json
{
  "type": "rect",
  "x": 100,
  "y": 100,
  "width": 200,
  "height": 80,
  "strokeColor": "#ffffff",
  "fillColor": "rgba(0,0,0,0.3)",
  "lineWidth": 1
}
```

**Render:** `ctx.fillRect(x, y, width, height)` + `ctx.strokeRect(x, y, width, height)`

---

### 2.5 Tipo: `path` (ruta de movimiento / línea animada)

Este es el tipo más complejo. Puede ser una **ruta de movimiento** para actores, o una **línea dibujada** con partículas animadas.

```json
{
  "type": "path",
  "name": "Ruta 1772517759336",
  "x": -1295,
  "y": 144,
  "points": [
    {"x": -1295.5181874041939, "y": 144.8375757055241},
    {"x": -1297.3598902962045, "y": 147.9012638671875},
    ...
  ],
  "strokeColor": "transparent",
  "fillColor": "transparent",
  "lineWidth": 5,
  "routeRole": true,
  "routeArcSide": "left",
  "routeArcDegrees": 120,
  "routeCircular": false,
  "closed": false
}
```

**Campos específicos de path:**

| Campo | Descripción |
|---|---|
| `points` | Array de `{x, y}` en coordenadas de mundo |
| `closed` | Si el path se cierra (forma polígono) |
| `routeArcSide` | `"left"` o `"right"` — lado del arco |
| `routeArcDegrees` | 0 = línea recta, 90/120/180 = arco curvado |
| `routeCircular` | Si el path es un círculo completo |

**Algoritmo de render de path:**
```js
// Para path con arco:
function drawPathWithArc(points, arcDegrees, arcSide) {
  ctx.beginPath();
  ctx.moveTo(points[0].x, points[0].y);
  
  for (let i = 0; i < points.length - 1; i++) {
    const p1 = points[i];
    const p2 = points[i + 1];
    
    if (arcDegrees === 0) {
      // Línea recta
      ctx.lineTo(p2.x, p2.y);
    } else {
      // Curva de Bézier cuadrática
      const cpx = (p1.x + p2.x) / 2 + perpendicular_offset(p1, p2, arcDegrees, arcSide);
      const cpy = (p1.y + p2.y) / 2 + perpendicular_offset(p1, p2, arcDegrees, arcSide);
      ctx.quadraticCurveTo(cpx, cpy, p2.x, p2.y);
    }
  }
  ctx.stroke();
}
```

---

### 2.6 Tipo: `image`

```json
{
  "type": "image",
  "x": -1773,
  "y": -321,
  "width": 2551,
  "height": 3402,
  "originalWidth": 2551,
  "originalHeight": 3402,
  "imageSrc": "https://ztp1rr121kcBagm0w.public.blob.vercel-storage.com/projects/bf062f6d6b794d5e/assets/1-636b06a056c8.jpg",
  "opacity": 1
}
```

**Campos específicos:**

| Campo | Descripción |
|---|---|
| `imageSrc` | URL absoluta de la imagen en Vercel Blob |
| `opacity` | 0.0 – 1.0 |
| `originalWidth/Height` | Tamaño original antes de escalar |

**Render:** Cargar la imagen con `loadImage(imageSrc)` luego `ctx.drawImage(img, x, y, width, height)`

> **⚠️ CORS para Android:** Las imágenes están en Vercel Blob (`blob.vercel-storage.com`) con CORS abierto. Puedes descargarlas directamente con `HttpUrlConnection` o Picasso/Glide.

---

### 2.7 Tipo: `mover` (actor animado — Metro, Hombre, Mujer)

```json
{
  "type": "mover",
  "moverKind": "metro",
  "x": -177,
  "y": -703,
  "width": 44,
  "height": 28,
  "fillColor": "#554702",
  "strokeColor": "#0b1027",
  "lineWidth": 2,
  "flowDirection": "right",
  "followRoute": false,
  "routeId": "1772517759336.8704",
  "routeSpeed": 40,
  "routeDirection": "right",
  "routeProgress": 0,
  "active": true
}
```

**Campos específicos:**

| Campo | Valores | Descripción |
|---|---|---|
| `moverKind` | `"metro"`, `"hombre"`, `"mujer"` | Tipo de actor visual |
| `flowDirection` | `"right"`, `"left"` | Orientación del sprite |
| `routeId` | string ID | ID del elemento `path` que sigue |
| `routeProgress` | 0.0 – 1.0 | Posición actual en la ruta (0=inicio, 1=fin) |
| `routeSpeed` | número px/s | Velocidad de movimiento |

**Algoritmo de animación del mover:**
```js
// En cada frame del requestAnimationFrame:
function updateMover(mover, deltaTime) {
  const route = elements.find(e => e.id === mover.routeId);
  if (!route || !mover.active) return;
  
  const speed = mover.routeSpeed / 1000; // px/ms
  const totalLength = getPathLength(route.points);
  mover.routeProgress += (speed * deltaTime) / totalLength;
  
  if (mover.routeProgress >= 1) {
    if (mover.routeMode === 'loop') mover.routeProgress = 0;
    else mover.routeProgress = 1;
  }
  
  const pos = getPointAtProgress(route.points, mover.routeProgress);
  mover.x = pos.x;
  mover.y = pos.y;
}
```

---

### 2.8 Tipo: `text`

```json
{
  "type": "text",
  "x": 100,
  "y": 200,
  "text": "Etiqueta",
  "fontSize": 14,
  "fontFamily": "Arial",
  "fillColor": "#ffffff",
  "textAlign": "center"
}
```

**Render:** `ctx.fillText(text, x, y)`

---

### 2.9 Tipo: `line` (línea simple con partículas)

```json
{
  "type": "line",
  "x1": 100,
  "y1": 100,
  "x2": 400,
  "y2": 300,
  "strokeColor": "#48ea79",
  "lineWidth": 2,
  "isAnim": true,
  "speed": 3,
  "active": true
}
```

---

## 3. Sistema de Cámara

La cámara es fundamental. **Todas las coordenadas en el JSON son en "espacio de mundo"**, no en píxeles de pantalla.

```json
"camera": {
  "x": -500,
  "y": -300,
  "zoom": 0.5
}
```

### Transformación mundo → pantalla:
```js
function worldToScreen(worldX, worldY, camera) {
  return {
    screenX: (worldX - camera.x) * camera.zoom,
    screenY: (worldY - camera.y) * camera.zoom
  };
}

// En canvas, antes de dibujar:
ctx.save();
ctx.scale(camera.zoom, camera.zoom);
ctx.translate(-camera.x, -camera.y);
// ... dibujar todos los elementos en coordenadas de mundo ...
ctx.restore();
```

### Transformación pantalla → mundo (para touch):
```js
function screenToWorld(screenX, screenY, camera) {
  return {
    worldX: screenX / camera.zoom + camera.x,
    worldY: screenY / camera.zoom + camera.y
  };
}
```

---

## 4. Orden de Render (Z-order)

Los elementos se dibujan en orden del array `elements[]`. El primero en el array queda debajo, el último encima. Para el Metro CDMX:

1. Imágenes de fondo (tipo `image`)
2. Rutas de metro (tipo `path`)
3. Actores/vagones (tipo `mover`)
4. Etiquetas (tipo `text`)

---

## 5. Opciones para la App Android

### Opción A — WebView (MÁS FÁCIL, recomendada para empezar)

Carga el sistema ya hecho en un WebView. Solo hay que pasar el modo correcto:

```java
// En tu Activity
WebView webView = findViewById(R.id.webview);
WebSettings settings = webView.getSettings();
settings.setJavaScriptEnabled(true);
settings.setDomStorageEnabled(true);

// URL para ver el diagrama sin editor:
String url = "https://flow-diagram-creator.vercel.app/?mode=sticker&id=" + projectId;
webView.loadUrl(url);

// Para fondo transparente:
webView.setBackgroundColor(Color.TRANSPARENT);
webView.setLayerType(WebView.LAYER_TYPE_SOFTWARE, null);
```

**Pros:** Funciona hoy, recibe actualizaciones automáticamente, render idéntico al web.
**Contras:** Requiere internet, no es nativo, el canvas de editor aún aparece (bug del sistema).

### Opción B — Render nativo con Canvas Android (FULL CONTROL)

Descarga el JSON y dibuja tú mismo usando `android.graphics.Canvas`:

```kotlin
// 1. Fetch del JSON
suspend fun fetchProject(id: String): ProjectData {
    val url = "https://flow-diagram-creator.vercel.app/api/project?id=$id"
    val response = httpClient.get(url)
    return json.decodeFromString(response.body())
}

// 2. Render en un SurfaceView o View personalizado
class DiagramView(context: Context) : View(context) {
    var project: ProjectData? = null
    var camera = Camera(x=0f, y=0f, zoom=1f)
    
    override fun onDraw(canvas: Canvas) {
        val p = project ?: return
        
        // Aplicar transformación de cámara
        canvas.save()
        canvas.scale(camera.zoom, camera.zoom)
        canvas.translate(-camera.x, -camera.y)
        
        // Dibujar cada elemento
        for (element in p.elements) {
            when (element.type) {
                "image"  -> drawImage(canvas, element)
                "circle" -> drawCircle(canvas, element)
                "rect"   -> drawRect(canvas, element)
                "path"   -> drawPath(canvas, element)
                "mover"  -> drawMover(canvas, element)
                "text"   -> drawText(canvas, element)
            }
        }
        canvas.restore()
    }
}
```

**Pros:** Funciona offline, rendimiento nativo, control total del render.
**Contras:** Debes implementar TODOS los tipos de elementos.

---

## 6. API Endpoint Reference para Android

### GET proyecto
```
GET https://flow-diagram-creator.vercel.app/api/project?id=<ID>

Response: application/json
Body: { name, date, elements[], camera }
```

### GET biblioteca (lista de proyectos)
```
GET https://flow-diagram-creator.vercel.app/api/library?prefix=<carpeta>/&mode=folded

Response: { keys: ["carpeta/nombre-1", "carpeta/nombre-2", ...] }
```

### GET inyección en vivo (polling)
```
GET https://flow-diagram-creator.vercel.app/api/inject?session=<SESION>

Response: el último proyecto inyectado en esa sesión
```

Para un visualizador en tiempo real, puedes hacer polling cada 2-3 segundos a este endpoint y re-renderizar cuando cambie el `date`.

---

## 7. Colores y Parsing

Los colores vienen como strings CSS estándar:

```js
// Formatos que encontrarás en el JSON:
"transparent"           // sin relleno
"#ffffff"               // hex 6 dígitos
"#fff"                  // hex 3 dígitos
"rgba(255,255,255,0.5)" // rgba
"rgb(255,0,0)"          // rgb
```

En Android, para parsear:
```kotlin
fun parseColor(colorStr: String): Int {
    if (colorStr == "transparent") return Color.TRANSPARENT
    return try {
        Color.parseColor(colorStr)
    } catch (e: Exception) {
        Color.TRANSPARENT
    }
}
```

---

## 8. Modelo de Datos Kotlin (Data Classes)

```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.json.JsonElement

@Serializable
data class ProjectData(
    val name: String = "",
    val date: String = "",
    val elements: List<DiagramElement> = emptyList(),
    val camera: CameraState = CameraState()
)

@Serializable
data class CameraState(
    val x: Float = 0f,
    val y: Float = 0f,
    val zoom: Float = 1f
)

@Serializable
data class Point(val x: Float, val y: Float)

@Serializable
data class DiagramElement(
    val id: String = "",
    val type: String = "",
    val name: String = "",
    
    // Posición y tamaño
    val x: Float = 0f,
    val y: Float = 0f,
    val width: Float = 0f,
    val height: Float = 0f,
    val radius: Float = 0f,
    
    // Estilo
    val strokeColor: String = "transparent",
    val fillColor: String = "transparent",
    val lineWidth: Float = 1f,
    val opacity: Float = 1f,
    
    // Path específico
    val points: List<Point> = emptyList(),
    val closed: Boolean = false,
    val routeArcDegrees: Float = 0f,
    val routeArcSide: String = "left",
    val routeCircular: Boolean = false,
    
    // Image específico
    val imageSrc: String = "",
    val originalWidth: Float = 0f,
    val originalHeight: Float = 0f,
    
    // Mover específico
    val moverKind: String = "",
    val flowDirection: String = "right",
    val routeId: String = "",
    val routeProgress: Float = 0f,
    val routeSpeed: Float = 40f,
    val routeMode: String = "loop",
    
    // Text específico
    val text: String = "",
    val fontSize: Float = 14f,
    val fontFamily: String = "Arial",
    val textAlign: String = "left",
    
    // Line específico
    val x1: Float = 0f,
    val y1: Float = 0f,
    val x2: Float = 0f,
    val y2: Float = 0f,
    val isAnim: Boolean = false,
    val speed: Float = 3f,
    
    // Control
    val active: Boolean = true,
    val locked: Boolean = false,
    val routeRole: Boolean = false,
    val followRoute: Boolean = false,
    val routeDirection: String = "right",
    val connectionStatus: String = "none"
)
```

---

## 9. Algoritmo: Punto en ruta dado progress (0.0 → 1.0)

Este es el algoritmo más crítico para animar los movers:

```kotlin
fun getPointAtProgress(points: List<Point>, progress: Float): Point {
    if (points.isEmpty()) return Point(0f, 0f)
    if (points.size == 1) return points[0]
    
    // 1. Calcular longitud total
    var totalLength = 0f
    val lengths = mutableListOf<Float>()
    for (i in 0 until points.size - 1) {
        val dx = points[i+1].x - points[i].x
        val dy = points[i+1].y - points[i].y
        val segLen = sqrt(dx*dx + dy*dy)
        lengths.add(segLen)
        totalLength += segLen
    }
    
    // 2. Encontrar segmento
    val targetDist = progress.coerceIn(0f, 1f) * totalLength
    var accumulated = 0f
    
    for (i in 0 until points.size - 1) {
        val segLen = lengths[i]
        if (accumulated + segLen >= targetDist) {
            val t = (targetDist - accumulated) / segLen
            return Point(
                x = points[i].x + t * (points[i+1].x - points[i].x),
                y = points[i].y + t * (points[i+1].y - points[i].y)
            )
        }
        accumulated += segLen
    }
    return points.last()
}
```

---

## 10. Acceso Directo al Viewer Embebible

Para integrar en la app como `<iframe>` o WebView **sin el canvas de editor**, usa el modo `sticker`:

```
https://flow-diagram-creator.vercel.app/?mode=sticker&id=<ID>
```

**Parámetros adicionales:**
- `&bg=transparent` — fondo transparente
- `&fit=1` — auto-encuadre al contenido
- `&zoom=0.5` — zoom inicial

**Para un proyecto local (sin publicar):**
```
https://flow-diagram-creator.vercel.app/?project=<URL_DEL_JSON>
```

O con datos embebidos en la URL (para proyectos pequeños):
```
https://flow-diagram-creator.vercel.app/?data=<JSON_URL_ENCODED>
```

---

## 11. Comunicación en Tiempo Real (modo listen)

Para que la app reciba actualizaciones del editor en vivo:

```kotlin
// Polling simple (cada 2 segundos)
CoroutineScope(Dispatchers.IO).launch {
    while (true) {
        val latest = fetchProject("mi-sesion-arkaios")
        withContext(Dispatchers.Main) {
            if (latest.date != currentProject.date) {
                currentProject = latest
                diagramView.project = latest
                diagramView.invalidate()
            }
        }
        delay(2000)
    }
}
```

Para inyectar desde la app hacia el canvas web:
```
POST https://flow-diagram-creator.vercel.app/api/inject?session=<SESION>
Content-Type: application/json
Body: { name, elements[], camera }
```

---

## 12. Resumen: Ruta Recomendada para la APK

### Fase 1 — WebView (1-2 días)
1. Crear Activity con WebView
2. Cargar `?mode=sticker&id=<ID>`
3. Implementar gestos: pinch-to-zoom, pan con 2 dedos
4. Manejar el botón "cargar proyecto" con lista de IDs

### Fase 2 — Render nativo parcial (1-2 semanas)
1. Implementar fetch + parser del JSON
2. Render de `image`, `circle`, `rect` (cubre ~90% de casos visuales)
3. Implementar cámara con pan/zoom táctil

### Fase 3 — Render completo (2-4 semanas)
1. Render de `path` con arcos
2. Animación de `mover` con `routeProgress`
3. Render de `text`
4. Polling de actualizaciones en tiempo real

---

*Generado el 2026-06-01 — Basado en análisis de Flow Diagram Creator v1.4-r1*
