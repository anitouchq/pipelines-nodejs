# 📦 pipelines-nodejs
## 📖 О проекте

Простое Node.js-приложение (`add`, `main`), для которого настроен CI-пайплайн.
При каждом `push` и `pull request` в ветки `main` / `master` автоматически:

- 🧪 запускается линтинг через **ESLint**
- ✅ прогоняются тесты через **Jest** на Node.js **18.x, 20.x, 22.x**
- 🐳 собирается **Docker-образ** (без публикации, только на `push` в `main`)

---

## 📂 Структура проекта

```
.
├── .github/
│   └── workflows/
│       └── ci.yml          # GitHub Actions workflow
├── src/
│   └── index.js            # основной код (add, main)
├── tests/
│   └── index.test.js       # тесты (Jest)
├── package.json            # зависимости и скрипты
├── package-lock.json       # lock-файл
├── .eslintrc.json          # конфиг ESLint
├── Dockerfile              # образ node:18-alpine
└── README.md
```

---

## ⚙️ Как работает пайплайн

| Шаг | Что делает |
|-----|-----------|
| **Checkout** | Клонирует репозиторий |
| **Setup Node.js** | Ставит Node.js (matrix 18.x / 20.x / 22.x) с кэшем npm |
| **Install** | `npm ci` |
| **Lint** | `npm run lint` (ESLint) |
| **Test** | `npm test` (Jest) |
| **Docker build** | `docker build -t my-node-app:test .` |

---

## 🐳 Проверка локально

### Скачивание Docker-образа

<img width="624" height="204" alt="image" src="https://github.com/user-attachments/assets/2eae5271-6d31-4d95-92da-b4678e31a4b3" />


### Сборка образа

```bash
docker build -t my-node-app:latest .
```

### Запуск контейнера

```bash
docker run --rm my-node-app:latest
```

Ожидаемый вывод:

```
Hello from Node.js app!
```

Зайти внутрь контейнера:

```bash
docker run --rm -it my-node-app:latest /bin/sh
```

Выход:

```bash
exit
```

---

## 🧪 Запуск тестов локально

```bash
npm ci
npm run lint
npm test
```

---

## 🏗️ Стек

- **Node.js 18 / 20 / 22**
- **Jest** — тесты
- **ESLint** — линтинг
- **Docker** — контейнеризация

---

## 📄 Лицензия

MIT — свободно для учебных целей.
