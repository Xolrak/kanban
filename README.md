# Kanban Board

Pequeño proyecto de tablero Kanban con:

- **Frontend**: HTML, CSS y JavaScript.
- **Backend**: PHP con API REST.
- **Base de datos**: MySQL.

## Estructura de carpetas

```text
/kanban-board
  /css
    styles.css
    responsive.css
  /js
    app.js
    kanban.js
    drag-drop.js
    api.js
  /php
    /config
      database.php
    /models
      Task.php
    /controllers
      TaskController.php
    /api
      tasks.php
  /sql
    database.sql
  index.html
  README.md
```

## Instalación

1. Clona o copia este proyecto en tu servidor, por ejemplo:

   ```bash
   C:\xampp\htdocs\kanban-board
   ```

2. Crea la base de datos en MySQL:

   - Abre tu cliente SQL (phpMyAdmin, consola, etc.).
   - Ejecuta el script:

   ```sql
   SOURCE /ruta/al/proyecto/kanban-board/sql/database.sql;
   ```

3. Configura la conexión a la base de datos en:

   - [`php/config/database.php`](php/config/database.php)

   Ajusta usuario y contraseña si es necesario (`$user`, `$pass`).

4. Asegúrate de que tu servidor Apache/PHP esté en marcha.

## Uso

- Abre en el navegador:

  ```text
  http://localhost/kanban-board/index.html
  ```

- La aplicación se conecta a la API:

  ```text
  http://localhost/kanban-board/php/api/tasks.php
  ```

### Funcionalidades

- Crear tareas con descripción, estado y prioridad.
- Ver tareas en columnas por estado:
  - `Some day`
  - `Today`
  - `In progress`
  - `Done`
- Mover tareas:
  - Con los botones izquierda/derecha.
  - Arrastrando y soltando entre columnas (drag & drop).
- Eliminar tareas.

## Endpoints de la API

Base URL:

```text
/php/api/tasks.php
```

### GET

Obtiene todas las tareas.

```bash
curl -X GET http://localhost/kanban-board/php/api/tasks.php
```

### POST

Crea una nueva tarea.

```bash
curl -X POST http://localhost/kanban-board/php/api/tasks.php \
  -H "Content-Type: application/json" \
  -d '{"description":"Nueva tarea","status":"Today","priority":"high"}'
```

### PUT

Actualiza una tarea completa.

```bash
curl -X PUT "http://localhost/kanban-board/php/api/tasks.php?id=1" \
  -H "Content-Type: application/json" \
  -d '{"description":"Tarea actualizada","status":"Done","priority":"medium"}'
```

### PATCH

Actualiza campos específicos.

```bash
curl -X PATCH "http://localhost/kanban-board/php/api/tasks.php?id=1" \
  -H "Content-Type: application/json" \
  -d '{"status":"In progress"}'
```

### DELETE

Elimina una tarea.

```bash
curl -X DELETE "http://localhost/kanban-board/php/api/tasks.php?id=1"
```

## Notas

- Mantiene el código lo más simple posible, sin frameworks.
- Si cambias la ruta del proyecto o el host, recuerda actualizar la constante `API_URL` en [`js/api.js`](js/api.js).