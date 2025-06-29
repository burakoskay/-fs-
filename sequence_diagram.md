```mermaid
sequenceDiagram
box rgb(255,150,0,0.25) Client Side
    participant browser
        end
box rgb(0,150,150,0.25) Server Side    
    participant server
        end
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes    
    activate server
    server-->>browser: server returns HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    Note right of browser: The HTML document contains a stylesheet so the browser makes a request for it.
    server-->>browser: Server sends the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    Note right of browser: Browser requests main.js
    Note left of server: Server sends main.js
    server-->>browser: *the JavaScript file goes to the browser*
    deactivate server

    rect rgb(255, 0, 0,0.5)
    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server
    end

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{content: "hola", date: "2025-06-29T00:24:22.909Z"},…]
    deactivate server

    rect rgb(255, 0, 0,0.5)
    Note right of browser: The browser executes the callback function that renders the notes
    end
