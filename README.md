# Gadget Hub

Курсовой интернет-магазин гаджетов: React-фронтенд и Express-бэкенд по макетам из `docs/templates/`.

## Запуск

Нужны Node.js 18+ и npm.

```bash
npm install
npm install --prefix server
npm install --prefix client
npm run dev
```

Остановка: в том же терминале **Ctrl+C**. Если процесс ушёл в фон — `kill` по PID из `npm run dev`.

- фронтенд: http://localhost:3000
- API: http://localhost:8080

Перед стартом скопируйте `.env.example` в `.env` и задайте `SESSION_SECRET`.

Учётная запись для демо: **student** / **gadget123**. Можно зарегистрировать нового пользователя.

## Что сделано

- Страницы: главная, логин / регистрация, каталог, корзина / история заказов
- Сессия на бэкенде (`POST /api/register`, `POST /api/login`, `POST /api/logout`, `GET /api/me`)
- Гость не может положить товар в корзину — показывается уведомление
- Статусы заказа считаются по загруженности магазина и меняются со временем
- Телефон проверяется как российский номер
- Товары из `server/data/goods.json` (`GET /api/goods`)
- Заказы в `server/data/orders.json` (`GET/POST /api/orders`, `DELETE /api/orders/:number` с причиной отмены)
- Корзина в `localStorage`, после оформления очищается
- Фильтры (цена, тип, цвет), сортировка, пагинация на фронте
- Карточка товара в модалке, закрытие по крестику и Esc

## Docker

```bash
cp .env.example .env
docker compose up --build
```

Порты те же, что у `npm run dev`:

- фронтенд: http://localhost:3000
- API: http://localhost:8080

Nginx на 3000 отдаёт сайт и проксирует `/api`; API слушает 8080 напрямую. Данные — в `server/data`. Перед `docker compose` остановите локальный `npm run dev`, иначе порты будут заняты.

## Макеты и исходники

| Файл | Содержание |
| --- | --- |
| `docs/templates/Course_project.pdf` | ТЗ |
| `docs/templates/Gadget Hub.fig` | Макет Figma |
| `docs/templates/Gadget Hub - pages.pdf` | Рендеры страниц |
| `docs/templates/Gadget Hub - UI kit.pdf` | UI kit |
| `docs/templates/Gadget Hub Assets.zip` | Исходный архив ассетов |
| `client/public/images` | Картинки и иконки |
| `client/public/fonts` | Rubik |

## Сценарий приёмки

1. Главная: карусели хитов и новинок.
2. Логин с пустыми полями — красная валидация.
3. Неверный пароль — сообщение об ошибке.
4. Вход student / gadget123.
5. Каталог: сортировка, фильтры, добавление в корзину.
6. Оформление заказа (телефон обязателен).
7. История заказов, отмена заказа с указанием причины.
8. Выход.
