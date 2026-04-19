# Лабораторная работа №3: CI/CD для статического сайта в SourceCraft

## 1. Цель работы
Изучение принципов автоматизации развертывания (CI/CD) статического сайта, построенного на движке MkDocs, с использованием платформ SourceCraft и GitHub Actions.

## 2. Задание
1. Реализовать сценарий автоматического развертывания статического сайта MkDocs на платформе SourceCraft.
2. Реализовать сценарий автоматического развертывания того же сайта с помощью GitHub Actions на GitHub Pages.
3. Настроить один локальный репозиторий для работы с двумя удаленными репозиториями (origin и sourcecraft).
4. Продемонстрировать результаты в виде работающих ссылок на сайты и репозитории.

## 3. Ход работы / Код

В ходе выполнения работы были выполнены следующие шаги:

### Шаг 1: Настройка GitHub Actions
Был создан файл `.github/workflows/deploy.yml` для автоматического деплоя в GitHub Pages при каждом пуше в ветку `main`.
```yml
name: Deploy MkDocs to GitHub Pages
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs mkdocs-material
      - run: |
          cd source
          mkdocs gh-deploy --force
```
### Шаг 2: Настройка CI/CD в SourceCraft
Был создан файл .sourcecraft/workflows/pages.yml для деплоя на платформе SourceCraft. Также в настройках организации был создан персональный токен (PAT) с правами Maintainer.
### Шаг 3: Настройка удаленных репозиториев
К локальному репозиторию был добавлен второй удаленный репозиторий с помощью команды:
git remote add sourcecraft https://<username>:<token>@git.sourcecraft.dev/afsaruddinsagor12/lab3-site.git
Шаг 4: Деплой
Код был отправлен в оба репозитория командами:
git push origin main
git push sourcecraft main

## 4. Выводы
В результате выполнения лабораторной работы был настроен процесс CI/CD, который позволяет автоматически обновлять статический сайт на двух разных хостингах одновременно.
**SourceCraft:**
*[SourceCraft static site](https://afsaruddinsagor12.sourcecraft.site/lab3-site/)
*[SourceCraft repository](https://sourcecraft.dev/afsaruddinsagor12/lab3-site)

**GitHub:**
* [GitHub static site(GitHub Pages)](https://sagorgit.github.io/)
* [GitHub repository](https://github.com/sagorgit/sagorgit.github.io)

