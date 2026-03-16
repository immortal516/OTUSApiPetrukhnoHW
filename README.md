# Wishlist API — Postman collection

## Цель
Проверить корректность работы REST API Wishlist:
- статус-коды
- структура ответов (JSON)
- базовые CRUD операции
- негативные сценарии (валидация, авторизация)

## Инструменты
- Postman (Collection Runner)

## API
Swagger: https://api.wishlist.otus.kartushin.su/swagger-ui/index.html  
Base URL: https://api.wishlist.otus.kartushin.su

## Как запустить
1. Импортировать коллекцию: `Postman/Wishlist_API.postman_collection.json`
2. Импортировать окружение: `Postman/wishlist-env.postman_environment.json`
3. Выбрать environment `wishlist-env`
4. Запустить коллекцию через Runner (Run collection)

## Переменные окружения
- baseUrl
- token (заполняется после Login)
- wishlistId (заполняется после Create wishlist)
- giftId (заполняется после Create gift)
- username/password/email (для логина)

## Покрытие эндпоинтов
### Auth
- POST /api/auth/login (positive)
- POST /api/auth/register (на стенде недоступен, см. Observations)

### Wishlists
- POST /api/wishlists
- GET /api/wishlists
- GET /api/wishlists/{id}
- PUT /api/wishlists/{id}
- DELETE /api/wishlists/{id}

### Gifts
- POST /api/gifts/wishlist/{wishListId}
- GET /api/gifts/{id}
- GET /api/gifts/wishlist/{wishListId}
- PUT /api/gifts/{id}
- PUT /api/gifts/{id}/reserve
- DELETE /api/gifts/{id}

### Users
- GET /api/users
- GET /api/users/{userId}/wishlists

## Негативные сценарии (примеры)
- Login с неверным паролем -> 401/403
- Запрос без токена -> 401/403
- Создание wishlist без title -> 400/403
- Создание gift без name -> 400/403
- Запрос несуществующего wishlist id -> 404/401

## Observations / Расхождения
1) POST /api/auth/register:
    - ожидание: 200/201 на валидных данных
    - факт: 401/403 (регистрация на стенде запрещена или требует авторизацию)

2) Валидационные негативные кейсы иногда возвращают 403 вместо 400.
