# Hono API - Assignment 2

Project ini dibuat untuk **Devscale Indonesia Students** sebagai materi pembelajaran untuk **Assignment 2 - Fullstack JavaScript Batch X**.

## Tentang Proyek

Ini adalah REST API sederhana yang dibangun menggunakan **Hono Framework** dan **Prisma ORM**. API ini mengelola data Event dan Participant dengan operasi CRUD (Create, Read, Update, Delete).

## Tech Stack

- **Hono** - Web framework yang ringan dan cepat untuk Node.js
- **Prisma** - ORM untuk database management
- **SQLite** - Database (file-based)
- **TypeScript** - Bahasa pemrograman utama
- **Zod** - Schema validation

## Struktur Codebase

```
src/
├── index.ts              # Entry point aplikasi
├── generated/            # Prisma generated files (auto-generated)
│   └── prisma/
│       ├── client.ts     # Prisma client
│       └── models/       # Database models
├── router/               # Route handlers
│   ├── events.ts         # Event endpoints (GET, POST, PATCH, DELETE)
│   └── participants.ts  # Participant endpoints (GET, POST, PATCH, DELETE)
├── utils/
│   └── prisma.ts         # Prisma client setup dengan SQLite adapter
└── validation/           # Zod validation schemas
    ├── event-validation.ts       # Validasi untuk Event
    └── participant-validation.ts # Validasi untuk Participant
```

## API Endpoints

### Events

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| GET | `/events` | Tampilkan semua event |
| GET | `/events/:id` | Tampilkan event berdasarkan ID |
| POST | `/events` | Buat event baru |
| PATCH | `/events/:id` | Update event |
| DELETE | `/events/:id` | Hapus event |

### Participants

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| GET | `/participants?eventId=xxx` | Tampilkan peserta untuk event tertentu |
| POST | `/participants` | Buat peserta baru |
| PATCH | `/participants/:id` | Update peserta |
| DELETE | `/participants/:id` | Hapus peserta |

## Cara Menjalankan

### 1. Install Dependencies
```bash
pnpm install
```

### 2. Setup Database
```bash
pnpm prisma generate
pnpm prisma db push
```

### 3. Jalankan Development Server
```bash
pnpm run dev
```

### 4. Buka di Browser
```bash
open http://localhost:3000
```

## Contoh Request

### Buat Event Baru
```bash
curl -X POST http://localhost:3000/events \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Workshop JavaScript",
    "description": "Belajar JavaScript dari dasar",
    "dateTime": "2026-01-15T10:00:00Z",
    "location": "Jakarta"
  }'
```

### Buat Participant
```bash
curl -X POST http://localhost:3000/participants \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "eventId": "event_id_here"
  }'
```

## Catatan Penting

- Semua endpoint mengembalikan response dalam format `{ data: ..., message: "..." }` untuk konsistensi
- Status code disertakan secara inline dalam `c.json({ message }, status)` untuk kode yang lebih bersih
- Input divalidasi menggunakan Zod sebelum diproses
- Comments dalam kode menggunakan Bahasa Indonesia untuk kemudahan pembelajaran
