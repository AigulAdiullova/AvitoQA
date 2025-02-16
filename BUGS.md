## 1. Отсутствие валидации обязательных полей
### 1.1 Создание объявление без указания ID
### Шаги выполнения
1. Отправка запроса `Post` `https://qa-internship.avito.com/api/1/item`
2. Тестовые данные
`"sellerId": "239049331"`
   
   Body JSON
```json
{
    "createdAt": "2025-02-18 11:28:35.164375 +0500 +0500",

    "name": "Мой товар2",
    "price": 1502,
    "sellerId": 239049331,
    "statistics": {
        "contacts": 6,
        "likes": 50,
        "viewCount": 100
    }
}
```
3. Получен статус ответа `202 OK`
   
### 1.2 Создание объявление без указания sellerId
### Шаги выполнения
1. Отправка запроса `Post` `https://qa-internship.avito.com/api/1/item`
2. Тестовые данные
   id": "0rptrptp-7777-4dfdf-8dfdfd-b5ororota"`
   
   Body JSON
```json
{
    "createdAt": "2025-02-12 11:28:35.164375 +0300 +0300",
    "id": "0rptrptp-7777-4dfdf-8dfdfd-b5ororota",
    "name": "Мой товар",
    "price": 1500,
    
    "statistics": {
        "contacts": 5,
        "likes": 50,
        "viewCount": 100
    }
}
```
3. Получен статус ответа `202 OK`
   
### Ожидаемый Результат:
Получен статус ответа `400 Bad Request`

### Фактический Результат:
Получен статус ответа `200 OK`

Body JSON
```json
{
    "status": "Сохранили объявление - 909b6bbb-2be2-4bae-ab30-d10f1fb73f62"
}
```
### Ожидаемый Результат:
Получен статус ответа `400 Bad Request`

### Фактический Результат:
Получен статус ответа `200 OK`

Body JSON
```json
{
    "status": "Сохранили объявление - 909b6bbb-2be2-4bae-ab30-d10f1fb73f62"
}
```



**Тело запроса:**

```json
{
  "name": "Example Item",
  "price": 1000,
  "description": "Description of the item"
}
```
**Ожидаемый результат:**  
Сервер возвращает 400 Bad Request, сообщение "sellerID is required" 

**Фактический результат:** 
Статус 200 ОК

```json
{
    "status": "Сохранили объявление - 5fc9d4a2-2fa8-4281-a21d-b22faf61720e"
}
```

---

#### bug-тк-09 Сервер возвращает некорректный код в теле ответа при формировании запроса GET https://qa-internship.avito.com/api/1/ads на несуществующий маршрут 

**Шаги:**  
1. Отправить `GET` запрос без авторизационного токена  
2. Проверить, что статус ответа `404Not Found`
3. Проверить сообщение об ошибке

**Запрос:**
GET https://qa-internship.avito.com/api/1/ads 

**Ожидаемый результат:**  
- Сервер возвращает `404Not Found`

```json
{
    "message": "route /api/1/ads not found",
    "code": 404
}
```
**Фактическийт результат:** 

```json
{
    "message": "route /api/1/ads not found",
    "code": 400
}
```
---

#### bug-тк-11 Повторно создается объявление с уже существующим sellerID при отправке запроса POST /api/1/item

**Шаги:**
1. Отправить `POST` запрос с повторяющимся `sellerID`, который уже существует в системе.
2. Проверить, что статус ответа `400 Bad Request`.
3. Проверить сообщение об ошибке, например, "SellerID already exists".

**Тело запроса:**

```json
{
  "sellerID": 112277,
  "name": "Another Example Item",
  "price": 1500,
  "description": "Another description of the item"
}
```

**Ожидаемый результат:**  
Сервер возвращает ошибку с кодом 400 Bad Request и сообщение "SellerID already exists". 

```json
{
    "message": "SellerID already exists",
    "code": 400
}
```
**Фактический результат:**  
Статус 200 ОК

```json
{
    "status": "Сохранили объявление - 352a8177-7200-4703-9005-0d66bd833060"
}
```
---

#### bug-тк-12 Сервер возвращает код 200 ОК при отправка запроса с некорректным значением price в ручке POST https://qa-internship.avito.com/api/1/item

**Шаги:**
1. Отправить `POST` запрос с некорректным значением `price`, например, отрицательным числом или нулем.
2. Проверить, что статус ответа `400 Bad Request`.
3. Проверить сообщение об ошибке, например, "Invalid price value".

**Тело запроса:**
```json
{
  "sellerID": 112277,
  "name": "Item with invalid price",
  "price": -500,
  "description": "This item has an invalid price"
}
```

**Ожидаемый результат:**  

Сервер возвращает ошибку с кодом 400 Bad Request и сообщение "Invalid price value".

```json
{
    "message": "Invalid price value",
    "code": 400
}
```
**Фактический результат:** 
Статус 200 ОК
```json
 {
    "status": "Сохранили объявление - ddd19a53-38ad-4461-bd43-0709331bb3d3"
}
```
---
