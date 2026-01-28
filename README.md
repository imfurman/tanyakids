# Таня — частная няня (Hugo)

SEO-first статический сайт для услуг частной няни в Варне. Контент полностью рендерится на сервере Hugo (без SPA и JS‑рендера). Основной домен: `https://tanyakids.com`.

## Локальный запуск

1) Установите Hugo Extended.
2) Запустите сервер:

```bash
hugo server -D
```

Сайт будет доступен по адресу `http://localhost:1313/`.

## Деплой на GitHub Pages

Деплой выполняется GitHub Actions workflow: `.github/workflows/hugo.yml`.

- Триггер: push в `main` или ручной запуск `workflow_dispatch`.
- Во время сборки используется `configure-pages` и `hugo --baseURL`.

## Структура URL

```
/
/about/
/services/
/prices/
/contact/
/varna/
/varna/pochasovo/
/varna/na-vecher/
/varna/polnyy-den/
```

## Как добавить новый город

1) Создайте папку `content/<город>/`.
2) Добавьте файл `content/<город>/_index.md` с локальным контентом и SEO-полями.
3) Скопируйте структуру услуг:

```
content/<город>/pochasovo.md
content/<город>/na-vecher.md
content/<город>/polnyy-den.md
```

4) Обновите ссылки на город в нужных местах (например, на главной и в `content/services.md`).

## Как добавить новую услугу

1) Создайте новую страницу услуги в нужном городе, например:

```
content/varna/noch.md
```

2) В front matter добавьте:

- `seo_title`, `seo_description`, `h1`
- `schema: ["Service", "FAQPage"]`
- `service_name`, `service_description`
- `faq` (список вопросов и ответов)

3) Добавьте ссылку на услугу в `content/services.md` и в локальной странице города.

## Где менять контакты

Контакты находятся в `hugo.toml`:

- `params.phone`
- `params.email`
- `params.address`

## Файлы и папки

- `layouts/` — шаблоны Hugo, SEO head, schema.org, FAQ.
- `content/` — все страницы сайта.
- `static/` — статические файлы (robots.txt, CSS, иконки).

## Примечания по SEO

- Для каждой страницы задан уникальный `title`, `description`, `H1`.
- Включены OpenGraph и Twitter Cards.
- Schema.org добавляется через `layouts/partials/schema.html`.
- Sitemap генерируется автоматически Hugo (`/sitemap.xml`).
