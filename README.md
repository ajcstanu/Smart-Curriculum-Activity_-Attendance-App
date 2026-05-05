# 🎓 EduTrack AI — Smart Attendance & Student Productivity System

> An AI-powered web application that automates classroom attendance and guides students toward productive use of free periods through personalized, goal-aligned suggestions.

---

## 📌 Problem Statement

Many educational institutions still depend on manual attendance systems, which are time-consuming and error-prone. Teachers spend a significant portion of class time marking attendance, reducing valuable instructional hours. Students also lack structured guidance during free periods, leading to poor time management and misalignment with long-term academic or career goals.

## 💡 Solution

EduTrack AI integrates automated attendance tracking with an intelligent student productivity planner — all in a single, minimal-infrastructure web application usable by both students and staff with basic training.

---

## ✨ Features

###  Smart Attendance
- Simulated auto-detection via **QR Code**, **Bluetooth/Wi-Fi proximity**, or **Face Recognition**
- Real-time classroom attendance board with present/absent/late status
- One-click manual override for teachers
- Live count display for classroom screen projection

###  Timetable & Schedule
- Daily period-by-period schedule with real-time "current class" indicator
- Free period and break tagging
- Room and faculty information per period

###  Free Period Productivity Suggestions
- Personalized task recommendations based on student interests, strengths, and career goals
- Tasks tagged by type: Study, Skill, Career, Wellness
- Match percentage scoring per suggestion (e.g. "93% match")

###  Goal Tracker
- Semester and long-term goal progress bars
- NEP 2020 alignment tracking (Multidisciplinary Learning, Experiential Learning)
- Academic year milestone breakdown

###  Daily Routine Planner
- Combined timeline of classes, free periods, and personal goals
- Active/done state tracking throughout the day

###  AI Academic Advisor (Claude-powered)
- In-app chat powered by the **Anthropic Claude API**
- Personalized advice on attendance, goals, internships, and study plans
- Context-aware: knows student profile, today's schedule, and long-term goals
- Falls back to curated responses if API is unavailable

###  Student Profile
- Learning style, strengths, and interest tags
- Notification preferences
- Privacy & data policy display (local biometric processing)

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML5, CSS3, JavaScript (ES6+) |
| Fonts | Google Fonts (DM Sans, Space Mono) |
| AI Chat | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Attendance Simulation | JavaScript timers + proximity detection mock |
| Deployment | Any static host (GitHub Pages, Netlify, Vercel) |

> **No build step required.** Open `src/index.html` directly in a browser or serve it from any static file server.

---

## 🚀 Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge, Safari)
- An [Anthropic API key](https://console.anthropic.com/) *(optional — app works without it using fallback responses)*

### Run Locally

```bash
git clone https://github.com/YOUR_USERNAME/edutrack-ai.git
cd edutrack-ai
open src/index.html        # macOS
# or
start src/index.html       # Windows
# or serve with any static server:
npx serve src/
```

### Enable AI Chat (Optional)

The AI Academic Advisor uses the Anthropic Claude API via a browser `fetch` call. To enable it:

1. The app calls `https://api.anthropic.com/v1/messages` from the browser.
2. In production, route this through a backend proxy to keep your API key secure (see [docs/api-proxy-setup.md](docs/api-proxy-setup.md)).
3. For local testing, you can temporarily inject your key — **never commit API keys to Git**.

---

## 📁 Project Structure

```
edutrack-ai/
├── src/
│   └── index.html          # Main application (single-file app)
├── docs/
│   ├── problem-statement.md
│   ├── api-proxy-setup.md
│   └── screenshots/        # Add app screenshots here
├── assets/                 # Icons, images (if any)
├── README.md
└── .gitignore
```

---

## 🎓 Alignment with NEP 2020

EduTrack AI is designed in accordance with India's **National Education Policy 2020** guidelines:

- **Personalized Learning** — suggestions adapt to each student's interests, strengths, and career goals
- **Experiential Learning** — career-oriented tasks like internship applications and portfolio building
- **Multidisciplinary Approach** — goal tracking spans academics, skills, wellness, and career
- **Technology Integration** — AI-powered advisor supports student decision-making

---

## 👥 Stakeholders & Beneficiaries

| Stakeholder | Benefit |
|---|---|
| Students | Productive free periods, goal alignment, attendance awareness |
| Teachers | Faster attendance, more instructional time |
| Administrators | Real-time engagement data, better institutional insights |
| Career Counselors | Student goal data and career readiness tracking |
| Education Departments | NEP 2020 compliance data and analytics |

---

## 🔭 Roadmap / Future Enhancements

- [ ] Backend API (Node.js/Python) for persistent data storage
- [ ] Real QR code generation and scanning via device camera
- [ ] Bluetooth/Wi-Fi proximity detection integration
- [ ] On-device face recognition (TensorFlow.js / MediaPipe)
- [ ] Teacher dashboard with class-level analytics
- [ ] Push notifications for free period nudges
- [ ] Admin portal for timetable management
- [ ] Export attendance reports as PDF/Excel
- [ ] Multi-language support (Hindi, Marathi, etc.)
- [ ] Mobile app (React Native / Flutter)

---

## 🙏 Acknowledgements

- [Anthropic](https://anthropic.com) for the Claude API
- [Google Fonts](https://fonts.google.com) for DM Sans and Space Mono

---

*Built as a solution to the Smart Attendance & Student Productivity problem for Indian educational institutions.*
