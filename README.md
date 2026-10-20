# StudyNotion – EdTech Platform

StudyNotion is a full-stack **MERN** (MongoDB, Express, React, Node.js) ed-tech platform where instructors can create and sell courses, and students can browse, buy and watch them while tracking their progress.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [1. Clone the repository](#1-clone-the-repository)
  - [2. Install dependencies](#2-install-dependencies)
  - [3. Set up environment variables](#3-set-up-environment-variables)
  - [4. Run the project](#4-run-the-project)
- [Environment Variables Reference](#environment-variables-reference)
- [Getting the Required Keys](#getting-the-required-keys)
- [Available Scripts](#available-scripts)
- [API Overview](#api-overview)
- [Troubleshooting](#troubleshooting)
- [Author](#author)

---

## Features

**Students**
- Sign up with email OTP verification, log in, reset password
- Browse courses by category, view course details, ratings and reviews
- Add courses to cart and pay securely with **Razorpay**
- Watch enrolled course videos and track progress lecture-by-lecture
- Rate and review courses
- Manage profile and profile picture

**Instructors**
- Create, edit, publish and delete courses
- Add sections and sub-sections (video lectures) to a course
- Instructor dashboard with earnings and student stats (charts)

**General**
- JWT-based authentication with role-based access (Student / Instructor / Admin)
- Media uploads (images & videos) stored on **Cloudinary**
- Transactional emails (OTP, enrollment, payment success, password update) via **Nodemailer**
- Contact Us form
- Fully responsive UI built with **Tailwind CSS**

---

## Tech Stack

| Layer      | Technologies |
|------------|--------------|
| Frontend   | React 18, Redux Toolkit, React Router v6, Tailwind CSS, Axios, React Hook Form, Chart.js, Swiper |
| Backend    | Node.js, Express.js |
| Database   | MongoDB (Mongoose) |
| Auth       | JSON Web Tokens (JWT), bcrypt |
| Media      | Cloudinary, express-fileupload |
| Payments   | Razorpay |
| Email      | Nodemailer (SMTP) |

---

## Project Structure

```
studyNotion/
├── public/                 # Static files for the React app
├── src/                    # React frontend
│   ├── assets/             # Images, logos
│   ├── components/         # Reusable (common) and page-specific (core) components
│   ├── data/               # Static data (nav links, footer links, etc.)
│   ├── hooks/              # Custom React hooks
│   ├── Pages/              # Route-level pages
│   ├── reducer/            # Root reducer
│   ├── sclices/            # Redux slices
│   ├── services/           # API endpoints and API call functions
│   └── utils/              # Helper functions and constants
├── SERVER/                 # Express backend
│   ├── config/             # MongoDB, Cloudinary and Razorpay setup
│   ├── controllers/        # Route handlers / business logic
│   ├── mail/templates/     # HTML email templates
│   ├── middleware/         # Auth & role middleware
│   ├── models/             # Mongoose schemas
│   ├── routes/             # API routes
│   ├── utils/              # Mail sender, image uploader, helpers
│   ├── index.js            # Server entry point
│   └── .env.example        # Backend environment variable template
├── .env.example            # Frontend environment variable template
├── package.json            # Frontend package + combined dev scripts
└── tailwind.config.js
```

---

## Prerequisites

Make sure you have the following installed / ready:

- [Node.js](https://nodejs.org/) **v16 or higher** (v18 LTS recommended) and npm
- [Git](https://git-scm.com/)
- A **MongoDB** database – local install or a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster
- A free **Cloudinary** account – for image/video uploads
- A **Razorpay** account (test mode is fine) – for payments
- An **SMTP email** account – e.g. Gmail with an App Password – for sending emails

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/arunrawatsde/studyNotion.git
cd studyNotion
```

### 2. Install dependencies

Install the frontend dependencies (in the project root):

```bash
npm install
```

Install the backend dependencies:

```bash
cd SERVER
npm install
cd ..
```

### 3. Set up environment variables

The real `.env` files are **not** committed to this repository (they are listed in `.gitignore`). Instead, each part of the app ships with a `.env.example` template. Copy them and fill in your own values.

**Backend** – create `SERVER/.env`:

```bash
cp SERVER/.env.example SERVER/.env
```

**Frontend** – create `.env` in the project root:

```bash
cp .env.example .env
```

> On Windows (Command Prompt) use `copy` instead of `cp`, e.g. `copy SERVER\.env.example SERVER\.env`.

Now open both `.env` files and replace the placeholder values. See the [Environment Variables Reference](#environment-variables-reference) below for what each value means.

> ⚠️ Never commit your `.env` files. Only `.env.example` (with placeholder values) should be pushed.

### 4. Run the project

**Option A – run frontend and backend together (recommended)**

From the project root:

```bash
npm run dev
```

This uses `concurrently` to start:
- the React app at **http://localhost:3000**
- the Express server at **http://localhost:4000**

**Option B – run them separately**

Terminal 1 – backend:

```bash
cd SERVER
npm run dev        # with auto-reload (nodemon)
# or
npm start          # plain node
```

Terminal 2 – frontend (project root):

```bash
npm start
```

Once both are running:
- Open **http://localhost:3000** in your browser to use the app.
- Visit **http://localhost:4000** – you should see `"Your server is up and running"`, which confirms the backend is working.

> If you change any value in a `.env` file, restart the corresponding server for it to take effect.

---

## Environment Variables Reference

### Backend – `SERVER/.env`

| Variable          | Description | Example |
|-------------------|-------------|---------|
| `PORT`            | Port the Express server runs on | `4000` |
| `DATABASE_URL`    | MongoDB connection string | `mongodb+srv://user:pass@cluster.mongodb.net/studyNotion` |
| `JWT_SECRET`      | Secret used to sign/verify JWT tokens (any long random string) | `a_long_random_string` |
| `MAIL_HOST`       | SMTP host | `smtp.gmail.com` |
| `MAIL_USER`       | Email address used to send mails | `you@gmail.com` |
| `MAIL_PASS`       | SMTP password / Gmail App Password | `abcd efgh ijkl mnop` |
| `CLOUD_NAME`      | Cloudinary cloud name | `my-cloud` |
| `API_KEY`         | Cloudinary API key | `123456789012345` |
| `API_SECRET`      | Cloudinary API secret | `xxxxxxxxxxxxxxxx` |
| `FOLDER_NAME`     | Cloudinary folder where uploads are stored | `StudyNotion` |
| `RAZORPAY_KEY`    | Razorpay Key ID | `rzp_test_xxxxxxxx` |
| `RAZORPAY_SECRET` | Razorpay Key Secret | `xxxxxxxxxxxxxxxx` |

### Frontend – `.env` (project root)

| Variable                 | Description | Example |
|--------------------------|-------------|---------|
| `REACT_APP_BASE_URL`     | Base URL of the backend API | `http://localhost:4000/api/v1` |
| `REACT_APP_RAZORPAY_KEY` | Razorpay Key ID (public key, same as `RAZORPAY_KEY` above) | `rzp_test_xxxxxxxx` |

> Create React App only exposes variables that start with `REACT_APP_` to the browser. Never put secrets (like `RAZORPAY_SECRET`) in the frontend `.env`.

---

## Getting the Required Keys

<details>
<summary><b>MongoDB Atlas</b></summary>

1. Sign up at [mongodb.com/atlas](https://www.mongodb.com/atlas) and create a free cluster.
2. Under **Database Access**, create a database user with a password.
3. Under **Network Access**, add your IP address (or `0.0.0.0/0` for development).
4. Click **Connect → Drivers** and copy the connection string.
5. Replace `<username>` / `<password>` and add the database name (e.g. `/studyNotion`) → use it as `DATABASE_URL`.

</details>

<details>
<summary><b>Cloudinary</b></summary>

1. Sign up at [cloudinary.com](https://cloudinary.com/).
2. On the dashboard, copy **Cloud Name**, **API Key** and **API Secret** into `CLOUD_NAME`, `API_KEY` and `API_SECRET`.
3. Set `FOLDER_NAME` to any folder name you like (e.g. `StudyNotion`).

</details>

<details>
<summary><b>Razorpay</b></summary>

1. Sign up at [razorpay.com](https://razorpay.com/) and switch to **Test Mode**.
2. Go to **Settings → API Keys → Generate Test Key**.
3. Put the **Key ID** in `RAZORPAY_KEY` (backend) and `REACT_APP_RAZORPAY_KEY` (frontend).
4. Put the **Key Secret** in `RAZORPAY_SECRET` (backend only).

</details>

<details>
<summary><b>Gmail SMTP (App Password)</b></summary>

1. Enable **2-Step Verification** on your Google account.
2. Go to **Google Account → Security → App passwords** and generate a new app password.
3. Use `smtp.gmail.com` as `MAIL_HOST`, your Gmail address as `MAIL_USER`, and the generated 16-character app password as `MAIL_PASS`.

</details>

---

## Available Scripts

**Project root (frontend)**

| Command          | Description |
|------------------|-------------|
| `npm start`      | Starts the React dev server on port 3000 |
| `npm run server` | Starts the backend (runs `npm run dev` inside `SERVER/`) |
| `npm run dev`    | Starts frontend and backend together |
| `npm run build`  | Creates a production build in `build/` |

**`SERVER/` (backend)**

| Command       | Description |
|---------------|-------------|
| `npm start`   | Starts the server with Node |
| `npm run dev` | Starts the server with nodemon (auto-restart on changes) |

---

## API Overview

All endpoints are prefixed with `/api/v1`.

| Base route  | Purpose |
|-------------|---------|
| `/auth`     | Sign up, log in, send OTP, change/reset password |
| `/profile`  | Get/update profile, display picture, enrolled courses, instructor dashboard, delete account |
| `/course`   | Courses, categories, sections, sub-sections, ratings & reviews, course progress |
| `/payment`  | Capture payment, verify payment, send payment success email |
| `/reach`    | Contact Us form |

---

## Troubleshooting

- **`MongooseError` / database won't connect** – check `DATABASE_URL`, your Atlas user's password, and that your IP is allowed under Network Access.
- **Frontend calls go to `undefined/...`** – the root `.env` is missing or `REACT_APP_BASE_URL` isn't set. Create it and restart `npm start`.
- **OTP / emails not arriving** – verify `MAIL_HOST`, `MAIL_USER`, `MAIL_PASS`. For Gmail, you must use an App Password.
- **Image/video upload fails** – check the Cloudinary credentials and `FOLDER_NAME`.
- **Razorpay checkout doesn't open** – make sure `REACT_APP_RAZORPAY_KEY` is set in the root `.env` and matches `RAZORPAY_KEY` in `SERVER/.env`.
- **Port already in use** – change `PORT` in `SERVER/.env` (and update `REACT_APP_BASE_URL` to match), or stop the process using the port.

---

## Author

**Arun Rawat**

- GitHub: [@arunrawatsde](https://github.com/arunrawatsde)
