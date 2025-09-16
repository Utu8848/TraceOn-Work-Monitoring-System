# TraceOn: Intelligent Activity-Based Screenshot Monitoring

## Overview

TraceOn is a Minimum Viable Product (MVP) for a remote workforce monitoring system designed to enhance accountability while rigorously protecting user privacy. It intelligently captures screenshots based on user activity or at set intervals, employs OCR to filter out sensitive information, and provides managers with a secure web dashboard to view organized screenshots stored on Google Drive.

## Key Features

- **Dual-Component System:** A Python desktop application for employees and a Flask-based web dashboard for managers.
- **Intelligent, Activity-Based Capture:** Takes screenshots every 15 minutes or instantly upon detection of new window/tab activity.
- **Privacy-First Filtering:** Uses Tesseract OCR to detect and discard screenshots containing sensitive keywords (e.g., passwords, PINs).
- **Secure Cloud Storage:** Automatically organizes screenshots in a hierarchical folder structure on Google Drive.
- **Role-Based Access Control:** Managers can only view screenshots of their assigned workers via secure, email-based Google Drive folder sharing.
- **User Authentication:** Secure login and registration for both workers and managers using hashed passwords.

## System Architecture

TraceOn follows a client-server model:

- **Client (Worker Application):** A Python/Tkinter app that handles authentication, activity monitoring, screenshot capture, privacy filtering, and uploads to Google Drive.
- **Server (Manager Dashboard):** A Flask web application that handles manager authentication, provides API endpoints for the client, and serves a web interface to view and manage screenshots.

## Technology Stack

### Client-Side (Worker Application)
- **Language:** Python
- **GUI:** Tkinter
- **Screenshot Capture:** PyAutoGUI
- **Activity Monitoring:** PyGetWindow, Psutil
- **OCR & Privacy Filtering:** Pytesseract (Tesseract OCR)
- **Cloud Integration:** Google Drive API (via custom `drive_utils`)
- **Local Storage:** SQLite
- **Networking:** Requests

### Server-Side (Manager Dashboard)
- **Backend Framework:** Flask
- **Templating:** Jinja2
- **Authentication:** Werkzeug Security
- **Database:** SQLite
- **CORS Handling:** Flask-CORS
- **Cloud Integration:** Google Drive API

## Installation & Setup

### Prerequisites
- Python 3.7+
- Tesseract OCR installed on the system and added to PATH
- Google Cloud Platform project with the Drive API enabled and OAuth 2.0 credentials downloaded (`credentials.json`)

### Steps

1.  **Clone the Repository**
    ```bash
    git clone [your-repo-link]
    cd TraceOn
    ```

2.  **Set Up a Virtual Environment (Recommended)**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install Python Dependencies**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure Google Drive API**
    - Place your downloaded `credentials.json` file in the project's root directory.
    - The first run will trigger an authentication flow, generating a `token.json` file.

5.  **Run the Applications**
    - **Worker Application:** Execute the main Python file (e.g., `python worker_app.py`).
    - **Manager Dashboard:** Run the Flask app (e.g., `python app.py` or `flask run`). Access the dashboard via the provided local URL (typically `http://127.0.0.1:5000`).

## Usage

### For Workers (Desktop App)
1.  Launch the worker application.
2.  Register using your details and a valid **Overseer Code** provided by your manager.
3.  Log in with your credentials.
4.  Click **Start** to begin monitoring. The app will run in the background, capturing screenshots based on activity and intervals.
5.  Click **Stop** to halt monitoring.

### For Managers (Web Dashboard)
1.  Access the TraceOn Manager Dashboard via your web browser.
2.  Register as an Overseer, providing a unique 4-digit Overseer Code.
3.  Log in to your dashboard.
4.  Use the **"View Screenshots"** button to see a list of your registered workers.
5.  Click on a worker to view folders organized by date.
6.  Click on a date folder to see all screenshots from that day. To view a full-size image, you must be logged into the Google Drive account associated with your registration email.

## Future Enhancements

- AI-powered classification of screenshots into productive/non-productive categories.
- Customizable monitoring settings and intervals.
- End-to-end encryption for uploaded screenshots.
- Cross-platform support (macOS, Linux).
- Real-time notification alerts for managers.

## Ethical Considerations

TraceOn is built with a **privacy-by-design** approach. It does not perform constant recording or keystroke logging. The use of OCR filtering and strict, role-based access controls ensures that sensitive information is protected and that monitoring is transparent and accountable.

## License

This project is created for academic purposes as part of a university project.

## Authors

- Anush Neupane
- Bibek Karki
- Nisan Gayak
- Utsav Rai

Faculty of Computing, Engineering and the Built Environment
Birmingham City University
