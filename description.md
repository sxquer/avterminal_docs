# Описание API Интеграционного Сервиса AmoCRM

## Эндпоинты

### `POST /alta/ptd/export`

**Название:** Запрос на формирование XML для ПТД

**Описание:**
AmoCRM (или виджет в AmoCRM) отправляет данные для генерации XML файла
для пассажирской таможенной декларации. Сервис генерирует XML и возвращает его.

**Теги:**
- Альта

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/PtdExportRequest`

**Ответы (Responses):**
- **200:** XML файл успешно сформирован.
  - Content-Type: `application/xml`
  - Схема: `string` (Здесь будет сам XML)
- **400:** Некорректный запрос (например, отсутствуют обязательные поля).
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /alta/ptd/status-webhook`

**Название:** Webhook для уведомлений о статусах ПТД от Альта

**Описание:** Альта отправляет уведомления об изменении статуса ПТД.

**Теги:**
- Альта

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/PtdStatusNotification`

**Ответы (Responses):**
- **200:** Уведомление успешно принято и обработано.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /alta/transit-declaration/status-webhook`

**Название:** Webhook для уведомлений о статусах транзитных ДТ от Альта

**Описание:** Альта отправляет уведомления о регистрации транзитной ДТ.

**Теги:**
- Альта

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/TransitDeclarationStatusNotification`

**Ответы (Responses):**
- **200:** Уведомление успешно принято и обработано.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /ved-sklad/svh-release-webhook`

**Название:** Webhook для уведомлений о выдаче товаров с СВХ от ВЭД-склада

**Описание:** ВЭД-склад отправляет уведомление о возможности выдачи товаров.

**Теги:**
- ВЭД-склад

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/SvhReleaseNotification`

**Ответы (Responses):**
- **200:** Уведомление успешно принято и обработано.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /ved-sklad/lab-documents-webhook`

**Название:** Webhook для документов из лаборатории

**Описание:** PHP скрипт отправляет информацию о документах (ЭПТС, СБКТС) из лаборатории.

**Теги:**
- ВЭД-склад

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/LabDocumentsNotification`

**Ответы (Responses):**
- **200:** Документы успешно приняты и обработаны.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /1c/client-data`

**Название:** Передача данных клиента из AmoCRM в 1С

**Описание:**
При срабатывании триггера в AmoCRM (например, смена стадии на "Договор"),
AmoCRM отправляет данные клиента на этот эндпоинт для создания/обновления контрагента в 1С.

**Теги:**
- 1С

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/ClientDataFor1C`

**Ответы (Responses):**
- **200:** Данные клиента успешно приняты для обработки в 1С.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /1c/service-data-for-invoice`

**Название:** Передача данных по услугам из AmoCRM для формирования счета в 1С

**Описание:**
При срабатывании триггера в AmoCRM, AmoCRM отправляет данные по услугам
для формирования счета в 1С.

**Теги:**
- 1С

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/ServiceDataFor1CInvoice`

**Ответы (Responses):**
- **200:** Данные по услугам успешно приняты для формирования счета в 1С.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`

---

### `POST /1c/invoice-payment-webhook`

**Название:** Webhook для уведомлений об оплате счетов от 1С

**Описание:** 1С отправляет уведомление об оплате счета.

**Теги:**
- 1С

**Тело запроса (Request Body):**
- Обязательный: Да
- Content-Type: `application/json`
- Ссылка на схему: `#/components/schemas/InvoicePaymentNotification`

**Ответы (Responses):**
- **200:** Уведомление об оплате успешно принято и обработано.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/SuccessResponse`
- **400:** Некорректный запрос.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
- **500:** Внутренняя ошибка сервера.
  - Content-Type: `application/json`
  - Ссылка на схему: `#/components/schemas/Error`
