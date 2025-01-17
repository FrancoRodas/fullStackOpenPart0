# fullStackOpenPart0
# ejercicio 0.4
sequenceDiagram
    participant browser
    participant server

    Note right of browser: El usuario completa el formulario y hace clic en "Save"
    browser->>server: POST /new_note
    activate server
    Note left of server: El servidor recibe los datos del formulario<br>{"content": "Nueva nota", "date": "2025-01-02"}
    server-->>browser: Responde con HTTP 302 (Redirección a /notes)
    deactivate server

    Note right of browser: El navegador sigue la redirección a /notes
    browser->>server: GET /notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET /main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    browser->>server: GET /data.json
    activate server
    server-->>browser: [{"content": "Nota existente", "date": "2024-12-31"}, {"content": "Nueva nota", "date": "2025-01-02"}, ...]
    deactivate server

    Note right of browser: El navegador actualiza la lista de notas en la interfaz
    
# ejercicio 0.5
sequenceDiagram
    participant browser
    participant server

    Note right of browser: El usuario completa el formulario y hace clic en "Save"
    browser->>browser: Ejecuta el event handler del formulario
    Note right of browser: El navegador crea la nota<br>{"content": "Nota SPA", "date": "2025-01-02"}<br>La agrega al DOM localmente
    browser->>server: POST /new_note_spa
    activate server
    Note left of server: Recibe la nota como JSON<br>{"content": "Nota SPA", "date": "2025-01-02"}
    server-->>browser: Responde con HTTP 201 Created
    deactivate server

    Note right of browser: El navegador no recarga la página<br>La nueva nota ya está visible en la lista
# ejercicio 0.6
sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Escribe en el formulario y hace clic en "Save"
    Browser->>Browser: Ejecuta el event handler del formulario<br>e.preventDefault()
    Note right of Browser: El navegador crea una nueva nota<br>{"content": "Nueva nota", "date": "2025-01-02"}
    Browser->>Browser: Actualiza el DOM para mostrar la nueva nota
    Browser->>Server: POST /new_note_spa con la nota en formato JSON
    activate Server
    Server-->>Browser: Responde con HTTP 201 Created
    deactivate Server
    Note right of Browser: La página no se recarga<br>La nueva nota ya es visible
