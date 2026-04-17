# English With Ease (EWE) — EdTech Monorepo & LMS Ecosystem

> **Category:** Enterprise EdTech SaaS / Monorepo  
> **Client:** EWE Academy  
> **Lead Architect:** Sebastian Hernandez ([Elevate Agency](https://your-elevate-link.com))  
> **Project Status:** In Production (v2.0)

---

## 🌎 Languages
Read this in [Spanish](./README-es.md)

---

# 📗 Table of Contents
- [📖 About the Project & Core Philosophy](#about-project)
- [🧠 Architecture: The "Engine vs. Fuel" Model](#architecture)
- [🚀 Key Features & Modules](#key-features)
- [🗄️ Database Schema & Gating Logic](#database-gating)
- [💻 Tech Stack & DevOps](#tech-stack)
- [🧗 Technical Deep-Dive](#technical-deep-dive)
- [🔒 Code Access Policy](#code-access)
- [👥 Authors](#authors)
- [📝 License](#license)

---

## 📖 About the Project & Core Philosophy <a name="about-project"></a>
EWE Academy is a modern, scalable EdTech platform designed to completely automate the language learning lifecycle. Built as a comprehensive **Monorepo**, it houses a highly optimized marketing Landing Page, a dynamic Placement Test Engine, and a custom Learning Management System (LMS) with strict data traceability.

The platform eliminates administrative friction (like manual Google Drive recording syncing) while providing a premium, conversion-optimized experience for prospects.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🧠 Architecture: The "Engine vs. Fuel" Model <a name="architecture"></a>
The core philosophy of this platform is the strict separation of logic and content.
* **The Engine:** The application codebase (LMS architecture, tracking, gating logic, and marketing funnel). It is entirely agnostic to the specific English content.
* **The Fuel:** The pedagogical content (The Syllabus), mapped to immutable IDs and injected dynamically into the database.

### LMS Data Hierarchy (The DNA)
The architecture strictly enforces this hierarchical progression:
1. **Book (Sublevel):** e.g., A1.1, A1.2.
2. **Unit:** 3 units per Book.
3. **Topic (Week):** 1 Conversation Topic per week.
4. **Assets (The Fuel):** Mini-Lessons rendered via dynamic F-Components (F1: Video, F2: Interactive, F3: Audio, F4: Grammar), plus Quizzes and Evidence uploads.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🚀 Key Features & Modules <a name="key-features"></a>
* **Automated Google Workspace Sync:** A background engine that detects Google Meet recordings, updates permissions, and publishes them securely to the student portal without human intervention.
* **Dynamic Placement Test Engine:** A polymorphic testing engine supporting multimedia and various question types. It features an **Early Termination Algorithm** that halts the test automatically if a user fails a specific level block, generating shareable results.
* **Marketing & Lead Generation Funnel:** CRO-optimized landing pages utilizing anchoring pricing strategies. Leads are safely stored in `ewe_marketing_leads` before routing to the test engine to prevent data leakage.
* **Admin Content Manager (In Development):** A collapsible tree-view interface for the academic team to upload "Fuel," set gating rules, and map CSV/Excel syllabus data directly into PostgreSQL.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🗄️ Database Schema & Gating Logic <a name="database-gating"></a>
* **Academic Gating:** Implements Soft/Hard gating. Students must interact with Mini-Lessons (ML1-ML3) to unlock the Weekly Quiz. 
* **Completion Formula:** A Topic reaches 100% completion via a strict mathematical calculation: **40% Mini-Lessons + 30% Quiz (requires >= 70% score) + 30% Evidence**. Tracked efficiently via the `user_topic_progress` pivot table.
* **JSONB Analytics Engine:** The placement test generates granular metrics (correct/total ratios by Section and Level). To prevent database bloat, this payload is processed and stored silently in a powerful `JSONB` column within `ewe_test_results`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 💻 Tech Stack & DevOps <a name="tech-stack"></a>
* **Frontend:** React 19, Vite, Tailwind CSS v4, React Router DOM, Lucide React.
* **Backend:** Node.js, Express.js.
* **Database:** PostgreSQL (Hosted on Neon.tech).
* **Performance:** Node.js automation scripts utilizing `sharp` for external image downloading and WebP conversion.
* **Deployment & DevOps:** * **Frontend (Netlify):** Configured via `netlify.toml` for strict SPA routing and MIME type injection to prevent Vite asset loading errors.
  * **Backend (Railway):** Secure SSL connections to Neon DB forced via `?sslmode=require&uselibpqcompat=true` flags.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🧗 Technical Deep-Dive: The Sync Engine & Auto-Healing <a name="technical-deep-dive"></a>
Alongside the complex 40/30/30 Gating Logic, the most significant backend challenge was the **Google Drive Synchronization Engine**. 

Handling Google API rate limits while moving large video files required building an **Auto-Healing Infrastructure**. The system uses custom error-handling to detect "File Not Found" errors if a directory is manually renamed, triggering a recursive directory rebuild to ensure links are never broken.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🔒 Code Access Policy <a name="code-access"></a>
The source code for this project is **Proprietary**. It is not open for public cloning or contribution.

I am available to perform a **Technical Walkthrough** via screen-share during an interview. During this session, I can demonstrate the Monorepo structure, the "Engine vs. Fuel" mapping logic, and the implementation of the JSONB analytics payload.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 👥 Authors <a name="authors"></a>

👤 **Sebastian Hernandez**
* **Role:** Lead Architect / Full-Stack Engineer
* **Agency:** [Elevate Agency](https://your-elevate-link.com)
* **LinkedIn:** [Sebastian Hernandez](https://www.linkedin.com/in/sebastian-hernandez-munoz/)
* **GitHub:** [@your-github](https://github.com/shm04)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 📝 License <a name="license"></a>
This project is **Proprietary and Closed Source**. All rights reserved by Elevate Agency and EWE Academy.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
