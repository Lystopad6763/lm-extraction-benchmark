# LM Extraction Benchmark

Порівняння **6 моделей** (4 локальні через Ollama + 2 хмарні API) на задачі екстракції структурованої інформації з протоколів зустрічей.

## Що в репозиторії

- [`extraction_agent.py`](extraction_agent.py) — код агента що викликає всі 6 моделей
- [`ANALYSIS.md`](ANALYSIS.md) — **повний аналіз з висновками**
- [`eval_results.csv`](eval_results.csv) — таблиця результатів з 7 метриками
- [`samples/`](samples/) — 3 датасети (simple, chaotic, technical)
- [`results/`](results/) — 18 JSON відповідей моделей
- [`screenshots/`](screenshots/) — скріншоти запусків

## Моделі що порівнювались

| Модель | Автор | Тип               |
| ------------ | ---------- | -------------------- |
| neural-chat  | Intel      | Self-hosted (Ollama) |
| phi3         | Microsoft  | Self-hosted (Ollama) |
| llama2       | Meta       | Self-hosted (Ollama) |
| mistral      | Mistral AI | Self-hosted (Ollama) |
| gpt-4o-mini  | OpenAI     | Cloud API            |
| claude-haiku | Anthropic  | Cloud API            |

## Швидкий старт

```bash
# 1. Створи venv і встанови залежності
python -m venv venv
.\venv\Scripts\Activate
pip install openai anthropic requests python-dotenv

# 2. Скопіюй .env.example як .env і встав свої ключі
cp .env.example .env

# 3. Запусти Ollama локально
ollama serve
ollama pull mistral neural-chat llama2 phi3

# 4. Запусти агента
python extraction_agent.py
```

## Ключові висновки

Детально читай в [ANALYSIS.md](ANALYSIS.md). Коротко:

- **Claude Haiku** — найкраща для критичних задач (3с latency, 0 галюцинацій на простих даних)
- **neural-chat** — найкраща локальна (12/12 завдань, $0)
- **phi3** — несподівано найгірша (0 валідних JSON на складних датасетах)
- **llama2** — погано працює з українською (перекладає на англійську)
- **Хмарні моделі вигадують роки** — Claude поставив 2024, GPT — 2023, замість поточного 2026

## Технології

`Python` `Ollama` `OpenAI API` `Anthropic API` `requests` `python-dotenv`
