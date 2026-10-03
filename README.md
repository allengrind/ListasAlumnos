# Registro de Inglés — control de grupos

App de una sola página: asistencia, participaciones, conducta, trabajos, calificaciones,
semáforo de dominio y notas por alumno, con exportación a Excel, Word y PDF.
Funciona sin conexión y, si lo configuras, sincroniza con tu propio Firebase.

## Publicar en GitHub Pages

1. Crea un repositorio (puede ser privado; Pages requiere plan de pago si lo quieres privado —
   con repositorio público el código es visible, no tus datos).
2. Sube al repositorio, en la raíz, estos archivos:
   - `index.html`
   - `sw.js`
   - `manifest.webmanifest`
   - `icon-180.png`, `icon-192.png`, `icon-512.png`
   - `firebase-config.json` (con tus valores)
3. En **Settings → Pages**, elige *Deploy from a branch*, rama `main`, carpeta `/ (root)`. Guarda.
4. En un minuto queda en `https://TU-USUARIO.github.io/TU-REPO/`.

## Instalar como app

- **iPad:** abre el enlace en Safari → botón Compartir → *Añadir a pantalla de inicio*.
- **Laptop (Chrome/Edge):** icono de instalar en la barra de direcciones.

Una vez instalada abre sin señal: el service worker guarda la app en el dispositivo.

## Cuentas y sincronización

Cada maestro entra con su correo y solo ve sus propios grupos. Pasos completos en la guía de Firebase.

1. En [console.firebase.google.com](https://console.firebase.google.com) crea un proyecto y una **app web**; copia `firebaseConfig`.
2. **Authentication → Método de acceso:** activa *Correo electrónico/contraseña*.
   Para registro cerrado, da de alta a cada maestro en *Usuarios* y desmarca *Habilitar creación* en *Configuración → Acciones del usuario*.
3. **Firestore Database** en modo producción, con estas reglas:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /usuarios/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

4. Edita `firebase-config.json` con tus valores (o descárgalo desde la app en *Ajustes → Cuenta y sincronización*).
   Publicado ese archivo, nadie pega configuración: solo entran con su correo.

Las claves de `firebaseConfig` no son secretas; la protección son las reglas del paso 3.

## Respaldo en archivo

**Ajustes → Respaldo y traspaso** descarga un `.json` con todo y lo restaura en otro dispositivo.
Úsalo al cerrar cada periodo, aunque tengas la nube activa.

## Editar el diseño

El fuente es `Control de Grupos.dc.html`; `index.html` es la compilación autocontenida.
No edites `index.html` a mano.
