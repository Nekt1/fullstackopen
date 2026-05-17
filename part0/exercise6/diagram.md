```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
    
    Note left of browser: The user enters the note text in the input field and presses on Save
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa {"content":"note content", "date":"currentDate"} 
    activate server
    server-->>browser: 201 Created {"message": "note created"}
    deactivate server 

    Note right of browser:
    The browser immediately after pressing save updates the list of notes and re-renders it without needing to wait for an update from BE