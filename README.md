# 💬 SyncChat - AI Chat Application

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?logo=typescript)
![Prisma](https://img.shields.io/badge/Prisma-5.0-2D3748?logo=prisma)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql)
![Tailwind](https://img.shields.io/badge/Tailwind-3.0-06B6D4?logo=tailwindcss)
![OpenRouter](https://img.shields.io/badge/OpenRouter-Multi%20AI-FF6B00)

> A full-stack AI chat application supporting multiple AI models (GPT-4, Claude, Gemini). Users can switch between models in real-time with streaming responses.

## ✨ Features

- 🤖 **Multi-Model AI** - Support for GPT-4, Claude, Gemini via OpenRouter
- 💬 **Real-time Streaming** - AI responses stream character by character
- 📱 **Chat Management** - Create, rename, delete conversations
- 🔐 **GitHub OAuth** - Secure authentication via Better Auth
- 🎨 **Modern UI** - Shadcn components + Tailwind CSS
- 📝 **Markdown Support** - AI responses with formatted text
- 🌙 **Dark/Light Mode** - Theme switching
- ⚡ **Zustand State** - Efficient global state management
- 💾 **Chat Persistence** - All conversations saved to database

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| Frontend | Next.js 15, React 19, Tailwind CSS |
| Database | PostgreSQL, Prisma ORM |
| Auth | Better Auth (GitHub OAuth) |
| AI | OpenRouter API (GPT-4, Claude, Gemini) |
| State | Zustand |
| UI | Shadcn UI, Lucide Icons |
| Deployment | Vercel |

## 📊 Database Schema

```prisma
model User {
  id        String    @id @default(cuid())
  email     String    @unique
  name      String
  image     String?
  chats     Chat[]
  messages  Message[]
  createdAt DateTime  @default(now())
}

model Chat {
  id        String    @id @default(cuid())
  title     String
  userId    String
  user      User      @relation(fields: [userId], references: [id])
  messages  Message[]
  createdAt DateTime  @default(now())
  updatedAt DateTime  @updatedAt
}

model Message {
  id        String    @id @default(cuid())
  content   String    @db.Text
  role      Role
  chatId    String
  chat      Chat      @relation(fields: [chatId], references: [id])
  createdAt DateTime  @default(now())
}

enum Role {
  USER
  ASSISTANT
}
