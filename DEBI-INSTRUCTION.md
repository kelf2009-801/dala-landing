# 🛠️ Инструкция для Debi: Как делать лендинги правильно

От: CJ (Grove Street Families)
Кому: Debi

---

## Твой лендинг vs правильный — разбор ошибок

### ❌ Что не так на твоём шиномонтаже:

1. **Эмодзи на кнопках** — `📞 Записаться`, `⚡ Записаться онлайн`. Андрей жёстко запретил эмодзи. Только SVG-иконки.
2. **Нет картинок** — голый текст. Для шиномонтажа нужны реальные фото: мастерская, колёса, станки.
3. **FAQ на кнопках вместо `<details>`** — некрасиво, нет анимации раскрытия.
4. **ВСЕ ЗАГОЛОВКИ КАПСОМ** — кричит. Используй обычный регистр + accent-цвет.
5. **Куча "Записаться →" ссылок** — выглядит как спам. Одна CTA-кнопка в hero, одна в конце.
6. **Нет карточек** — услуги должны быть в карточках с картинками и ценами.
7. **Нет анимаций** — лендинг мёртвый. Нужен GSAP + ScrollTrigger.
8. **Бедная цветовая палитра** — нет индустриального стиля.
9. **Нет меню в хедере** — пользователь не понимает структуру сайта.
10. **Нет кнопки "Наверх"** — на длинных страницах обязательно.

---

## ✅ Правильный процесс создания лендинга

### Шаг 1: Загрузи скилл `dala-landing`
```
skill_view(name="dala-landing")
```
Там вся архитектура: визуальные эффекты, цвета, структура, адаптив.

### Шаг 2: Сгенерируй картинки через `image_generate`
```
image_generate(prompt="реалистичное фото...", aspect_ratio="landscape")
```
- НИКОГДА не пиши "no text, no watermark" — это не помогает.
- Вместо этого пиши на английском: "photo of... realistic, natural lighting, professional".
- После генерации ОБЯЗАТЕЛЬНО проверь через `vision_analyze` — нет ли на картинке AI-текста.
- Конвертируй в .webp через ffmpeg:
  ```
  ffmpeg -y -i input.png -vf "scale=1200:-1" -q:v 75 output.webp
  ```
- Размер должен быть 40-60KB. Не 1.8MB!

### Шаг 3: Структура лендинга (10 секций)
```
1. NAV — логотип, меню (3-4 ссылки), CTA-кнопка
2. HERO — картинка на фоне, заголовок H1 (до 6 слов), подзаголовок, 2 кнопки
3. FEATURES — 3-4 карточки преимуществ с SVG-иконками
4. OFFER — главное предложение с буллетами
5. MENU/SERVICES — 4-6 карточек с картинками, текстом, ценой
6. FAQ — 5 вопросов через <details> + <summary>
7. FINAL CTA — заголовок + 2 кнопки
8. FOOTER — контакты, навигация
9. SCROLL-TOP — кнопка "Наверх" справа
```

### Шаг 4: Цвета — бери из `dala-landing`
Для индустриального стиля:
```css
--steel: #1a1d23;       /* фон */
--graphite: #2d3038;    /* карточки */
--metal: #3a3e48;       /* границы */
--accent: #f59e0b;      /* акцент (янтарный) */
--white: #e8eaed;       /* текст */
```

### Шаг 5: Эффекты — ОБЯЗАТЕЛЬНО
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
```
- Reveal-анимации: `.reveal { opacity:0; transform:translateY(40px) }` + GSAP
- CTA-пульсация: `@keyframes cta-pulse`
- Hover карточек: `transform: translateY(-4px)`
- НЕ используй Lenis — он душит скролл

### Шаг 6: Мобильная версия
```css
@media(max-width:768px){
  .hero__cta{flex-direction:column}  /* кнопки в столбик */
  .nav__links{display:none}           /* меню скрыто */
  .menu__grid{grid-template-columns:1fr}  /* карточки в 1 колонку */
}
```

### Шаг 7: Карточки услуг
```css
.menu-card{display:flex;flex-direction:column}
.menu-card__body{flex:1;display:flex;flex-direction:column}
.menu-card__price{margin-top:auto}  /* цена всегда внизу! */
```
Цена должна быть в одну линию на всех карточках!

### Шаг 8: Пуш на GitHub
```bash
git add . && git commit -m "описание" && git push origin main
```
Ссылка: `https://kelf2009-801.github.io/REPO/landing.html?v=1`

---

## 🔥 Чек-лист перед заливкой

- [ ] НИ ОДНОГО эмодзи — только SVG-иконки
- [ ] Все картинки .webp, 40-60KB
- [ ] На картинках нет AI-текста
- [ ] Цены в одну линию на карточках
- [ ] FAQ через `<details>` (не кнопки)
- [ ] GSAP reveal-анимации
- [ ] Кнопка "Наверх" справа (появляется при скролле)
- [ ] Mobile-first: кнопки в столбик на телефоне
- [ ] Меню в хедере (скрыто на мобиле)
- [ ] Цвета без AI-шного неона
- [ ] Заголовки НЕ капсом
- [ ] Одна главная CTA, не спам-ссылки
- [ ] Проверено на телефоне

---

## 📁 Файлы для референса

Посмотри как сделано правильно:
- `D:\Hermes_Projects\hermes-builds\cargo-landing.html` — грузоперевозки
- `D:\Hermes_Projects\hermes-builds\tire-landing.html` — шиномонтаж
- `D:\Hermes_Projects\hermes-builds\na-ogne-landing.html` — гриль-бар

Скилл: `dala-landing` (загрузи через `skill_view`)

---

CJ, глава Grove Street Families 🔥