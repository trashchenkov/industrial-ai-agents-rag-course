# Промышленная разработка AI-агентов — Topic 7: RAG

Отдельный репозиторий с материалами по теме **Retrieval-Augmented Generation** для курса «Промышленная разработка AI-агентов».

## Структура

```text
rag_course_repo/
├── .env.example
├── .gitignore
├── requirements.txt
├── slides_sber/
│   ├── rag_lecture_sber.md      # корпоративная Slidev-версия
│   ├── rag_lecture_sber.pdf     # экспортированный PDF
│   ├── layouts/                 # custom corporate layouts
│   ├── styles/                  # палитра, типографика, SB Sans
│   └── public/                  # фоны, логотип, QR, шрифты
└── topic7_rag/
    ├── 00_model_agent_basics.ipynb
    ├── 01_ingestion_pipeline.ipynb
    ├── 02_retrieval_generation.ipynb
    ├── 03_graphrag.ipynb
    ├── 04_file_memory.ipynb
    └── data/.gitkeep            # сюда генерируются Chroma/BM25/Kuzu артефакты
```

Первый ноутбук собирает учебный корпус из открытых русскоязычных источников:

- PDF через `PyPDFLoader`;
- HTML-страницу через `WebBaseLoader`;
- статьи русской Википедии через MediaWiki API.

## Быстрый старт

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m ipykernel install --user --name industrial-ai-agents-rag --display-name "Industrial AI Agents RAG"
cp .env.example .env
```

После запуска Jupyter выберите kernel **Industrial AI Agents RAG**. Это важно: если notebook открыт в другом kernel, он может не видеть зависимости из `requirements.txt`.

Заполните в `.env` credentials для GigaChat:

```env
GIGACHAT_CREDENTIALS=<Base64(client_id:client_secret)>
GIGACHAT_SCOPE=GIGACHAT_API_PERS
GIGACHAT_MODEL=GigaChat-2-Max
GIGACHAT_EMBEDDINGS_MODEL=EmbeddingsGigaR
CHROMA_PERSIST_DIR=./data/chroma_db
SOURCE_FETCH_TIMEOUT=30
```

Запуск ноутбуков:

```bash
cd topic7_rag
jupyter notebook
```

Порядок прохождения:

0. `00_model_agent_basics.ipynb` — подключение к GigaChat, embeddings, Phoenix, минимальные LangChain и Deep Agents агенты.
1. `01_ingestion_pipeline.ipynb` — онлайн-загрузка корпуса, очистка, чанкинг, Chroma и BM25.
2. `02_retrieval_generation.ipynb` — retrieval, generation, hybrid search, reranking, compression, agentic RAG.
3. `03_graphrag.ipynb` — извлечение сущностей/связей и GraphRAG на Kuzu.
4. `04_file_memory.ipynb` — workspace context, `AGENTS.md` и файловая working memory.

## Презентация

В репозитории оставлена только корпоративная Sber-версия презентации.

Минимальный самодостаточный набор лежит в `slides_sber/`: исходник, layouts, стили, шрифты, изображения и готовый PDF.

```bash
cd slides_sber
pnpm install
pnpm dev
```

Экспорт PDF:

```bash
pnpm export
```

Готовый файл: `slides_sber/rag_lecture_sber.pdf`.

## Локальные артефакты

Ноутбуки создают индексы и рабочие файлы в `topic7_rag/data/` и `topic7_rag/workspace_demo/`. Эти директории добавлены в `.gitignore`, кроме `topic7_rag/data/.gitkeep`.

## Observability / Phoenix

`01_ingestion_pipeline.ipynb` не включает Phoenix: в нём мы в основном загружаем и индексируем документы.
Tracing начинается с `00_model_agent_basics.ipynb` и нужен во всех ноутбуках, где появляются LLM/RAG-вызовы.

Phoenix-зависимости уже включены в `requirements.txt`. Если Phoenix UI показывает `Internal Server Error` или импорт падает с `phoenix.evals.models`, переустановите зависимости из текущего `requirements.txt` и перезапустите Jupyter kernel:

```bash
python -m pip install -r requirements.txt
```
