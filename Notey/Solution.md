# Blackhat Flagyard CTF Challenge Write-Up: Notey (Web Medium)

During the analysis of a web application for the Blackhat Flagyard CTF, I delved deep into its backend code to uncover how it manages key workflows like registration, login, and note retrieval. My objective was to access critical endpoints and ensure a persistent session to extract sensitive information.

## Methodology:

### 1. Backend Exploration:
- I thoroughly reviewed the backend code to map out how user interactions were processed, with a focus on `/registration`, `/login`, and the note retrieval mechanisms.
- The code revealed that fetching notes required two key components: a `note_id` and a corresponding `note_secret`.

### 2. Capturing Endpoints and Sessions:
- Using Burp Suite, I intercepted HTTP requests during both the registration and login phases. These were `POST` requests, allowing me to register and authenticate users within the app.
- A persistent challenge was session management—sessions would frequently expire, triggering an `Authentication Required` error.

### 3. Automating Session Management with Python:
- To address the session timeout issue, I crafted a Python script to automate login and ensure an active session. The script periodically sent requests to the required endpoints, simulating continuous activity.
- This automation proved invaluable in maintaining session integrity, allowing for uninterrupted interaction with the app.

### 4. Note Retrieval:
- The backend logic hinted that notes could only be accessed via a combination of `note_id` and `note_secret`.
- By making a `GET` request to the `note_id` endpoint and passing the `note_secret` (which, in this case, was the `username`), I began the note extraction process.

### 5. The Flag Hunt:
- As my notes were getting started by id 67 so i tried with id **66**, using the `username` as the `note_secret`.
- On reaching `note_id` **66**, the contents of the note were revealed, and the flag was captured:  
  `BHFlagY{Flag}`.
