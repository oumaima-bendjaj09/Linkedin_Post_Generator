# 📝 LinkedIn Post Generator
****Author:** Oumaima Bendjaj

An AI-powered tool that learns the writing style of past LinkedIn posts and generates new ones on any topic, in **English** or **French**. Built with **LangChain**, **Groq** and **Streamlit**.

## 📌 Overview
![Customer Behavior Dashboard](<Post Generator.JPG>)
Writing consistent LinkedIn content takes time. This app analyzes a set of existing posts, extracts their topics, language and length, then uses them as **few-shot examples** so the LLM writes new posts that match the same tone and style.

**What you can do:**
- Pick a **topic**, a **length** (Short / Medium / Long) and a **language** (English / Français)
- Generate a ready-to-use post in one click
- Download the result as a `.txt` file
- Use your own posts to personalize the style

## ⚙️ How It Works

**Stage 1 – Preprocessing** (`preprocess.py`)
Raw posts from `data/raw_posts.json` are sent to the LLM, which extracts the line count, language and tags of each post. Similar tags are merged into a unified list (e.g. "Job Hunting" and "Jobseekers" become "Job Search"). The result is saved to `data/processed_posts.json`.

**Stage 2 – Generation** (`post_generator.py`)
Given a topic, length and language, the app selects up to two matching past posts as examples, builds a prompt and asks the LLM to write a new post in the same style.

```
Raw posts ──► LLM metadata extraction ──► Processed posts (topic, language, length)
                                                   │
        Topic + Length + Language ──► Few-shot filter ──► Prompt ──► LLM ──► New post
```

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| Language | Python 3.10+ |
| LLM framework | LangChain |
| LLM provider | Groq API (`openai/gpt-oss-120b` by default) |
| Interface | Streamlit |
| Data handling | pandas, JSON |
| Configuration | python-dotenv |



## ▶️ Getting Started

**Prerequisites:** Python 3.10 or higher and a free Groq API key.

**1. Clone the repository**


**2. Create a virtual environment and install dependencies**
```bash
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # Mac / Linux

pip install -r requirements.txt
```

**3. Add your API key**
Create a free key at groq.com, then copy `.env.example` to `.env` and add it:
```
GROQ_API_KEY=your_api_key_here
```

**4. Run the app**
```bash
streamlit run main.py
```
The app opens at `http://localhost:8501`.





