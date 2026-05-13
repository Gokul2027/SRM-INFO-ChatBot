<div align="center">

<h1>🤖 SRMINFO — College Assistant Chatbot</h1>

<p>
  <strong>An AI-powered chatbot for SRM Institute of Science and Technology, Ramapuram</strong><br/>
  Instant answers about admissions, placements, fees, facilities, and more — right from the browser.
</p>

<p>
  <img src="https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-Neural%20Network-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/Flask-REST%20API-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask"/>
  <img src="https://img.shields.io/badge/NLTK-NLP-76B900?style=for-the-badge" alt="NLTK"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License"/>
</p>

<p>
  <a href="#-demo">Demo</a> •
  <a href="#-features">Features</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#️-setup--installation">Setup</a> •
  <a href="#-how-it-works">How It Works</a> •
  <a href="#-api-reference">API</a> •
  <a href="#-contributing">Contributing</a>
</p>

</div>

---

## 📸 Demo

> The chatbot is served via a static frontend (`frontend/index.html`) connected to a Flask backend. Open the HTML file in your browser after starting the server and ask anything about SRM Ramapuram.

```
User:  "What is the average placement package?"
Bot:   "The average salary package at SRM Ramapuram is 5–7 LPA,
        with a highest package of 47.5 LPA."
```

---

## ✨ Features

SRMINFO can answer real student questions across these domains:

| Domain | What It Covers |
|---|---|
| 🎓 **Admissions** | Process, eligibility (B.Tech / B.Arch), documents, SRMJEEE details |
| 💰 **Fees & Scholarships** | Course fees, Founder's Scholarship, SRM Merit Scholarship |
| 🏢 **Placements** | Recruiting companies (TCS, Infosys, Amazon, Wipro…), avg & highest CTC |
| 📚 **Academics** | UG and PG programmes offered |
| 🏠 **Facilities** | Hostels, library, Wi-Fi, medical, transport, auditoriums |
| 📞 **Contact** | Campus address, phone number, email |
| 🏫 **About SRM** | College history, overview, and significance |

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| **ML / NLP** | Python · PyTorch · NLTK (tokenisation, stemming, bag-of-words) |
| **Backend** | Flask · Flask-CORS |
| **Frontend** | HTML · CSS · Vanilla JavaScript |
| **Training Data** | `intents.json` — intent / pattern / response triples |
| **Model Storage** | `data.pth` — serialised PyTorch weights |

---

## 📁 Project Structure

```
SRM-INFO-ChatBot/
│
├── frontend/           # Chat UI  (HTML + CSS + JS)
│   └── index.html
│
├── app.py              # Flask REST API  →  POST /predict
├── chat.py             # Inference logic — tokenise → vectorise → predict → respond
├── model.py            # Feed-forward neural network (PyTorch)
├── train.py            # Training script — reads intents.json, saves data.pth
├── nltk_utils.py       # NLP helpers — tokenizer, stemmer, bag-of-words builder
│
├── intents.json        # 25 intent definitions (patterns + responses)
├── data.pth            # Pre-trained model weights (ready to use)
│
├── CNAME               # Custom domain config for GitHub Pages
└── README.md
```

---

## ⚙️ Setup & Installation

### Prerequisites

- Python **3.8+**
- `pip`

### 1 — Clone the repository

```bash
git clone https://github.com/Gokul2027/SRM-INFO-ChatBot.git
cd SRM-INFO-ChatBot
```

### 2 — Install dependencies

```bash
pip install flask flask-cors torch nltk
```

### 3 — Download NLTK data (one-time)

```python
import nltk
nltk.download('punkt')
```

### 4 — (Optional) Retrain the model

A pre-trained `data.pth` is already included. Skip this step unless you've modified `intents.json`.

```bash
python train.py
```

The script reads `intents.json`, trains the neural network, and saves the updated weights to `data.pth`.

### 5 — Start the Flask server

```bash
python app.py
```

The API is now live at **`http://127.0.0.1:5000`**.

### 6 — Open the frontend

Open `frontend/index.html` directly in your browser, or serve it with any static file server:

```bash
# Quick option using Python's built-in server
cd frontend
python -m http.server 8080
# Then visit http://localhost:8080
```

---

## 🔍 How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                        User Message                             │
│              "What companies recruit from SRM?"                 │
└───────────────────────────┬─────────────────────────────────────┘
                            │  POST /predict  { "message": "..." }
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  chat.py — NLP Pre-processing (nltk_utils.py)                   │
│  • Tokenise  →  Stem  →  Bag-of-Words vector                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  model.py — Feed-Forward Neural Network (PyTorch)               │
│  • Input layer  →  Hidden layers  →  Softmax output             │
│  • Predicts intent tag  (e.g. "placements_company")             │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  intents.json — Response Lookup                                 │
│  • Match predicted tag  →  Pick a random response               │
└───────────────────────────┬─────────────────────────────────────┘
                            │  { "answer": "Top recruiters include..." }
                            ▼
                       Chat UI renders response
```

---

## 🗂️ Intent Reference

<details>
<summary>Click to expand all 25 intents</summary>

| Tag | Description |
|---|---|
| `greeting` | Hello, Hi, Good morning |
| `admissions_general` | Admission process overview |
| `admissions_entrance` | SRMJEEE and entrance exam details |
| `admissions_eligibility` | General eligibility criteria |
| `admissions_eligibility_btech` | B.Tech-specific eligibility |
| `admissions_eligibility_Barch` | B.Arch-specific eligibility |
| `admissions_documents` | Required documents for admission |
| `admissions_fees` | Course fee information |
| `admissions_status` | How to check application status |
| `application_form` | Link to the online application |
| `scholarships` | Available scholarships and financial aid |
| `placements` | Placement cell overview |
| `placements_company` | Companies that recruit from SRM |
| `placements_pay` | Salary package ranges |
| `placements_highestpay` | Highest package — **47.5 LPA** |
| `placements_averagepay` | Average package — **5–7 LPA** |
| `academics_undergraduate` | UG programmes offered |
| `academics_postgraduate` | PG programmes offered |
| `facilities` | Campus facilities and amenities |
| `hostel` | Hostel details and amenities |
| `contact` | Campus address, phone, email |
| `srm_info` | About SRM Ramapuram |
| `thanks` | Thank you responses |
| `goodbye` | Farewell responses |

</details>

---

## 📡 API Reference

### `POST /predict`

Send a user message and receive a chatbot response.

**Request**

```http
POST http://127.0.0.1:5000/predict
Content-Type: application/json
```

```json
{
  "message": "What is the admission process?"
}
```

**Response**

```json
{
  "answer": "The admission process for SRM Ramapuram requires candidates to meet eligibility criteria..."
}
```

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** the repository
2. **Create** a feature branch
   ```bash
   git checkout -b feature/my-new-intent
   ```
3. **Add** new intents to `intents.json` or improve the model in `model.py`
4. **Retrain** the model
   ```bash
   python train.py
   ```
5. **Commit** your changes and open a **Pull Request**

### Adding a new intent

Open `intents.json` and add an entry following this structure:

```json
{
  "tag": "library_hours",
  "patterns": [
    "What are the library timings?",
    "When does the library open?",
    "Library hours"
  ],
  "responses": [
    "The SRM Ramapuram library is open Monday–Saturday, 8 AM to 8 PM."
  ]
}
```

Then retrain with `python train.py`.

---

## 🗺️ Roadmap

- [ ] Add context-aware multi-turn conversation support
- [ ] Integrate live data (exam schedules, notice board) via scraping
- [ ] Deploy backend to a cloud platform (Render / Railway)
- [ ] Add a typing indicator and timestamps to the chat UI
- [ ] Support voice input via Web Speech API

---

## 👤 Author

**Gokul** — [@Gokul2027](https://github.com/Gokul2027)

> Built for SRM Ramapuram students to get instant, accurate answers about campus life, admissions, and opportunities — without digging through the college website.



<div align="center">
  <sub>⭐ If this project helped you, please consider giving it a star on GitHub!</sub>
</div>
