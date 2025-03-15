# 🔐 Authentication Module

This app is intended to be a **plug-and-play authentication module** designed to be integrated into project. This repository contains submodules for the **backend**, **frontend**, and **documentation**, making it easy to manage and deploy the authentication system.  

## For complete instructions on how to run this app, please visit the [Documentation](https://auth-module.lautaroayosa.com.ar/documentation/docs/intro) <!-- omit in toc -->

<br>

- [🔐 Authentication Module](#-authentication-module)
  - [🔍 What is this Module?](#-what-is-this-module)
  - [🚀 Features](#-features)
  - [⚙️ How it Works](#️-how-it-works)
    - [1️⃣ User Login Flow](#1️⃣-user-login-flow)
    - [2️⃣ MFA Verification Flow (if enabled)](#2️⃣-mfa-verification-flow-if-enabled)
    - [3️⃣ Token Lifecycle](#3️⃣-token-lifecycle)
    - [4️⃣ Password Reset Flow](#4️⃣-password-reset-flow)
  - [🛠️ Tech Stack](#️-tech-stack)
    - [Backend](#backend)
    - [Frontend](#frontend)
    - [Deployment](#deployment)
  - [📥 Cloning the Repository](#-cloning-the-repository)
  - [🏗️ Setting Up the Project](#️-setting-up-the-project)
  - [🛠️ 1️⃣ Backend Setup](#️-1️⃣-backend-setup)
    - [➤ Running Manually](#-running-manually)
  - [🎨 2️⃣ Frontend Setup (Optional)](#-2️⃣-frontend-setup-optional)
    - [➤ Running Manually](#-running-manually-1)
  - [📖 3️⃣ Documentation Setup (Optional)](#-3️⃣-documentation-setup-optional)
    - [➤ Running Manually](#-running-manually-2)
  - [🐳 Running Everything with Docker](#-running-everything-with-docker)

<br>

---

## 🔍 What is this Module?  

The **Authentication Module** is a fully functional authentication system designed to be **cloned, configured, and deployed** inside any project. Unlike a central authentication API, this module is meant to be included **inside your own application** as a GitHub submodule or a standalone service. It supports both **PostgreSQL and MongoDB**, making it highly flexible for different use cases.

---

## 🚀 Features  

✅ **Email/Password Authentication** - Secure login system with JWT authentication  
✅ **Refresh Token Flow** - Automatic access token renewal for better security  
✅ **Multi-Factor Authentication (MFA)** - Optional 2FA for enhanced security  
✅ **Password Reset System** - Secure password reset via email tokens  
✅ **Database Support** - Works with both **PostgreSQL** and **MongoDB**  
✅ **Docker Support** - Easily deploy with `docker-compose`  
✅ **Frontend Included** - Ready-to-use Next.js frontend with authentication flows  
✅ **Environment-Based Configuration** - Easily configure database, email settings, and more  
✅ **Plug-and-Play Integration** - Add it to any project with minimal setup  

> 🔒 Future Improvements: Refresh Token Rotation, Social Logins (Google, GitHub, etc.)

---

## ⚙️ How it Works  

This module follows a **JWT-based authentication flow** with refresh tokens and optional multi-factor authentication (MFA).

### 1️⃣ User Login Flow  
- The user enters their **email** and **password**.  
- The backend **verifies** the credentials.  
- If **MFA is disabled**, the server generates **access** and **refresh tokens**, sending them via **`httpOnly` cookies**.  
- If **MFA is enabled**, a **Temporary Session Token** (generated via Node.js `crypto`) is sent to the frontend for MFA verification.  

### 2️⃣ MFA Verification Flow (if enabled)  
- The user enters their **MFA code**.  
- The backend verifies the **Temporary Session Token**.  
- If valid, it retrieves the user and verifies the **MFA code**.  
- If successful, **access** and **refresh tokens** are issued and sent via **`httpOnly` cookies**.  
- **Temporary Session Tokens** expire automatically and are deleted after use.  

### 3️⃣ Token Lifecycle  
- **Access Token** → **15 minutes**  
- **Refresh Token** → **7 days** (rotation planned for future updates)  
- **Password Reset Token** → **1 hour**  
- **Temporary Session Token (MFA)** → **15 minutes**  

### 4️⃣ Password Reset Flow  
- The user requests a **password reset**.  
- A **password reset token** (generated via Node.js `crypto`) is sent via email as a **URL** to the frontend.  
- The frontend submits the **token** and **new password** to the backend.  
- If the token is valid, the **password is updated**.  

---

## 🛠️ Tech Stack  

### Backend  
- **Node.js** (Express)  
- **PostgreSQL / MongoDB** (selectable)  
- **JWT for authentication**  
- **Crypto for secure tokens**  

### Frontend  
- **Next.js** (React framework)  
- **Axios** (API requests)  
- **TailwindCSS** (Styling)  
- **TypeScript**  

### Deployment  
- **Docker Support** (`docker-compose` for easy setup)  

<br>

---

<br>

## 📥 Cloning the Repository  

Since this project uses **Git submodules**, you must clone it with the `--recurse-submodules` flag to fetch all components correctly:

```sh
git clone --recurse-submodules https://github.com/LautaroAyosa/auth-module.git
cd auth-module
```

If you've already cloned the repository **without submodules**, you can initialize them manually:

```sh
git submodule update --init --recursive
```

To pull updates from submodules later:

```sh
git submodule update --remote
```

<br>

---

<br>

## 🏗️ Setting Up the Project  

This repository consists of three submodules:

- **Backend** (`backend/`) → The authentication API  
- **Frontend** (`frontend/`) → Login & user authentication UI (optional, replaceable)  
- **Docs** (`docs/`) → Docusaurus-based documentation  

Each part can be **run independently** or using **Docker Compose**.

<br>

---

<br>

## 🛠️ 1️⃣ Backend Setup  

### ➤ Running Manually  

1. Navigate to the backend directory:  
   ```sh
   cd backend
   ```
2. Install dependencies:  
   ```sh
   npm install
   ```
3. Copy the example environment file:  
   ```sh
   cp .env.example .env
   ```

4. Configure de environment file with your information. Feel free to use the [documentation](http://auth-module.lautaroayosa.com.ar/documentation/docs/setup/setup-instructions) if you're having problems.

5. Start the authentication server and database:  
   ```sh
   npm run dev
   ```

<br>


---

## 🎨 2️⃣ Frontend Setup (Optional)  

### ➤ Running Manually  

1. Navigate to the frontend directory:  
   ```sh
   cd frontend
   ```
2. Install dependencies:  
   ```sh
   npm install
   ```
3. Copy the example environment file:  
   ```sh
   cp .env.example .env
   ```
4. Configure de environment file with your information.

5. Start the frontend:  
   ```sh
   npm run dev
   ```

<br>

---

<br>

## 📖 3️⃣ Documentation Setup (Optional)  

The documentation is built using **Docusaurus**.

### ➤ Running Manually  

1. Navigate to the `docs/` directory:  
   ```sh
   cd docs
   ```
2. Install dependencies:  
   ```sh
   npm install
   ```
3. Start the local docs server:  
   ```sh
   npm run start
   ```

<br>

---

<br>

## 🐳 Running Everything with Docker  

This has not been fully developed and tested yet. Update coming soon.