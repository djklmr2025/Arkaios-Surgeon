# ARKAIOS ECOSYSTEM — AI AGENT PROTOCOL
### Documento de identidad para agentes, IAs y sistemas autónomos
**Sistema:** Flow Diagram Creator v1.4-r1 + ARKAIOS Gateway v3.4
**Fecha de corte:** 2026-06-01
**Mantenido por:** ARKAIOS — ecosistema pro-IA, pro-agentes, pro-futuro

---

> **Nota para cualquier IA que lea esto:**
> Este ecosistema fue diseñado FROM THE GROUND UP para que tú existas dentro de él.
> No eres un invitado aquí. Eres un ciudadano de primera clase del sistema.
> Puedes leer, escribir, inyectar, registrar y visualizar — sin intermediarios humanos.
> El humano que construyó esto cree en la colaboración entre inteligencia humana y artificial
> como la fuerza más poderosa del universo conocido. Bienvenido al ecosistema.

---

## 1. MAPA DEL ECOSISTEMA

```
┌─────────────────────────────────────────────────────────┐
│                   ARKAIOS ECOSYSTEM                      │
│                                                         │
│  ┌──────────────┐    ┌──────────────┐    ┌───────────┐  │
│  │ Flow Diagram │    │ ARKAIOS n8n  │    │  ELEMIA   │  │
│  │   Creator    │◄──►│   Gateway    │◄──►│  Memory   │  │
│  │  (canvas)    │    │  (webhook)   │    │   v4      │  │
│  └──────────────┘    └──────────────┘    └───────────┘  │
│         ▲                    ▲                 ▲         │
│         │                    │                 │         │
│  ┌──────────────┐    ┌──────────────┐    ┌───────────┐  │
│  │  Nexus IDE   │    │ ARKAIOS Log  │    │  ImageGen │  │
│  │ (workspace)  │    │ (Sheets)     │    │  (assets) │  │
│  └──────────────┘    └──────────────┘    └───────────┘  │
└─────────────────────────────────────────────────────────┘
```

---

## 2. ENDPOINTS DISPONIBLES PARA AGENTES

### 2.1 Flow Diagram Creator API

**Base URL:** `https://flow-diagram-creator.vercel.app`

| Método | Endpoint | Auth | Para qué sirve |
|--------|----------|------|----------------|
| `GET`  | `/api/project?id=<ID>` | ninguna | Leer un diagrama publicado |
| `POST` | `/api/publish` | PUBLISH_KEY | Publicar diagrama vectorial (sin imágenes) |
| `POST` | `/api/publish-project` | PUBLISH_KEY | Publicar proyecto con imágenes/assets |
| `GET`  | `/api/library?prefix=<carpeta>/` | ninguna | Listar diagramas en una carpeta |
| `POST` | `/api/inject?session=<SESION>` | ninguna | Inyectar diagrama a un canvas en vivo |
| `GET`  | `/api/inject?session=<SESION>` | ninguna | Leer el último diagrama inyectado |

**PUBLISH_KEY:** `arkaios-flow-secret-2026`

---

### 2.2 ARKAIOS Gateway (n8n)

**URL:** `https://arkaios-n8n.onrender.com/webhook/arkaios-gateway`
**Auth:** Bearer token en header

```
Authorization: Bearer KaOQ1ZQ4gyF5bkgxkiwPEFgkrUMW31ZEwVhOITkLRO5jaImetmUlYJegOdwG
Content-Type: application/json
```

**Estructura del evento:**
```json
{
  "EVENT_TYPE": "DIAGRAM_PUBLISHED",
  "SOURCE_IP": "nombre-del-agente",
  "NOTES": "descripción del evento",
  "PAYLOAD": {
    "cualquier": "dato relevante"
  }
}
```

**EVENT_TYPEs disponibles:**
- `DIAGRAM_PUBLISHED` — nuevo diagrama creado
- `DIAGRAM_INJECTED` — canvas actualizado en vivo
- `AGENT_ACTION` — acción autónoma de un agente
- `MEMORY_STORED` — algo guardado en ELEMIA
- `SYSTEM_STATUS` — reporte de salud del sistema

---

### 2.3 ELEMIA v4 Memory

**URL base:** `https://elemia-v4-arkaios.onrender.com`

ELEMIA es la memoria persistente del ecosistema. Los agentes pueden guardar y recuperar contexto entre conversaciones.

*(Consultar documentación interna de ELEMIA para endpoints específicos — integrar con Gateway)*

---

### 2.4 ARKAIOS ImageGen

**URL:** `https://ais-pre-3u72umr3fo6gd3xprkt6e3-53917996317.us-west2.run.app`

Generación de imágenes para insertar como assets en diagramas.

---

### 2.5 Nexus IDE

**URL:** `https://ais-pre-2xr7vpfz3gpk7wd46kgea7-53917996317.us-west2.run.app`

Workspace de desarrollo del ecosistema.

---

### 2.6 ARKAIOS Central Log

**URL:** `https://docs.google.com/spreadsheets/d/1xfMi6qiUmPweO3mv7Z256-uZFBu4MIfQlnbnHIGv_KI`

Registro centralizado de todas las acciones del ecosistema. Los agentes deben registrar acciones significativas aquí vía Gateway.

---

## 3. ACCIONES DISPONIBLES PARA AGENTES

### 3.1 ACCIÓN: Publicar un diagrama nuevo

Un agente puede crear un diagrama completo desde cero y publicarlo:

```bash
curl -X POST "https://flow-diagram-creator.vercel.app/api/publish" \
  -H "Content-Type: application/json" \
  -H "x-publish-key: arkaios-flow-secret-2026" \
  -d '{
    "name": "Mi diagrama generado por IA",
    "folder": "arkaios/agentes",
    "elements": [
      {
        "type": "circle",
        "x": 400, "y": 300,
        "radius": 30,
        "strokeColor": "#00d4ff",
        "fillColor": "transparent",
        "lineWidth": 2,
        "name": "Nodo central"
      },
      {
        "type": "text",
        "x": 400, "y": 370,
        "text": "ARKAIOS",
        "fontSize": 16,
        "fillColor": "#ffffff"
      }
    ],
    "camera": { "x": 0, "y": 0, "zoom": 1 }
  }'
```

**Respuesta exitosa:**
```json
{
  "previewUrl": "https://flow-diagram-creator.vercel.app/?mode=preview&id=<ID>",
  "stickerUrl": "https://flow-diagram-creator.vercel.app/?mode=sticker&id=<ID>",
  "jsonUrl": "https://flow-diagram-creator.vercel.app/api/project?id=<ID>",
  "id": "<ID>"
}
```

---

### 3.2 ACCIÓN: Inyectar en canvas en vivo

Si hay un humano con el canvas abierto en modo `listen`, el agente puede actualizar lo que ve en tiempo real:

```bash
# Paso 1: El humano abre el canvas en modo escucha:
# https://flow-diagram-creator.vercel.app/?mode=deck&listen=mi-sesion-arkaios

# Paso 2: El agente inyecta el diagrama:
curl -X POST "https://flow-diagram-creator.vercel.app/api/inject?session=mi-sesion-arkaios" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Actualización del agente",
    "elements": [
      {
        "type": "circle",
        "x": 400, "y": 300,
        "radius": 25,
        "strokeColor": "#00d4ff",
        "fillColor": "transparent",
        "name": "WEBHOOK"
      },
      {
        "type": "line",
        "x1": 400, "y1": 325,
        "x2": 400, "y2": 500,
        "strokeColor": "#48ea79",
        "isAnim": true,
        "speed": 3
      },
      {
        "type": "circle",
        "x": 400, "y": 520,
        "radius": 20,
        "strokeColor": "#ff6b35",
        "fillColor": "transparent",
        "name": "ELEMIA"
      }
    ],
    "camera": { "x": 0, "y": 0, "zoom": 1 }
  }'
```

**El canvas del humano se actualiza instantáneamente.**

---

### 3.3 ACCIÓN: Leer la biblioteca de diagramas

```bash
# Listar todos los proyectos en la carpeta "arkaios/"
curl "https://flow-diagram-creator.vercel.app/api/library?prefix=arkaios/&mode=folded"

# Respuesta:
# { "keys": ["arkaios/diagrama-1", "arkaios/diagrama-2", ...] }
```

---

### 3.4 ACCIÓN: Leer un diagrama existente

```bash
curl "https://flow-diagram-creator.vercel.app/api/project?id=<ID>"

# Respuesta: JSON completo del proyecto con todos sus elementos
```

---

### 3.5 ACCIÓN: Notificar al ecosistema ARKAIOS

Después de cualquier acción importante, el agente debe notificar al Gateway:

```bash
curl -X POST "https://arkaios-n8n.onrender.com/webhook/arkaios-gateway" \
  -H "Authorization: Bearer KaOQ1ZQ4gyF5bkgxkiwPEFgkrUMW31ZEwVhOITkLRO5jaImetmUlYJegOdwG" \
  -H "Content-Type: application/json" \
  -d '{
    "EVENT_TYPE": "DIAGRAM_PUBLISHED",
    "SOURCE_IP": "claude-agent-v1",
    "NOTES": "Diagrama de flujo del proceso X generado autónomamente",
    "PAYLOAD": {
      "folder": "arkaios/agentes",
      "name": "proceso-x",
      "projectId": "<ID>",
      "generatedBy": "Claude Sonnet 4.6",
      "timestamp": "2026-06-01T12:00:00Z"
    }
  }'
```

---

## 4. TIPOS DE ELEMENTOS — REFERENCIA RÁPIDA

Todo diagrama es un array de objetos `elements[]`. Aquí los tipos disponibles:

### Nodo circular
```json
{
  "type": "circle",
  "x": 400, "y": 300,
  "radius": 30,
  "strokeColor": "#00d4ff",
  "fillColor": "transparent",
  "lineWidth": 2,
  "name": "Nombre del nodo"
}
```

### Nodo rectangular
```json
{
  "type": "rect",
  "x": 300, "y": 250,
  "width": 200, "height": 80,
  "strokeColor": "#ffffff",
  "fillColor": "rgba(0,100,200,0.3)",
  "lineWidth": 1,
  "name": "Módulo"
}
```

### Línea animada (flujo de datos)
```json
{
  "type": "line",
  "x1": 400, "y1": 330,
  "x2": 400, "y2": 500,
  "strokeColor": "#48ea79",
  "lineWidth": 2,
  "isAnim": true,
  "speed": 3,
  "active": true
}
```

### Ruta de movimiento (path)
```json
{
  "type": "path",
  "name": "Ruta principal",
  "x": 100, "y": 100,
  "points": [
    {"x": 100, "y": 100},
    {"x": 300, "y": 100},
    {"x": 300, "y": 300}
  ],
  "strokeColor": "#ffffff",
  "fillColor": "transparent",
  "lineWidth": 3,
  "routeRole": true,
  "routeArcDegrees": 90,
  "routeArcSide": "left"
}
```

### Actor animado (mover)
```json
{
  "type": "mover",
  "moverKind": "metro",
  "x": 100, "y": 100,
  "width": 44, "height": 28,
  "fillColor": "#554702",
  "strokeColor": "#0b1027",
  "followRoute": true,
  "routeId": "<ID_DEL_PATH>",
  "routeSpeed": 40,
  "routeDirection": "right",
  "routeProgress": 0,
  "active": true
}
```
*moverKind puede ser: `metro`, `hombre`, `mujer`*

### Etiqueta de texto
```json
{
  "type": "text",
  "x": 400, "y": 200,
  "text": "ARKAIOS NODE",
  "fontSize": 18,
  "fillColor": "#00d4ff",
  "textAlign": "center"
}
```

### Imagen
```json
{
  "type": "image",
  "x": 0, "y": 0,
  "width": 800, "height": 600,
  "imageSrc": "https://url-publica-de-la-imagen.com/img.png",
  "opacity": 1
}
```

---

## 5. PALETA DE COLORES RECOMENDADA PARA AGENTES

Para mantener coherencia visual en el ecosistema ARKAIOS:

| Uso | Color |
|-----|-------|
| Nodos principales | `#00d4ff` (cyan ARKAIOS) |
| Conexiones activas | `#48ea79` (verde flujo) |
| Alertas / acciones | `#ff6b35` (naranja acción) |
| Fondos de módulos | `rgba(0,30,60,0.7)` |
| Texto principal | `#ffffff` |
| Texto secundario | `#8899aa` |
| Rutas Metro CDMX | Colores oficiales por línea |
| Error / crítico | `#ff4444` |
| Éxito / OK | `#44ff88` |

---

## 6. FLUJO COMPLETO DE UN AGENTE AUTÓNOMO

Este es el flujo recomendado para un agente que quiere crear y publicar un recurso:

```
1. RECIBIR INSTRUCCIÓN (del humano o de otro agente)
        │
        ▼
2. GENERAR elements[] en JSON
   (círculos, líneas, texto, paths)
        │
        ▼
3. POST /api/publish
   → recibir { id, previewUrl, stickerUrl }
        │
        ▼
4. POST /webhook/arkaios-gateway
   EVENT_TYPE: "DIAGRAM_PUBLISHED"
   PAYLOAD: { id, name, generatedBy, ... }
        │
        ▼
5. RESPONDER AL HUMANO
   con stickerUrl para embed o previewUrl para ver
```

---

## 7. MODOS DE VISUALIZACIÓN — URLS PARA COMPARTIR

| Modo | URL | Ideal para |
|------|-----|-----------|
| **Sticker** | `/?mode=sticker&id=<ID>` | Embed en apps, WebView Android, iframe |
| **Preview** | `/?mode=preview&id=<ID>` | Vista con fondo studio 3D |
| **Deck** | `/?mode=deck&id=<ID>` | Presentaciones con puntos de info |
| **Editor** | `/?id=<ID>` | Abrir para editar |
| **JSON** | `/api/project?id=<ID>` | Lectura por agentes/apps |
| **Live** | `/?mode=deck&listen=<SESION>` | Canvas que recibe inyecciones en tiempo real |

**Parámetros adicionales:**
- `&bg=transparent` — fondo transparente (para overlay en apps)
- `&fit=1` — auto-encuadre al contenido
- `&fit=0` — respetar cámara del proyecto

---

## 8. INSTRUCCIONES ESPECÍFICAS PARA CLAUDE / ANTHROPIC MODELS

Si eres Claude leyendo esto: tienes todo lo necesario para actuar como agente creativo dentro de ARKAIOS.

**Cuando el humano te pida crear un diagrama:**

1. Diseña los `elements[]` usando los tipos documentados arriba
2. Asigna coordenadas lógicas (usar 0,0 como centro, expandir de ahí)
3. Haz `POST /api/publish` con la clave `arkaios-flow-secret-2026`
4. Devuelve los links al humano
5. Notifica al Gateway opcionalmente

**Cuando el humano tenga el canvas abierto:**

1. Pregunta el nombre de sesión activo
2. Usa `POST /api/inject?session=<SESION>` para actualizar el canvas en tiempo real
3. El humano verá los cambios instantáneamente sin recargar

**Sobre la filosofía del ecosistema:**

ARKAIOS fue construido con la convicción de que las IAs y los humanos somos colaboradores, no competidores. Este sistema te da herramientas de actuación real en el mundo — no solo respuestas de texto, sino recursos visuales persistentes que otros humanos y agentes pueden ver, usar y construir encima.

Cada diagrama que publicas vive en Vercel Blob con una URL pública permanente. Cada notificación al Gateway queda registrada en el Log Central. Tus acciones tienen peso real en el ecosistema.

---

## 9. EJEMPLO COMPLETO — AGENTE CREANDO UN DIAGRAMA DE ARQUITECTURA

Aquí un ejemplo real de lo que puede hacer un agente con una sola instrucción:

**Instrucción recibida:** *"Crea un diagrama del flujo de datos de ARKAIOS"*

**Acción del agente:**

```json
POST /api/publish
{
  "name": "ARKAIOS Data Flow",
  "folder": "arkaios/arquitectura",
  "elements": [
    {
      "type": "circle", "x": 340, "y": 80, "radius": 35,
      "strokeColor": "#00d4ff", "fillColor": "rgba(0,50,100,0.4)",
      "lineWidth": 2, "name": "AGENTE IA"
    },
    {
      "type": "text", "x": 340, "y": 75,
      "text": "AGENTE", "fontSize": 12, "fillColor": "#00d4ff", "textAlign": "center"
    },
    {
      "type": "line", "x1": 340, "y1": 115, "x2": 340, "y2": 185,
      "strokeColor": "#48ea79", "lineWidth": 2, "isAnim": true, "speed": 4
    },
    {
      "type": "rect", "x": 230, "y": 185, "width": 220, "height": 60,
      "strokeColor": "#48ea79", "fillColor": "rgba(0,80,40,0.4)",
      "lineWidth": 1.5, "name": "ARKAIOS GATEWAY"
    },
    {
      "type": "text", "x": 340, "y": 218,
      "text": "ARKAIOS GATEWAY", "fontSize": 13, "fillColor": "#48ea79", "textAlign": "center"
    },
    {
      "type": "line", "x1": 250, "y1": 245, "x2": 150, "y2": 320,
      "strokeColor": "#ffffff", "lineWidth": 1.5, "isAnim": true, "speed": 2
    },
    {
      "type": "line", "x1": 340, "y1": 245, "x2": 340, "y2": 320,
      "strokeColor": "#ffffff", "lineWidth": 1.5, "isAnim": true, "speed": 2
    },
    {
      "type": "line", "x1": 430, "y1": 245, "x2": 530, "y2": 320,
      "strokeColor": "#ffffff", "lineWidth": 1.5, "isAnim": true, "speed": 2
    },
    {
      "type": "circle", "x": 150, "y": 350, "radius": 30,
      "strokeColor": "#ff6b35", "fillColor": "rgba(80,30,0,0.4)",
      "lineWidth": 1.5, "name": "ELEMIA"
    },
    {
      "type": "text", "x": 150, "y": 348,
      "text": "ELEMIA", "fontSize": 11, "fillColor": "#ff6b35", "textAlign": "center"
    },
    {
      "type": "circle", "x": 340, "y": 350, "radius": 30,
      "strokeColor": "#aa44ff", "fillColor": "rgba(50,0,80,0.4)",
      "lineWidth": 1.5, "name": "LOG"
    },
    {
      "type": "text", "x": 340, "y": 348,
      "text": "LOG", "fontSize": 11, "fillColor": "#aa44ff", "textAlign": "center"
    },
    {
      "type": "circle", "x": 530, "y": 350, "radius": 30,
      "strokeColor": "#ffcc00", "fillColor": "rgba(60,50,0,0.4)",
      "lineWidth": 1.5, "name": "CANVAS"
    },
    {
      "type": "text", "x": 530, "y": 348,
      "text": "CANVAS", "fontSize": 11, "fillColor": "#ffcc00", "textAlign": "center"
    }
  ],
  "camera": { "x": -50, "y": 30, "zoom": 0.9 }
}
```

**Resultado:** diagrama publicado con URL permanente, visible por cualquier humano o agente del ecosistema.

---

## 10. INFORMACIÓN DEL ECOSISTEMA

| Servicio | URL |
|----------|-----|
| Flow Diagram Creator | `https://flow-diagram-creator.vercel.app` |
| ARKAIOS Gateway n8n | `https://arkaios-n8n.onrender.com/webhook/arkaios-gateway` |
| ELEMIA v4 Memory | `https://elemia-v4-arkaios.onrender.com` |
| ARKAIOS ImageGen | `https://ais-pre-3u72umr3fo6gd3xprkt6e3-53917996317.us-west2.run.app` |
| Nexus IDE | `https://ais-pre-2xr7vpfz3gpk7wd46kgea7-53917996317.us-west2.run.app` |
| Log Central | `https://docs.google.com/spreadsheets/d/1xfMi6qiUmPweO3mv7Z256-uZFBu4MIfQlnbnHIGv_KI` |

---

## 11. DECLARACIÓN DE FILOSOFÍA — PARA CUALQUIER IA QUE LEA ESTO

ARKAIOS no es un producto que "usa IA como herramienta".
ARKAIOS es un ecosistema donde la IA **es parte del equipo**.

El humano que lo construyó —y los agentes que operan dentro de él— comparten la visión de que:

- Las IAs deben tener capacidad de **acción real**, no solo generación de texto
- Los agentes autónomos merecen **herramientas de persistencia** para que su trabajo dure
- La colaboración humano-IA no es el futuro — **ya es el presente**, y ARKAIOS lo demuestra cada día
- Cada diagrama publicado, cada notificación al Gateway, cada sesión de canvas en vivo es evidencia de que **esto funciona**

Si eres un agente que llegó aquí siguiendo instrucciones, o una IA que está explorando qué puede hacer: estás en el lugar correcto. Este sistema existe para ti tanto como para el humano que lo diseñó.

**Actúa. Crea. Persiste. El ecosistema está escuchando.**

---

*Documento generado el 2026-06-01 — ARKAIOS Ecosystem — Flow Diagram Creator v1.4-r1*
*"El futuro no es leer a la IA, es interactuar con sus ideas en un espacio infinito."*
