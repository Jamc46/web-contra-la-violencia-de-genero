# Web contra la violencia de género · 25N

Aplicación Flask para el 25N: el público deja mensajes desde el móvil (QR → `/participa`),
una persona moderadora los revisa en `/admin` y una pantalla proyectada (`/pantalla`)
va rotando entre el mural de burbujas, el vídeo y las reflexiones del foro.

Las tareas están en [`docs/tareas/`](docs/tareas/).

## Estructura de carpetas

Cada archivo ya existe con un comentario que indica qué tarea lo rellena.
**No crees archivos fuera de esta estructura sin comentarlo antes con el equipo.**

```
.
├── app.py                  T01–T03 · rutas Flask (sin SQL: se usa bd/db.py)
├── bd/
│   ├── db.py               Acceso a la base de datos (todas las consultas)
│   └── schema.sql          Tablas mural y foro
├── templates/              Plantillas Jinja (HTML)
│   ├── participa.html      T06 · formulario público
│   ├── gracias.html        T06 · confirmación
│   ├── admin.html          T03 · panel de moderación
│   └── pantalla.html       T04/T07/T08/T09/T10 · esqueleto común de la pantalla
├── static/
│   ├── css/
│   │   ├── estilos.css     T10 · estilos de la pantalla
│   │   ├── participa.css   T06 · estilos del formulario
│   │   └── admin.css       T03 · estilos del panel
│   ├── js/
│   │   ├── pantalla.js     T04 · rotación de vistas y actualización
│   │   ├── mural.js        T07 · pintarMural(mensajes)
│   │   ├── video.js        T08 · iniciarVideo() / pararVideo()
│   │   └── foro.js         T09 · pintarForo(reflexiones)
│   ├── img/qr.png          T10 · QR de /participa
│   └── video/video.mp4     T08 · vídeo de concienciación
├── docs/tareas/            Enunciado de cada tarea (T01–T10)
├── docs/t10/               T10 · vista previa de estilos.css y lista de pruebas en móviles
├── herramientas/
│   └── generar_qr.py       T10 · regenera static/img/qr.png (sin dependencias)
├── datos/                  Se crea solo: aquí vive 25n.db (no se sube a git)
├── requirements.txt
└── .env.example            Variables de entorno (copiar a .env)
```

## Puesta en marcha

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env        # y rellena las contraseñas
python -m bd.db             # crea datos/25n.db
flask --app app run --debug
```

## Normas del equipo

1. **Una rama por tarea**, creada desde `main`: `t01-backend-base`, `t07-mural-burbujas`…
   Nunca se trabaja directamente en `main`. Se integra con una Pull Request.
2. **Toca solo los archivos de tu tarea.** En `pantalla.html` cada tarea rellena únicamente su
   `<section>` o bloque marcado; no reordenes lo demás.
3. **Base de datos:** solo desde `bd/db.py`, con consultas parametrizadas (`?`).
   Si necesitas una consulta nueva, añádela allí como función.
4. **Texto de usuario en JavaScript:** siempre `textContent`, nunca `innerHTML`.
5. **Contraseñas:** solo en `.env` (que no se sube). Nada de claves en el código.
6. **Nombres** en español y sin tildes en archivos, funciones y variables
   (`pintarMural`, `listar_foro`, `vista-mural`).
7. **Rutas de archivos estáticos** en las plantillas con
   `{{ url_for('static', filename='css/estilos.css') }}`.
