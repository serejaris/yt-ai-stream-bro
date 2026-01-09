# YT-Chat Project

YouTube канал помощник с live chat интеграцией и статистикой.

## Critical Rules

- **Избегай `search.list`** — 100 единиц квоты. Используй `channels.list`, `playlistItems.list`, `videos.list` (1 ед. каждый)
- **DB_USER=ris** — не postgres! См. `.env.example`

## Agents

Для фронтенд задач используй агента `frontend-developer`.

## Stack

Next.js 14 (App Router), PostgreSQL, YouTube Data API v3, TypeScript

## Commands

```bash
npm run dev             # Development server
npm run build           # Production build
npm run test:connection # Тест YouTube API
npm run test:serejaris  # Тест получения chat ID
```

## Structure

| Path | Purpose |
|------|---------|
| `app/api/` | API routes (messages, videos, channel-stats, overlay) |
| `app/obs/` | OBS Browser Source интерфейс |
| `app/transmissions/` | Live chat трансляций |
| `components/` | React компоненты |
| `lib/database.ts` | PostgreSQL подключение |
| `lib/youtube-api.ts` | YouTube API wrapper |

## API Endpoints

| Endpoint | Purpose |
|----------|---------|
| `/api/messages/stream` | SSE поток сообщений |
| `/api/messages/db` | Сообщения из PostgreSQL |
| `/api/live-chat-id` | Chat ID активной трансляции |
| `/api/overlay` | POST/DELETE для OBS оверлея |

## Database

PostgreSQL, таблицы создаются автоматически (`lib/database.ts:initDatabase`):
- `chat_messages` — сообщения из live chat
- `api_request_logs` — логи API запросов

## OBS Overlay

Два режима работы (переключаются при движении мыши):

| Режим | Описание |
|-------|----------|
| **Лента (feed)** | Автоматический показ сообщений из live chat, новые появляются снизу |
| **Ручной (manual)** | Показ через API с эффектом печатной машинки |

```bash
# Ручной режим — отправка
curl -X POST http://localhost:3000/api/overlay -H "Content-Type: application/json" -d '{"author":"Name","message":"Text"}'

# Ручной режим — очистка
curl -X DELETE http://localhost:3000/api/overlay
```
