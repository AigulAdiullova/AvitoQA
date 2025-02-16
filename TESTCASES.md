## Задание 2.1 (Тест-кейс)
### 1. Получение данных о товаре по ID

### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/item/:id`
2. Тестовые данные
`"id": "0cd4183f-a699-4486-83f8-b513dfde477a"`
3. Получен статус ответа `200 OK`
   
### Результат:
Получен статус ответа `200 OK`

Body JSON
```json
{
        "createdAt": "2025-02-12 11:28:35.164375 +0300 +0300",
        "id": "0cd4183f-a699-4486-83f8-b513dfde477a",
        "name": "dsdsd",
        "price": 1,
        "sellerId": 1234345231,
        "statistics": {
            "contacts": 3,
            "likes": 123,
            "viewCount": 12
        }
    }
```

### 2. Получение данных о товаре при вводе неккоректного ID

### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/item/:id`
2. Тестовые данные `"id": "0cd4183f-a699-4486-83f8-b513dfde477b"`
3. Получен статус ответа `404 Not Found`
   
### Результат:
Получен статус ответа `404 Not Found`

Body JSON
```json
{
    "result": {
        "message": "item 0cd4183f-a699-4486-83f8-b513dfde477b not found",
        "messages": null
    },
    "status": "404"
}
```

### 3. Получение статистики по объявлению 
### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/item/:id`
2. Тестовые данные
`"id": "0cd4183f-a699-4486-83f8-b513dfde477a"`
3. Получен статус ответа `200 OK`
   
### Результат:
Получен статус ответа `200 OK`

Body JSON
```json
[
    {
        "contacts": 3,
        "likes": 246,
        "viewCount": 258
    }
]
```
### 4. Получение статистики по объявлению по несуществующему ID
### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/item/:id`
2. Тестовые данные
`"id": "0cd4183f-a699-4486-83f8-b513dfde477b"`
3. Получен статус ответа `404 Not Found`
   
### Результат:
Получен статус ответа `404 Not Found`

Body JSON
```json
{
    "result": {
        "message": "statistic 0cd4183f-a699-4486-83f8-b513dfde477b not found",
        "messages": null
    },
    "status": "404"
}
```

### 5. Получение всех объявлений по sellerID 
### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/:sellerID/item`
2. Тестовые данные `"sellerID": "1234345231"`
3. Получен статус ответа `200 OK`
   
### Результат:
Получен статус ответа `200 OK`, объявления отображены

### 6. Получение всех объявлений с пустым полем sellerID 
### Шаги выполнения
1. Отправка запроса `GET` `https://qa-internship.avito.com/api/1/statistic/:sellerId`
2. Тестовые данные `"sellerID": " "`
3. Получен статус ответа `400 Bad Request`
   
### Результат:
Получен статус ответа `200 OK`, объявления отображены
Body JSON
```json
{
    "result": {
        "message": "передан некорректный идентификатор продавца",
        "messages": {}
    },
    "status": "400"
}
```

### 7. Создание объявления

### Шаги выполнения
1. Отправка запроса `Post` `https://qa-internship.avito.com/api/1/item?=&sellerId=239049330&id=856601f9-785f-4b5b-8404-515b0f5f3a2f`
2. Тестовые данные
`"id": "0cd4183f-a699-4486-83f8-b513dfde477b"`
`"sellerId": "0cd4183f-a699-4486-83f8-b513dfde477b"`

    Body JSON
```json
{
    "createdAt": "2025-02-18 11:28:35.164375 +0500 +0500",
    "id": "856601f9-785f-4b5b-8404-515b0f5f3a2f",
    "name": "Мой товар",
    "price": 1500,
    "sellerId": 239049330,
    "statistics": {
        "contacts": 5,
        "likes": 50,
        "viewCount": 100
    }
}
```
3. Получен статус ответа `200 OK`
   
### Результат:
Получен статус ответа `200 OK`

Body JSON
```json
{
    "status": "Сохранили объявление - 909b6bbb-2be2-4bae-ab30-d10f1fb73f62"
}
```

### 8. Сохранение объявления с незаполненными полями
### Шаги выполнения
1. Отправка запроса `Post` `https://qa-internship.avito.com/api/1/item`
2. Тестовые данные
   
   Body JSON
```json
{
  "sellerID": "<integer>",
  "name": "<string>",
  "price": "<integer>",
  "statistics":{
    "contacts":"<integer>",
    "likes":"<integer>",
    "viewCount":"<integer>"
  }
}
```
3. Получен статус ответа `400 Bad Request`
   
### Результат:
Получен статус ответа `400 Bad Request`

Body JSON
```json
{
  "result": {
    "messages": {
      "nostrudffb": "<string>",
      "Ut__": "<string>"
    },
    "message": "<string>"
  },
  "status": "<string>"
}
```
