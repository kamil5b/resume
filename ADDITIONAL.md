# Project 1
🚀 bev-fs — Bun - Elysia - Vue Fullstack Framework
A Fullstack Framework Without Vercel Dependencies

bev-fs is a fullstack TypeScript framework built on non-Vercel-backed tools:
• ⚡ Bun runtime
• 🧠 Elysia backend
• 🎨 Vue 3 frontend
It focuses on developer experience, type safety, and deployment freedom — no platform lock-in.

What bev-fs offers:
• 📁 Directory-based routing for API & pages
• 🔒 End-to-end TypeScript types (shared client & server)
• 🔁 Automatic route discovery (no manual wiring)
• 🌍 Single-port production deployment (API + SPA)
• ⚙️ Config via .env and YAML
• 🧩 Composable middleware system

📦 Built-in templates
• Base template → minimal starter, no opinionated setup
• Full template → clean monolith and showcasing full features with CRUD examples
• Optional Tailwind CSS → choose with or without Tailwind at scaffold time

🛠 Tooling
• bev-fs — core framework
• create-bev-fs — project scaffolding CLI
npx create-bev-fs my-app bun install bun run dev 
If you like Next.js-style conventions but want a Vue + Elysia + Bun stack without Vercel dependencies, this is built for you.
Feedback & contributors welcome 🙌

This is an open source project and not backed by anyone including Bun, Elysia, nor Vue 3.
🔗 GitHub: https://github.com/kamil5b/bev-fs


# Project 2
🚀 Introducing Go-PSTE-Boilerplate: Go Plug and Swap Modular Monolith Framework!

I'm excited to share Go-PSTE-Boilerplate – an open-source Go framework implementing the PSTE Architecture (Plug, Swap, Toggle, Extract).

What makes it different?
🔌 Plug – Swap HTTP frameworks (Echo, Gin, Fiber), cache backends, storage providers, and message queues without touching business logic
🔄 Swap – Change databases per module (PostgreSQL ↔ MongoDB) via configuration
🎛️ Toggle – Enable/disable features with YAML-based feature flags
📦 Extract – Domain-per-module pattern makes microservices migration seamless

Key Features:
✅ Complete JWT/Session/Basic authentication
✅ gRPC + HTTP dual-protocol support
✅ Worker queues (Asynq, RabbitMQ, Redpanda)
✅ Storage abstraction (S3, GCS, Local)
✅ Built-in dependency linter enforcing module isolation
✅ 80-100% test coverage on core modules

Who is this for?
Teams building medium-to-large Go applications who want clean architecture without the complexity of premature microservices.
The architecture enforces strict boundaries today while keeping the door open for extraction tomorrow.

🔗 GitHub: https://github.com/kamil5b/go-pste-monolith

Would love feedback from the Go community! 

# Project 3
🚀 NextJS Fullstack Monolith – Eksplorasi Arsitektur MVP

Akhir-akhir ini saya bereksperimen mencari cara membangun fullstack monolith yang tetap sederhana, cepat, dan mudah dirawat—namun tetap menjaga pemisahan tujuan di dalam satu repo, satu aplikasi.

Hasilnya:
👉 MVP Fullstack Monolith berbasis NextJS, dirancang untuk tim kecil, solo engineer, atau siapa pun yang butuh fondasi arsitektur yang bersih dan scalable.

Saya juga sedang mencari alternatif selain NextJS (😭 tolong rekomendasinya), selama framework tersebut tetap support pola arsitektur seperti ini.

https://lnkd.in/g9mMB6sS
---

🧱 Design Architecture 

`src/server` – Backend / Controller

Menggunakan design 3-layer architecture:

- Handler → HTTP layer (parse request/response, tanpa business logic)

- Service → Business logic + transaction handling (BEGIN/COMMIT/ROLLBACK)

- Repository → Data access layer, raw SQL (tanpa ORM, pakai PoolClient agar transaction handling di service dapat dibawa ke repository)


Migrasi menggunakan sql-migrate, dan database menggunakan PostgreSQL

---
`src/client` – Frontend / View

Dibangun dengan:

- React 19
- Tailwind CSS v4
- shadcn/ui + Radix UI
- lucide-react
- recharts

Struktur modular yang berisi:
Components, Hooks, Helpers, Layouts, Templates, dan Pages per domain.

---
`src/shared` – Shared Model & Contracts

Berisi definisi yang dibutuhkan FE & BE:

- Entities
- Request / Response
- Enums
- Types
- Role-based Access Control (RBAC)

Tujuannya menjaga konsistensi API contract dan RBAC Control di seluruh aplikasi.
---
`src/app` – Routing Layer

Lapisan routing minimal:
- page.tsx → import dari @/client/pages
- layout.tsx → import dari @/client/layouts
- api/route.ts → import dari @/server/handlers
✔️ Tanpa business logic
✔️ Routing lebih clean dan predictable
---
Fitur unggulan lain: 

- Authentication Menggunakan JWT Bearer Auth.
- File upload support dengan S3-Compatible dan fallback ke local

---

🎯 Tujuan Utama

- Simple, , tapi tetap maintainable
- FE fokus di @/client, BE fokus di @/server, tipe data dan kontrak disamakan via @/shared
- 1 app, 1 deployment, tidak perlu split deploying FE & BE
- Cocok untuk: Tim kecil (1 FE – 1 BE) / Solo engineer (termasuk yang ditemani AI)
- Dokumentasi rapi agar mudah di-extend dan di-maintain
- Berfungsi sebagai base/reference, bukan produk final
---
🤝 Terbuka untuk Feedback & Kontribusi

Repo ini public, jadi saya sangat terbuka untuk:

- Saran
- Kritik
- Issue
- Pull Request

Kalau menemukan bug atau punya ide perbaikan, feel free untuk langsung buat PR atau issue.

---

🔍 Mencari Rekomendasi Framework

Jika ada framework selain NextJS yang memenuhi kriteria:
- Support Fullstack monolith
- TypeScript / JavaScript
- FE & BE bisa dalam satu project
- Tidak dibacked oleh Vercel
- (Bonus) Bisa ganti client ke Vue

Tolong bantu share rekomendasinya 🙏
---
Terima kasih sudah membaca — dan saya sangat terbuka untuk berdiskusi, memberi masukan, atau berkolaborasi 🙌
---

Show translation