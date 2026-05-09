# yt-ai-stream-bro

Локальный TypeScript/Node prototype для live-помощников вокруг стримов и выступлений. В repo есть два исторических слоя: YouTube Live Chat Fetcher/OBS overlay и backlog Granola Live Copilot для live-презентаций по transcript stream.

## Что здесь есть

| Слой | Назначение |
|---|---|
| YouTube chat fetcher | находит активный YouTube live, читает live chat, показывает web/OBS overlay и может сохранять сообщения в PostgreSQL |
| Granola Live Copilot | backlog для презентационного copilot: transcript delta, outline matcher, progress/timeline/prompts UI |
| API routes | live chat id, messages, SSE stream, DB history |

## Запуск YouTube chat layer

```bash
npm install
cp .env.example .env
npm run dev
```

Локально: `http://localhost:3000`.
OBS Browser Source: `http://localhost:3000/obs`.

## Основные env

```bash
YOUTUBE_API_KEY=...
YOUTUBE_CHANNEL_ID=...
PORT=3000
DB_HOST=...
DB_PORT=...
DB_NAME=...
DB_USER=...
DB_PASSWORD=...
```

PostgreSQL опционален: без него можно использовать live overlay, но история сообщений не будет сохраняться.

## Для агента

- Не путать этот repo с `news-scraper`: задачи новостного crawler/digest перенесены туда.
- Для YouTube chat work смотри код web/API/OBS overlay и issue `epic: YouTube Stream Companion`.
- Для Granola work смотри issue `epic: Granola Live Copilot` и его sub-issues.
- Перед выводом о live-интеграции проверяй реальный источник transcript/chat, а не только static UI.