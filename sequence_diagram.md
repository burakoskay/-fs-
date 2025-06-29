```mermaid
sequenceDiagram

box rgb(255,150,0,0.25) Client Side
    participant browser
        end
box rgb(0,150,150,0.25) Server Side    
    participant server
        end
    browser->>server: GET <br> https://studies.cs.helsinki.fi/exampleapp/spa    
    activate server
    server-->>browser: server returns HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    Note right of browser: The HTML document contains a stylesheet so the browser makes a request for it.
    server-->>browser: Server sends the css file
    deactivate server

    browser->>server: GET <br> https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    Note right of browser: Browser requests spa.js
    Note left of server: Server sends spa.js
    server-->>browser: *the JavaScript file goes to the browser*
    deactivate server

    rect rgb(255, 0, 0,0.5)
    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server
    end

    browser->>server: GET <br> https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{content: "hola", date: "2025-06-29T00:24:22.909Z"},…]
    deactivate server

    rect rgb(255, 0, 0,0.5)
    Note right of browser: The browser executes the callback function that renders the notes
    end

    browser->>server: GET <br> https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{content: "efd", date: "2025-06-29T02:19:43.593Z"}, {content: "ok", date: "2025-06-29T02:48:41.455Z"},…]
    deactivate server

    rect rgb(255, 0, 0,0.5)
    Note right of browser: The browser executes the callback function that renders the notes
    end
    
    browser->>server: POST<br>browser submits the form as a new note<br>https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    server->>browser: server returns {message: "note created"} message:"note created" <br>and<br>Payload: {content: "whoa", date: "2025-06-29T18:55:30.354Z"}content:"whoa" date: "2025-06-29T18:55:30.354Z"
    Note right of browser: spa.js renders the new note without the need of refreshing the whole page etc.
