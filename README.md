# Stilometry

![Stilometry — лингвистический отпечаток автора](https://raw.githubusercontent.com/samsebeingener/stilometry/main/docs/assets/github-cover.png)

**Stilometry** — project-local [Cursor](https://cursor.com) plugin для построения **лингвистического отпечатка** русскоязычного автора: 28 стилометрических метрик, LLM-интерпретация с цитатами, черновик профиля, approve/revise, гипотезы о языковых осях и промпт для имитации стиля без нейрослопа.

> Как ДНК, только для слов.

## Возможности

- **Сессионный intake** — `/stilometry-start`: приветствие, папка сессии, загрузка корпуса из чата или путей проекта
- **28 метрик** — лексика, синтаксис, морфология, пунктуация, ритм, риторика, прагматика, цифровой стиль
- **Offline NLP** — `razdel`, `pymorphy3`, `slovnet` (синтаксис + морфология)
- **LLM-разбор** — 10+ блоков отчёта с цитатами из текстов автора (plain Russian, без жаргона TTR/MTLD в основном тексте)
- **Workflow** — draft → approve → revise → personality → compile style prompt
- **Fixer** — post-run исправления пайплайна по `pipeline-fix-queue.md` (как в Excalibur)

## Быстрый старт

### 1. Установка

```powershell
git clone https://github.com/samsebeingener/stilometry.git
cd stilometry
pip install -e .
python stilometry.py install-models
```

Модели (~32 МБ) скачиваются в `model-cache/` (не в git).

### 2. Открыть в Cursor

Откройте папку `stilometry` как workspace — подхватятся `.cursor/agents`, commands, skills, rules.

### 3. Запуск анализа

```
/stilometry-start
```

Прикрепите **свои** тексты (рекомендуется ≥ 5000 символов) или укажите путь, например `corpus/notes.txt`.

## Команды Cursor

| Команда | Назначение |
|---------|------------|
| `/stilometry-start` | Старт, сессия, intake, полный анализ |
| `/stilometry-draft` | Машинный draft JSON |
| `/stilometry-approve` | Подтверждение отчёта пользователем |
| `/stilometry-revise` | Правки по замечаниям |
| `/stilometry-personality` | Языковые гипотезы (после approve) |
| `/stilometry-compile` | Промпт стиля для LLM |
| `/stilometry-fix` | Fixer по открытым инцидентам |

## Архитектура

```text
/stilometry-start (Director)
  → corpus-guardian
  → metrics-analyst      (razdel + pymorphy3 + slovnet)
  → report-auditor
  → linguistic-interpreter (LLM, цитаты)
  → profile-writer
  → profile-reviewer
  → [stilometry-fixer при инцидентах]
```

Память сессии: `stilometry-memory/sessions/<id>/` (`corpus/`, `runs/`, `reports/`, `fragments/`).

## Приватность

- Исходные тексты и отчёты сессий **не коммитятся** (см. `.gitignore`)
- Детерминированные метрики считаются **локально**
- LLM-интерпретация — через Cursor; не отправляйте чужие персональные данные без согласия

## Разработка

```powershell
python -m pytest -q
python scripts/validate_install.py
```

Подробнее: [docs/VALIDATION.md](docs/VALIDATION.md)

## Лицензия

MIT — см. [LICENSE](LICENSE).

## Автор

Проект разработал [Никита Куликов](https://samsebeingener.ru/).

---

**GitHub About (краткое описание):**

> Cursor plugin: Russian author stylometry — 28 metrics, offline NLP (Slovnet), LLM profile report & style prompt. Linguistic fingerprint from your texts.

<!-- SAIFER_REPO_PASSPORT_BEGIN: #435 -->
## Паспорт

- **Что это:** Cursor plugin: Russian author stylometry — 28 metrics, Slovnet NLP, LLM profile & style prompt.
- **Статус:** не знаю (работает / пауза / заморожено ❄️ / брошено — нет runtime-проверки).
- **Где работает:** не знаю (сервер/ПК/сайт/облако не подтверждены).
- **Как запустить или открыть:** [репозиторий](https://github.com/SaiferSMART/my-stilometry); запуск приложения — не знаю (ищите инструкции в README).
- **Связанные открытые PR:** [актуальный список](https://github.com/SaiferSMART/my-stilometry/pulls?q=is%3Apr+is%3Aopen).
- **Связанные открытые Issue:** [актуальный список](https://github.com/SaiferSMART/my-stilometry/issues?q=is%3Aissue+is%3Aopen).
- **Дата последнего изменения GitHub:** 2026-08-14T12:20:17Z (поле `pushed_at`, любая ветка; не равно проверке эксплуатации).
- **Кто ведёт:** не знаю; владелец репозитория GitHub — `SaiferSMART`.
- **Вопрос к владелице:** подтвердить статус, площадку, точку входа и фактического ведущего.
- **Задание:** [Issue №435](https://github.com/SaiferSMART/saifer-ai-ops/issues/435).
<!-- SAIFER_REPO_PASSPORT_END -->
