# Публикация на GitHub Pages (бесплатно)

Адрес после публикации: **https://megurte.github.io/**

GitHub Pages для «пользовательского» сайта требует ровно одно: публичный репозиторий с именем `<логин>.github.io`, у которого `index.html` лежит в корне ветки `main`. Никакой сборки, никаких GitHub Actions, домен и HTTPS бесплатные.

## 1. Создать репозиторий

1. Открыть https://github.com/new
2. Repository name: `megurte.github.io` (имя должно совпадать буква в букву)
3. Public
4. Ничего не добавлять (README, .gitignore, лицензия) — папка уже собрана локально
5. Create repository

## 2. Залить папку

Из папки `E:\Gamejam\megurte.github.io`:

```bash
git init -b main
git add .
git commit -m "links page"
git remote add origin https://github.com/megurte/megurte.github.io.git
git push -u origin main
```

## 3. Включить Pages

Settings → Pages → Build and deployment:

- Source: **Deploy from a branch**
- Branch: **main**, folder **/ (root)**
- Save

Первый деплой занимает 1–10 минут, ход виден во вкладке Actions (workflow `pages build and deployment`). Потом страница живёт на https://megurte.github.io/.

## 4. Обновлять

Правишь `index.html` / `style.css` → commit → push. Через минуту-две страница обновится. Если браузер показывает старую версию — Ctrl+F5.

```bash
git add . && git commit -m "update links" && git push
```

## 5. Свой домен (необязательно, платно)

Если когда-нибудь захочется адрес вроде `megurt.dev` (домен покупается отдельно, ~10–15 $/год; сама публикация на Pages остаётся бесплатной):

1. В корень репозитория положить файл `CNAME` с одной строкой: `megurt.dev`
2. У регистратора домена прописать DNS:
   - четыре записи `A` на `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - (по желанию) четыре `AAAA` на `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - `CNAME` для `www` → `megurte.github.io`
3. Settings → Pages → Custom domain: `megurt.dev` → Save, дождаться зелёной галочки DNS check, включить **Enforce HTTPS**

Зона `.dev` работает только по HTTPS, Pages выдаёт сертификат сам.

## Файлы

- `index.html` — разметка, ссылки, иконки (инлайновый SVG), описания кнопок
- `style.css` — палитра (`:root`), рисованные кнопки, акварельные капли
- `.nojekyll` — отключает обработку Jekyll на стороне GitHub (для чистого HTML она не нужна)

Что править чаще всего:

- **добавить ссылку** — скопировать любой блок `<a class="link ...">` в `index.html`, поменять `href`, `label`, `desc`, класс `tint-*` для цвета
- **цвета** — переменные в `:root` в `style.css`; капли фона задаются в `index.html` через `--c: R G B` у каждого `.drop`
- **аватар** — файл `avatar.jpg` рядом с `index.html` (квадрат 400×400, страница сама скругляет); чтобы сменить, просто заменить файл. Исходник `avatar-source.png` лежит рядом, но через `.gitignore` в репозиторий не попадает
- **подпись под именем** — `<p class="tagline">`
