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
3. En **Settings → Pages**, elige *Deploy from a branch*, rama `main`, carpeta `/ (root)`. Guarda.
4. En un minuto queda en `https://TU-USUARIO.github.io/TU-REPO/`.

## Instalar como app

- **iPad:** abre el enlace en Safari → botón Compartir → *Añadir a pantalla de inicio*.
- **Laptop (Chrome/Edge):** icono de instalar en la barra de direcciones.

Una vez instalada abre sin señal: el service worker guarda la app en el dispositivo.

## Sincronización (opcional)

1. En [console.firebase.google.com](https://console.firebase.google.com) crea un proyecto.
2. Agrega una **app web** y copia el objeto `firebaseConfig`.
3. Crea una base **Firestore** en modo producción.
4. En Reglas, pega esto y publica — sustituye el nombre del espacio por el tuyo:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /registros/{espacio} {
      allow read, write: if espacio == 'ingles-primaria-2026-x7k2';
    }
  }
}
```

5. En la app: **Ajustes → Sincronización en la nube**, pega la configuración, escribe el mismo
   nombre de espacio y toca **Conectar**. Activa *Sincronizar sola* para que suba tras cada cambio.

El nombre del espacio es la única llave: quien lo conozca puede leer y escribir esos datos.
Usa uno largo y no lo compartas. Si más adelante entran varios maestros, conviene cambiar a
cuentas con Firebase Authentication.

## Respaldo en archivo

**Ajustes → Respaldo y traspaso** descarga un `.json` con todo y lo restaura en otro dispositivo.
Úsalo al cerrar cada periodo, aunque tengas la nube activa.

## Editar el diseño

El fuente es `Control de Grupos.dc.html`; `index.html` es la compilación autocontenida.
No edites `index.html` a mano.
