# 📃 Smart AI Resume Analyzer

An AI-powered career tool that analyzes how well a resume matches a specific job description — instantly, transparently, and with actionable AI coaching, not just a number.

## 🎯 The Problem

Most job seekers apply to dozens of jobs without knowing *why* they aren't getting callbacks. Applicant Tracking Systems (ATS) silently filter out resumes that don't sufficiently match a job description, but candidates almost never get told **what's actually missing** or **how to fix it**.

This hits entry-level and early-career candidates the hardest — for example, a fresh graduate applying for a **Junior Data Analyst** role in Karachi with 0–1 years of experience has no way to know whether their resume clears the bar, which specific skills recruiters are filtering for, or how to phrase their existing experience to match what's actually being asked for.

**Smart AI Resume Analyzer** solves this for job seekers — especially students and early-career candidates in Pakistan's job market — by giving them the same kind of quantitative + qualitative resume feedback a paid career coach or recruiter would normally provide, for free and in seconds.

## 🔗 Live Demo

**[https://smart-ai-resume.streamlit.app/](https://smart-ai-resume.streamlit.app/)**

## 💻 GitHub Repository

**[https://github.com/RimshaKhan2345/Smart_Ai_resume_analyzer](https://github.com/RimshaKhan2345/Smart_Ai_resume_analyzer)**

## ✨ Features

- 📄 **Resume Upload** — Upload a resume as a PDF, parsed and word-counted automatically
- 📋 **Job Description Input** — Paste any job posting to compare the resume against
- ✅ **Weighted Match Score (0–100%)** — Calculated using a custom algorithm:
  - Skills match — 40%
  - Experience relevance — 30%
  - TF-IDF / cosine similarity (text relevance) — 20%
  - Keyword overlap — 10%
- 🎯 **Visual Match Score** — Circular progress indicator with a color-coded score guide:
  - 🟢 70%+ → Excellent match
  - 🟠 50–70% → Moderate match
  - 🔴 Below 50% → Needs improvement
- 🔧 **Skill Gap Analysis** — Side-by-side breakdown of ✅ Matched Skills vs ❌ Missing Skills, extracted from both documents
- 💡 **Personalized Recommendations** — Suggestions tagged by priority (HIGH / MEDIUM / LOW) so users know what to fix first
- 🔍 **Two analysis modes:**
  - **"Analyze with NLP"** — runs the deterministic scoring engine (TF-IDF, cosine similarity, skill/keyword matching)
  - **"Analyze with AI"** — sends the computed results to an AI coach for human-readable, personalized feedback *(see AI Feature below)*
- 👁️ **Preview extracted text** — lets users confirm their PDF was parsed correctly before analyzing
- 🎨 Clean, custom-styled dark-themed UI built with Streamlit + custom CSS

## 🤖 The AI Feature: "Analyze with AI"

Rather than asking an LLM to guess a resume's quality from scratch, this app's AI feature works **on top of** its own deterministic scoring engine. The NLP/algorithmic layer first computes an objective match score, identifies matched vs. missing skills, and generates rule-based recommendations. The **AI layer then takes those specific, already-computed results** and turns them into clear, human-readable coaching — explaining *why* the score is what it is and *what to actually do next*.

This two-layer design means the AI's feedback is always grounded in real, calculated data instead of hallucinated impressions of the resume — the AI explains and coaches, it doesn't re-guess the score.

**What it does:**
1. Takes the computed match score, matched/missing skill lists, and system-generated recommendations as input
2. Explains in plain language why the candidate received that score
3. Highlights the candidate's strongest matching qualifications
4. Gives specific, realistic suggestions for closing each skill gap (e.g., a course, a project idea, or how to reframe existing experience)
5. Ends with an honest, motivating next step — no generic filler

**System prompt used (written for this project):**

```
You are a career coach reviewing a candidate's resume-to-job match.
You will receive a computed match score and skill gap data — this is 
NOT a raw guess, it comes from an actual scoring algorithm. Your job 
is to translate this quantitative analysis into clear, encouraging, 
human-readable advice.

Rules:
- Never contradict the given match score or skill list
- Explain WHY the score is what it is, in plain language
- Point out the candidate's 2 strongest matching qualifications
- For each missing skill, suggest ONE realistic way to close that gap
  (a course, a project idea, or how to reframe existing experience)
- End with a short, honest, motivating next step — no generic fluff
- Keep the response under 250 words

Output in this exact format:
### Why This Score
### Your Strengths
### Closing the Gap
### Next Step
```

**Model used:** OpenAI `gpt-4o-mini` via the Chat Completions API (temperature 0.6–0.7, max ~600–1000 tokens)

## 🛠️ Tools, Services & Models Used

| Category | Tool/Service |
|---|---|
| Language | Python |
| Web framework | Streamlit |
| PDF parsing | PyPDF2 |
| NLP / text processing | NLTK |
| Matching algorithm | scikit-learn (TF-IDF vectorizer, cosine similarity), regex |
| AI model | OpenAI `gpt-4o-mini` (Chat Completions API) |
| Styling | Custom CSS (dark theme) |
| Hosting/Deployment | Streamlit Community Cloud |
| Secrets management | `python-dotenv` (`.env` file, excluded from repo) |

## 📸 Screenshots

> Screenshots below are from the live deployed app.

**1. Home screen — upload resume & paste job description**
![Home screen with upload and job description panels](screenshots/home-screen.png)

**2. NLP Analysis results — match score & skills breakdown**
![Match score circular gauge and matched/missing skills](screenshots/analysis-results.png)

**3. Analyze with AI**
![AI and NLP analysis mode buttons](screenshots/Ai-analysis.png)
## 🚀 How to Run Locally

### Prerequisites
- Python 3.9+
- An OpenAI API key ([get one here](https://platform.openai.com/api-keys))

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/RimshaKhan2345/Smart_Ai_resume_analyzer.git
cd Smart_Ai_resume_analyzer

# 2. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add your OpenAI API key
# Create a file named .env in the project root with:
echo "OPENAI_API_KEY=your_api_key_here" > .env

# 5. Run the app
streamlit run app.py
```

The app will open automatically at `http://localhost:8501`.

### Environment Variables

| Variable | Description |
|---|---|
| `OPENAI_API_KEY` | Your OpenAI API key — required for the "Analyze with AI" feature. Never commit this to the repository; on Streamlit Community Cloud, set it under **Settings → Secrets**. |

## 📁 Project Structure

```
Smart_Ai_resume_analyzer/
├── main.py                  # Main Streamlit application & UI
├── resume.py              # Weighted scoring algorithm (TF-IDF, skills, keywords)               # "Analyze with AI" — OpenAI integration
├── requirements.txt
|___ project.toml
├── screenshots/
└── README.md
```

## 👤 Author

**Rimsha Khan**
[GitHub: RimshaKhan2345](https://github.com/RimshaKhan2345)

---

*Built as a final project — combining a transparent, weighted resume-matching algorithm with an AI coaching layer, so job seekers get explainable, actionable feedback instead of a black-box score.*
