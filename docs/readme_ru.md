# Система управления музыкальной библиотекой (перевод не проверен)

Веб-приложение на Clojure для управления музыкальными партитурами с использованием 
Redis в качестве хранилища. Предоставляет RESTful API и простой фронтенд-интерфейс.

## Доступные переводы:

<center>

[Spanish](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_es.md)

[Deutsch](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ge.md) 

[English](https://github.com/jero98772/Music-Library-Management-System/blob/main/README.md)


</center>

## Описание

**Для музыкантов и хранителей музыки:**  
Представьте место, где ваши ноты оживают мгновенно — без скачиваний и громоздкого ПО. Это цифровое убежище для ваших партитур, созданное, чтобы ваши работы сияли прямо в браузере. Будь то набросок полуночной мелодии на мятой бумаге, воскрешение забытой классической пьесы или эксперименты с электронными битами — ваши композиции не просто хранятся, а проживаются. Прощайте, статичные PDF и нечитаемые файлы: здесь партитуры идеально отображаются на любом устройстве, позволяя коллегам видеть, играть и чувствовать ваше творчество без преград. Больше никаких утерянных рукописей или войн форматов — только ваше искусство, свободно дышащее в сети, достигающее слушателей быстрее, чем когда-либо.

**Почему открытый исходный код? Потому что музыка принадлежит всем.**  
Этот проект не скрыт за корпоративными воротами или платными подписками — он создан для и сообществом тех, кто живёт музыкой. Открытый код означает, что каждая строка — это общий гимн, коллективное усилие по защите творчества. Как джем-сейшн, где каждый может взять инструмент, разработчики, музыканты и мечтатели со всего мира могут дорабатывать и улучшать этот инструмент. Хотите функцию для расшифровки рукописных нот? Добавьте её. Мечтаете о тегах по настроению или культурным корням? Реализуйте. Прозрачность здесь — не модное слово, а обещание. Никаких скрытых целей, только сообщество, сплетающее технологии и страсть во что-то, что переживёт нас всех. Вместе мы не просто архивируем ноты — мы сохраняем истории, борьбу и искры, делающие музыку универсальным языком человечества. Присоединяйтесь, превратив сохранение искусства в акт любви.


## Возможности

- **CRUD-операции**: Создание, чтение, обновление, удаление партитур
- **Хранилище Redis**: Постоянное хранение данных в Redis
- **Сериализация EDN**: Сохранение сложных структур данных Clojure
- **REST API**: API на основе JSON для программного доступа
- **Веб-интерфейс**: Базовые HTML-страницы для ручного управления

## Технологии

- **Clojure** (1.10+)
- **Ring/Compojure** (веб-фреймворк)
- **Carmine** (клиент Redis)
- **Redis** (5.0+)
- **Leiningen** (сборка)

## Требования

- Java JDK 8+
- Leiningen 2.9.8+
- Redis Server 5.0+

## Установка

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/yourusername/music-lib.git
   cd music-lib/src
   ```

2. Установите зависимости:
   ```bash
   lein deps
   ```

3. Запустите Redis-сервер:
   ```bash
   redis-server
   ```

4. Запустите приложение:
   ```bash
   lein ring server
   ```

Приложение будет доступно по адресу `http://localhost:3000`

## Скриншоты

![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/screenshots/2.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/screenshots/3.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/screenshots/4.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/screenshots/5.png)

## Документация API

### Получить все партитуры
```
GET /api/partiture
```
**Ответ:**
```json
{
  "count": 2,
  "partitureList": [
    {
      "id": "partiture:uuid1",
      "title": "Лунная соната",
      "composer": "Бетховен",
      "created-at": "2023-09-20"
    }
  ]
}
```

### Создать партитуру
```
POST /api/partiture
```
**Параметры:**
- `title` (обязательный)
- `composer` (обязательный)
- `opus` (опциональный)
- `key` (опциональный)

**Пример ответа:**
```json
{
  "id": "partiture:550e8400-e29b-41d4-a716-446655440000"
}
```

### Получить партитуру
```
GET /api/partiture/:id
```
**Ответ:**
```json
{
  "id": "partiture:uuid1",
  "title": "Claro de Luna",
  "composer": "Beethoven",
  "instrumenr": "piano",
  "abc": "
        X:3
        T:Simple Song
        M:4/4
        L:1/8
        K:C
        [C]C2 [F]F2 [G]G2 [C]C2 |
        w: This is a sim-ple song, sing a-long with me.
  ",
}

```

### Обновить партитуру
```
PUT /api/partiture/:id
```
**Параметры:** Аналогично POST

### Удалить партитуру
```
DELETE /api/partiture/:id
```

## Маршруты фронтенда

- `/` — Главная страница
- `/add-partiture` — Форма добавления партитуры
- `/partiture/:id` — Просмотр партитуры
- `/edit/:id` — Редактирование
- `/delete/:id` — Подтверждение удаления

## Структура проекта

```
├── src
│   └── music_lib
│       ├── core.clj    # Основные маршруты
│       └── db.clj      # Операции с Redis
├── resources
│   └── public          # Статические файлы
│       ├── index.html
│       ├── add-partiture.html
│       └── ...остальные HTML-файлы
├── project.clj         # Конфигурация Leiningen
└── README.md
```

## Конфигурация

Настройки подключения к Redis (в `db.clj`):
```clojure
(def server-conn {
  :spec {
    :host "127.0.0.1"
    :port 6379
    :password nil
    :timeout-ms 3000}})
```

## Тестирование API

Примеры с curl:
```bash
# Создать партитуру
curl -X POST -d "title=К Элизе&composer=Бетховен" http://localhost:3000/api/partiture

# Получить все партитуры
curl http://localhost:3000/api/partiture

# Обновить партитуру
curl -X PUT -d "opus=WoO59" http://localhost:3000/api/partiture/partiture:uuid1
```

## Обработка ошибок

API возвращает HTTP-статусы:
- 200 OK
- 201 Created
- 404 Not Found
- 500 Internal Server Error

Ошибки содержат JSON с описанием:
```json
{
  "error": "Партитура не найдена"
}
```

## Возможные улучшения

1. Добавить аутентификацию
2. Валидация данных
3. Поиск по партитурам
4. Пагинация
5. Улучшенные сообщения об ошибках
6. Тестирование
7. Докеризация
8. Документация Swagger/OpenAPI

## Решение проблем

Частые проблемы:
1. **Ошибка подключения к Redis**
   - Проверьте запущен ли Redis
   - Убедитесь в правильности настроек в `db.clj`

2. **Ошибки EDN**
   - Проверьте данные через `redis-cli`
   - Убедитесь в корректности EDN-структур

3. **Отсутствующие зависимости**
   - Выполните `lein deps`

## Лицензия

Лицензия GPLv3. Вы можете использовать проект для любых целей, но обязаны указать ссылку на [https://github.com/jero98772/Music-Library-Management-System](https://github.com/jero98772/Music-Library-Management-System).

## Авторы

Создано с использованием:
- [Compojure](https://github.com/weavejester/compojure)
- [Carmine](https://github.com/ptaoussanis/carmine)
- [Ring](https://github.com/ring-clojure/ring)