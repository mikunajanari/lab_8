# Практично-лабораторне заняття №8

Тема: Неперервна інтеграція.

Мета: ознайомитися з принципами і практиками неперервної інтеграції, сформувати навички автоматизації CI/CD процесів в GitHub Actions.

## 1. Завершено практичні роботи на GitHub Skills. Результати останніх завдань з Publish Packages прикріплені у файлі my_result_Bryzhyniuk.md

   - Hello GitHUb Actions: https://github.com/mikunajanari/skills-hello-github-actions

   - Publish Packages: https://github.com/mikunajanari/skills-publish-packages

## 2. Створимо GitHub Workflow для CI/CD з Docker. Для цього створимо файл .github/workflows/docker-publish.yml

![image](https://github.com/user-attachments/assets/296038df-83ec-403e-9a43-2913015ae7f4)

![image](https://github.com/user-attachments/assets/5d615011-106a-47a6-b916-9706061537cf)

```tags: ghcr.io/mikunajanari/bryzhyniuk_lb8:latest```

Змінимо Dockerfile:

![image](https://github.com/user-attachments/assets/52380372-2dae-49ed-86ec-0dd2be92b5e5)

Також створимо файл nginx.conf:

![image](https://github.com/user-attachments/assets/f75db082-23fd-49db-9ada-be79ebdaa9f3)

Перевіримо, щоб у .dockerignore були додані всі необхідні файли:

![image](https://github.com/user-attachments/assets/0e6856e3-f52c-456a-a17b-969767110481)

Змінимо файл e2e/example.spec.ts для уникнення помилок

![image](https://github.com/user-attachments/assets/3f7c9861-332b-420d-b3a2-5713ca6f7aa5)


Результат:
![image](https://github.com/user-attachments/assets/59e6eb43-2be1-400b-b81e-ac07b6f0f112)

![image](https://github.com/user-attachments/assets/74716540-c52d-4abb-a9a5-42a44b2a3e78)

Перейдемо в акаунт GitHub на вкладку Packages та побачимо там Докер-образ:

![image](https://github.com/user-attachments/assets/5399d390-06b6-4c5a-b40f-2c94e374655a)

Коментарі до результату:

```name: Build and Push Docker Image``` - Назва workflow, відображається в GitHub у вкладці Actions

Визначає, коли запускається workflow:
```
on:
  push:
    branches:
      - main
      - feature/*
```

Дозволяє вручну запустити workflow через GitHub:

```workflow_dispatch:```

Дозволи для GitHub Actions (читання вмісту репозиторію та запис пакетів у GitHub Container Registry):

```
permissions:
  contents: read
  packages: write
```

Оголошення завдання з назвою build, яке буде виконуватись на віртуальній машині з Ubuntu останньої версії:

```
jobs:
  build:
    runs-on: ubuntu-latest
```

Початок списку кроків, які виконаються в рамках завдання: 

```
steps:
```

Для завантаження коду з репозиторію до віртуального середовища, де буде виконуватись збірка:

```
- name: Checkout repository
        uses: actions/checkout@v3
```

Встановлення Node.js версії 20:

```
- name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 20
```

Встановлення менеджера пакетів pnpm глобально:

```
 - name: Install pnpm
        run: npm install -g pnpm
```

Встановлення залежності проєкту та виконання скриптів з package.json):

```
 - name: Install dependencies and build project
        run: |
          pnpm install
          pnpm run build
```

Вхід у GitHub Container Registry:

```
 - name: Log in to GitHub Container Registry (GHCR)
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.repository_owner }}
          password: ${{ secrets.GITHUB_TOKEN }}
```

Створення Docker-образу із поточного контексту (.), його пуш в GHCR з тегом latest:

```
 - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ghcr.io/mikunajanari/bryzhyniuk_lb8:latest
```




