# Integración de Base de Datos en la Nube (Firebase Firestore)

El objetivo de este plan es habilitar una base de datos real en la nube para que el sistema pueda leer, guardar y compartir los archivos de proyectos `.json` con múltiples usuarios y agentes de IA.

Dado que la creación de la base de datos requiere acceso a tu cuenta de Google, el proceso se divide en dos fases: **una configuración manual que debes hacer tú**, y **la integración del código que haré yo en AMBOS proyectos**.

## 1. Pasos Manuales Requeridos (Tu turno)

> [!IMPORTANT]
> Necesitas realizar estos pasos en tu navegador web para crear la base de datos y obtener las credenciales de conexión.

1. **Ir a la Consola de Firebase:**
   - Entra a [https://console.firebase.google.com/](https://console.firebase.google.com/) e inicia sesión con tu cuenta de Google.
2. **Crear un Proyecto:**
   - Haz clic en **"Agregar proyecto"** (o "Crear proyecto").
   - Ponle un nombre (ej. `Arkaios-Flow-Gallery`).
   - Sigue los pasos y acepta (puedes desactivar Google Analytics por ahora si lo deseas).
3. **Habilitar Firestore Database:**
   - En el menú lateral izquierdo, ve a **Compilación (Build)** > **Firestore Database**.
   - Haz clic en **"Crear base de datos"**.
   - **MUY IMPORTANTE:** Cuando te pregunte por las reglas de seguridad, selecciona **"Comenzar en modo de prueba" (Test mode)**. Esto permitirá que podamos leer y escribir sin configurar autenticación compleja al principio.
   - Selecciona la ubicación más cercana y finaliza.
4. **Registrar tu Aplicación Web:**
   - Ve a la página principal de tu proyecto de Firebase (haciendo clic en el ícono de la casa o en "Descripción general del proyecto").
   - Haz clic en el ícono de **Web (</>)** para agregar una app.
   - Ponle un apodo (ej. `web-app`) y dale a "Registrar app".
5. **Obtener las Credenciales:**
   - Firebase te mostrará un bloque de código con algo llamado `firebaseConfig`. Se ve más o menos así:
     ```javascript
     const firebaseConfig = {
       apiKey: "AIzaSy...",
       authDomain: "tu-proyecto.firebaseapp.com",
       projectId: "tu-proyecto",
       storageBucket: "tu-proyecto.appspot.com",
       messagingSenderId: "123456789",
       appId: "1:123456789:web:abcde"
     };
     ```
   - **Copia ese código de configuración y pégalo aquí en el chat.**

## 2. Cambios Propuestos en el Código (Mi turno)

Una vez que me des el código de configuración, implementaremos la base de datos en los **dos** proyectos:

### A. Integración en el Generador/Editor (`C:\ARKAIOS\flow-diagram-creator-main`)
- Conectar el editor a Firebase.
- Modificar la función de "Guardar" o "Exportar" para que envíe el `.json` generado directamente a una colección de `proyectos` en Firestore en la nube, en lugar de (o además de) descargarlo localmente.

### B. Integración en la Red Social / Galería (`C:\ARKAIOS\stitch_json_flow_social_gallery`)
- Conectar la galería a Firebase usando el mismo `firebaseConfig`.
- Modificar el sistema para que, en lugar de leer archivos locales, consulte Firestore y descargue la lista de proyectos en tiempo real para mostrarlos en el "muro".

### C. Migración Inicial
- Crearemos un script rápido que tome los 19 proyectos de `Demos Validos` que separamos hace un momento, y los suba automáticamente a tu nueva base de datos para que la red social ya tenga contenido.

---

## Preguntas Abiertas

> [!TIP]
> Esperando a que finalices la configuración manual. Pega el `firebaseConfig` cuando estés listo.
