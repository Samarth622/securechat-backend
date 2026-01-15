# 🔐 End-to-End Encrypted Real-Time Chat Backend

A **security-first, production-style real-time chat backend** built with **Node.js, Express, and Socket.IO**, implementing **true End-to-End Encryption (E2EE)** using **AES-256-GCM + RSA hybrid cryptography**.

> 🔒 Even the backend server **cannot read messages**  
> ⚡ Messages are delivered in **real time**  
> 🧠 Designed with **system design & security principles**, not tutorials

---

## 🚀 Features

### 🔐 End-to-End Encryption (E2EE)
- AES-256-GCM for message encryption
- RSA-based key exchange (hybrid encryption)
- Unique AES key per message
- Backend stores only encrypted data
- Database breach ≠ message leak

### ⚡ Real-Time Messaging
- Socket.IO (WebSockets)
- JWT-authenticated socket connections
- Online / offline user handling
- Encrypted message relay
- Offline message persistence

### 🟣 Chat UX Features
- Read receipts (sent → delivered → read)
- Typing indicators
- Secure metadata handling (content encrypted, metadata not)

### 🛡️ Security-First Backend
- JWT-based stateless authentication
- Secure password hashing (bcrypt)
- Rate-limited login (brute-force protection)
- Helmet security headers
- Zero plaintext message exposure

### 🧱 Clean Backend Architecture
- Modular Express structure
- Feature-based folders
- Separation of routes, controllers, sockets, and crypto logic

---

## 🧠 Tech Stack

**Backend**
- Node.js
- Express.js

**Real-Time**
- Socket.IO

**Security**
- JWT
- bcrypt
- Helmet
- express-rate-limit

**Cryptography**
- AES-256-GCM
- RSA (OAEP padding)
- Hybrid encryption

**Database**
- MongoDB
- Mongoose

---

## 🏗️ System Architecture (High Level)

```text
┌──────────────┐           Encrypted Payload           ┌──────────────┐
│  Client A    │ ───────────────────────────────────▶ │  Client B    │
│ (Sender)     │                                       │ (Receiver)   │
│              │ ◀─────────────────────────────────── │              │
└──────┬───────┘           Encrypted Payload           └──────┬───────┘
       │                                                      │
       │                    (Blind Relay)                    │
       ▼                                                      ▼
┌────────────────────────────────────────────────────────────────────┐
│                     Backend Server (Node.js)                         │
│                                                                      │
│  - JWT Auth (HTTP + WebSocket)                                       │
│  - Socket.IO (Real-time relay)                                       │
│  - Stores ONLY encrypted blobs                                       │
│  - Cannot decrypt messages                                           │
│                                                                      │
│  MongoDB                                                            │
│  ┌───────────────────────────────────────────────────────────────┐ │
│  │ encryptedMessage | encryptedAESKey | iv | authTag | metadata  │ │
│  └───────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────┘
```
