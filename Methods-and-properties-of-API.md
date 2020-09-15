#### Table of contents
* [General info](#general-info)
* [Visibility settings](#visibility-settings)
	* [`SDK API ThreadsWidget.showChat()`](#sdk-api-threadswidgetshowchat)
		* [Example](#example)
	* [`SDK API ThreadsWidget.hideChat()`](#sdk-api-threadswidgethidechat)
		* [Example](#example)
	* [`SDK API ThreadsWidget.onHideChat(callback)`](#sdk-api-threadswidgetonhidechatcallback)
		* [Parameters](#parameters)
		* [Example](#example)
	* [`SDK API ThreadsWidget.version()`](#sdk-api-threadswidgetversion)
		* [Example](#example)
	* [`SDK API ThreadsWidget.commitHash()`](#sdk-api-threadswidgetcommithash)
		* [Example](#example)
	* [`SDK API ThreadsWidget.onLoad(callback)`](#sdk-api-threadswidgetonloadcallback)
		* [Parameters](#parameters)
		* [Example](#example)
	* [`SDK API ThreadsWidget.on(event, callback)`](#sdk-api-threadswidgetonevent-callback)
		* [Parameters](#parameters)
			* [For the event name you can set the following](#for-the-event-name-you-can-set-the-following)
	* [`SDK API ThreadsWidget.setLocale(locale)`](#sdk-api-threadswidgetsetlocalelocale)
		* [Example](#example)
	* [`SDK API ThreadsWidget.getUnreadCounter()`](#sdk-api-threadswidgetgetunreadcounter)
		* [Example](#example)
	* [`SDK API ThreadsWidget.setUnavailable([Boolean])`](#sdk-api-threadswidgetsetunavailable[boolean])
		* [Example](#example)

### General info

Use global object `ThreadsWidget` to access methods and properties of API.

### Visibility settings

The below methods are devised to manage chat visibility. For example, use them if you deploy custom methods to show/hide the chat instead of the start button [стандартной стартовой кнопки](Настройка-темы-оформления#chatbutton). To switch the chat in the mode without standard start button set the parameter `isContainerHidden` in [конфигурации Чата](Структура-конфигурационного-файла-settings.json) as `true`:

```json
"isContainerHidden": true
``` 

The full example of custom button creation to manage the visibility of the chat you can find in the folder `examples/Custom button`.

#### `SDK API ThreadsWidget.showChat()`

Show chat container. 

##### Example

```html
<button onclick="ThreadsWidget.showChat()">Show</button>
```

#### `SDK API ThreadsWidget.hideChat()`

Hide chat container.

##### Example

```html
<button onclick="ThreadsWidget.hideChat()">Hide</button>
```

#### `SDK API ThreadsWidget.onHideChat(callback)`

The method is used to identify the callback function executed at the chat closure. E.g., the function can be used to make the custom button visible.

##### Parameters

`callback` - function executed at the chat closure

##### Example

```js
ThreadsWidget.onHideChat(function() {
    $('#custom').fadeIn('fast')
})
```

#### `SDK API ThreadsWidget.version()`

Method returning chat version

##### Example

```js
ThreadsWidget.version()
```

#### `SDK API ThreadsWidget.commitHash()`

Method returning the hash of the commit of the chat build

##### Example

```js
ThreadsWidget.commitHash()
```

#### `SDK API ThreadsWidget.onLoad(callback)`

The method is used to identify the callback function executed when the chat is loaded.

##### Parameters

`callback` - function executed when the chat is loaded 

##### Example

```js
ThreadsWidget.onLoad(function() {
    // remove preloaders etc.
})
```

#### `SDK API ThreadsWidget.on(event, callback)`

This method allows to set an event handler. It is necessary to set the event handlers after initializing a web chat with the `ThreadsWidget.onLoad(callback)`

##### Parameters

`callback` - the function what will be executed by the event occurrence

`event` - event name

###### For the event name you can set the following

`hideChat` -  this event occurs when the chat container is hiding

`showChat` - this event occurs when the chat container is showing

`closeChat` - this event occurs when the chat is closing (from full chat window into chat-button)

`openChat` - this event occurs when the chat is opening (from chat-button into full chat window)

`showInviteMessage` - this event occurs when an invite message is shown

`hideInviteMessage` - this event occurs when the invite message is disappearing

`changeOperationMode` - this event occurs when operation mode is changed. When an event occurs, handler will be called with data:
```js
{ 
    isNowInactive: Boolean - Get the value true / false, then the web chat should be be hidden or shown according Threads operation mode settings.
}
``` 

`changeUnreadCounter` - this event occurs when count of unread messages is changed. When an event occurs, handler will be called with new counter


#### `SDK API ThreadsWidget.setLocale(locale)`

Method changing chat locale language

##### Example

```js
ThreadsWidget.setLocale('ru')
```


#### `SDK API ThreadsWidget.getUnreadCounter()`

This method return count of unread messages in widget.

##### Example

```js
ThreadsWidget.getUnreadCounter()
```

#### `SDK API ThreadsWidget.setUnavailable([Boolean])`

The method allows to manage widget visibility.
Threads provides processing of a business scenarios when the conditions come:
* after getting call <название вызова> Threads leaves a widget visible, if a client has active thread.
* after getting call <название вызова> Threads leaves a widget visible and blocks an input field, if a client has an opened widget.
* All other calls hide the widget.

##### Example

```js
ThreadsWidget.setUnavailable(true)
```