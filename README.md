# Sentimental-Analyzer

# Smart Feedback Wall — Frontend

A sentiment analysis frontend that lets users type a message and see it classified as Positive, Neutral, or Negative using AI.

---

## How to Run

### Backend (FastAPI + PostgreSQL)

The frontend needs the backend running on `http://localhost:8000`.

**Option 1 — Docker (recommended)**
```bash
# Build the image (first time only)
docker build -t sentimental-backend .

# Run the container
docker run -p 8000:8000 -e database_url="postgresql://user:pass@host/db" sentimental-backend
```

**Option 2 — Local Python**
```bash
# Terminal 1
cd backend

# If you have Python 3.13 or newer:
pip install fastapi uvicorn psycopg psycopg-binary python-dotenv httpx

# If you have Python 3.12 or older:
pip install -r requirements.txt

# Set your database URL in a .env file:
# database_url=postgresql://user:pass@host/db

# Start server
uvicorn main:app --reload --port 8000
```

### Frontend
```bash
# Terminal 2
cd frontend
python -m http.server 5500
```

Open **http://localhost:5500** in your browser.

## How It Works

The page has two sections:

**1. Input Form (top)** : User types a message (up to 500 characters) and clicks "Analyze Sentiment". The frontend sends a POST request to `http://localhost:8000/messages` with the message text.

**2. Feedback Wall (bottom)** : Displays all submitted messages as colored cards. Each card shows the message text, a timestamp, an emoji representing the sentiment (happy/neutral/sad), and a background color that matches the sentiment. The wall loads all messages from the backend on page load via a GET request, and new messages are instantly prepended to the top after submission.

### Sentiment Colors & Emojis

| Sentiment | Background Color | Emoji     |
|-----------|------------------|-----------|
| Positive  | `#7FA19D` (sage) | happy.png |
| Neutral   | `#746D91` (muted purple) | neutral.png |
| Negative  | `#C4A193` (rose) | sad.png   |

---

## File Structure

```
frontend/
├── index.html      # Page layout: header, form, feedback wall
├── style.css       # All styling (form card, wall cards, responsive)
├── script.js       # Form submit handler, fetch calls, card rendering
├── emojis/         # Sentiment emoji images
│   ├── happy.png
│   ├── neutral.png
│   └── sad.png
└── README.md
```

---

## Our Contributions

### Abhay — Input Interface

- Built the input form in `index.html` (textarea, submit button, character counter, labels)
- Wrote the form submission logic in `script.js` (event listener, input validation, character counting, loading state on button, POST request to backend API)
- Styled the form card, textarea, input group, and submit button in `style.css`

### Adithya — Output / Feedback Wall

- Built the feedback wall section in `index.html` (section, container, card structure)
- Wrote the message retrieval and card rendering logic in `script.js` (GET request to load messages, `addCard()` function for creating and appending cards, sentiment-to-color/emoji mapping, error handling when backend is unavailable)
- Styled the wall section, feedback cards, and card layout in `style.css`

---

## What We Learned

We learned how to collaborate on a shared codebase using Git and GitHub, including creating branches, working with pull requests, handling merges, and coordinating changes while working on the same frontend project. We also learned the importance of communication, task division, and brainstorming ideas as a team before implementation. On the technical side, we learned how to connect a static frontend to a FastAPI backend using fetch, handle asynchronous requests with async/await, dynamically create and update DOM elements with JavaScript, and design a responsive, accessible UI with CSS.
