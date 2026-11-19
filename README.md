<img width="1024" height="1024" alt="1000866664" src="https://github.com/user-attachments/assets/00a5149d-c3cc-43f8-8cd9-67be8b9d9082" alt="Логотип." />

# 🔘 Melon Playground API
***API мелона*** *- для регистрации взаимодействия с серверами и прочем. через playmelonpg.com.
Сами сервера склона находится на амозон, с под доменом pg, хоть есть и другие 2 типа API.
Половину всех запросов на сервера через POST или GET, и заголовок для запросов после выхода в аккаунт лучше юзать такой:*

``
{
    "Authorization": "Bearer TOKEN",
    "Content-Type": "application/json"
}
``

<hr>

# 🧠 Вход в аккаунт
**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-login-password``

**Тело:**
```json
{
  "login": "Логин",
  "password": "Пароль"
}
```
**Ответ:**
```json
{
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGl0eVR5cGUiOiJ1c2VyIiwiaWRlbnRpdHlJZCI6ImUwODY0MDFhLTk2NWQtNDMwMy1iNGM5LTRlNWM1NjExMDM4MyIsImlkZW50aXR5Um9sZSI6InBsYXllciIsImV4cCI6MTc4MjM3ODY0MywiaWRlbnRpdHlLaW5kIjoidmVyaWZpZWRQbGF5ZXIiLCJ2ZXJzaW9uIjoidjEiLCJpYXQiOjE3ODExNjkwNDMsImlzcyI6ImF1dGgtc2VydmljZSJ9.dN1E_-DCJP1gdOcThlZht9BCvXR7zJDC-_BiN4ZaWAo",
  "jwtExpiredAt": 1782378643000,
  "userId": "e086401a-965d-4303-b4c9-4e5c56110383",
  "userKind": "verifiedPlayer",
  "userRole": "player",
  "tokenTtlSeconds": 1209600,
  "eventJwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGl0eVR5cGUiOiJ1c2VyLWV2ZW50IiwiaWRlbnRpdHlJZCI6ImUwODY0MDFhLTk2NWQtNDMwMy1iNGM5LTRlNWM1NjExMDM4MyIsImlkZW50aXR5Um9sZSI6IiIsImV4cCI6MTkzODg0OTA0MywiaWF0IjoxNzgxMTY5MDQzLCJpc3MiOiJhdXRoLXNlcnZpY2UifQ.qcSnAnjNBDuzN51_09yhHn0ay1g_H8oYLBKP8rAkEIA"
}
```

*Вход в аккаунт мелона по логину и паролю если раскопилировать jwt 
то получим:*

```json
{"alg":"HS256","typ":"JWT"}{"identityType":"user","identityId":"e086401a-965d-4303-b4c9-4e5c56110383","identityRole":"player","exp":1782378643,"identityKind":"verifiedPlayer","version":"v1","iat":1781169043,"iss":"auth-service"}
```
``userKind`` *- показывает подверждёна ли почта или нет.*

``userRole`` *- ваша роль* ``player`` *или* ``moderator``

*eventJwt - токен от ивентов если расшифровать из base64:*
```json
{"alg":"HS256","typ":"JWT"}{"identityType":"user-event","identityId":"e086401a-965d-4303-b4c9-4e5c56110383","identityRole":"","exp":1938849043,"iat":1781169043,"iss":"auth-service"}
```

***Важно - токены появляются только при регистрации и больше нигде.
Все следующие ответы будет такии же.***

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-email-password``

**Тело:**
```json
{
  "email": "Email",
  "password": "Пароль"
}
```

*Вход через почту.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-social/web``

**Тело:**
```json
{
  "socialProviderKind": "google" | "apple",
  "socialToken": "Токен сессии"
}
```

*Вход тоже через гугл или эпл, если надо создать авторизацию через гугл илм эпл, то используйте Google Cloud Console или Apple Developer Account*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-social/web``

**Тело:**
```json
{
  "externalDeviceId": "externalDeviceId",
  "deviceName": "deviceName" // необязательно
}
```

*Вход через ID устройство. (Анонимно.)*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/webhook-verify-login``

**Тело:**
```json
{
  "user": {
    "id": "Ник пользователя"
  },
  "projectId": 226733,
  "merchantId": 418104
}
```

**Ответ:**
```json
{
  "user": {
    "id": "123456l",
    "name": "123456l"
  }
}
```

*Вход через Xsolla по логину, но вы* ***никак НЕ можете*** *взаимодействовать с аком мелона, не зная его логин и пароль*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/admin/by-login-password``

**Тело:**
```json
{
  "login": "Логин",
  "password": "Пароль"
}
```

*Вход в аккаунт админа по логину, но у вас скорее всего ничего не получится.*

# 🦾 Информация о аккаунте
**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/user/me``

**Ответ:**
```json
{
  "id": "e086401a-965d-4303-b4c9-4e5c56110383",
  "login": "123456l",
  "kind": "verifiedPlayer",
  "role": "player",
  "withPassword": true,
  "device": {
    "id": "c067bb7b-ee60-40c7-addc-cb727d26858c",
    "platform": "IPhonePlayer",
    "externalDeviceId": "8180D8EF-B389-4EF8-AB9E-E1CEE002BF73",
    "name": "iPad",
    "systemName": "iPad7,5",
    "systemVersion": "iPadOS 17.5.1",
    "appAccountToken": "",
    "appsFlyerId": "1766619637876-1633812356075774279"
  },
  "socials": [],
  "blocked": false,
  "deleted": false,
  "createdAt": 1723877306491,
  "updatedAt": 1781175532891,
  "userEmail": {
    "notActiveEmail": "GoreBox@gmail.com",
    "consentToReceive": false
  },
  "lastActiveAt": 1781176925386,
  "avatarFileId": "95c3c925-7e29-4d9a-9f72-40285a483326",
  "referralCode": "XVJR-GLWZ-XMUA",
  "language": "en",
  "country": "FR"
}
```

*Информация о аккаунте и телефоне пользователя, и да ваш аккаунт* ***могут забанить или удалить.***
*Самое интересное что на сервере есть ещё реферальные коды, но их не используют.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/account-preview/wallet/me``

**Ответ:**
```json
{
  "walletId": "f9e5e093-7595-476c-9902-1d5b1a2bf9d6",
  "userId": "e086401a-965d-4303-b4c9-4e5c56110383",
  "coins": 8,
  "availableWithdrawFiatCoins": 0,
  "hasActiveOperations": false
}
```

*Показывает ваш баланс в мелсах и прочее.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/fiat/order/me``

**Ответ:**
```json
{ }
```
```json
[
  {
    "createdAt": "2024-01-13T10:32:00Z",
    "usdAmount": 190,
    "state": "waitRefundCoins",
    "orderId": "ORD-1452"
  }
]
```

*Показывает историю и статусы заявок на вывод средств, если нет, то по молчанию пустое.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/fiat/order/create``

**Тело:**
```json
{
  "coinsAmount": 75000
}
```

*Создание заявок на вывод средств. Минум 75000 мелсов, и вряд-ли это получится сделать в России.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/game-store/order/yandex-pay/create``

**Тело:**
```json
{
  "billingKind": "yandexPay",
  "skus": [
    {
      "skuId": "ID",
      "price": { "amount": 123, "currency": "MELS" },
      "promotionId": ""
    }
  ]
}
```

**Ответ:**
```json
{ "paymentUrl": "https://" }
```

*Создаёт покупку мелсов/предметов в магазине через Яндекс.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/internal-notice/filter?limit={limit}&offset={offset}``

**Ответ:**
```json
{
  "objects": [
    {
      "id": "id",
      "receiverId": "receiverId",
      "status": "read" | "unread",
      "createdAt": 44,
      "updatedAt": 2,
      "notificationContent": {
        "body": "body",
        "meta": {
          "kind": "content_status" | "store_item_status" | "store_item_status",
          "contentId": "content",
          "itemId": "item"
        }
      }
    }
  ],
  "filterMeta": {
    "totalItems": 4,
    "offset": 2
  }
}
```

*Показывает ваши уведомления, надо указывать лимит и offset.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/internal-notice/count-unread``

**Ответ:**
```json
{
  "unreadCount": 0
}
```

*Показывает количество непрочитанных уведомлений*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/read``

**Тело:**
```json
{
  "internalNoticeIds": ["id", "id"]
}
```

*Прочивает сообщение по ID.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/read-all``

*Прочитывает все уведомления, и не имеет тела и ответ пустой.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/archive``

**Тело:**
```json
{
  "internalNoticeIds": ["id", "id"]
}
```

*Архивирует/Удаляет сообщения, ответ тоже пустой.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/content-management/creator/available-slots``

**Ответ:**
```json
{"slots":3}
```

*Показывает количество доступных слотов для контента.*

<hr>

**Ссылыка:** (GET)
``https://pg.playmelonpg.com/api/content/slot-config/actual``

**Ответ:**
```json
{
  "id": "8239246d-7ea7-4cbb-b096-68b0fbe46ce9",
  "slotsForDownloadsMsg": {
    "en": "Initially, you have 3 slots for posting content on Workshop. However, you can increase this number by receiving downloads for your content. For every 100 new downloads, an additional slot will be unlocked.\nYou can unlock up to 500 slots.",
    "ru": "Изначально у вас есть 3 слота для размещения контента в мастерской. Однако вы можете увеличить это количество, за загрузки вашего контента. За каждые 100 новых загрузок будет открываться дополнительный слот.\nВсего можно открыть до 500 слотов."
  },
  "createdAt": 1779189114126,
  "updatedAt": 1779189114126
}
```

*Показывает подсказку на русском и англ.*

<hr>

**Ссылыка:** (GET)
`https://pg.playmelonpg.com/api/content-management/creator/me?limit={limit}&offset={offset}`

*Показывает ваши созданные работаты.*

# 🌀 Настройка акаунта
**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/set-email``

**Тело:**
```json
{
  "email": "user@gmail.com"
}
```

*Отправляет сообщение с добавлением почты на ак на ваш email.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/confirm-email``

**Тело:**
```json
{
  "tokenValue": "123456"
}
```

*Вводите туда свой код и подтверждаете свой email. Код действует плоть до 1 минуты.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/init-password``

**Тело:**
```json
{
  "password:" "Новый пароль."
}
```
*Просто меняет сразу пароль.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/change-password``

**Тело:**
```json
{
  "currentPassword": "Старый пароль",
  "newPassword:" "Новый пароль"
}
```
*Меняет пароль, но нужно знать старый пароль.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/reset-password/init``

**Тело:**
```json
{
  "email": "user@gmail.com"
}
```

*Отправка на email сброс пароля.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/reset-password/confirm``

**Тело:**
```json
{
  "email": "user@gmail.com",
  "proofTokenValue": "123456",
  "newPlainTextPassword": "Новый пароль."
}
```

*Сбрасывает пароль, нужно знать код, email и потом устанавливаете новый пароль. (от 5 до 50 символов и нужна хотя-бы 1 англ буква, и только англ. буквы, цифры и _ после первого символа.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/set-login``

**Тело:**
```json
{
  "login": "Новый логин."
}
````

*Устанавливает новый логин пользователя от 2 до 50 символов, и только англ. буквы, цифры и _ после первого символа.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/remove/issue/create-without-user``

**Тело:**
```json
{
  "name": "Имя",
  "description": "Причина",
  "email": "Тут он принимает gmail."
}
```

*Запрос на удаление аккаунта, дальше на вашу почту может прити сообщение о удаление ака.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/logout``

*Не имеет тела и ответа, просто выходит из аккаунта, правда смысл если можно зайти сразу в другой.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/set-avatar``

**Тело:**
```json
{
  "avatarFileId": "id на сервере"
}
```

*Меняет аву на указанный ID, вот все авы с этими ID:*

**ID:** ``72e68dea-7213-486f-bd87-4238350840d3``
*- Мелон.*

<img src="https://pgstatic.playmelonpg.com/content/compressed-images/95c3c925-7e29-4d9a-9f72-40285a483326_w512.png" alt="Тыква">

**ID:** ``95c3c925-7e29-4d9a-9f72-40285a483326``
*- Тыква.*

<img src="https://pgstatic.playmelonpg.com/content/compressed-images/9d89048a-1495-472a-89ed-c1c4fda4c57b_w512.png" alt="Кукуруза">

**ID:** ``9d89048a-1495-472a-89ed-c1c4fda4c57b_w512.png`` *- Кукуруза.*

**ID:** ``b39f758d-6562-45c1-95c1-95d915d4345e_w512.png`` *- Робот.(Премиум.)*

**ID:** ``4d53b455-72e8-47c1-8e68-d8631e463877.png`` *- Яблоко.*

**ID:** ``9d89048a-1495-472a-89ed-c1c4fda4c57b_w512`` *- Кукуруза.*

**ID:** ``6dc7c4c8-e67d-4d84-9179-3ed69520283f`` *- Кактус.*

**ID:** ``1b29bc6b-1217-4fec-891c-aab2a1f3a01c`` *- Скелет.*

# 🧱 Другое
**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/web-link/actual/actualNews``

**Заголовок:** *(Только для этого запроса.)*
```json
{
  'x-app-version': 'global',
  'x-platform': 'web'
}
```

**Ответ:**
```json
{
  "id": "abb98d35-11d5-460f-9d11-8b991b876eb9",
  "appVersion": "global",
  "link": {
    "ru": "news-09-06-26",
    "en": "news-09-06-26"
  },
  "kind": "actualNews",
  "publicComment": " "
}
```

*Показывает последние обновления новостей.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/app-section-status`` 
``https://pg.playmelonpg.com/api/app-section-status/active/easterEggRadio?AppVersion=Версия игры.``

**Ответ:**
```json
{"tabIndex":3}
```

*Не особо понятный API, а вторая его версия вообще не понятно зачем нужна.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/storage/file/compressed/public/direct-link/Id файла на сервере.``

*Скачивает файлы с сервера к примеру:*

``https://pgstatic.playmelonpg.com/content/compressed-images/95c3c925-7e29-4d9a-9f72-40285a483326_w512.png``

*Он может скачивать авы, скрины и авы контента и текстуры с ивентов, но,* ***НЕ*** *может скачивать файлы контента, id можно достать из самих файлов игры в папке* ```Images/Avatars``` *Всё находится по пути:* ```https://pgstatic.playmelonpg.com/content/compressed-images/id файла на сервере.``` *и ID различаются.*

<hr>

**Ссылка:** (GET)
``http://pg.playmelonpg.com/api/game-store/sku/all-list``

**Ответ:**
```json
[
  "mels_01",
  "mels_05",
  "mels_03",
  "mels_02",
  "mels_07",
  "mels_06",
  "mels_04"
]
```

*Показывает товары.*

<hr>

*Пока это все известные API если у вас есть API или какие-то ошибки в API документации, пишите мне в ЛC:@gap0135*

<img width="96" height="96" alt="1000866663" src="https://github.com/user-attachments/assets/3c5d27f4-15c8-4daf-b896-5b71ef4aa6d0" alt="Melon." />
<hr>
