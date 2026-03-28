<div align="center">

<br/>

<img src="https://img.shields.io/badge/EduFlow-LMS%20Platform-2563eb?style=for-the-badge&logo=bookstack&logoColor=white" height="36"/>

<br/><br/>

# 📚 EduFlow — Full-Stack Learning Management System

**Learn · Teach · Grow**

<br/>

[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-6.x-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4.x-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![Express](https://img.shields.io/badge/Express-Node.js-000000?style=flat-square&logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://mongodb.com/)
[![Clerk](https://img.shields.io/badge/Clerk-Auth-6C47FF?style=flat-square&logo=clerk&logoColor=white)](https://clerk.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](LICENSE)

<br/>

> A production-ready, full-stack Learning Management System where educators publish rich courses and students discover, enroll, and learn at their own pace — powered by React 19, Express, MongoDB, and Clerk authentication.

<br/>

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [User Flow Diagrams](#-user-flow-diagrams)
- [Data Models](#-data-models)
- [Component Tree](#-component-tree)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [API Reference](#-api-reference)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🔭 Overview

EduFlow is a modern, full-stack learning platform that bridges the gap between educators and learners. Educators can create structured, multi-chapter courses with rich-text descriptions, video lectures, and flexible pricing. Students browse, search, enroll, and track their learning progress — all within a clean, responsive interface.

| Capability | Details |
|---|---|
| 🔐 Authentication | Clerk-powered — Google, GitHub, email sign-in |
| 🎓 Course Creation | Rich-text editor (Quill), dynamic chapters & lectures |
| 💳 Enrollment | Students enroll in courses and track chapter-level progress |
| 📊 Educator Dashboard | Revenue, enrollment stats, and student management |
| 🔍 Search | Real-time course filtering by title |
| ⭐ Ratings | Student rating system per course |
| 🎬 Video Player | Embedded YouTube player with free preview support |
| 📱 Responsive | Mobile-first design across all pages |

---

## 🏛️ Architecture

```
┌──────────────────────────────────────────────────────────────────────────┐
│                           CLIENT  (React + Vite)                          │
│                                                                            │
│  ┌──────────────────────┐    ┌────────────────────────────────────────┐  │
│  │   Student Interface   │    │          Educator Dashboard             │  │
│  │                       │    │                                        │  │
│  │  Home · CourseList    │    │  Dashboard · AddCourse · MyCourses     │  │
│  │  CourseDetail         │    │  StudentEnrolled                       │  │
│  │  MyEnrollments        │    │                                        │  │
│  │  Player               │    │  (Protected — isEducator flag)         │  │
│  └──────────┬────────────┘    └───────────────┬────────────────────────┘  │
│             │                                 │                            │
│  ┌──────────▼─────────────────────────────────▼────────────────────────┐  │
│  │                      AppContext (Global State)                        │  │
│  │   allCourses · myCourses · isEducator · navigate                     │  │
│  │   calculateRating · calCourseDuration · calLecCount                  │  │
│  └──────────────────────────────┬───────────────────────────────────────┘  │
│                                 │                                           │
│  ┌──────────────────────────────▼───────────────────────────────────────┐  │
│  │                    Clerk Provider (Auth Layer)                         │  │
│  │  useUser · useClerk · UserButton — wraps entire app                   │  │
│  └──────────────────────────────┬───────────────────────────────────────┘  │
└─────────────────────────────────┼──────────────────────────────────────────┘
                                  │ HTTP (REST API)
┌─────────────────────────────────▼──────────────────────────────────────────┐
│                         SERVER  (Express + Node.js)                         │
│                                                                              │
│   ┌──────────────────────────────────────────────────────────────────────┐  │
│   │  Express App                                                           │  │
│   │  ├── CORS Middleware                                                   │  │
│   │  ├── JSON Body Parser                                                  │  │
│   │  └── Route Handlers                                                    │  │
│   └──────────────────────────────┬───────────────────────────────────────┘  │
│                                  │                                           │
│   ┌──────────────────────────────▼───────────────────────────────────────┐  │
│   │                     Mongoose ODM Layer                                 │  │
│   │   User Model  ·  Course Model                                          │  │
│   └──────────────────────────────┬───────────────────────────────────────┘  │
└─────────────────────────────────┼──────────────────────────────────────────┘
                                  │
┌─────────────────────────────────▼──────────────────────────────────────────┐
│                           MongoDB Atlas (Cloud DB)                           │
│   Collections:  users  ·  courses                                            │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔄 User Flow Diagrams

### Student Journey

```
                         ┌─────────────────┐
                         │   Visit EduFlow  │
                         └────────┬────────┘
                                  │
                    ┌─────────────▼─────────────┐
                    │  Clerk Sign In / Sign Up    │
                    │  (Google · GitHub · Email)  │
                    └─────────────┬─────────────┘
                                  │
                    ┌─────────────▼─────────────┐
                    │         Home Page           │
                    │  Hero · Companies · Courses │
                    │  Testimonials · CTA         │
                    └──────┬──────────┬──────────┘
                           │          │
              ┌────────────▼──┐   ┌───▼──────────────────┐
              │  Search Bar   │   │  Browse Courses        │
              │  (live filter)│   │  (4 featured cards)    │
              └────────┬──────┘   └───┬──────────────────┘
                       │              │
              ┌────────▼──────────────▼──────────────────┐
              │              Course List Page              │
              │   Full grid · filtered by search param    │
              └──────────────────────┬────────────────────┘
                                     │
              ┌──────────────────────▼────────────────────┐
              │            Course Detail Page              │
              │  ┌────────────────────────────────────┐   │
              │  │  Left Panel        Right Panel      │   │
              │  │  • Title           • Thumbnail /    │   │
              │  │  • Description       YouTube        │   │
              │  │  • Ratings         • Price + disc.  │   │
              │  │  • Chapter list    • Enroll Now     │   │
              │  │  • Accordion view  • What's inside  │   │
              │  └────────────────────────────────────┘   │
              └──────────────────────┬────────────────────┘
                                     │
                          ┌──────────▼──────────┐
                          │   Enroll Now Button  │
                          └──────────┬──────────┘
                                     │
                          ┌──────────▼──────────┐
                          │  My Enrollments Page │
                          │  Progress bars per   │
                          │  course (rc-progress)│
                          └──────────┬──────────┘
                                     │
                          ┌──────────▼──────────┐
                          │    Player Page       │
                          │  YouTube embed       │
                          │  Chapter sidebar     │
                          │  Mark as Complete    │
                          │  Star Rating         │
                          └─────────────────────┘
```

### Educator Journey

```
          ┌───────────────────────────────────────┐
          │  User visits /educator route           │
          └──────────────────┬────────────────────┘
                             │
          ┌──────────────────▼───────────────────┐
          │  isEducator flag check (AppContext)   │
          │  → Sidebar rendered conditionally     │
          └──────┬────────────────────────────────┘
                 │
    ┌────────────┼──────────────────────────────┐
    │            │                              │
    ▼            ▼                              ▼
┌───────┐  ┌────────────┐            ┌──────────────────┐
│Dash-  │  │ Add Course │            │ Student Enrolled  │
│board  │  │            │            │                  │
└───┬───┘  └─────┬──────┘            └────────┬─────────┘
    │             │                            │
    │      ┌──────▼────────────────┐          │
    │      │ Course Builder Form   │          │
    │      │ ─────────────────── - │   ┌──────▼─────────────┐
    │      │ Title                 │   │ Table:              │
    │      │ Description (Quill)   │   │ Student avatar      │
    │      │ Price / Discount %    │   │ Name · Course Title │
    │      │ Thumbnail Upload      │   │ Purchase Date       │
    │      │ Chapters (dynamic)    │   └────────────────────┘
    │      │   └─ Lectures popup   │
    │      │       ├─ Title        │
    │      │       ├─ Duration     │
    │      │       ├─ YouTube URL  │
    │      │       └─ Free preview │
    │      └───────────────────────┘
    │
┌───▼──────────────────────────────────┐
│ Stats Cards                           │
│  ┌───────────┐ ┌────────┐ ┌────────┐ │
│  │ Enrolled  │ │Courses │ │Earning │ │
│  │ Students  │ │        │ │        │ │
│  └───────────┘ └────────┘ └────────┘ │
│ Latest Enrollments Table              │
│  Avatar · Student Name · Course       │
└───────────────────────────────────────┘
```

---

## 🗄️ Data Models

### User Schema

```
┌─────────────────────────────────────────────┐
│                  User                        │
├─────────────────────────────────────────────┤
│  _id            : String  (Clerk userId)    │
│  name           : String  required          │
│  email          : String  required          │
│  imageUrl       : String  required          │
│  enrolledCourses: [ObjectId → Course]       │
│  createdAt      : Date    (timestamps)      │
│  updatedAt      : Date    (timestamps)      │
└─────────────────────────────────────────────┘
```

### Course Schema

```
┌──────────────────────────────────────────────────────┐
│                       Course                          │
├──────────────────────────────────────────────────────┤
│  _id               : ObjectId                        │
│  courseTitle       : String                          │
│  courseDescription : String  (Quill-generated HTML)  │
│  courseThumbnail   : String  (URL)                   │
│  coursePrice       : Number                          │
│  discount          : Number  (0–100 %)               │
│  educator          : String  (Clerk userId)          │
│  enrolledStudents  : [String]  (Clerk userIds)       │
│  courseRatings     : [{ userId: String, rating: N }] │
│  courseContent     : [Chapter]                       │
│  createdAt         : Date                            │
└──────────────────────────────────────────────────────┘

Chapter {
  chapterId      : String  (uniqid)
  chapterTitle   : String
  chapterOrder   : Number
  chapterContent : [Lecture]
}

Lecture {
  lectureId      : String  (uniqid)
  lectureTitle   : String
  lectureDuration: Number  (minutes)
  lectureUrl     : String  (YouTube URL)
  isPreviewFree  : Boolean
  lectureOrder   : Number
}
```

### Entity Relationship Diagram

```
          ┌──────────┐                   ┌──────────────┐
          │   User    │──── enrolls in ──▶│    Course     │
          │          │                   │              │
          │  _id     │◀──── creates ──── │  educator    │
          │  name    │                   │  courseTitle │
          │  email   │                   │  courseConten│
          └──────────┘                   └──────┬───────┘
                                                │ contains
                                         ┌──────▼───────┐
                                         │   Chapter    │
                                         └──────┬───────┘
                                                │ contains
                                         ┌──────▼───────┐
                                         │   Lecture    │
                                         └──────────────┘
```

---

## 🧩 Component Tree

```
App.jsx
│
├── Navbar (student)                  ← hidden on /educator routes
│   ├── Logo (click → Home)
│   ├── Become Educator / Dashboard link
│   ├── My Enrollments link
│   └── Clerk UserButton / Sign In button
│
└── Routes
    ├── / → Home
    │   ├── Hero
    │   │   └── SearchBar
    │   ├── Companies
    │   ├── CourseSection
    │   │   └── CourseCard (×4)
    │   ├── TestimonialSection
    │   ├── CalltoAction
    │   └── Footer (student)
    │
    ├── /courseList/:input? → CourseList
    │   ├── SearchBar (pre-filled)
    │   └── CourseCard (×n, filtered)
    │
    ├── /course/:id → CourseDetail
    │   ├── Chapter Accordion
    │   │   └── Lecture items w/ Preview button
    │   ├── YouTube (free preview embed)
    │   ├── Enroll Now button
    │   └── Footer
    │
    ├── /my-enrollments → MyEnrollment
    │   ├── Enrollment table
    │   │   └── rc-progress Line per course
    │   └── Footer
    │
    ├── /player/:id → Player
    │   ├── Chapter Sidebar (accordion)
    │   ├── YouTube Embed
    │   ├── Rating (interactive stars)
    │   └── Footer
    │
    └── /educator/* → Educator (layout wrapper)
        ├── Navbar (educator)
        ├── Sidebar (NavLink items)
        └── <Outlet>
            ├── /educator → Dashboard
            │   ├── Stats Cards ×3
            │   └── Latest Enrollments table
            ├── /educator/add-course → AddCourse
            │   ├── Quill Rich-Text Editor
            │   ├── Chapter Manager (add/remove/toggle)
            │   │   └── Lecture Popup Modal
            │   └── Thumbnail Upload
            ├── /educator/my-course → MyCourse
            │   └── Course table (earnings · students · date)
            └── /educator/student-enrolled → StudentEnrolled
                └── Student table (avatar · name · course · date)
```

---

## 🚀 Features

### 👩‍🎓 Student Features

| Feature | Description |
|---|---|
| 🔐 Auth | Clerk sign-in — Google, GitHub, or email; persistent sessions |
| 🏠 Home Feed | Hero, trusted companies banner, top 4 courses, testimonials |
| 🔍 Search | URL-based real-time search — `/courseList/:query` |
| 📖 Course Detail | Full description, chapter accordion, YouTube previews, pricing |
| ⭐ Ratings | Star rating display + interactive widget for enrolled students |
| 🎓 My Enrollments | Table of enrolled courses with live progress bars per chapter |
| 🎬 Video Player | YouTube embed, chapter-by-chapter nav, mark-as-complete |
| 📱 Responsive | Fully responsive across mobile, tablet, and desktop |

### 👨‍🏫 Educator Features

| Feature | Description |
|---|---|
| 🖊️ Rich Course Creation | Quill HTML editor for detailed, formatted course descriptions |
| 🗂️ Dynamic Chapters | Add/remove/collapse chapters with real-time preview |
| 🎥 Lecture Management | Per-lecture: title, duration, YouTube URL, free preview toggle |
| 🖼️ Thumbnail Upload | File upload with live preview before submission |
| 💰 Pricing & Discounts | Set course price and percentage discount (0–100%) |
| 📊 Dashboard | Enrollment count, course count, and total earnings at a glance |
| 📋 Student Roster | Full table of enrolled students with course and purchase date |
| 🏷️ My Courses | Per-course breakdown: earnings, student count, publish date |

---

## 🏗️ Tech Stack

```
┌────────────────────────────────────────────────────────────────────┐
│  FRONTEND                           BACKEND                         │
│  ──────────────────────             ─────────────────────────       │
│  React 19           ← UI            Express.js    ← REST server     │
│  React Router DOM   ← routing       Node.js       ← runtime         │
│  Tailwind CSS 4     ← styling       Mongoose      ← ODM             │
│  Vite 6             ← build tool    MongoDB Atlas ← cloud database  │
│  Quill              ← rich text     dotenv        ← env config      │
│  Clerk              ← auth          CORS          ← middleware       │
│  react-youtube      ← video player                                   │
│  rc-progress        ← progress bars                                  │
│  humanize-duration  ← time formats                                   │
│  uniqid             ← client IDs                                     │
└────────────────────────────────────────────────────────────────────┘
```

---

## 📂 Project Structure

```
eduflow/
│
├── 📁 client/                          # React frontend (Vite)
│   ├── index.html
│   ├── vite.config.js                  # Vite + Tailwind + React plugins
│   ├── package.json
│   │
│   └── src/
│       ├── main.jsx                    # Entry — ClerkProvider + BrowserRouter
│       ├── App.jsx                     # Route definitions + layout logic
│       ├── App.css                     # Global styles, Quill theme, Outfit font
│       │
│       ├── 📁 context/
│       │   └── AppContext.jsx          # Global state + course helper functions
│       │
│       ├── 📁 assets/
│       │   └── assets.js              # Icons, dummy data exports
│       │
│       ├── 📁 components/
│       │   ├── 📁 student/
│       │   │   ├── Navbar.jsx          # Responsive nav + Clerk auth buttons
│       │   │   ├── Hero.jsx            # Landing hero section + SearchBar
│       │   │   ├── SearchBar.jsx       # Controlled input → navigate
│       │   │   ├── CourseCard.jsx      # Course thumbnail card with rating
│       │   │   ├── CourseSection.jsx   # Featured 4-course grid
│       │   │   ├── Companies.jsx       # Trusted logos banner
│       │   │   ├── TestimonialSection.jsx
│       │   │   ├── CalltoAction.jsx
│       │   │   ├── Rating.jsx          # Interactive 5-star rating widget
│       │   │   ├── Loading.jsx         # Animated Atom spinner
│       │   │   └── Footer.jsx          # Dark footer + newsletter form
│       │   │
│       │   └── 📁 educator/
│       │       ├── Navbar.jsx          # Educator greeting navbar
│       │       ├── Sidebar.jsx         # NavLink sidebar with active states
│       │       └── Footer.jsx          # Compact footer with logo
│       │
│       └── 📁 pages/
│           ├── 📁 student/
│           │   ├── Home.jsx            # Landing page assembly
│           │   ├── CourseList.jsx      # Filterable course grid
│           │   ├── CourseDetail.jsx    # Full course page + enrollment
│           │   ├── MyEnrollement.jsx   # Progress tracking table
│           │   └── Player.jsx          # Video player + chapter sidebar
│           │
│           └── 📁 educator/
│               ├── Educator.jsx        # Layout shell (Navbar + Sidebar + Outlet)
│               ├── Dashboard.jsx       # Stats cards + enrollment table
│               ├── AddCourse.jsx       # Full course builder with Quill
│               ├── MyCourse.jsx        # Educator course management table
│               └── StudentEnrolled.jsx # All students enrollment table
│
└── 📁 server/                          # Express backend
    ├── server.js                       # App init, middleware, port listener
    ├── 📁 configs/
    │   └── mongo.js                    # Mongoose connection setup
    └── 📁 models/
        ├── user.js                     # User Mongoose schema
        └── course.js                   # Course Mongoose schema (in progress)
```

---

## ⚙️ Getting Started

### Prerequisites

- Node.js `>= 18.x`
- npm or yarn
- [MongoDB Atlas](https://www.mongodb.com/atlas) account (free tier)
- [Clerk](https://clerk.com/) account (free tier)

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/eduflow-lms.git
cd eduflow-lms
```

### 2. Setup the Client

```bash
cd client
npm install
```

### 3. Setup the Server

```bash
cd ../server
npm install
```

### 4. Configure Environment Variables

**`client/.env.local`**
```env
VITE_CLERK_PUBLISHABLE_KEY=pk_test_your_clerk_publishable_key
VITE_BACKEND_URL=http://localhost:5000
```

**`server/.env`**
```env
MONGODB_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/eduflow
PORT=5000
CLERK_SECRET_KEY=sk_test_your_clerk_secret_key
```

### 5. Run the Development Servers

```bash
# Terminal 1 — Backend
cd server
npm run dev

# Terminal 2 — Frontend
cd client
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) — the app is running!

---

## 🔐 Environment Variables

### Client (`client/.env.local`)

| Variable | Description | Required |
|---|---|---|
| `VITE_CLERK_PUBLISHABLE_KEY` | Clerk frontend publishable key | ✅ |
| `VITE_BACKEND_URL` | Express server base URL | ✅ |

### Server (`server/.env`)

| Variable | Description | Required |
|---|---|---|
| `MONGODB_URI` | MongoDB Atlas connection string | ✅ |
| `PORT` | Server port (default: 5000) | ✅ |
| `CLERK_SECRET_KEY` | Clerk backend secret key | ✅ |

---

## 📡 API Reference

> Base URL: `http://localhost:5000`

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| `GET` | `/` | Health check | — |
| `GET` | `/api/courses` | Fetch all published courses | — |
| `GET` | `/api/courses/:id` | Fetch single course by ID | — |
| `POST` | `/api/courses` | Create a new course | Educator |
| `PUT` | `/api/courses/:id` | Update course details | Educator |
| `DELETE` | `/api/courses/:id` | Delete a course | Educator |
| `POST` | `/api/enroll` | Enroll student in course | Student |
| `GET` | `/api/user/enrollments` | Get student's enrolled courses | Student |
| `GET` | `/api/educator/dashboard` | Get educator stats and data | Educator |
| `GET` | `/api/educator/students` | Get all enrolled students | Educator |

> ⚠️ The backend is partially scaffolded. Full API implementation is part of the active roadmap (Phase 2).

---

## 🗺️ Roadmap

```
Phase 1 — Core MVP ✅
├── React + Vite + Tailwind 4 scaffold
├── Clerk authentication (sign in/sign up)
├── Course listing, detail, and player pages
├── Educator dashboard with Quill course builder
├── Dynamic chapter and lecture management
├── Student enrollment tracking + progress bars
└── YouTube video embedding + preview support

Phase 2 — Backend Integration 🔄
├── Connect all pages to live Express + MongoDB APIs
├── Clerk webhook → sync users to MongoDB on register
├── Full CRUD for courses, chapters, and lectures
├── Enrollment and progress persistence to database
└── Revenue calculation from real purchase data

Phase 3 — Payments & Advanced Features 📋
├── 💳 Stripe integration for course purchases
├── 🎟️ Coupon and discount code system
├── 📜 Certificate generation on course completion
├── 🔔 Email notifications (enrollment updates)
└── 💬 Course Q&A / discussion system

Phase 4 — Scale & Polish 🔮
├── 🧠 Course recommendation engine
├── 📈 Advanced educator analytics
├── 🌍 Multi-language i18n support
├── 🎙️ Live session / webinar integration
└── 📱 React Native mobile companion app
```

---

## 🤝 Contributing

Contributions are warmly welcome!

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/your-username/eduflow-lms.git

# 3. Create a feature branch
git checkout -b feature/your-feature-name

# 4. Make your changes and commit
git commit -m "feat: describe your change"

# 5. Push to your fork
git push origin feature/your-feature-name

# 6. Open a Pull Request
```

**Commit Convention** — this project follows [Conventional Commits](https://www.conventionalcommits.org/): `feat:` · `fix:` · `docs:` · `style:` · `refactor:` · `chore:`

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙌 Acknowledgements

| Tool | Role |
|---|---|
| [React](https://react.dev/) | Core UI framework |
| [Vite](https://vitejs.dev/) | Lightning-fast dev server and bundler |
| [Tailwind CSS](https://tailwindcss.com/) | Utility-first styling |
| [Clerk](https://clerk.com/) | Auth — sign in, session, and user management |
| [Quill](https://quilljs.com/) | Rich-text editor for course descriptions |
| [react-youtube](https://github.com/tjallingt/react-youtube) | YouTube video embedding |
| [rc-progress](https://github.com/react-component/progress) | Course progress bars |
| [humanize-duration](https://github.com/EvanHahn/HumanizeDuration.js) | Human-readable time formatting |
| [MongoDB Atlas](https://www.mongodb.com/atlas) | Cloud-hosted NoSQL database |
| [Express.js](https://expressjs.com/) | Backend REST API framework |

---

<div align="center">

**Built with ❤️ by Soumya Hedaoo**

⭐ If you found this useful, please give it a star!

[![GitHub stars](https://img.shields.io/github/stars/your-username/eduflow-lms?style=social)](https://github.com/your-username/eduflow-lms)

</div>
