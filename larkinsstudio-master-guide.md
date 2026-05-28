# 🌿 Larkinsstudio — Мастер-гайд
### Полная документация: система, сайт, контент, бизнес
*Обновлено: май 2026*

---

## 🗺️ Общая картина — что построено

```
Instagram / Pinterest / YouTube Shorts
              ↓
    larkinsstudio.com (главная)
              ↓
    /free-pattern.html (лендинг)
              ↓
    beehiiv форма подписки
              ↓
    Welcome Email → ссылка на бесплатную схему 🍓
              ↓
    Человек в email-базе
              ↓
    Рассылка → анонс клуба Garden Primitives Club
              ↓
    Tribute подписка $5/мес → Resend → PDF схема
              ↓
    💰 Выплата 10-го и 25-го числа
```

---

## 🧩 Карта всех сервисов

| Сервис | Зачем | Где |
|--------|-------|-----|
| **Namecheap** | Домен larkinsstudio.com | namecheap.com |
| **GitHub** | Хранение кода сайта, автодеплой | github.com → репозиторий `larkinsstudio` |
| **Vercel** | Хостинг сайта + API вебхук | vercel.com → проект `tribute-webhook` |
| **Resend** | Автоотправка писем с PDF | resend.com |
| **Tribute** | Приём платежей, подписки | @tribute в Telegram |
| **beehiiv** | Email-рассылка, форма подписки | beehiiv.com |
| **Instagram** | Основная соцсеть | @larkinsstudio |
| **Pinterest** | Пины, трафик на сайт | pinterest.com/larkinsstudio |
| **YouTube** | Shorts, flosstube | youtube.com/@larkinsstudio |

---

## 📁 Два отдельных проекта — важно понимать

### Проект 1 — GitHub репозиторий `larkinsstudio`
- Хранит: `index.html`, `free-pattern.html`, `privacy-policy.html`, фото
- Автоматически деплоится на Vercel при каждом commit
- Редактировать: через браузер на github.com — карандаш ✏️ → Commit
- Добавить файл: Add file → Upload files → Commit

### Проект 2 — локальная папка `~/tribute-webhook`
- Хранит: `api/webhook.js`, `api/subscribe.js`, `public/downloads/`
- Деплоится вручную командой: `cd ~/tribute-webhook && npx vercel --prod`
- Здесь живёт логика: вебхук Tribute → отправка PDF покупателю

> ⚠️ Сайт управляется через GitHub. Вебхук и скачиваемые файлы — через tribute-webhook.

---

## 🌐 Структура сайта

| URL | Файл | Где лежит |
|-----|------|-----------|
| larkinsstudio.com | index.html | GitHub: larkinsstudio/index.html |
| larkinsstudio.com/free-pattern.html | free-pattern.html | GitHub: larkinsstudio/free-pattern.html |
| larkinsstudio.com/privacy-policy.html | privacy-policy.html | GitHub: larkinsstudio/privacy-policy.html |
| larkinsstudio.com/fox/ | fox/index.html | GitHub: larkinsstudio/fox/ |
| larkinsstudio.com/downloads/ | ZIP файлы схем | tribute-webhook/public/downloads/ |

---

## 📁 Структура tribute-webhook на компьютере

```
~/tribute-webhook/
  api/
    webhook.js       ← вебхук Tribute: получает оплату → шлёт PDF
    subscribe.js     ← API для формы подписки beehiiv
  public/
    downloads/
      cozy-reading-fox.zip   ← схема Лиса (платная)
      [новые схемы].zip      ← сюда добавлять новые
  package.json
  node_modules/
```

---

## 🔑 API ключи и переменные

| Ключ | Где найти | Где используется |
|------|-----------|-----------------|
| Resend API Key | resend.com → API Keys | Vercel env: `RESEND_API_KEY` |
| Tribute Webhook URL | @tribute → API | `https://tribute-webhook-six.vercel.app/api/webhook` |
| beehiiv Publication ID | beehiiv → Settings → API | `pub_ca4d885a-e858-4216-a60c-587cfdf664a5` |
| beehiiv Form ID | beehiiv → Forms → embed code | `012c2b53-50ab-45cf-8c8d-92fe8d980aa0` |

---

## 💰 Продукты и цены

| Продукт | Цена | Тип | Статус |
|---------|------|-----|--------|
| Cozy Reading Fox | $5-7 | Разовая покупка | ✅ Работает |
| Wild Strawberry | Бесплатно | Лид-магнит за подписку | 🔄 В процессе |
| Garden Primitives Club | $5/мес | Подписка | 🔄 Настроена в Tribute, вебхук не дописан |

---

## 📧 Email-воронка

### Как работает сейчас
1. Человек заходит на `larkinsstudio.com/free-pattern.html`
2. Вводит email → форма beehiiv принимает
3. beehiiv отправляет Welcome Email (настроен в beehiiv → Emails → Welcome Email)
4. В письме: ссылка на бесплатную схему земляники

### Что нужно ещё сделать
- Загрузить PDF земляники в `~/tribute-webhook/public/downloads/`
- Обновить ссылку в Welcome Email на реальный файл

---

## 🔄 Как обновить сайт (через GitHub)

```
1. Открой github.com → репозиторий larkinsstudio
2. Найди нужный файл → нажми карандаш ✏️
3. Внеси изменения
4. Нажми Commit changes
5. Vercel автоматически задеплоит за ~1 минуту
```

---

## 🔄 Как задеплоить tribute-webhook (терминал)

```bash
cd ~/tribute-webhook
npx vercel --prod
```

---

## ➕ Как добавить новый платный паттерн

**Шаг 1** — Подготовь ZIP архив (PDF + все файлы схемы)
```
Назови без пробелов: autumn-poppy.zip
Скопируй в: ~/tribute-webhook/public/downloads/
```

**Шаг 2** — Создай донат-ссылку в Tribute
```
@tribute → Создать → Фиксированная цена → Название точь-в-точь как будет в коде
Например: 🌸 Autumn Poppy: Cross Stitch Pattern 🍂
```

**Шаг 3** — Добавь в webhook.js
```javascript
// Открой ~/tribute-webhook/api/webhook.js
// Найди const PATTERNS = { и добавь:
'🌸 Autumn Poppy: Cross Stitch Pattern 🍂': {
  downloadUrl: 'https://larkinsstudio.com/downloads/autumn-poppy.zip',
  name: 'Autumn Poppy'
}
```

**Шаг 4** — Задеплой
```bash
cd ~/tribute-webhook && npx vercel --prod
```

---

## 🔄 Что ещё нужно сделать (незаконченное)

### Приоритет 1 — дописать подписочный клуб
Файл `api/subscribe.js` создан, но нужно добавить в `webhook.js` обработку событий подписки:
```
newSubscription    → прислать все архивные схемы + текущую
renewedSubscription → прислать схему текущего месяца
```
Tribute уже настроен с тарифом подписки $5/мес.

### Приоритет 2 — загрузить схему земляники
```bash
# Скопируй PDF в папку:
cp ~/Downloads/wild-strawberry.zip ~/tribute-webhook/public/downloads/
npx vercel --prod
```
Затем обнови ссылку в Welcome Email в beehiiv.

### Приоритет 3 — когда будет 300+ подписчиков Instagram
Открыть Etsy магазин (без VPN — напрямую или через удалённый сервер)

---

## 🌿 Контент-стратегия

### Платформы
| Платформа | Формат | Лучшее время |
|-----------|--------|--------------|
| Instagram | Reels 7-15 сек | 1:30 ночи (= 18:30 EST) |
| YouTube Shorts | 13-30 сек | То же время |
| Pinterest | Видео + фото пины | Со ссылкой на free-pattern.html |

### Лучший контент по статистике
- YouTube Shorts: 1500 просмотров, США 46%, женщины 100% ✅
- Instagram: пока слабее, skip rate 69% → нужно начинать с сильного кадра

### Правило первого кадра (Instagram)
Первые 0.5 секунды решают всё. Начинай с:
- Готовой вышивки крупно, ИЛИ
- Яркого текста на экране: "I design my own cross stitch patterns"
- НЕ с наброска карандашом

### Хэштеги (только 5 для Instagram)
```
#crossstitchersofinstagram #primitivecrossstitch #cottagecore #crossstitchpattern #freecrossstitch
```

---

## 📊 Комиссии и расходы

| Сервис | Стоимость |
|--------|-----------|
| Namecheap домен | ~$1/мес (~$12/год) |
| Vercel | Бесплатно |
| Resend | Бесплатно до 3000 писем/мес |
| beehiiv | Бесплатно до 2500 подписчиков |
| Tribute комиссия | 10% с каждого платежа |
| **Итого фиксированных расходов** | **~$1/мес** |

### Калькулятор клуба
| Подписчиков | Валовой доход | После Tribute −10% | После домена |
|-------------|---------------|---------------------|--------------|
| 20 | $100 | $90 | $89 |
| 50 | $250 | $225 | $224 |
| 100 | $500 | $450 | $449 |
| 200 | $1000 | $900 | $899 |

**Выплаты Tribute:** 10-го и 25-го числа месяца. Минимум для вывода: 100 EUR.

---

## 🚨 Что делать если что-то сломалось

### Сайт не открывается
```
1. Проверь DNS: Namecheap → Advanced DNS → A Record = 76.76.21.21
2. Подожди 30 минут (DNS обновляется медленно)
3. Проверь статус деплоя: vercel.com → tribute-webhook → Deployments
```

### Письма с PDF не приходят покупателям
```
1. Vercel логи: vercel.com → tribute-webhook → Logs
2. Resend логи: resend.com → Emails
3. Убедись что домен верифицирован: resend.com → Domains → larkinsstudio.com
4. Проверь Webhook URL в Tribute: https://tribute-webhook-six.vercel.app/api/webhook
```

### Случайно сломала что-то в коде
```bash
# Восстановить из GitHub (если файл в репозитории larkinsstudio):
# Открой файл в GitHub → History → выбери предыдущую версию → Restore

# Восстановить локальный файл tribute-webhook:
cp ~/tribute-webhook/public/index.html.backup ~/tribute-webhook/public/index.html
cd ~/tribute-webhook && npx vercel --prod
```

---

## 🌐 DNS записи Namecheap (НЕ ТРОГАТЬ)

| Type | Host | Value |
|------|------|-------|
| A Record | @ | 76.76.21.21 |
| CNAME | www | cname.vercel-dns.com |
| TXT | resend._domainkey | p=MIGfMA0GCS... (длинный ключ) |
| TXT | send | v=spf1 include:amazonses.com ~all |
| TXT | _dmarc | v=DMARC1; p=none; |
| MX | send | feedback-smtp.us-east-1.amazonses.com |

---

## 📱 Полезные ссылки

| Что | Ссылка |
|-----|--------|
| Сайт | https://larkinsstudio.com |
| Лендинг бесплатной схемы | https://larkinsstudio.com/free-pattern.html |
| Политика конфиденциальности | https://larkinsstudio.com/privacy-policy.html |
| Vercel проект | https://vercel.com/mishoricos-projects/tribute-webhook |
| GitHub репозиторий | https://github.com/Mishorico/larkinsstudio |
| Resend домены | https://resend.com/domains |
| beehiiv | https://app.beehiiv.com |
| Tribute | @tribute в Telegram |

---

## ✅ Итог: что сделано

### Техническая база
- ✅ Домен larkinsstudio.com (Namecheap)
- ✅ Хостинг и автодеплой (Vercel + GitHub)
- ✅ Автоматическая отправка PDF после оплаты (Resend + webhook.js)
- ✅ Вебхук Tribute настроен и работает
- ✅ Платная схема Cozy Reading Fox продаётся автоматически

### Сайт
- ✅ Главная страница с магазином
- ✅ Лендинг /free-pattern.html с формой подписки beehiiv
- ✅ Privacy Policy /privacy-policy.html
- ✅ Страница Cozy Reading Fox /fox/

### Email-маркетинг
- ✅ beehiiv подключён, форма на сайте работает
- ✅ Welcome Email настроен (нужно добавить ссылку на PDF земляники)

### Клуб Garden Primitives
- ✅ Тариф подписки $5/мес создан в Tribute
- 🔄 Вебхук для подписки (newSubscription / renewedSubscription) — нужно дописать
- 🔄 Архив схем для новых подписчиков — нужно организовать

### Контент и маркетинг
- ✅ Instagram @larkinsstudio — первые ролики опубликованы
- ✅ YouTube Shorts — 2 видео, хорошая статистика (1500+ просмотров)
- ✅ Pinterest — первые пины
- ✅ PDF паттерн Wild Strawberry с брендингом создан
- ✅ DMC Color Finder инструмент создан (можно добавить на сайт)

### Дизайн и паттерны
- ✅ Wild Strawberry нарисован и вышивается для теста
- ✅ Схема готова, PDF создан с полным брендингом Larkinsstudio
- 🔄 Серия Garden Primitives — 12 месяцев, 12 цветов — в плане

---

*🌿 Larkinsstudio — от наброска карандашом до автоматического магазина схем*
