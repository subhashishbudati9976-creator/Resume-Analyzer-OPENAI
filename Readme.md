# Resume Toolkit — AI Resume Analyzer & Career Roadmap

> **AI-powered resume analysis, interview preparation, career guidance, and application tracking toolkit built with Python, Streamlit, LangChain, RAG, and Generative AI.**

Resume Toolkit is an AI-assisted career platform designed to help users analyze resumes, prepare for interviews, identify skill gaps, build career roadmaps, and organize their job-search workflow in one place.

The project was developed as a hands-on exploration of **Generative AI, LangChain, RAG pipelines, Streamlit application development, API integration, and cloud deployment**.

---

## 🚀 What is Resume Toolkit?

Resume Toolkit brings multiple career-development workflows into a single application.

### Core Modules

- 📄 **Resume Analyzer & Builder**
  - Analyze resume content
  - Extract relevant skills and experience
  - Generate improvement suggestions
  - Assist with resume optimization

- 🎯 **Interview Preparation**
  - Practice technical and behavioral questions
  - Generate structured answers
  - Improve interview responses
  - Prepare explanations for technical concepts

- 🧠 **Skill Roadmap**
  - Identify missing or weak skills
  - Generate learning directions
  - Build a personalized technical roadmap

- 📋 **Application Tracker**
  - Organize job applications
  - Track application progress
  - Maintain a structured job-search workflow

- 💾 **Saved Resumes**
  - Keep previously analyzed resume information
  - Reuse resume data during different workflows

---

## 🧠 AI Architecture

The application combines multiple AI concepts rather than treating the LLM as a simple chatbot.

```text
                    ┌──────────────────────┐
                    │      User Input      │
                    │ Resume / Questions   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Streamlit Frontend │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Application Logic  │
                    │   Python + LangChain │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┼─────────────┐
                 ▼             ▼             ▼
          ┌────────────┐ ┌────────────┐ ┌────────────┐
          │ Resume     │ │ Interview  │ │ Career /   │
          │ Analysis   │ │ Preparation│ │ Skill Path  │
          └─────┬──────┘ └─────┬──────┘ └─────┬──────┘
                │              │              │
                └──────────────┼──────────────┘
                               ▼
                    ┌──────────────────────┐
                    │  LLM / AI Provider   │
                    │ OpenAI / Gemini      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Structured AI Output  │
                    └──────────────────────┘
```

## 🛠️ Technology Stack
Category	Technology
Language	Python
UI Framework	Streamlit
AI Framework	LangChain
AI / LLM	OpenAI / Google Gemini
Retrieval	RAG
Resume Processing	PyPDF2
Configuration	Environment Variables
Version Control	Git & GitHub
Deployment	Streamlit Community Cloud
Development	Local Python Environment


## 📸 Application & Development Journey
This project was not built as a perfect first attempt.
A major part of the development process involved building, deploying, breaking things, identifying the actual cause, fixing the issue, and trying again.
The screenshots below document that process.
1. First Deployment Attempt — Build Failure
The first deployment attempt exposed a problem during the production build.
The deployment successfully installed the required packages, but the build process failed while executing the frontend build command.
npm run build

tsc -b && vite build

Error: Command "npm run build" exited with 126

This was the first indication that the local development environment and the deployment environment were not behaving identically.
<p align="center">
  <img src="./images/Screenshot 2026-09-19 005859.png" alt="Vercel build failure" width="100%">
</p>

What this taught me
A project working locally does not automatically mean the deployment environment will execute it correctly.
The debugging process required checking:
- Build commands
- Dependency installation
- Node.js environment
- Executable permissions
- Production build configuration
- Differences between local and cloud environments
2. GitHub Repository Setup
After working through the initial deployment problems, the project was organized into a dedicated GitHub repository.
The repository contains the application code, dependency configuration, and supporting files required to reproduce the project.
<p align="center">
  <img src="./images/Screenshot 2026-09-19 125026(1).png" alt="Resume Toolkit GitHub repository" width="100%">
</p>

Repository Structure
Resume-Analyzer-Langchain-Workshop-OPENAI/
│
├── app_openai.py
├── commands_openai.txt
├── requirements_openai.txt
└── README.md

The repository provided a stable source of truth for the application and became important for cloud deployment.
3. Deployment Attempt — Repository Connection Issue
The next deployment attempt revealed a different problem.
Streamlit Community Cloud reported that the application was not connected to a remote GitHub repository.
Unable to deploy

The app's code is not connected to a remote GitHub repository.

To deploy on Streamlit Community Cloud,
please put your code in a GitHub repository
and publish the current branch.

<p align="center">
  <img src="./images/Screenshot 2026-09-19 125115.png" alt="Streamlit deployment repository error" width="100%">
</p>

What changed
This was not an application-code failure.
The problem was related to the deployment workflow itself.
The debugging process therefore moved from:
Application Code
       ↓
Build System

to:
Repository
       ↓
GitHub Branch
       ↓
Streamlit Deployment

This highlighted an important distinction between application errors and deployment configuration errors.
4. Runtime Failure — Missing Python Dependency
Once the application reached the Streamlit environment, another issue appeared.
The application failed during startup with:
ModuleNotFoundError

The traceback pointed to:
from PyPDF2 import PdfReader


<p align="center">
  <img src="./images/Screenshot 2026-09-19 125448.png" alt="Streamlit ModuleNotFoundError" width="100%">
</p>

Root Cause
The deployment environment did not have the required Python dependency available.
The local environment had the package installed, but the cloud environment relies on the project's dependency declaration to recreate the environment.
This made the dependency configuration just as important as the application code.
## 🔧 Debugging Process
The development process gradually evolved into a repeatable debugging workflow:
Build
  ↓
Deploy
  ↓
Observe Failure
  ↓
Read Logs
  ↓
Identify Layer
  ↓
Fix Configuration / Code
  ↓
Commit
  ↓
Deploy Again
  ↓
Verify

Instead of treating deployment errors as isolated failures, each error was used to identify which layer of the system needed attention.
## 🧩 Problems Encountered
Problem	Layer	What it revealed
Build exited with code 126	Build / Deployment	Local and cloud build environments can differ
Repository connection failure	Deployment	Cloud deployment depends on correct repository configuration
ModuleNotFoundError	Python Runtime	Dependencies must be explicitly declared
PDF import failure	Application Runtime	External libraries must exist in the deployment environment


## 📚 Key Learning Outcomes
This project became more than an AI application experiment.
It provided practical experience with the complete development cycle:
Generative AI
- Working with LLM APIs
- Prompt-driven application workflows
- AI-generated career guidance
- Structured AI responses
LangChain
- LLM application architecture
- Prompt and chain concepts
- Retrieval-Augmented Generation workflows
- Connecting application logic with AI models
RAG
The project explores the concept of grounding AI responses with relevant contextual information instead of relying entirely on unrestricted model generation.
User Query
    ↓
Retrieve Relevant Context
    ↓
Combine Context + Query
    ↓
LLM
    ↓
Grounded Response

Streamlit
- Rapid Python application development
- Interactive UI components
- Multi-section application navigation
- Cloud deployment
Deployment & Debugging
One of the biggest practical lessons was understanding that:
Writing the application is only one part of building a usable software project.

The project also required dealing with:
- Dependency management
- Build environments
- Repository configuration
- Cloud deployment
- Runtime errors
- Production debugging
- Reading deployment logs
## 📁 Project Files
Resume-Analyzer-Langchain-Workshop-OPENAI/
│
├── app_openai.py
│   └── Main Streamlit application
│
├── commands_openai.txt
│   └── Development / execution commands
│
├── requirements_openai.txt
│   └── Python dependencies
│
└── README.md

## ▶️ Running Locally
1. Clone the repository
git clone <your-repository-url>
cd Resume-Analyzer-Langchain-Workshop-OPENAI

2. Create a virtual environment
Windows
python -m venv .venv
.venv\Scripts\activate

Linux / macOS
python3 -m venv .venv
source .venv/bin/activate

3. Install dependencies
pip install -r requirements_openai.txt

4. Configure API credentials
Set the required AI provider API key as an environment variable.
Do not commit API keys or other secrets to GitHub.
5. Run the application
streamlit run app_openai.py

The application will then be available through the local Streamlit server.
## 🔐 Security
API keys and credentials should be stored using environment variables or the deployment platform's secret-management system.
Never commit:
.env
API keys
Passwords
Private credentials
Service-account secrets

to the repository.
## 🎯 Future Improvements
Potential future improvements include:
- More advanced resume parsing
- Improved RAG pipelines
- Resume-to-job matching
- ATS-oriented analysis
- Job description comparison
- Automated skill-gap detection
- More detailed career roadmaps
- Persistent resume storage
- Authentication
- Application analytics
- Production-grade observability
- Automated testing and CI/CD
## 💡 Final Takeaway
Resume Toolkit represents a practical journey from an AI prototype toward a deployable software application.
The most valuable part of the project was not simply getting an LLM to generate an answer.
It was learning how the complete system behaves when things go wrong:
Idea
 ↓
Prototype
 ↓
AI Integration
 ↓
Application
 ↓
Build
 ↓
Deployment
 ↓
❌ Failure
 ↓
Debug
 ↓
Fix
 ↓
Deploy Again
 ↓
Verify

The errors documented above were part of the development process and helped build a stronger understanding of AI application development, dependency management, GitHub workflows, Streamlit deployment, and production debugging.
## 👨‍💻 Project
Resume Toolkit — AI Resume Analyzer & Career Roadmap
Built as a hands-on project exploring:
Python • Streamlit • LangChain • RAG • Generative AI • Git • GitHub • Cloud Deployment