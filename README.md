# 🚀 HireSprint - AI-Powered Career & Interview Preparation Platform

HireSprint is a full-stack, microservices-driven AI career platform designed to accelerate candidate preparation through AI mock interviews, intelligent resume generation, ATS scoring, personalized career roadmaps, and automated billing.

---

## 🏗 System Architecture

HireSprint is architected with a decoupled **Microservices Backend** and a high-performance **React + Vite Frontend**:

```
                                  +-------------------+
                                  | React + Vite App  |
                                  |  (Frontend Client)|
                                  +---------+---------+
                                            |
                                            v
                                  +---------+---------+
                                  |    API Gateway    |
                                  |  (Reverse Proxy)  |
                                  +----+----+----+----+
                                       |    |    |    |
        +------------------------------+    |    |    +-----------------------------+
        |                                   |    |                                  |
        v                                   v    v                                  v
+---------------+                   +---------------+                   +-----------------+
| Auth Service  |                   | Resume Service|                   |Interview Service|
| (Firebase/DB) |                   | (ATS & Builder|                   | (LangGraph & AI)|
+-------+-------+                   +-------+-------+                   +--------+--------+
        |                                   |                                    |
        +-----------------+                 |                 +------------------+
                          |                 |                 |
                          v                 v                 v
                    +-----------------------------------------------+
                    |             Redis & MongoDB Layer             |
                    +-----------------------------------------------+
                          ^                 ^                 ^
        +-----------------+                 |                 +------------------+
        |                                   |                                    |
+-------+-------+                   +-------+-------+                            |
|Billing Service|                   |Roadmap Service|                            |
|  (Razorpay)   |                   | (LangGraph/YT)|                            |
+---------------+                   +---------------+----------------------------+
```

---

## ✨ Core Features

### 1. 🤖 AI Mock Interview Engine
- Real-time interactive technical and HR interview rounds powered by **LangGraph** state machine agents.
- **Monaco Code Editor** integration for coding assessments and problem-solving.
- Live conversational AI avatars with voice synthesis and speech recognition.
- In-depth post-interview performance evaluation reports and improvement feedback.

### 2. 📄 AI Resume Builder & ATS Scorer
- Dynamic resume builder with real-time preview and exportable ATS-friendly templates.
- Automated ATS compatibility scoring with semantic keyword matching and actionable suggestions.
- PDF parsing and automated data extraction.

### 3. 🗺️ AI Career Roadmap Generator
- Generates structured, milestone-based learning paths customized to target job roles.
- Curated educational video resources fetched via the **YouTube Data API**.

### 4. 💳 Token Credits & Billing
- Secure payment processing via **Razorpay**.
- Usage-based credit system for running AI interviews and resume evaluations.

---

## 🛠 Tech Stack

### **Frontend**
- **Framework**: React 19, Vite
- **Styling**: Tailwind CSS, Framer Motion
- **State Management**: Redux Toolkit
- **Code Editor**: Monaco Editor (`@monaco-editor/react`)
- **Authentication**: Firebase Authentication
- **Icons & UI**: React Icons, Lucide Icons, Recharts

### **Backend Microservices**
- **Runtime**: Node.js, Express.js (ES Modules)
- **AI / LLM Orchestration**: LangChain, LangGraph, Groq SDK (Llama 3 / Mixtral)
- **Databases**: MongoDB (Mongoose), Redis (ioredis)
- **Payments**: Razorpay Node SDK
- **Containerization**: Docker, Docker Compose

---

## 📁 Repository Structure

```
HireSprint/
├── backend/
│   ├── docker-compose.yml           # Redis infrastructure
│   ├── gateway/                     # API Gateway & route proxy
│   ├── services/
│   │   ├── auth/                    # Authentication & User microservice
│   │   ├── billing/                 # Razorpay & subscription microservice
│   │   ├── interview/               # LangGraph AI mock interview microservice
│   │   ├── resume/                  # AI resume parser & ATS scorer microservice
│   │   └── roadmap/                 # LangGraph AI roadmap microservice
│   └── shared/
│       └── redis/                   # Shared Redis client configuration
└── frontend/
    ├── public/                      # Static assets & brand logos
    └── src/
        ├── apis/                    # API client layer
        ├── assets/                  # Video avatars & visual media
        ├── components/              # Reusable React components
        │   ├── interview/           # Interview session & code editor components
        │   ├── resume/              # Resume builder & template components
        │   └── roadmap/             # Roadmap module cards & visualizers
        ├── pages/                   # Main route pages
        ├── redux/                   # Redux slices & store configuration
        └── utils/                   # Firebase and Axios setup
```

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18+)
- [MongoDB](https://www.mongodb.com/) (local or MongoDB Atlas)
- [Redis](https://redis.io/) (or Docker for Redis)
- [Groq API Key](https://console.groq.com/)
- [Firebase Project](https://firebase.google.com/)
- [Razorpay Account](https://razorpay.com/)

### 1. Clone the Repository
```bash
git clone https://github.com/summar22/HireSprint.git
cd HireSprint
```

### 2. Environment Configuration
Copy the `.env.example` in each service folder to `.env` and fill in the required keys:

```bash
# Backend services
cp backend/gateway/.env.example backend/gateway/.env
cp backend/services/auth/.env.example backend/services/auth/.env
cp backend/services/billing/.env.example backend/services/billing/.env
cp backend/services/interview/.env.example backend/services/interview/.env
cp backend/services/resume/.env.example backend/services/resume/.env
cp backend/services/roadmap/.env.example backend/services/roadmap/.env

# Frontend
cp frontend/.env.example frontend/.env
```

### 3. Start Infrastructure & Services
```bash
# Start Redis
cd backend
docker-compose up -d

# Start backend services (in separate terminals or via process manager)
cd backend/gateway && npm install && npm run dev
cd backend/services/auth && npm install && npm run dev
cd backend/services/billing && npm install && npm run dev
cd backend/services/interview && npm install && npm run dev
cd backend/services/resume && npm install && npm run dev
cd backend/services/roadmap && npm install && npm run dev

# Start frontend client
cd frontend
npm install
npm run dev
```

---

## 📜 License
This project is licensed under the MIT License.
