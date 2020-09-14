<!--mdMenu:ru-->

### Руководство по началу работы

Виджет Чата предназначен для взаимодействия ваших клиентов и компании, обеспечивает прием и отправку сообщений. Передача сообщений происходит с помощью протокола WebSocket.

В этом руководстве вы найдете инструкции для настройки и включения чата на своем сайте.

### Следуйте приведенному алгоритму:

#### 1. Получите у аккаунт-менеджера реквизиты для подключения библиотеки для следующих параметров:

    webchat/package 
    webchat/uid
    webchat/websocket
    webchat/datastore 
    webchat/apiUrl
    webchat/history/url 
    webchat/unauthorizedHistory/url

#### 2. Скачайте файл [web-notification-sw.js](../demo/WebPush/web-notification-sw.js)

Файл нужно положить в папку с `settings.json`, который содержит стандартные настройки + `skins` + `WebPush`, об этом же `settings.json` идет информация ниже в п.5 (для включения браузнерных веб-нотификаций о получении новых сообщений в виджете)

#### 3. Скачайте актуальную версию виджета для настройки чата

Либо со страницы: releases (Важно: версия виджета не должна быть новее версии backend приложения)
Либо с главной страницы -> нажать на кнопку `Code` -> нажать на `Download ZIP`

#### 4. Разместите файлы виджета `***.min.js`, `***.min.css` в корне или каком-либо каталоге своего сайта

#### 5. Скачайте пример конфигурационного файла [`settings.json`]()

Указать ссылку на файл, который содержит и `examples/Skins` и `examples/WebPush` (т.е. файл должен быть 1 и содержать: все базовые настройки+настройка темы `skins` + `pushNotification`, пример: `settings.json`)

#### 6. Настройте в файле `settings.json` параметры, данные которых были получены от аккаунт-менеджера на шаге 1.

#### 7. Настройте цветовую схему, подходящую вашему сайту.

В секции `skin`. В примере файла параметры отвечают за цвета следующих элементов:
![Цвета в skin](assets/ru/skin-palette.png)

<table>
<tr>
    <td>
        <img src="assets/ru/chat-colors.png">
    </td>
    <td valign="top">
        <b>colorMain</b><br>
        1: фон сообщений клиента><br>
        2: фон поля ввода сообщения<br>
        <br>
        <b>colorSecond</b><br>
        3: фон области предпросмотра вложений<br>
        <br>
        <b>colorLines</b><br>
        4: фон сообщений оператора<br>
        <br>
        <b>colorSubText</b><br>
        5: цвет кнопки скрытия чата<br>
        6: цвет системных сообщений<br>
        <br>
        <b>colorText</b><br>
        7: цвет текста в шапке<br>
        <br>
        <b>colorBackground</b><br>
        8: фон виджета<br>
        9: цвет текста области предпросмотра вложений<br>
        10: цвет текста поля ввода сообщения<br>
    </td>
</tr>
</table>


#### 8. Настройте WebPush уведомления: 

Создайте проект Firebase для работы пушей (Вставить инструкцию со скринами из документа )
Настройте файл `firebase-messaging-sw.js` по этому шаблону <ссылка на пример в github> файл нужно положить в папку с `settings.json`, который содержит стандартные настройки + `skins` + `WebPush`, об этом же `settings.json` идет информация в п.5. В config приведите параметры service worker для виджета:
 
Пример:
<details>
    <summary>Пример развернуть</summary>

    var config = {
        "enable": false,
        "firebaseConfig": {"apiKey": "AIzaSyD2pk0enxE82dREjQhnhwhwTcgAoH3x0hs",
        "authDomain": "peterbald-d876e.firebaseapp.com",
        "databaseURL": "https://peterbald-d876e.firebaseio.com",
        "projectId": "peterbald-d876e",
        "storageBucket": "peterbald-d876e.appspot.com",
        "messagingSenderId": "252946030934",
        "appId": "1:252946030934:web:bf31cad72130232e43f6f7"},
        "title": "Threads Chat",
        "icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAMAAAAp4XiDAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAABOUExURUxpcejo6Onp6enp6eTk5Onp6erq6uvr6+np6eXl5enp6ejo6Ovr6+zs7Ojo6Onp6ePj4+rq6pmZmdPT06enp+bm5p6entra2sLCwrm5ueNweO8AAAARdFJOUwBOiKUcunn78A3dnllqk8XwLooT9gAAAWVJREFUSMedllmShSAMRXHggYq+YhLd/0bbtluLJODA/SR1yiQmFxgj6tTEeymE7PmkOnarduRCRxJ8bK+BQSc05KGuljopWWfyqzLADlUp4qMv9aFJNfpGDUqu++pbfSHT6AdqXtSRqKeiUR+Cp6dn3zrcXW+d2eQs6fVRTo0CYQd2KKBQ/T8l6CNhNqdmxMi/2UFz5SNiY1BFw/4R9O3VAK0o/PuZEZ3NEJlReNwQjvIySCgzvnVYvENEx5R+h2jFprfIhEu5Rzjr3yI9I9t702QtmcBHDiIOxwVFFogsFCGJBYgEmlivLzMjeW3lc3JmY4Rs2dbkia7rmp/j/VcquvYxQg1A0bFc4IotdCxhMQhIQBytmHUmIeA0I1jkkASQ07SxXQRzoRDbxWlK9gqxwJQO63uC1NBgvcsTzkODPWzc26w8svGSy6LkSiq5+Aqu15JLvOipUPIgKXn2FD2uHj3hfgChdIQNPQdYDAAAAABJRU5ErkJggg=="
    };
</details>

где
enable - настройка включения/выключения функционала; Значения: true, false
firebaseConfig - параметры подключений к платформе firebase, настройка service worker;
title - заголовок, который будет видеть клиент в пуш-уведомлении;
icon - иконка пуш-уведомления.

Аналогично настройте секцию `pushNotification` в `settings.json`.
Передайте аккаунт-менеджеру sender_id и api_key из вашего проекта Firebase (указаны в разделе Cloud Messaging) 

#### 9. Встройте виджет на сайт: 
 Подключите виджет: 
 Для установки виджета Чата на странице, где он будет отображаться, необходимо перед закрывающим тегом `</body>` добавить следующий инициализационный код: 

```
<!-- BEGIN THREADS {literal} -->
<script type="text/javascript">
!function(configurationFile,e){"use strict";configurationFile=configurationFile||"/settings.json";var t=window,a=document;t.ThreadsWidget={isDummy:!0},["hideInvite","version","commitHash","showChat","hideChat","onHideChat","onScenarios","onLoad"].forEach(function(e){t.ThreadsWidget[e]=function(a){var n,i,o;n=e,i=a,o=setInterval(function(){t.ThreadsWidget&&!t.ThreadsWidget.isDummy&&(clearInterval(o),t.ThreadsWidget[n]&&t.ThreadsWidget[n](i))},100)}});var n,i=(n=new XMLHttpRequest,function(e,t,a,i){n.onreadystatechange=function(){if(4===n.readyState)if(200===this.status)a(n.response);else{if("function"!=typeof i)throw new Error(n.response);i(n)}},n.open(e,t),n.send()});function o(t){t.webchat&&(t.webchat.filename=t.filename),t.style&&(t.webchat.style=t.style),e&&"string"==typeof e&&(t.webchat.currentLocale=e),e&&"object"==typeof e&&(e.locale&&"string"==typeof e.locale&&(t.webchat.currentLocale=e.locale),e.unavailable&&"boolean"==typeof e.unavailable&&(t.webchat.isUnavailableOnStart=e.unavailable));try{sessionStorage.setItem("__threadsWidget",JSON.stringify(t.webchat))}catch(e){window.__threadsWidget=JSON.stringify(t.webchat)}if(t.filename){var n=a.createElement("script");n.type="text/javascript",n.async=!0,n.src=t.filename;var i=a.getElementsByTagName("script")[0];i?i.parentNode.insertBefore(n,i):a.body.appendChild(n)}else console&&console.error("Invalid bundle")}function s(){i("GET",configurationFile+"?rnd="+Math.random(),function(e){var t=JSON.parse(e);o(t)})}"complete"===a.readyState?s():t.attachEvent?t.attachEvent("onload",s):t.addEventListener("load",s,!1)}("settings.json",{});
</script>
<!-- {/literal} END THREADS -->
```

 Подключите файл настроек:
 Скопируйте файл `settings.json` в тот же каталог, где расположен Чат.
 Обратите внимание: в самом конце скрипта инициализации задается путь к файлу настроек `settings.json`: 
... (`settings.json`);
 Обязательно установите в качестве значения этого параметра абсолютный путь к файлу настроек от корня вашего сайта. Пример: 
(`/your/path/to/settings.json`)
 В корне сайта разместите файл "web-notification-sw.js" для работы браузнерных веб-нотификаций и файл "firebase-messaging-sw.js" для работы WebPush. Скрипты должны быть доступны по адресам http(s):/****/web-notification-sw.js и http(s):/****/firebase-messaging-sw.js (**** - домен на котором осуществляете настройки)
 Сохраните изменения и опубликуйте их на своем сайте

#### 10. Откройте страницу на своем сайте

#### 11. В случае корректной настройки в нижнем правом углу браузера появится кнопка для открытия чата. При нажатии на нее загрузится стартовое окно чата.

После встраивания убедитесь, что все настройки выполнены корректно, проведя несколько простых базовых тестов:
- Авторизуйтесь в Интерфейсе оператора Threads и переведите оператора в статус "Активен" с помощью ползунка в правой верхней части интерфейса (реквизиты для доступа вам сообщит аккаунт-менеджер);
- Отправьте сообщение из виджета. В интерфейсе оператора вы увидите обращение из чата;
- Ответьте на сообщение в Интерфейсе оператора. В чате вы увидите ответ оператора;
- Попробуйте отправить таким образом несколько сообщений, в том числе отправить вложения. Убедитесь, что после прочтения сообщения получателем в чате отправителя у сообщения появляются 2 галочки, свидетельствующие о работе статусов прочитанности;

При возникновении проблем с отправкой и/или получением сообщений необходимо проверить корректность выполненных настроек.

В случае возникновения вопросов по деталям настройки вы всегда можете уточнить необходимую информацию у наших инженеров внедрения, написав на [support@mfms.ru](mailto:support@mfms.ru), или обратиться к своему аккаунт-менеджеру
