# News Posts API - Swagger Documentation

## Огляд

Цей проект включає повну автоматичну генерацію API документації за допомогою Swagger UI та swagger-autogen.

## 🚀 Швидкий старт

1. Запустіть сервер:
```bash
npm run dev:server
```

2. Відкрийте Swagger UI:
```
http://localhost:8000/api-docs
```

3. Переглядайте JSON документацію:
```
http://localhost:8000/api-docs.json
```

## 📖 Доступ до документації

### Swagger UI
Інтерактивна документація з можливістю тестування API:
- **URL**: `http://localhost:8000/api-docs`
- **Функції**: Тестування endpoint'ів, авторизація, приклади запитів/відповідей

### JSON документація
Raw JSON схема для інтеграції з іншими інструментами:
- **URL**: `http://localhost:8000/api-docs.json`
- **Використання**: Імпорт в Postman, автогенерація клієнтів

## ⚙️ Генерація документації

### Автоматична генерація
Документація автоматично генерується при кожному запуску сервера за допомогою `swagger-autogen`.

### Ручна генерація
```bash
npm run swagger:generate
```

## 🔗 API Endpoints

### 📰 News Posts
- **GET** `/api/newsposts` - Список постів з пагінацією та фільтрацією
- **GET** `/api/newsposts/{id}` - Отримати конкретний пост
- **POST** `/api/newsposts` - Створити новий пост (потребує авторизації)
- **PUT** `/api/newsposts/{id}` - Оновити пост (потребує авторизації)  
- **DELETE** `/api/newsposts/{id}` - Видалити пост (потребує авторизації)

### 📂 Categories
- **GET** `/api/newsposts/categories` - Список всіх категорій

### 🏥 Health Check
- **GET** `/api/health` - Перевірка стану сервера

## 🔐 Авторизація

### Bearer Token
1. Отримайте JWT token через процес автентифікації
2. Використайте кнопку **"Authorize"** в Swagger UI
3. Введіть: `Bearer <your-token>`

### Ручні запити
Додайте header:
```
Authorization: Bearer <your-token>
```

## 📊 Схеми даних

### Основні моделі
- **Post** - Повна модель новинного поста
- **PostCreateRequest** - Дані для створення (required: header, content)
- **PostUpdateRequest** - Дані для оновлення (всі поля опціональні)
- **PaginatedResponse** - Відповідь з пагінацією
- **Category** - Модель категорії
- **User** - Модель користувача
- **ErrorResponse** - Стандартний формат помилок

## 📝 HTTP коди відповідей

| Код | Опис |
|-----|------|
| 200 | Успішно |
| 201 | Створено |
| 204 | Успішно без контенту |
| 400 | Невірний запит |
| 401 | Не авторизований |
| 403 | Заборонено |
| 404 | Не знайдено |
| 500 | Внутрішня помилка сервера |

## 🔒 Безпека в Production

У продакшені Swagger UI автоматично відключається. Для увімкнення встановіть змінну середовища:
```bash
ALLOW_SWAGGER_IN_PRODUCTION=true
```

## 🛠️ Технічні деталі

### Використані пакети
- `swagger-ui-express` - UI для документації
- `swagger-autogen` - Автогенерація документації
- `@types/swagger-ui-express` - TypeScript типи

### Конфігурація
- Файли конфігурації: `config/swagger.ts`
- Генератор: `scripts/generateSwagger.ts`
- Вихідний файл: `swagger-output.json`

### Кастомізація
- Тема: Кастомний CSS для кращого вигляду
- Авторизація: Збереження токенів між сесіями
- Фільтрація: Пошук по endpoint'ах

## 🔧 Налаштування

### Змінні середовища
```env
NODE_ENV=development              # Режим розробки
ALLOW_SWAGGER_IN_PRODUCTION=false # Дозвіл Swagger в продакшені
PORT=8000                        # Порт сервера
```

### Файли конфігурації
- `swagger.ts` - Основна конфігурація Swagger UI
- `generateSwagger.ts` - Налаштування автогенерації
- `swaggerGuard.ts` - Middleware для безпеки
