# 🤖 Automated App Builder API

> **Tools in Data Science Project**: An intelligent API that receives app briefs, generates complete web applications using LLMs, and automatically deploys them to GitHub Pages.

---

## 📋 Overview

This project is part of the **Tools in Data Science** course assignment. It creates an automated system that:

1. **Receives** task requests via REST API
2. **Generates** complete web applications using Google Gemini AI
3. **Deploys** to GitHub repositories with GitHub Pages enabled
4. **Notifies** evaluation servers with deployment details
5. **Updates** existing applications based on new requirements (Round 2+)

### 🎯 Key Features

- ✅ Secret Verification
- ✅ AI-Powered Code Generation
- ✅ Automated Git Operations
- ✅ GitHub Pages Deployment
- ✅ Multi-Round Support
- ✅ Robust Error Handling

---

## 🏗️ Architecture

```
Evaluation Server → POST /ready → FastAPI App
                                      ↓
                    1. Verify Secret
                    2. Generate Code (Gemini AI)
                    3. Create/Update GitHub Repo
                    4. Enable GitHub Pages
                    5. Notify Evaluation Server
                                      ↓
                    GitHub Repo + Pages
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- GitHub Account & Personal Access Token
- Google Gemini API Key
- Student Secret (from course Google Form)

### Installation

1. **Clone this repository:**
   ```bash
   git clone <your-repo-url>
   cd app-builder-api
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables:**
   
   Create a `.env` file (for local testing only):
   ```env
   GEMINI_API_KEY=your_gemini_api_key
   GITHUB_TOKEN=your_github_personal_access_token
   STUDENT_SECRET=your_secret_from_form
   GITHUB_USERNAME=your_github_username
   ```

4. **Run the application:**
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

---

## 📡 API Endpoints

### `POST /ready`

Receives task requests and triggers the app generation pipeline.

**Request Body:**
```json
{
  "email": "student@example.com",
  "secret": "your-secret-key",
  "task": "captcha-solver-abc123",
  "round": 1,
  "nonce": "unique-nonce-value",
  "brief": "Create a captcha solver",
  "checks": ["Repo has MIT license", "README.md is professional"],
  "evaluation_url": "https://example.com/notify",
  "attachments": []
}
```

**Response:**
```json
{
  "status": "ready",
  "message": "Task captcha-solver-abc123 received and processing started."
}
```

### `GET /`

Health check endpoint.

### `GET /status`

Returns the last received task information.

---

## 🔧 Configuration

| Variable | Description | Required |
|----------|-------------|----------|
| `GEMINI_API_KEY` | Google Gemini API key | ✅ Yes |
| `GITHUB_TOKEN` | GitHub Personal Access Token | ✅ Yes |
| `STUDENT_SECRET` | Secret key for verification | ✅ Yes |
| `GITHUB_USERNAME` | Your GitHub username | ✅ Yes |

---

## 📂 Project Structure

```
app-builder-api/
├── main.py              # FastAPI application & core logic
├── models.py            # Pydantic data models
├── config.py            # Settings & configuration
├── requirements.txt     # Python dependencies
├── Dockerfile          # Docker configuration
├── .gitignore          # Git ignore rules
└── README.md           # This file
```

---

## 🐳 Deployment (Hugging Face Spaces)

1. **Create a new Docker Space** on [Hugging Face](https://huggingface.co/spaces)

2. **Add Repository Secrets** in Space Settings:
   - `GEMINI_API_KEY`
   - `GITHUB_TOKEN`
   - `STUDENT_SECRET`
   - `GITHUB_USERNAME`

3. **Push your code:**
   ```bash
   git remote add space https://huggingface.co/spaces/YOUR_USERNAME/SPACE_NAME
   git push space main
   ```

4. **Your API will be live at:** `https://YOUR_USERNAME-SPACE_NAME.hf.space`

---

## 📊 Workflow

### Round 1: Initial App Creation
1. Receive & verify task request
2. Generate app using Gemini AI
3. Create GitHub repository
4. Deploy to GitHub Pages
5. Notify evaluation server

### Round 2+: App Updates
1. Receive & verify update request
2. Clone existing repository
3. Generate updated files
4. Commit and push changes
5. Notify evaluation server

---

## 🛠️ Technologies Used

- FastAPI - Web framework
- Pydantic - Data validation
- Google Gemini - AI code generation
- GitPython - Git operations
- GitHub API - Repository management
- Docker - Containerized deployment

---

## 🐛 Troubleshooting

**"Unauthorized: Secret does not match"**
→ Verify your `STUDENT_SECRET` matches the Google Form submission.

**"GitHub API call failed"**
→ Check your `GITHUB_TOKEN` has `repo` scope enabled.

**"LLM Code Generation Failure"**
→ Verify your `GEMINI_API_KEY` is valid and has quota.

---

## 📖 Course Context

This project is part of the **Tools in Data Science** course evaluation system where students build automated app deployment pipelines and instructors test them with task requests.

---

## 📄 License

MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Student Submission for Tools in Data Science**

- GitHub: [@your-username](https://github.com/your-username)
- Course: Tools in Data Science

---

<div align="center">

**Built for Tools in Data Science**

</div>