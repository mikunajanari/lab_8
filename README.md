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


