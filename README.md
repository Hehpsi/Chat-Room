# 💬 Real-Time Chat Rooms

A lightweight, real-time group chat application built with **Flask** and **Socket.IO**. Users can create or join private chat rooms using a unique code, send messages instantly, and see who enters or leaves — no accounts or sign-up required.

---

## Features

- **Instant messaging** — Messages are delivered in real time using WebSockets via Flask-SocketIO.
- **Room creation** — Generate a unique 4-character room code with one click.
- **Room joining** — Share your code with others so they can join your room directly.
- **Join/leave notifications** — The room announces when members enter or exit.
- **Message history** — Messages sent before you joined are shown when you enter a room.
- **Auto-cleanup** — Rooms are automatically deleted when the last member leaves.
- **No accounts needed** — Just pick a name and go.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Real-time | Flask-SocketIO |
| Frontend | HTML, CSS, Jinja2 templates |
| Client WebSocket | Socket.IO (CDN) |
| Session management | Flask sessions |

---

## Project Structure

```
project/
├── main.py               # Flask app, routes, and SocketIO event handlers
├── templates/
│   ├── base.html         # Base layout (loads CSS + Socket.IO)
│   ├── home.html         # Landing page — create or join a room
│   └── room.html         # Chat room UI + client-side Socket.IO logic
└── static/
    └── css/
        └── style.css     # App styles
```

---

## Getting Started

### Prerequisites

- Python 3.7+
- pip

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/flaskchat.git
cd flaskchat

# 2. Install dependencies
pip install flask flask-socketio

# 3. Run the app
python main.py
```

The app will start at `http://127.0.0.1:5000` in debug mode.

---

## Usage

1. Open the app in your browser.
2. Enter a **display name**.
3. Either:
   - Click **Create a Room** to generate a new room code, or
   - Paste a **Room Code** and click **Join a Room**.
4. Share your room code with others so they can join.
5. Click **Leave Room** (or close the tab) to exit.

---

## How It Works

- **Rooms** are stored in a server-side Python dictionary (`rooms`), keyed by their 4-character code.
- Each room tracks its active **member count** and a **message history** list.
- When a user connects via Socket.IO, they join a SocketIO room matching their code.
- All messages are broadcast to everyone in the room using `send()` with the `to=room` argument.
- When the last member leaves (via page navigation or disconnect), the room is deleted automatically.

---

## Notes & Limitations

- **In-memory storage only** — Room data and message history are lost when the server restarts. For persistence, integrate a database (e.g. SQLite, PostgreSQL).
- **No authentication** — Any user can join any room if they know the code.
- **Secret key** — The default `SECRET_KEY` in `main.py` should be replaced with a secure random value before deploying to production.

---

## License

MIT — free to use, modify, and distribute.
