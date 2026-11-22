<div align="center">

# 🥗 NutriBot: AI Nutrition Agent

**An AI-powered nutrition assistant with an Indian dietary focus, built on IBM watsonx.ai**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![IBM watsonx](https://img.shields.io/badge/IBM%20watsonx.ai-052FAD?style=for-the-badge&logo=ibm&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap%205-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📌 Overview

NutriBot is a full-stack web app where users chat with an LLM-powered nutrition agent, analyse meals, generate personalised meal plans, check BMI, and plan nutrition for a whole family. It is tuned for **Indian food and Indian BMI thresholds**, and its behaviour is controlled through a single, editable system prompt.

> ⚠️ **Disclaimer:** NutriBot gives general nutrition guidance, not medical advice. Consult a doctor or registered dietitian for health conditions.

## ✨ Features

| Module | What it does |
|---|---|
| 💬 **Chat** (`/`) | Real-time chat with markdown responses, typing indicator, quick-prompt chips, profile sidebar (BMI, calorie target) |
| 🔬 **Calorie Analyzer** (`/nutrition`) | Describe a meal and get calories, protein, carbs, fat and fibre with animated macro bars; Indian meal presets (Idli-Sambar, Dal-Roti, etc.) |
| 📅 **Meal Planner** (`/meal-plan`) | 7-day plan by goal, diet type, activity level, cuisine and health conditions, with calories per meal |
| ⚖️ **BMI Calculator** (`/bmi`) | Animated gauge, colour-coded scale, Asian (Indian) thresholds, AI-generated advice |
| 👨‍👩‍👧‍👦 **Family Planner** (`/family`) | Profiles for each family member (role, diet, goals, conditions) and one unified family meal plan |

**UI:** dark mode, fully responsive, toast notifications, markdown rendering via marked.js.

## 🧱 Tech Stack

- **Backend:** Python, Flask
- **LLM:** IBM watsonx.ai (`meta-llama/llama-3-3-70b-instruct`) via the `ibm-watsonx-ai` SDK
- **Frontend:** HTML, CSS, JavaScript, Bootstrap 5.3, marked.js
- **Config & deployment:** python-dotenv, Gunicorn

## 🗂️ Project Structure

```
Nutrition-Agent/
├── app.py               # Flask backend and API routes
├── agent.py             # AGENT_INSTRUCTIONS + watsonx.ai integration
├── requirements.txt
├── .env.example         # Environment variable template
├── templates/           # base, index, nutrition, meal_plan, bmi, family
└── static/
    ├── css/style.css
    └── js/              # app, chat, nutrition, mealplan, bmi, family
```

## ⚡ Quick Start

**Prerequisites:** Python 3.10+, an IBM Cloud account with a watsonx.ai project.

```bash
git clone https://github.com/Riddhi375/Nutrition-Agent.git
cd Nutrition-Agent

python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # macOS / Linux

pip install -r requirements.txt
copy .env.example .env         # Windows  (cp .env.example .env on macOS/Linux)
```

Edit `.env`:

```env
IBM_API_KEY=your_ibm_cloud_api_key
WATSONX_PROJECT_ID=your_watsonx_project_id
WATSONX_URL=https://au-syd.ml.cloud.ibm.com
WATSONX_MODEL_ID=meta-llama/llama-3-3-70b-instruct
FLASK_SECRET_KEY=your-random-secret-key
```

Run the app:

```bash
python app.py
```

Open **http://127.0.0.1:5000**

> 🌏 **Important:** `WATSONX_URL` must match the region of your watsonx.ai project (e.g. `us-south` or `au-syd`). A mismatch causes authentication or model-not-found errors. Choose a model that is available in your region.

## 🔑 Getting IBM Cloud Credentials

1. **API key:** [IBM Cloud Console](https://cloud.ibm.com) → Manage → Access (IAM) → API keys → *Create*.
2. **Project ID:** open your project on [watsonx.ai](https://dataplatform.cloud.ibm.com) → Manage → General → Details.

## 🧠 Customising the Agent

All behaviour lives in `AGENT_INSTRUCTIONS` inside `agent.py`: persona, dietary specialisations, Indian food preferences, safety rules, language and response format. Temperature and length are set in `.env` via `AGENT_TEMPERATURE` and `AGENT_MAX_TOKENS`.

## 🔒 Security Notes

- `.env` is git-ignored. Never commit API keys; rotate any key that was ever exposed.
- Keys are read only from environment variables.
- User input is validated before it reaches the model.
- Sessions are HTTP-only, SameSite=Lax and limited to 20 chat turns.

## 🐛 Troubleshooting

| Problem | Fix |
|---|---|
| `IBM_API_KEY is not set` | Copy `.env.example` to `.env` and fill it in |
| `401 Authentication failed` | Check the API key is active and `WATSONX_URL` matches your project's region |
| Model not found / not supported | Pick a model available in your region (see `WATSONX_MODEL_ID`) |
| `429 Rate limit` | Wait a minute or upgrade your IBM Cloud plan |
| Empty chat responses | Set `AGENT_MAX_TOKENS` to 512 or more |
| Port 5000 in use | Set `FLASK_PORT=5001` in `.env` |

## 🚀 Deployment

```bash
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

Set `FLASK_ENV=production`, `FLASK_DEBUG=False` and a strong `FLASK_SECRET_KEY`.

## 🗺️ Roadmap

- [ ] Persistent user profiles with a database
- [ ] Food-image calorie estimation
- [ ] Docker image and cloud deployment
- [ ] Hindi language support

## 👩‍💻 Author

**Riddhi Sharma**: [GitHub](https://github.com/Riddhi375) · [LinkedIn](https://www.linkedin.com/in/riddhi-sharma-076bbb343)

Built during an internship project at Edunet Foundation × AICTE × IBM SkillsBuild.

## 📄 License

MIT License
