# English With Ease (EWE) — Enterprise LMS

> **Category:** Private EdTech SaaS
> **Client:** EWE Academy  
> **Project Status:** In Production (v1.2)

---

## 🌎 Languages
Read this in [Spanish](./README-es.md)

---

# 📗 Table of Contents
- [📖 About the Project](#about-project)
- [🚀 Key Features](#key-features)
- [🏗️ Architectural Design](#architectural-design)
- [💻 Tech Stack](#tech-stack)
- [🧗 Technical Deep-Dive](#technical-deep-dive)
- [🔒 Intellectual Property & Code Access](#code-access)
- [🔭 Future Features Roadmap](#future-features)
- [👥 Authors](#authors)
- [📝 License](#license)

---

## 📖 About the Project <a name="about-project"></a>
Before the EWE platform, academy operations were fragmented. Instructors lost **5–10 hours per week** on manual administrative tasks: sifting through Google Drive, renaming Google Meet recordings, adjusting sharing permissions, and manually distributing links via WhatsApp. 

EWE is a custom-built Learning Management System (LMS) designed to centralize academic management and eliminate administrative friction through deep automation.

**Key Links:**
* [Live Demo / Website](#) 
* [Video Walkthrough (Loom)](#)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🚀 Key Features <a name="key-features"></a>
* **Automated Google Workspace Sync:** A custom background engine that identifies Google Meet recordings in real-time, moves them to organized directories, updates viewing permissions via API, and publishes them securely.
* **Auto-Healing Infrastructure:** A resilient file-system logic that detects if Google Drive directories are renamed or deleted, automatically re-mapping them to prevent broken links.
* **Multi-Tenant Role Portals:** Tailored environments for Admins, Teachers, and Students.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🏗️ Architectural Design <a name="architectural-design"></a>
The project follows a **Modular Layered Architecture** inspired by **Hexagonal/Clean Architecture** principles.

* **Domain-Driven Modules:** The system is divided into logical domains: `Auth`, `Courses`, `Enrollments`, `Recordings`, and `Dashboard`.
* **Primary Adapters (Driving):** Express.js v5 Controllers handling strictly HTTP concerns.
* **Service Layer (Business Logic):** Pure logic residing in services like `SyncRecordingsService`.
* **Secondary Adapters (Driven):** * **Repository Pattern:** Decoupling PostgreSQL (Neon DB) operations from the business layer.
  * **Infrastructure Adapters:** Dedicated modules for Google Drive API and Google Meet API.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 💻 Tech Stack <a name="tech-stack"></a>
* **Frontend:** React 19, Vite v7, Tailwind CSS v4, Zustand, TanStack Query v5.
* **Backend:** Node.js, Express v5, `node-cron`.
* **Database:** PostgreSQL (Neon DB).
* **Infrastructure:** Google Workspace APIs, Netlify, Railway.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🧗 Technical Deep-Dive: The Sync Engine Challenge <a name="technical-deep-dive"></a>
The most complex engineering challenge was handling Google API rate limits while moving large video files and ensuring 100% uptime for permissions.  

**The Engineering Solution:** 1. Implemented a **Validation State Machine** that checks folder integrity before any sync operation.
2. Developed an **Auto-Healing mechanism** using custom error-handling to detect "File Not Found" errors and trigger a recursive directory rebuild.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🔒 Intellectual Property & Code Access <a name="code-access"></a>
The source code for this project is **Proprietary** to Elevate Agency and EWE Academy. It is not open for public cloning or contribution.

**Reviewing the code:**
I am available to perform a **Technical Walkthrough** via screen-share during an interview. During this session, I can demonstrate the folder structure, the Repository Pattern implementation, and the state management logic.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🔭 Future Features Roadmap <a name="future-features"></a>
- [ ] **Integrated Advanced Test Engine:** Interactive diagnostic assessments (gap-fill, reading comprehensions, live grading) directly on the platform to benchmark student progress.
- [ ] **AI-Powered Analytics:** Tracking student engagement metrics based on video watch time.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 👥 Authors <a name="authors"></a>

👤 **Sebastian Hernandez**
* **Role:** Lead Developer / Architect
* **Agency:** [Elevate Agency](https://your-elevate-link.com)
* **LinkedIn:** [Sebastian Hernandez](https://www.linkedin.com/in/your-profile)
* **GitHub:** [@your-github](https://github.com/your-github)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 📝 License <a name="license"></a>
This project is **Proprietary and Closed Source**. All rights reserved by Elevate Agency and EWE Academy.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
