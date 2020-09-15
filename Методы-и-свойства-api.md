#### Содержание
* [Общая информация](#общая-информация)
* [Управление видимостью виджета](#управление-видимостью-виджета)
	* [`SDK API ThreadsWidget.showChat()`](#sdk-api-threadswidgetshowchat)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.hideChat()`](#sdk-api-threadswidgethidechat)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.onHideChat(callback)`](#sdk-api-threadswidgetonhidechatcallback)
		* [Параметры](#параметры)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.version()`](#sdk-api-threadswidgetversion)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.commitHash()`](#sdk-api-threadswidgetcommithash)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.onLoad(callback)`](#sdk-api-threadswidgetonloadcallback)
		* [Параметры](#параметры)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.on(event, callback)`](#sdk-api-threadswidgetonevent-callback)
		* [Параметры](#параметры)
			* [Для event аргумента могут использоваться следующие имена событий](#для-event-аргумента-могут-использоваться-следующие-имена-событий)
	* [`SDK API ThreadsWidget.setLocale('localeCode')`](#sdk-api-threadswidgetsetlocalelocalecode)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.reInit([Object])`](#sdk-api-threadswidgetreinit[object])
		* [Пример перехода в неавторизованный режим](#пример-перехода-в-неавторизованный-режим)
		* [Пример перехода в авторизованный режим](#пример-перехода-в-авторизованный-режим)
	* [`SDK API ThreadsWidget.getUnreadCounter()`](#sdk-api-threadswidgetgetunreadcounter)
		* [Пример](#пример)
	* [`SDK API ThreadsWidget.setUnavailable([Boolean])`](#sdk-api-threadswidgetsetunavailable[boolean])
		* [Пример](#пример)

### Общая информация

Для обращения методам и свойствам API используется глобальный объект `ThreadsWidget`

### Управление видимостью виджета

Нижеприведенные методы предназначены для управления видимостью Чата. Их следует использовать в случае, когда вместо [стандартной стартовой кнопки](настройка-темы-оформления#chatbutton) используется другой способ (например, пользовательская стартовая кнопка) чтобы показать/скрыть Чат. Для переключения Чата в режим без стандартной стартовой кнопки нужно установить в [конфигурации Чата](Структура-конфигурационного-файла-settings.json) параметр `isContainerHidden` в значение `true`:

```json
"isContainerHidden": true
``` 

Полный пример создания собственной кнопки для управления видимостью Чата вы найдете в директории `examples/Custom button` SDK.

#### `SDK API ThreadsWidget.showChat()`

Отобразить контейнер с Чатом. 

##### Пример

```html
<button onclick="ThreadsWidget.showChat()">Показать</button>
```

#### `SDK API ThreadsWidget.hideChat()`

Скрыть контейнер с Чатом. 

##### Пример

```html
<button onclick="ThreadsWidget.hideChat()">Скрыть</button>
```

#### `SDK API ThreadsWidget.onHideChat(callback)`

Метод позволяет указать функцию обратного вызова, выполняющуюся при закрытии Чата. Например, эта функция может использована для того, чтобы сделать пользовательскую стартовую кнопку видимой.

##### Параметры

`callback` - функция, которая будет выполнена при закрытии Чата

##### Пример

```js
ThreadsWidget.onHideChat(function() {
    $('#custom').fadeIn('fast')
})
```

#### `SDK API ThreadsWidget.version()`

Метод, возвращающий версию Чата

##### Пример

```js
ThreadsWidget.version()
```

#### `SDK API ThreadsWidget.commitHash()`

Метод, возвращающий хеш коммита, на котором собран Чат

##### Пример

```js
ThreadsWidget.commitHash()
```

#### `SDK API ThreadsWidget.onLoad(callback)`

Метод позволяет указать функцию обратного вызова, выполняющуюся при завершении загрузки Чата. 

##### Параметры

`callback` - функция, которая будет выполнена при завершении загрузки Чата

##### Пример

```js
ThreadsWidget.onLoad(function() {
    // remove preloaders etc.
})
```

#### `SDK API ThreadsWidget.on(event, callback)`

Метод позволяет установить обработчики событий. Устанавливать обработчики событий необходимо после инициализации используя метод `ThreadsWidget.onLoad(callback)`

##### Параметры

`callback` - функция, которая будет выполнена при наступлении события

`event` - наименование события

###### Для event аргумента могут использоваться следующие имена событий

`hideChat` - событие наступает при скрытии контейнера чата

`showChat` - событие наступает при появлении контейнера чата

`closeChat` - событие наступает при закрытии чата

`openChat` - событие наступает при открытии чата

`showInviteMessage` - событие наступает при появлении приветственного сообщения

`hideInviteMessage` - событие наступает при скрытии приветственного сообщения

`changeOperationMode` - событие наступает при изменении режима работы чата. После наступление события вызовется обработчик в который будут переданы данные. 
```js
{ 
    isNowInactive: Boolean - Принимает значение true/false, если наступило событие когда чат стал не актиывным/активным, согласно настройкам режима работы чата
}
``` 

`changeUnreadCounter` - событие наступает при появлении непрочитанных сообщений в чате. В обработчик будет передано количество непрочитанных сообщений. 


#### `SDK API ThreadsWidget.setLocale('localeCode')`

Метод позволяет на лету изменять язык локализации Чата

##### Пример

```js
ThreadsWidget.setLocale('en')
```

#### `SDK API ThreadsWidget.reInit([Object])`

Переинициализация Чата. Для SPA веб-сайтов метод позволяет без перезагрузки страницы перевести чат из авторизованного режима в неавторизованный и наоборот. `Object` - объект, где ключем является значение параметра `webchat/clientId` файла конфигурации `settings.json`, а его значением идентификатор авторизованного клиента. Если передать в качестве значения пустую строку, то чат перейдет в неавторизованный режим.

##### Пример перехода в неавторизованный режим

```js
ThreadsWidget.reInit({
	clientId: ''
})
```

##### Пример перехода в авторизованный режим

```js
ThreadsWidget.reInit({
	clientId: 'h5lkdj3dxdkjdn123oxsdmvkaffqef'
})
```


#### `SDK API ThreadsWidget.getUnreadCounter()`

Метод возвращает количество непрочитанных сообщений в виджете

##### Пример

```js
ThreadsWidget.getUnreadCounter()
```

#### `SDK API ThreadsWidget.setUnavailable([Boolean])`

Метод позволяет на лету изменять доступность чата.

При этом Threads обеспечивает обработку бизнес-сценария, при наступлении соответсвующих условий:
* если был вызов "сделать чат недоступным", когда у клиента активный тред, то threads оставляет чат доступным
* если был вызов "сделать чат недоступным", когда у клиента не было активного треда, но виджет был развернут - чат остается видимым, но поле ввода не доступно
* в остальных случаях произойдет скрытие чата

##### Пример

```js
ThreadsWidget.setUnavailable(true)
```