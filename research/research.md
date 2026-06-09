# Research — TrackOn

Зведення ресерчу для застосунку трекінгу часу для фрілансерів.
Контекст продукту (аудиторія, цілі, модель даних) — у [`../CLAUDE.md`](../CLAUDE.md).
Стан: червень 2026. Наочна версія — [`research.html`](./research.html).

**Правила цитування:** кожен зовнішній факт має посилання на джерело або скрін у
[`screens/`](./screens/). `[?]` = не підтверджено цим ресерчем (не вигадано).
`[оцінка]` = власна експертна інтерпретація, а не зовнішній факт.

---

## 1. КОНКУРЕНТИ

### 1.1 Матриця за осями
Осі: основа продукту · ключовий механізм · звіти · монетизація.

| Продукт | Основа | Ключовий механізм | Звіти | Монетизація | Джерело |
|---|---|---|---|---|---|
| **Harvest** | «Години → прибуток» для сервісних бізнесів і фрілансерів; час + білінг | Live-таймер **+ ручне введення** (day/week view) | Бюджети, capacity, cost; client-facing звіти | Per-seat: Free (1 seat, 2 проєкти) / Teams **$9** / Enterprise **$14** за seat/міс | [features](https://www.getharvest.com/features), [pricing](https://www.getharvest.com/pricing); скрін `harvest-home.png` |
| **Clockify** | Трекер часу й таймшити; команди + фрілансери | Timer + тижневий timesheet + calendar + auto-tracker + kiosk | Time / activity / rate / profit; бюджети; CSV-експорт | Freemium per-seat; **free урізано у 2026** (billable, CSV, private projects → платні) | [clockify.me](https://clockify.me/); free-cut: [TallyHo](https://tallyho.app/blog/the-best-time-tracking-apps-for-freelancers-in-2025); скрін `clockify-home.png` |
| **Paymo** | Інтегрований **проєкт-менеджмент** (таски + час + інвойси); Клієнт→Проєкт | Web/desktop/mobile + **Paymo Track** (авто-захват активності) | Прибутковість: маржа проєкту, profitability по клієнту | Per-seat: Free (1/1/2) / Solo **$5.90** / Plus **$10.90** / Pro **$16.90** | [paymoapp.com](https://www.paymoapp.com/), [pricing](https://www.paymoapp.com/pricing/); скрін `paymo-home.png` |
| **TimeCamp** | AI workforce mgmt для прибутковості; ставки/білабельність | One-click timer + авто-моніторинг + **AI-агент (TIC)**, що сам заповнює таймшит | Real-time дашборди, productivity, labor cost, BI, export | Freemium: **Free необмежені користувачі/проєкти** / $3.99 / $6.99 / $9.99 за user; AI ~$6 | [timecamp.com](https://www.timecamp.com/); скрін `timecamp-home.png` |
| **Timely** | «Таймшит, що пише себе сам» — автоматичний AI-трекінг | **Memory Tracker** (фоновий захват) + **AutoSheet** (AI-чернетка, 1-click) | Work analytics: people/project dashboards, utilization, billable vs non | Per-seat підписка; **ціни не публічні на лендингу `[?]`** | [timely.com/features](https://www.timely.com/features); скрін `timely-home.png` |

### 1.2 Три спільні патерни ринку
1. **Час монетизується через гроші** — усі мають білабельні ставки + інвойси/прибутковість.
   ([Harvest](https://www.getharvest.com/features), [Clockify](https://clockify.me/),
   [Paymo](https://www.paymoapp.com/), [TimeCamp](https://www.timecamp.com/),
   [Timely](https://www.timely.com/features))
2. **Рух до зниження тертя вводу** — auto-tracker (Clockify, Paymo, TimeCamp) і
   AI-перший підхід (Timely, TimeCamp). (ті ж джерела;
   [Jobbers огляд](https://www.jobbers.io/best-time-tracking-apps-for-freelancers-2026-toggl-vs-harvest-vs-clockify-compared/))
3. **Freemium з per-seat апселом** — безкоштовний вхід → платні per-seat тарифи.
   (pricing-сторінки Harvest / Paymo / TimeCamp вище)

### 1.3 Три відмінності
1. **Філософія вводу:** Harvest/Clockify — таймер-перші; Timely — AI-перший;
   TimeCamp — гібрид з AI-агентом. (джерела продуктів вище)
2. **Широта продукту:** Paymo — повний PM (таски, Gantt); Harvest/Timely — вузько
   час+білінг; Clockify/TimeCamp — час + моніторинг продуктивності.
3. **Модель free:** TimeCamp — необмежені користувачі безкоштовно; Harvest/Paymo —
   жорсткі ліміти (1 seat / 2 проєкти); Clockify — урізав free у 2026
   ([TallyHo](https://tallyho.app/blog/the-best-time-tracking-apps-for-freelancers-in-2025)).

---

## 2. БЕНЧМАРК — вимір «таймшит, що пише себе сам»

Один вимір: автоматичний AI-трекінг, мінімум тертя. Продукти, де це ядро:
[Rize](https://rize.io/), [Timely](https://www.timely.com/features),
[Memtime](https://memtime.com/), [RescueTime](https://www.rescuetime.com/),
[TimeCamp](https://www.timecamp.com/).
Оцінки 1–5 `[оцінка]` (інтерпретація публічних описів, без hands-on; блог
[rize.io](https://rize.io/blog/best-automated-time-tracking-software) упереджений —
враховано): середнє Rize **4.4**, Timely **4.4**, RescueTime/TimeCamp **3.75**, Memtime **3.6**.
Повна таблиця критеріїв — у git-історії / [`research.html`](./research.html) §06.

### Топ-3 механізми для нашого MVP
1. **One-tap confirm замість форм.** Зупинка таймера → запис передзаповнений (останній/
   найчастіший проєкт, ставка) → підтвердження в 1 тап.
   *Звідки:* Timely **AutoSheet** — «one click, done-for-you timesheets»
   ([timely.com/features](https://www.timely.com/features)).
   *Чому нам:* прямо реалізує ціль «1–2 тапи» з [CLAUDE.md](../CLAUDE.md).
2. **Idle-detection + чесне підрізання.** «Тебе не було 20 хв — обрізати?».
   *Звідки:* Memory/Memtime таймлайн активності ([memtime.com](https://memtime.com/)).
   *Чому нам:* реалізовно клієнтськи у PWA через Page Visibility API `[?]` (точну поведінку
   в фоні треба перевірити), без бекенду й без стеження.
3. **Локальна пам'ять контексту для підказок.** Підказати проєкт за часом доби/останнім
   записом, «продовжити з місця».
   *Звідки:* ML-патерни Rize/Timely ([rize.io](https://rize.io/)).
   *Чому нам:* легка локальна частотна модель лягає на local-first ([CLAUDE.md](../CLAUDE.md)),
   без важкого AI.

### Що НЕ спрацює
**Повний фоновий auto-capture апок/сайтів/доків** (суть Rize/Timely:
[rize.io](https://rize.io/), [timely.com](https://www.timely.com/features)).
*Чому:* mobile-first **PWA в пісочниці браузера не має доступу** до нативних застосунків/
файлів і не працює у фоні постійно; вимагає нативного агента + хмари, що суперечить
local-first/без-бекенду MVP ([CLAUDE.md](../CLAUDE.md)). На мобільному вебі тривалий
фоновий моніторинг неможливий `[?]` (точні ліміти залежать від платформи). Висновок —
архітектурне обмеження, не маркетинг.

---

## 3. ПАТЕРНИ — обраний механізм старту

Розглянуто 5 принципово різних патернів старту (плитки · глобальна Start/Stop ·
natural-language · resume з історії · calendar-drag). Приклади продуктів —
ілюстративні, з загального знання, не верифіковані цим ресерчем `[?]`.

### Обрано: **Плитки-проєкти (launchpad)**
Сітка кнопок-проєктів; тап = миттєвий старт таймера для проєкту.

**Чому саме він під наш контекст ([CLAUDE.md](../CLAUDE.md)):**
1. **Mobile-first + ціль «1–2 тапи».** Плитка — буквально один тап великим пальцем;
   прямо реалізує головний принцип швидкості.
2. **Масштаб фрілансера.** Аудиторія веде жменю активних проєктів → сітка лишається
   компактною, тож умова поломки патерну (десятки проєктів) у нас не настає.
3. **Прямий мапінг на модель даних.** Плитки = `Project` (є `project.color`); тап →
   `TimeEntry(projectId, source:'timer')`; проєкт несе `currency` + `hourlyRate` →
   гроші фіксуються на старті; «один активний таймер» лягає природно (тап іншої = switch).

**Другий, за умови X:** Resume з історії — X = коли є історія / для щоденно повторюваних
проєктів (надбудова над launchpad; продовжує механізм «локальна пам'ять контексту», §2).
**Не підходить:** Calendar/timeline-drag — суперечить mobile-first (дрібний drag) і швидкому
старту (парадигма планування). Natural-language лишаємо як **вторинний** ручний ввід.

---

## 4. ВИСНОВКИ — gaps і гіпотези

### Gaps (незакриті місця)
- **G1. Mobile-first як позиція.** Усі 5 конкурентів — desktop/web-перші, мобільне як
  додаток (їхні лендинги десктоп-орієнтовані: скріни `screens/*.png`; якість їхніх
  мобільних застосунків окремо не тестувалась `[?]`).
- **G2. Автоматизм vs простота.** Ринок іде в auto/AI-трекінг (§2), але це недоступно у PWA.
- **G3. Глибина білінгу.** Конкуренти мають вбудовані платежі (Stripe/PayPal у Harvest:
  скрін `harvest-home.png`); наш MVP — лише PDF + статуси.
- **G4. Деградація free у конкурентів.** Clockify урізав free у 2026
  ([TallyHo](https://tallyho.app/blog/the-best-time-tracking-apps-for-freelancers-in-2025));
  Harvest/Paymo жорстко лімітують.

### Гіпотези (якщо / то / бо [дані])
- **H1.** **Якщо** стартовий екран = сітка плиток-проєктів (1 тап), **то** час до старту
  трекінгу впаде до 1–2 тапів, **бо** ціль і аудиторія в [CLAUDE.md](../CLAUDE.md) вимагають
  швидкості, а патерн-фіт обґрунтовано в §3 (приклад «one-tap у лідерів» — `[?]`, не верифіковано).
- **H2.** **Якщо** зробити по-справжньому mobile-first, **то** отримаємо незайнятий простір,
  **бо** всі 5 конкурентів desktop/web-перші (G1; скріни `screens/*.png`). Ризик: потрібен
  аналіз їхніх мобільних застосунків для підтвердження `[?]`.
- **H3.** **Якщо** замість auto-capture дати «1-tap confirm + idle-trim + локальні підказки»,
  **то** збережемо простоту й ~80% відчуття автоматизму, **бо** ринок рухається до зниження
  тертя (Timely AutoSheet, TimeCamp TIC — §2), а повний auto-capture у PWA недоступний (G2).
- **H4.** **Якщо** в MVP лишити інвойс = PDF + статуси (1 валюта), **то** покриємо базову
  потребу білінгу, **бо** всі конкуренти монетизують зв'язок час→інвойс (§1.2 п.1); вбудовані
  платежі — поза MVP, момент додавання відкритий `[?]` (G3).
- **H5.** **Якщо** позиціонувати як простий локальний інструмент для одного фрілансера,
  **то** виграємо на тлі деградації free у конкурентів, **бо** Clockify урізав free у 2026,
  а Harvest/Paymo лімітують 1 seat / 2 проєкти (G4; pricing-джерела §1.1).

---

## Додаток — скріни та джерела

### Скріни (публічні лендинги, headless Chrome) — [`screens/`](./screens/)
`harvest-home.png` · `harvest-features.png` · `clockify-home.png` · `paymo-home.png` ·
`timecamp-home.png` · `timely-home.png`.
**Не знято `[?]`** (за логіном, нема акаунтів): in-app екрани кожного продукту
(таймер, dashboard, reports, форма інвойсу).

### Зовнішні джерела
Сайти: getharvest.com · clockify.me · paymoapp.com · timecamp.com · timely.com ·
rize.io · memtime.com · rescuetime.com.
Огляди: [TallyHo](https://tallyho.app/blog/the-best-time-tracking-apps-for-freelancers-in-2025) ·
[Jobbers](https://www.jobbers.io/best-time-tracking-apps-for-freelancers-2026-toggl-vs-harvest-vs-clockify-compared/) ·
[Connecteam](https://connecteam.com/clockify-vs-harvest/) ·
[Toggl blog](https://toggl.com/blog/clockify-vs-harvest) ·
[Rize (упереджений)](https://rize.io/blog/best-automated-time-tracking-software) ·
[Timing](https://timingapp.com/blog/rescuetime-alternatives/) ·
[Digital PM](https://thedigitalprojectmanager.com/tools/best-ai-time-tracking-software/).
