# Sber-styled RAG lecture slides

Корпоративная Slidev-версия лекции по теме 7 (`RAG`) для курса «Промышленная разработка AI-агентов».

Папка содержит минимальный перенос `rag_lecture_sber.md` и всех локальных зависимостей, которые нужны для запуска и экспорта презентации.

## Быстрый старт

```bash
pnpm install
pnpm dev
```

Откроется Slidev dev server для `rag_lecture_sber.md`.

## Экспорт PDF

```bash
pnpm export
```

Готовый PDF сохраняется рядом с исходником:

```text
rag_lecture_sber.pdf
```

Текущий экспорт уже лежит в этой папке.

## Состав

```text
slides_sber/
├── rag_lecture_sber.md
├── rag_lecture_sber.pdf
├── package.json
├── pnpm-lock.yaml
├── layouts/              # corporate Slidev layouts
├── styles/               # SB palette / typography styles
└── public/
    ├── fonts/            # SB Sans Display woff2
    ├── image39.jpg       # title background
    ├── image8.jpg        # content background
    ├── image20.jpeg      # section background
    ├── image32.png       # corner logo
    └── qr-gigatrash.png  # Telegram QR
```

## Примечания

- `node_modules/` не должен попадать в репозиторий.
- `dist/` и `.slidev/` — локальные build/runtime артефакты.
- Если меняете `.md`, перезапустите `pnpm export`, чтобы обновить PDF.
