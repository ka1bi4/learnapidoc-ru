# Руководство OpenAPI Шаг 7: Объект `tags`

| [*Шаг 1: объект* `openapi`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.5.%20Step%201%20The%20openapi%20object.md) | --> | [*Шаг 2: объект* `info`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.6.%20Step%202%20The%20info%20object.md) | --> | [*Шаг 3: объект* `servers`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.7.%20Step%203%20The%20servers%20object.md) | --> | [*Шаг 4: объект* `paths`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md) | --> | [*Шаг 5: объект* `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md) | --> | [*Шаг 6: объект* `security`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.10.%20Step%206%20security%20object.md) | --> | [**Шаг 7: объект** `tags`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.11.%20Step%207%20The%20tags%20object.md) | --> | [*Шаг 8: объект* `externalDocs`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.12.%20Step%208%20The%20externalDocs%20object.md) |

Объект `tags` позволяет группировать пути (конечные точки) в Swagger UI.

[Определение `tags` на корневом уровне](#define)

[`tags` на уровне объекта `paths`](#level)

[Отображение в Swagger UI](#appearanse)

<a name="define"></a>
## Определение `tags` на корневом уровне

На корневом уровне [объект `tags`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#tagObject) перечисляет все теги, которые используются в [объектах операций](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#operationObject) (которые появляются в объекте `paths`, как описано в [Шаге 4: объект `paths`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md)). Вот пример объекта тегов для нашего API OpenWeatherMap:

    tags:
      - name: Current Weather Data
      description: "Get current weather details"

Здесь только один тег, но их может быть столько, сколько вы хотите (если у вас много конечных точек, имеет смысл создать несколько тегов для их группировки). Вы можете перечислить как `name`, так и `description` для каждого тега. `description`  отображается в виде подзаголовка для имени тега на дисплее пользовательского интерфейса Swagger.

<a name="level"></a>
## Тэги на уровне объекта `paths`

Объект `tags` на корневом уровне должен содержать список всех тегов (групп), которые вы хотите использовать в своем API. Затем в каждом объекте пути под `paths` вы указываете тег, под которым вы хотите сгруппировать этот путь.

Например, в объекте операций для `/current` пути мы использовали тег `Current Weather Data`:

    paths:
      /weather:
        get:
          tags:
          - Current Weather Data


Этот тег определен на глобальном уровне, поэтому путь `/weather` будет сгруппирован здесь.

<a name="appearanse"></a>
## Отображение в Swagger UI

Добавьте следующий код к корневому уровню документа OpenAPI в редакторе Swagger:

    tags:
      - name: Current Weather Data
      description: "Get current weather details"

Посмотрите, как описание отображается рядом со свернутым разделом «Данные о текущей погоде».

![tags](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/16.png?raw=true)

> Тэг определен на корневом уровне


Все пути, имеющие одинаковый тег, сгруппированы на дисплее. Например, пути с тегом `Current Weather Data` будут сгруппированы под заголовком `Current Weather Data`. Каждое название группы представляет собой складной / расширяемый переключатель.

![name](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/17.png?raw=true)

Порядок тегов в объекте `tags` на корневом уровне определяет их порядок в интерфейсе Swagger. Кроме того, `descriptions`  появляются справа от имени тега.

В нашем примере спецификации OpenAPI теги не кажутся необходимыми, поскольку мы просто документируем один путь / конечную точку. (Кроме того, настроена [демо версию Swagger UI](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.15.%20Swagger%20Ui%20demo.md) для расширения раздела по умолчанию.) Но представьте, что у вас есть надежный API с более чем 30 путями описания. Вы наверняка захотите организовать пути в логические группы для навигации пользователей.