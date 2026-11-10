# Денис Сытиков — сайт-визитка WAF / AppSec

Одностраничный сайт-визитка по профессиональному резюме: инженер по защите
веб-приложений (WAF) / AppSec, 27 лет в ИТ, 12+ лет в информационной безопасности.

**Сайт:** https://dsytikov.github.io/ (после публикации)

## Что внутри

| Файл | Назначение |
| --- | --- |
| `index.html` | Весь сайт: встроенные CSS и JS, без внешних зависимостей и шрифтов |
| `resume.pdf` | PDF-резюме для кнопки «Скачать резюме» |
| `publish.ps1` | Публикация в GitHub Pages через REST API (git и gh не нужны) |
| `.nojekyll` | Отключает обработку Jekyll на GitHub Pages |
| `README.md` | Это описание репозитория |

## Содержание сайта

- первый экран: имя, специализация, ключевые технологии, статус поиска работы;
- «Обо мне»: путь в ИТ и ИБ, чем занимаюсь сейчас, принципы работы;
- «Опыт работы»: 11 записей с раскрывающимися подробностями и тегами технологий;
- «Навыки и инструменты»: 6 категорий;
- «Образование и сертификаты»: вуз и вендорские сертификаты Positive Technologies;
- «Контакты»: почта, Telegram, телефон, локация и формат работы.

## Локальный просмотр

```powershell
Start-Process .\index.html
```

## Публикация на GitHub Pages

Нужен GitHub-токен: classic PAT со scope `repo` или fine-grained PAT с правами
`Contents: Read and write`, `Administration: Read and write`, `Pages: Read and write`.

```powershell
$env:GITHUB_TOKEN = "ghp_..."
.\publish.ps1                      # репозиторий dsytikov.github.io → https://dsytikov.github.io/
.\publish.ps1 -Repo site           # репозиторий site → https://dsytikov.github.io/site/
.\publish.ps1 -Owner <login> -Repo <repo>
```

Скрипт создаёт публичный репозиторий (если его нет), загружает файлы в ветку
`main`, включает GitHub Pages с источником «ветка `main`, папка `/ (root)`» и
печатает ссылки. Первая сборка занимает 1–3 минуты.

### Вручную, если есть git

```bash
git init -b main
git add index.html resume.pdf README.md .nojekyll
git commit -m "Publish personal site"
git remote add origin https://github.com/<owner>/<repo>.git
git push -u origin main
```

Затем: **Settings → Pages → Build and deployment → Source: Deploy from a branch →
Branch: main, folder: / (root) → Save**.

### Совсем без инструментов и токена

1. Создайте на github.com публичный репозиторий `dsytikov.github.io`.
2. Нажмите **Add file → Upload files** и перетащите `index.html`, `resume.pdf`,
   `README.md` и `.nojekyll` в корень; **Commit changes**.
3. **Settings → Pages → Source: Deploy from a branch → Branch: main, папка / (root) → Save**.
4. Через 1–3 минуты сайт откроется по адресу `https://dsytikov.github.io/`.

## Технические детали

- один файл `index.html`, CSS и JS встроены, внешних запросов нет;
- адаптивность: контрольные точки 980 / 820 / 560 px, проверено на 390 и 1440 px;
- доступность: семантическая разметка, `aria`-атрибуты, видимый фокус,
  поддержка `prefers-reduced-motion`, данные не скрываются без JavaScript;
- контент без анимационных зависимостей: страница читается при отключённом JS.

## Приватность

`resume.pdf` и контакты в `index.html` содержат персональные данные (телефон,
почта, Telegram, город). Всё это публикуется открыто. Если что-то не нужно на
публичном сайте — удалите соответствующий файл/блок и запустите `publish.ps1`
ещё раз.
