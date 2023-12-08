```mermaid
sequenceDiagram
  participant User
  participant Browser
  participant Server


  User->>Browser: Writes note and clicks Save
  activate Browser

  Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
  activate Server
  Server-->>Browser: 201 Created (No redirect)
  deactivate Server

  Browser->>Server: Fetch notes (via SPA JavaScript)
  activate Server
  
  
  Server-->>Browser: Notes as JSON data
  deactivate Server
  Note right of Browser: Browser updates UI without page reload


