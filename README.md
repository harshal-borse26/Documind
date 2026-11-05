# DocuMind: AI-Powered Document Intelligence & Active Recall Platform

[![Next.js](https://img.shields.io/badge/Next.js-16.1.4-black?logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.2.3-blue?logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9.3-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.1.18-38bdf8?logo=tailwindcss)](https://tailwindcss.com/)
[![NVIDIA NIM](https://img.shields.io/badge/AI_Engine-Meta_Llama--3.3--70B-76b900?logo=nvidia)](https://build.nvidia.com/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB_7.0-green?logo=mongodb)](https://www.mongodb.com/)
[![Razorpay](https://img.shields.io/badge/Payments-Razorpay_API-0c2340?logo=razorpay)](https://razorpay.com/)

> **DocuMind** is an end-to-end, serverless document intelligence and automated pedagogical synthesis platform. It transitions learners from passive rereading to active recall by automatically generating multi-level summaries, spaced-repetition flashcards, 4-option MCQ assessments, conversational document chat, and intuitive conceptual analogies from heterogeneous study materials.

---

## 🏛️ Academic Attribution
- **Institute:** The Shirpur Education Society’s R. C. Patel Institute of Technology, Shirpur *(Autonomous Institute affiliated to DBATU, Lonere)*
- **Department:** Department of Computer Engineering
- **Academic Year:** 2025–2026
- **Project Team:**
  1. **Harshal Arjun Borse** (PRN: 231101154)
  2. **Pratik Rajendra Bhadane** (PRN: 231101160)
  3. **Khushi Amol Chaudhari** (PRN: 231101191)
  4. **Madhavi Pravin Pawar** (PRN: 241201009)
- **Project Guide:** Dr. J. S. Sonawane (Assistant Professor)

---

## 🚀 Key Features

- **Multi-Format Ingestion:** Ingests PDF documents, Word documents (`.docx`), PowerPoint decks (`.pptx`), scanned files, and YouTube video lecture URLs.
- **DOM-Virtualized PDF Parsing:** Headless serverless extraction utilizing `pdfjs-dist/legacy` with custom DOM stubs, eliminating native C++ canvas dependencies.
- **Sliding-Window Chunking:** Implements an overlapping sliding window (500-word window with 50-word overlap) to eliminate context loss across token boundaries.
- **NVIDIA NIM LLM Engine:** Powered by Meta Llama-3.3-70B-Instruct with strict JSON schema enforcement (`response_format: { type: 'json_object' }`).
- **Active Recall Flashcards:** Auto-generated question-and-answer pairs categorized by difficulty (`Easy`, `Medium`, `Hard`) with 3D flip card animations and review tracking.
- **MCQ Assessment Engine:** 4-option multiple-choice quizzes with distractor rationales, real-time scoring, and confetti feedback.
- **Conversational Document Chat (RAG):** Context-aware conversational Q&A bounded by a 10-message sliding window and 20,000-character context limit.
- **Concept Explainer & Analogies:** Translates complex textbook concepts into real-world analogies (Simple, Detailed, or Analogy mode).
- **Edge Security & Cryptography:** Stateless HS256 JWT authorization at the Next.js edge runtime via `jose` library without database lookup overhead.
- **Resilient Uploads & Storage:** Dual-tier document upload pipeline (Cloudinary CDN with automated fallback to local disk `/public/uploads/` on 403 errors).
- **Idempotent Billing & Subscriptions:** Tiered plans (`Starter`, `Professional`, `Enterprise`) processed via Razorpay with HMAC-SHA256 webhook signature verification and coupon codes (`DOCUMIND50`, `DOCUMIND75`, `DOCUMIND90`).

---

## 📐 System Architecture

![DocuMind Architecture](public/documind_architecture_diagram.jpg)

### Architecture Highlights
1. **Presentation Layer:** Next.js 16 App Router, React 19 Server/Client Components, Framer Motion animations, and Tailwind CSS v4.
2. **Security & Middleware Layer:** Edge middleware route protection verifying JWTs with sub-millisecond latency.
3. **Processing Pipeline:** Multi-format streaming parser with sliding-window chunker ensuring cohesive semantic chunks.
4. **AI Synthesis Layer:** NVIDIA NIM microservices executing Meta Llama-3.3-70B with anti-prompt-injection system guardrails.
5. **Persistence Layer:** MongoDB 7.0 database modeled via Mongoose 9.3 with indexing on user, document, and session collections.

---

## 🛠️ Technology Stack & Versions

| Layer | Technology | Version | Purpose |
| :--- | :--- | :--- | :--- |
| **Runtime** | Node.js | `v22.14.0` (LTS) | JavaScript runtime |
| **Framework** | Next.js | `16.1.4` | Full-stack framework (Turbopack + App Router) |
| **Frontend** | React | `19.2.3` | UI component architecture |
| **Language** | TypeScript | `5.9.3` (Strict) | Compile-time type safety |
| **Styling** | Tailwind CSS | `4.1.18` | Modern utility-first CSS |
| **AI Microservices** | NVIDIA NIM | API | Meta Llama-3.3-70B-Instruct inference |
| **Database** | MongoDB & Mongoose | `7.0` / `9.3.3` | Document store and ODM |
| **Security** | jose / bcryptjs | `6.2.2` / `3.0.3` | Edge JWT verification & password hashing |
| **Parsing** | pdfjs-dist | `5.5.207` | DOM-virtualized PDF text extraction |
| **Payments** | Razorpay SDK | `2.9.6` | Idempotent checkout & webhook verification |

---

## 🏁 Getting Started

### Prerequisites
- **Node.js:** `v20.x` or `v22.x` installed ([Download Node.js](https://nodejs.org/))
- **MongoDB:** Local MongoDB instance running on `mongodb://localhost:27017` or MongoDB Atlas URI
- **API Keys:**
  - NVIDIA NIM API Key ([NVIDIA Build](https://build.nvidia.com/))
  - Cloudinary Account ([Cloudinary Console](https://cloudinary.com/))
  - Razorpay Test Keys ([Razorpay Dashboard](https://dashboard.razorpay.com/))

### Installation Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/pratikBhadane18/Studygeni-frontend.git
   cd Studygeni-frontend
   ```

2. **Install project dependencies:**
   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
   Fill in your API keys and credentials in `.env`:
   ```env
   NODE_ENV=development
   PORT=3000
   MONGODB_URI=mongodb://localhost:27017/studygeni
   JWT_SECRET=your_super_secret_jwt_key_here
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   NVIDIA_API_KEY=nvapi-your_nvidia_api_key
   NVIDIA_MODEL=meta/llama-3.3-70b-instruct
   RAZORPAY_TEST_MODE=true
   RAZORPAY_KEY_ID=rzp_test_your_id
   RAZORPAY_KEY_SECRET=your_secret
   ```

4. **Seed Promo / Discount Coupons (Optional):**
   ```bash
   node scripts/seed-coupons.mjs
   ```

5. **Start the Development Server:**
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 📂 Repository Structure

```text
├── public/                     # Static media, icons, and architecture diagrams
│   ├── documind_architecture_diagram.jpg
│   └── uploads/                # Local disk fallback upload folder (.gitkeep)
├── scripts/                    # Database seeding and utility scripts
│   └── seed-coupons.mjs        # Seed discount vouchers (50%, 75%, 90%)
├── src/
│   ├── app/                    # Next.js App Router pages & API routes
│   │   ├── api/v1/             # RESTful API route handlers
│   │   │   ├── ai/             # Summary, flashcards, quiz, chat routes
│   │   │   ├── auth/           # Login, registration, session routes
│   │   │   ├── documents/      # Upload, extraction, listing routes
│   │   │   └── payments/       # Razorpay order, verify, webhook routes
│   │   ├── dashboard/          # Authenticated user learning dashboard
│   │   ├── login/              # Authentication login UI
│   │   └── register/           # User signup UI
│   ├── components/             # Reusable UI components
│   │   ├── dashboard/          # Flashcard flip, quiz modal, document viewer
│   │   └── landing/            # Responsive marketing & feature showcase UI
│   ├── lib/                    # Shared client utilities, pricing plans, API client
│   ├── proxy.ts                # Edge middleware JWT verification (jose)
│   ├── server/                 # Backend business logic & models
│   │   ├── models/             # Mongoose schemas (User, Document, Flashcard, etc.)
│   │   ├── services/           # AI, Auth, Billing, Razorpay services
│   │   └── utils/              # PDF and Office text parsing utilities
│   └── types/                  # TypeScript interface definitions
├── .env.example                # Sample environment template
├── .gitignore                  # Git ignore rules
├── DOCUMIND_COMPREHENSIVE_PROJECT_REPORT.md # 50-page academic report
├── package.json                # Project dependencies and npm scripts
└── tsconfig.json               # TypeScript strict configuration
```

---

## 🧪 Verification & Testing

To verify static typing and ensure zero build/type errors:
```bash
npx tsc --noEmit
```

To run the Next.js production build:
```bash
npm run build
```

---

## 📄 License
This project is developed for academic and educational purposes under the Department of Computer Engineering, R. C. Patel Institute of Technology, Shirpur.
