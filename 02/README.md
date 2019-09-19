# profi.ru-test-task
Link contractor(Node.js)

## Task

Предположим, мы хотим написать свой собственный сокращатель ссылок (такой,
как bit.ly), и попросили вас написать API, который будет реализовывать
основную функциональность сервиса.

Для пользователя должны быть доступны следующие возможности:

1. Создать новую сокращенную ссылку (дать длинную, получить короткую)
2. Перейти по короткой ссылке и быть перенаправленным на исходную длинную ссылку
3. Просмотреть список «своих» ссылок, которые он сокращал
4. Просмотреть статистику переходов по каждой ссылке

## Desc
В качестве БД используется no-sql хранилище MongoDB. БД развернута на 
удаленном ресурсе (mlab). Для сокращения ссылок используется node-emoji,
которая генерирует ссылку из 5ти emoji. Для создания REST сервиса используется Express.

## Endpoints
*followCount - количество переходов по ссылке

### GET /api/getAll
Получение всех ссылок
Example: http://localhost:5000/api/getAll
Возвращает json: 
```json
[
    {
        "_id": "5d839731c34d7d3a70f33a10",
        "url": "https://stackoverflow.com",
        "url_short": "https://⭐️⭐️.ws/🇹🇴🔺📖😈🇱🇻",
        "followCount": 1,
        "createdAt": "2019-09-19T14:56:49.686Z"
    },
    {
        "_id": "5d826cecfedcfa3f30e4171f",
        "url": "https://yandex.com",
        "url_short": "https://⭐️⭐️.ws/🇹🇦🐴🛤️🕐❕",
        "followCount": 3,
        "createdAt": "2019-09-18T17:44:12.183Z"
    },
    {
        "_id": "5d826675bda1ec2d50023fb7",
        "url": "https://google.com",
        "url_short": "https://⭐️⭐️.ws/🧛‍♀️⚕️😅🇲🇺🚫",
        "followCount": 0,
        "createdAt": "2019-09-18T17:16:37.375Z"
    },
    {
        "_id": "5d82666ebda1ec2d50023fb6",
        "url": "https://vk.com",
        "url_short": "https://⭐️⭐️.ws/📞🔅🕛👨‍👨‍👧‍👧🍳",
        "followCount": 2,
        "createdAt": "2019-09-18T17:16:30.345Z"
    }
]

```

### POST /api/saveUrl
Создание сокращенной ссылки
Example: http://localhost:5000/api/saveUrl
req.body: 
```json
{
	"long_url": "https://yandex.com"
}
```

Возвращает json:
```json
{
        "success": true,
        "result": "shortUrl"
}
```
### GET /api/:id
Переход по сокращенной ссылке
Example: http://localhost:5000/api/🧛‍♀️⚕️😅🇲🇺🚫, где 🧛‍♀️⚕️😅🇲🇺🚫 - сокращенная ссылка.
Если такая ссылка существует, произойдет переадресация на настоящую ссылку. Проверить можно, запустив данный запрос в браузере.

### GET /api/statistics/:id
Получение статистики по конкретной ссылке
Example: http://localhost:5000/api/statistics/5d839731c34d7d3a70f33a10
Возвращает json:
```json
{
    "item": {
        "_id": "5d839731c34d7d3a70f33a10",
        "url": "https://stackoverflow.com",
        "url_short": "https://⭐️⭐️.ws/🇹🇴🔺📖😈🇱🇻",
        "followCount": 1,
        "createdAt": "2019-09-19T14:56:49.686Z"
    }
}
```

## How to run

Install dependencies - **```npm install```**  
Run **```npm run start```** or **```npm run dev```** (to run dev server)
Go to **localhost:5000**
