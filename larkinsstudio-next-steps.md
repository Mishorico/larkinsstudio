# 🌿 Larkinsstudio — Что делать дальше
### Приоритетный план действий · май 2026

---

## 🚨 ПРЯМО СЕЙЧАС (сегодня-завтра)

### 1. Починить картинки на главной странице
Проблема: tribute-webhook не видит картинки из GitHub.
Решение — запусти в терминале:
```bash
curl -o ~/tribute-webhook/public/straw-stitched.jpg https://raw.githubusercontent.com/Mishorico/larkinsstudio/main/straw-stitched.jpg
curl -o ~/tribute-webhook/public/strawberry-sampler.jpg https://raw.githubusercontent.com/Mishorico/larkinsstudio/main/strawberry-sampler.jpg
cd ~/tribute-webhook && npx vercel --prod
```
**После** — проверь что главная страница выглядит нормально.

### 2. Дошить землянику + фотосет
- Дошить Wild Strawberry
- Сделать фотосет: готовая работа в пяльцах, на деревянном фоне, с мулине рядом
- Лучший кадр → обложка free-pattern.html (заменить заглушку)
- Тот же лучший кадр → страница клуба

---

## 📸 ПОСЛЕ ФОТОСЕТА

### 3. Обновить free-pattern.html (лендинг бесплатной схемы)
- Загрузить фото готовой вышивки в GitHub
- Заменить заглушку `[ Add photo of finished embroidery here ]` на реальное фото
- Как: GitHub → free-pattern.html → карандаш → найти заглушку → заменить на `<img src="/имя-фото.jpg">`

### 4. Добавить PDF земляники на сайт
```bash
# Скопируй PDF в папку:
cp ~/Downloads/wild-strawberry.zip ~/tribute-webhook/public/downloads/
cd ~/tribute-webhook && npx vercel --prod
```
Затем в beehiiv → Emails → Welcome Email → обнови ссылку на реальный файл.

### 5. Опубликовать ролик с готовой вышивкой
- Финальный reveal ролик: процесс → готовая вышивка
- Instagram + YouTube Shorts + Pinterest
- Текст: *"The free pattern is now available — link in bio 🍓"*

---

## 🌲 WOODLAND PRIMITIVES CLUB (создаём вместе)

### 6. Создать страницу клуба
Новая страница `larkinsstudio.com/club.html`:
- Описание клуба и что входит в подписку
- Галерея зверей (по мере создания)
- Кнопка подписки через Tribute
- $5/мес · новый паттерн каждый месяц · доступ к архиву

### 7. Создать тариф подписки в Tribute
- @tribute → Создать подписку → "Woodland Primitives Club — $5/мес"
- Это отдельный тариф от разовых покупок

### 8. Дописать webhook.js для подписки
Добавить три обработчика событий:
```
newSubscription     → письмо со ВСЕМИ схемами архива
renewedSubscription → письмо с паттерном текущего месяца  
cancelledSubscription → ничего не слать
```
Мы сделаем это вместе — ты просто запустишь команды в терминале.

### 9. Создать структуру архива
```bash
mkdir ~/tribute-webhook/public/downloads/club
# Потом добавлять файлы:
# month-01-hedgehog.zip
# month-02-rabbit.zip
# и т.д.
```

### 10. Нарисовать первого зверя
Серия Woodland Primitives · cottagecore folk art:
- Ёж с грибом · Кролик · Лиса · Медведь · Мышка
- Сова · Белка · Олень · Утка · Барсук
Рисуем карандашом → схема → вышиваем тест → PDF пакет

---

## 🔧 ТЕХНИЧЕСКАЯ ПРОБЛЕМА (решить один раз)

### 11. Синхронизировать GitHub и tribute-webhook
Сейчас: два проекта конфликтуют — GitHub деплоит одно, CLI деплоит другое.
Нужно решить раз и навсегда чтобы не терять картинки.

**Вариант** — один bash скрипт который синхронизирует всё:
```bash
# Сохранить как ~/deploy.sh
curl -o ~/tribute-webhook/public/index.html https://raw.githubusercontent.com/Mishorico/larkinsstudio/main/index.html
curl -o ~/tribute-webhook/public/straw-stitched.jpg https://raw.githubusercontent.com/Mishorico/larkinsstudio/main/straw-stitched.jpg
cd ~/tribute-webhook && npx vercel --prod
```
Запускать как: `bash ~/deploy.sh` — и всё синхронизируется автоматически.

---

## 📊 РОСТ АУДИТОРИИ (параллельно)

### Правило контента
- **Минимум 3 ролика в неделю** пока база маленькая
- Начинай каждый ролик с сильного кадра (готовая вышивка или яркий текст)
- Дублируй каждый Instagram ролик на YouTube Shorts и Pinterest

### Когда запускать клуб
- Не раньше чем 50 человек в email-базе beehiiv
- Проверить базу: beehiiv → Audience → Subscribers

### Milestones
| Цель | Что делать |
|------|-----------|
| 50 email подписчиков | Анонсировать клуб |
| 100 email подписчиков | Первый SAL для подписчиков |
| 300 Instagram подписчиков | Открыть Etsy |
| 100 платных клуб | $450/мес стабильно |

---

## 📋 СТАНДАРТНЫЕ КОМАНДЫ — шпаргалка

```bash
# Синхронизировать и задеплоить (использовать ВСЕГДА вместо просто vercel)
curl -o ~/tribute-webhook/public/index.html https://raw.githubusercontent.com/Mishorico/larkinsstudio/main/index.html && cd ~/tribute-webhook && npx vercel --prod

# Добавить новый файл в downloads
cp ~/Downloads/имя-файла.zip ~/tribute-webhook/public/downloads/
cd ~/tribute-webhook && npx vercel --prod

# Посмотреть логи
npx vercel logs https://larkinsstudio.com --limit 20

# Восстановить сайт из GitHub (если что-то сломалось)
# Просто сделай любое изменение в GitHub → Commit → автодеплой исправит
```

---

## ✅ Что уже готово (не трогать)

- ✅ Домен larkinsstudio.com
- ✅ Автодеплой GitHub → Vercel
- ✅ Вебхук Tribute → работает (проверено 28 мая)
- ✅ Автоотправка PDF при покупке (Resend)
- ✅ beehiiv форма на free-pattern.html
- ✅ Welcome Email настроен (нужна ссылка на PDF)
- ✅ Privacy Policy на сайте
- ✅ PDF паттерн Wild Strawberry с брендингом
- ✅ Тариф подписки Tribute создан

---

*Следующий большой шаг: фотосет земляники → лендинг → анонс → первые подписчики 🍓*
