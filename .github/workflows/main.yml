name: CI/CD Pipeline

on:
  push:
    branches:
      - main
      - development
      - release
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout репозитория
        uses: actions/checkout@v4

      - name: Установка Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.11'

      - name: Установка зависимостей
        run: |
          pip install pytest  # Установка pytest

      - name: Запуск тестов
        run: |
          python -m pytest  # Запуск тестов

  generate_docs:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout репозитория
        uses: actions/checkout@v4

      - name: Генерация документации
        run: |
          mkdir -p docs
          echo "## Документация проекта" > docs/index.md
          echo "Документация обновлена автоматически" >> docs/index.md

      - name: Коммит и пуш обновленной документации
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "github-actions@github.com"
          git add docs/
          git commit -m "Автоматическое обновление документации"
          git push origin release || echo "Нет изменений для коммита"

  deploy:
    needs: generate_docs
    runs-on: ubuntu-latest
    steps:
      - name: Деплой приложения
        run: echo "Развертывание приложения..."
