```mermaid
sequenceDiagram
  participant User
  participant Browser
  participant Server

  User->>Browser: Writes note and clicks Save
  activate Browser

  Browser->>Browser: Prevent Default Form Submission (e.preventDefault())
  note over Browser: Stops the form from following the usual submission process, which would otherwise trigger a new GET request. This helps maintain an asynchronous flow, ensuring a smoother user experience.

  Browser->>Browser: Create New Note (Extract content, assign timestamp)
  note over Browser: Create a new note object with content from the form and assign a timestamp

  Browser->>Browser: Update Local Data (notes.push(note))
  note over Browser: Add the new note to a local list of notes in-memory, updating the client-side data

  Browser->>Browser: Rerender UI (Display updated notes)
  note over Browser: Dynamically update the user interface locally to visually reflect the newly added note without a page reload

  Browser->>Server: Send Note POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
  activate Server
  note over Server: Initiates an asynchronous request (POST) to send the new note data to the server for processing and storage

  Server->>Server: Process Note (Create new note on the server)
  note over Server: Server processes the incoming request, creates a new note on the server, and handles any server-side logic

  Server-->>Browser: 201 Created (Server response)
  note over Browser,Server: Server responds with a status code 201, indicating successful processing of the request

  Browser-->>Server: Fetch Updated Notes
  note over Browser: Initiates another asynchronous request (GET) to fetch the latest notes from the server

  Server-->>Browser: Updated Notes (JSON data)
  note over Browser,Server: Server responds with the updated notes in JSON format, providing the most current data to the client

  Browser->>Browser: Update UI with Fetched Data
  note over Browser: Update the user interface again based on the newly fetched notes from the server


  deactivate Server
  deactivate Browser
