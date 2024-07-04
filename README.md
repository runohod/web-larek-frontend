# Проектная работа "Веб-ларёк"

### Учебная проектная работа с [макетом "Веб-ларёк"](https://www.figma.com/file/50YEgxY8IYDYj7UQu7yChb/Веб-ларёк?type=design&node-id=0-1&mode=design&t=tQ9xTmGuVtBDpWT6-0) по курсу Яндекс Практикума "Фронтенд-разработчик"

**Стек**: `HTML`, `SCSS`, `TS`, `Webpack`

**Структура проекта**:

- `src/` — исходные файлы проекта
- `src/components/` — папка с JS компонентами
- `src/components/base/` — папка с базовым кодом

**Важные файлы**:

- `src/pages/index.html` — HTML-файл главной страницы
- `src/types/index.ts` — файл с типами
- `src/index.ts` — точка входа приложения
- `src/styles/styles.scss` — корневой файл стилей
- `src/utils/constants.ts` — файл с константами
- `src/utils/utils.ts` — файл с утилитами

## Установка и запуск

Для установки и запуска проекта необходимо выполнить команды:

```
npm install
npm run start
```

или:

```
yarn
yarn start
```

## Сборка

Сборка осуществляется при помощи команды:

```
npm run build
```

или:

```
yarn build
```

## Описание классов проекта [A-Z]

### `Api`

Класс для выполнения `HTTP`-запросов на сервер, таких как `GET`, `POST`, `PUT` и `DELETE`.

Методы / свойства класса:

- `constructor` — принимает базовый `URL` и дополнительные параметры для настройки запросов;
- `get` — позволяет снять установленный обработчик события;
- `post` — выполняет `HTTP`-запрос типа `POST` (по умолчанию) или других методов (`PUT`, `DELETE`) по указанному `URI` с передачей данных в формате `JSON`;
- `handleResponse` — обрабатывает ответ от сервера, проверяет его статус. Если статус успешный (`ок`), возвращает распарсенные `JSON`-данные. В противном случае, возвращает ошибку с сообщением об ошибке.

### `AppState`

Класс состояния приложения, отслеживающую данные о корзине, каталоге товаров и оформлении заказа.

Методы / свойства класса:

- `basket` — массив товаров в корзине;
- `catalog` — массив товаров в каталоге;
- `loading` — указывает состояние загрузки данных;
- `order` — данные оформляемого заказа;
- `preview` — идентификатор выбранного товара для предварительного просмотра;
- `formErrors` — объект с ошибками валидации формы;
- `clearBasket` — очищает корзину;
- `getTotal` — устанавливает общую сумму товаров в корзине;
- `setCatalog` — устанавливает список товаров в каталоге и генерации события изменения каталога;
- `setPreview` — устанавливает предварительный просмотр выбранного товара;
- `validateDeliveryForm` — валидирует данные формы доставки;
- `validateContactForm` — валидирует данные формы контактов;
- `setOrderField` — устанавливает значение поля заказа и проверки валидности формы контактов.

### `Basket`

Класс отображения списка выбранных товаров и их общей стоимости в корзине.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент и и объект событий для обработки действий пользователя;
- `items` — отображает товаров в корзине;
- `selected` — блокирует / разблокирует кнопку оформления заказа в зависимости от наличия товаров в корзине;
- `total` — выводит общую стоимость товаров в корзине.

### `Card`

Класс карточки товара для отображения информации о товаре.

Методы / свойства класса:

- `constructor` — принимает имя блока, `HTML`-элемент и объект событий для обработки действий пользователя;
- `id` — идентификатор товара в каталоге;
- `basketId` — идентификатор товара в корзине;
- `category` — категория товара;
- `title` — название товара;
- `image` — изображение товара;
- `description` — описание товара;
- `button` — кнопка карточки товара;
- `price` — стоимость товара;
- `set` — устанавливает значение у свойства товара;
- `get` — получает значение у свойства товара.

### `Component`

Абстрактный класс базового компонента для работы с интерфейсом.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент;
- `toggleClass` — переключает класс элемента;
- `setText` — устанавливает текстового содержимого элемента;
- `setDisabled` — устанавливает состояния блокировки элемента;
- `setHidden` — скрывает элемент;
- `setVisible` — отображает элемент;
- `setImage` — устанавливает изображения с альтернативным текстом;
- `render` — рендерит компонент с передачей данных, если они есть.

### `EventEmitter`

Класс управления событиями в веб-приложении. Обеспечивает взаимодействие между различными компонентами.

Методы / свойства класса:

- `on` — устанавливает обработчик на определённое событие;
- `off` — позволяет снять установленный обработчик события;
- `emit` — инициирует событие с переданными данными;
- `onAll` — предоставляет возможность подписаться на все события;
- `offAll` — удаляет все зарегистрированные обработчики для всех событий;
- `trigger` — создаёт коллбэк-триггер, генерирующий указанное событие при вызове.

Использование в приложении:

- **Инициализация и подписка на события**. Компоненты, такие как `Basket`, `Card`, `Form`, `Order`, `Page`, и другие, инициализируются с экземпляром `EventEmitter`. При инициализации, компоненты подписываются на определенные события с помощью метода `on`;
- **Генерация и передача событий**. Различные действия пользователей, например: добавление товара в корзину, отправка данных формы заказа, клик на кнопку закрытия модального окна и т. д., инициируются в компонентах. Когда происходят эти действия, компоненты используют метод `emit` для генерации событий с соответствующими данными;
- **Обработка событий**. Другие компоненты, которые подписаны на эти события, получают уведомления.
  Например, при добавлении товара в корзину, компонент `Basket` подписан на событие и обновляет список выбранных товаров и общую стоимость. При отправке данных формы заказа, компонент `Order` подписан на событие и обрабатывает введенные данные;
- **Удаление обработчиков событий**. При необходимости компоненты могут снять подписку на определенные события, используя метод `off`;
- **Групповая подписка и отписка от событий**: Методы `onAll` и `offAll` предоставляют возможность подписаться на все события или отписаться от всех событий соответственно.

### `Form`

Класс ввода данных с возможностью валидации и отображения ошибок в форме.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент формы и объект событий для обработки действий пользователя;
- `onInputChange` — обрабатывает изменение значения в поле формы;
- `valid` — устанавливает состояние валидности формы;
- `errors` — выводит сообщение об ошибке;
- `render` — рендерит форму с передачей данных о состоянии и ошибках, если они есть.

### `LarekAPI`

Класс для взаимодействия с `API`.

Методы / свойства класса:

- `constructor` — принимает `API_URL`, `CDN_URL` и дополнительные опции запроса;
- `getProductItem` — получает список товаров;
- `order` — оформляет заказ.

### `Modal`

Класс отображения модального окна.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент и объект событий для обработки действий пользователя;
- `content` — устанавливает контента модального окна;
- `open` — открывает модальное окно;
- `close` — закрывает модальное окно;
- `render` — рендерит модальное окно с передачей данных о контенте.

### `Model`

Абстрактный класс базовой модели для работы с данными.

Методы / свойства класса:

- `constructor` — принимает данные базовой модели и объект событий для обработки изменений;
- `emitChanges` — передаёт указанное событие и, при необходимости, дополнительные данные;
- `isModel` — проверяет объект на принадлежность к типу `Model`.

### `Order`

Класс оформления заказа.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент и объект событий для обработки действий пользователя;
- `address ` — устанавливает адрес доставки;
- `email` — устанавливает электронную почту;
- `phone` — устанавливает номер телефона;
- `selected` — устанавливает выбранный метод оплаты.

### `Page`

Класс главной страницы приложения.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент и объект событий для обработки действий пользователя;
- `_counter` — элемент счетчика товаров в корзине;
- `_catalog` — каталога товаров;
- `_wrapper` — обертка страницы;
- `_basket` — элемент корзины;
- `_locked` — указывает на состояние блокировки страницы;
- `set` — устанавливает значение у свойства страницы;
- `get` — получает значение у свойства страницы.

### `Success`

Класс отображения сообщения об успешном оформлении заказа.

Методы / свойства класса:

- `constructor` — принимает `HTML`-элемент и объект действий для обработки событий клика;
- `total` — устанавливает стоимость заказа.