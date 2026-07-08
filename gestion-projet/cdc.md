# CDC — Nexus Messenger Project

## 1. Objective

Create a simple, self-hostable web messaging application that can be used on a homelab.

The application must allow several users to:

* create an account;
* log in;
* send messages in real time;
* see the list of conversations;
* receive new messages without reloading the page.

## 2. Required technical stack

* Backend: Python 3.12+
* Backend framework: FastAPI
* Web hosting: Nginx
* Templates: Jinja2
* Frontend: HTML + vanilla JavaScript
* CSS: Tailwind CSS
* Real time: WebSocket via FastAPI
* Database: SQLite
* Authentication: sessions or JWT
* Tests: pytest
* Deployment: optional Docker Compose

Node.js is allowed only as a build tool for Tailwind CSS.

Node.js must not be used for the application backend.

React, Vue, Angular, Next.js and Electron must not be used for the V1.

## 3. Mandatory features

### Authentication

* Registration with email, username and password.
* Login with email + password.
* Password hashing with bcrypt or argon2.
* Creation of a session or generation of a token.
* Protection of private routes.

### Messaging

* List of the user's conversations.
* Creation of a private conversation between two users.
* Sending text messages.
* Receiving messages in real time via WebSocket.
* Saving messages in the database.
* Message history when loading a conversation.

### Interface

* Login page.
* Registration page.
* Dashboard with conversation list.
* Chat area with messages.
* Message input field.
* Simple, responsive and clean design with Tailwind CSS.

## 4. Features not requested for the V1

Do not implement for now:

* audio/video calls;
* end-to-end encryption;
* attachments;
* groups;
* push notifications;
* mobile application;
* complex friend system.

## 5. Expected data model

### users

* id
* email
* username
* password_hash
* created_at

### conversations

* id
* created_at

### conversation_members

* id
* conversation_id
* user_id

### messages

* id
* conversation_id
* sender_id
* content
* created_at

## 6. Expected API

### Auth

* `POST /api/auth/register`
* `POST /api/auth/login`
* `GET /api/auth/me`
* `POST /api/auth/logout`

### Users

* `GET /api/users/search?query=...`

### Conversations

* `GET /api/conversations`
* `POST /api/conversations`

### Messages

* `GET /api/conversations/:id/messages`
* `POST /api/conversations/:id/messages`

## 7. WebSocket

Expected events:

### Client to server

* `join_conversation`
* `send_message`

### Server to client

* `new_message`
* `message_error`

## 8. Security

* Never store passwords in plain text.
* Never expose secrets in logs.
* Validate user inputs.
* Refuse access to a conversation if the user is not a member.
* Use environment variables for secrets.
* Add a `.env.example`.
* Protect private routes.
* Prevent a user from accessing messages from a conversation they are not a member of.

## 9. Docker

The project may contain:

* a `Dockerfile` for the FastAPI application;
* a `docker-compose.yml`;
* a persistent volume for SQLite;
* clean environment variables.

The project must also be able to run locally without Docker.

## 10. Expected commands

Create the Python environment:

```bash
python -m venv .venv
```

Activate the environment on Linux/macOS:

```bash
source .venv/bin/activate
```

Activate the environment on Windows:

```powershell
.\.venv\Scripts\activate
```

Install Python dependencies:

```bash
pip install -r requirements.txt
```

Run the application:

```bash
uvicorn app.main:app --reload
```

Install Tailwind dependencies:

```bash
npm install
```

Compile Tailwind CSS:

```bash
npm run css:build
```

Tailwind watch mode:

```bash
npm run css:watch
```

Run the tests:

```bash
pytest
```

With Docker Compose, the project must be able to run with:

```bash
docker compose up -d --build
```

The logs must be readable with:

```bash
docker compose logs -f
```

## 10.1 Current project management structure

At the beginning of the project, the repository may only contain the project management files:

```txt
project/
├── AGENTS.md
├── README.md
├── opencode.json
└── gestion-projet/
|    ├── backlog.md
|    ├── cdc.md
|    └── sprints.md
└── .opencode/
```

## 11. Expected final application structure

```txt
project/
├── app/
│   ├── main.py
│   ├── config.py
│   ├── database.py
│   ├── models.py
│   ├── schemas.py
│   ├── routes/
│   │   ├── auth.py
│   │   ├── users.py
│   │   ├── conversations.py
│   │   └── messages.py
│   ├── services/
│   │   ├── auth_service.py
│   │   ├── user_service.py
│   │   ├── conversation_service.py
│   │   └── message_service.py
│   ├── realtime/
│   │   └── websocket_manager.py
│   └── templates/
│       ├── base.html
│       ├── login.html
│       ├── register.html
│       └── chat.html
├── static/
│   ├── src/
│   │   └── input.css
│   ├── dist/
│   │   └── output.css
│   └── app.js
├── data/
├── tests/
├── requirements.txt
├── package.json
├── tailwind.config.js
├── .env.example
├── Dockerfile
├── docker-compose.yml
├── README.md
├── AGENTS.md
└── cdc.md
```

## 12. Acceptance criteria

The project is considered complete if:

* a user can create an account;
* two users can log in;
* user A can create a conversation with user B;
* A can send a message;
* B receives the message without refresh;
* messages remain present after restarting the application;
* messages remain present after restarting the containers if Docker is used;
* the interface uses Tailwind CSS;
* the project starts with Uvicorn;
* the project can be launched with Docker Compose;
* a README explains the installation.

## 13. Constraints for OpenCode

OpenCode must follow these rules:

* Read this file before coding.
* Do not add features outside the V1 without asking.
* Do not use Node.js for the backend.
* Do not use React, Vue, Angular, Next.js or Electron.
* Use Python, FastAPI, SQLite, Jinja2 and Tailwind CSS.
* Node.js is allowed only to compile Tailwind CSS.
* Do not replace the required stack.
* Do not delete existing files without a reason.
* Make simple and logical changes.
* Prefer simple, readable and maintainable code.
* Add comments only when they are useful.
* After each major modification, indicate the modified files.
* Always propose the test or launch commands at the end.

## 14. Recommended work order

1. Create the project structure.
2. Set up the Python environment.
3. Install FastAPI, Uvicorn and the required dependencies.
4. Set up Tailwind CSS.
5. Create the FastAPI backend.
6. Add SQLite and the data models.
7. Add authentication.
8. Add conversations.
9. Add messages.
10. Add the WebSocket.
11. Create the HTML templates with Tailwind.
12. Test the complete user flow.
13. Add Docker Compose if necessary.
14. Write the README.

