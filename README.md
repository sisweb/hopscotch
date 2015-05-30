Russian docs examples: http://devdocs.ru/verstka/virtual-tour-your-site-or-application/


Виртуальный тур по вашему сайту или приложению
24 декабря 2014 Автор: maxyc·Нет комментариев	

Представляю вам простой и легкий фреймворк на Javascript для быстрого и удобного создания виртуального тура по вашему сайту или приложению.

Hopscotch

Имя этого фреймворка - Hopscotch. Этот фреймворк принимает в качестве опций обычный JSON объект и предлагает разработчикам интерфейс для удобного и простого позиционирования каждого шага тура.
Основные преимущества

    Коллбэки (например, onStart, onEnd, onShow, onNext, onPrev, onClose)
    Возможность работы со множеством страниц по средствам sessionStorage (используются Cookies в качестве запасного варианта)
    Интернационализация
    и т.д.

Как использовать

Для начала использования просто подключите hopscotch.css и hopscotch.js на странице. Эти действия подключат объект в глобальную область видимости js.
?

	
<html>
  <head>
    <title>Мой первый тур по сайту</title>
    <link rel="stylesheet" href="css/hopscotch.css"></link>
  </head>
  <body>
    <h1 id="header">Мой первый тур по сайту</h1>
    <div id="content">
      <p>Контент помещается здесь...</p>
    </div>
    <script src="js/hopscotch.js"></script>
    <script src="js/my_first_tour.js"></script> <!-- в этом файле прописывайте ваш тур -->
  </body>
</html>

В файле my_first_tour.js опишите и запустите ваш тур.
?

	
// определение тура
   var tour = {
     id: "hello-hopscotch",
     steps: [
       {
         title: "Мой заголовок",
         content: "Это заголовок на моей странице.",
         target: "header",
         placement: "right"
       },
       {
         title: "Мой контент",
         content: "Здесь я размещаю свой контент.",
         target: document.querySelector("#content p"),
         placement: "bottom"
       }
     ]
   };
 
   // Запустите ваш тур по сайту
   hopscotch.startTour(tour);

И это все что требуется!
Определение шагов тура

Hopscotch содержит ID тура, массив шагов, определенный в виде JSON данных где для каждого шага указываются специфические настройки. ID тура простой и уникальный идентификатор-строка. Тур должен содержать как минимум ID тура и массив из 1 или более шагов.
Основные настройки шагов тура
?

{
  id: "welcome_tour",
  steps: [
    {
      target: "header",
      placement: "bottom",
      title: "Это основное меню сайта",
      content: "Используйте меню для навигации по сайту"
    },
    {
      target: "profile-pic",
      placement: "right",
      title: "Изображение вашего профиля",
      content: "Загрузите изображение кликнув по этой кнопке."
    },
    {
      target: "inbox",
      placement: "bottom",
      title: "Ваша почта",
      content: "Сообщения от других участников сайта."
    }
  ]
}

Очень важно: title и content указываются с помощью element.innerHTML. Это позволяет вставлять html элементы в эти поля. Будьте осторожны, помимо html туда можно вставить и вредоносный код. Всегда проверяйте, что вставляете в это поле.
Основной список настроек шагов тура:
 Обязательные

    target [STRING/ELEMENT/ARRAY] - id DOM элемента или сам DOM элемент, к которому привязывается шаг. Также можно указать массив из нескольких элементов. В этом случае Hopscotch прикрепит шаг к первому найденному элементу из списка.
    placement [STRING] - указывается где будет выводиться всплывающее окошко. Возможные значения: "top", "bottom", "right", "left".

Необязательные

    title [STRING] - заголовок шага
    content [STRING] - Содержимое
    width [INT] - ширина всплывающего окна
    padding [INT] - паддинг всплывающего окна
    xOffset [INT] - горизонтальное положение для всплывающего окна. Значение можно указать в пикселях или "center". По умолчанию: 0.
    yOffset [INT] - вертикальное положение для всплывающего окна. Значение можно указать в пикселях или "center". По умолчанию: 0.
    arrowOffset [INT] - положение стрелки всплывающего окна. Значение можно указать в пикселях или "center". По умолчанию: 0.
    delay [INT] - сколько милисекунд ждать перед переходом к следующему шагу. По умолчанию: 0.
    zindex [INT] - z-index для всплывающего окна
    showNextButton [BOOLEAN] - Показывать кнопку далее. По умолчанию: true.
    showPrevButton [BOOLEAN] - Показывать кнопку назад. По умолчанию: true.
    showCTAButton [BOOLEAN] - Показывать кнопку call-to-action. По умолчанию: false.
    ctaLabel [STRING] - заголовок для кнопки call-to-action.
    multipage [BOOLEAN] - следует ли считать следующий шаг на другой странице. По умолчанию: false.
    showSkip [BOOLEAN] - Если true, кнопка 'Далее' определяется как 'Пропустить'. Default: false.
    fixedElement [BOOLEAN] - укажите true если требуемый элемент имеет фиксированное позиционирование. По умолчанию: false.
    nextOnTargetClick [BOOLEAN] - вызывает событие nextStep() когда по требуемому элементу кликнули мышкой. По умолчанию: false.

События

    onPrev [FUNCTION] - коллбэк на событие нажатия кнопки "Назад"
    onNext [FUNCTION] - коллбэк на событие нажатия кнопки "Далее"
    onShow [FUNCTION] - коллбэк на событие показа первого шага
    onCTA [FUNCTION] - коллбэк на событие нажатия кнопки "call-to-action"

Настройки тура в целом

Настройки могут быть указаны с использованием JSON данных или вызовом метода hopscotch.configure(). Данные настройки применяются ко всему туру на странице. В случае когда настройки тура перекрещиваются с настройками отдельнго шага , (например, "showPrevButton") приоритет отдается настройкам шага. Когда коллбэки определяются и в туре, и в шаге, то вызывается сначала коллбэк шага, затем коллбэк тура.

    id [STRING] - Обязательно: уникальный строковый идентификатор тура.
    bubbleWidth [NUMBER] - Ширина всплывающего окна по умолчанию. По умолчанию: 280.
    bubblePadding [NUMBER] - Паддинг всплывающего окна по умолчанию. По умолчанию: 15.
    smoothScroll [BOOLEAN] - Использовать ли плавную прокрутку к следующему шагу? По умолчанию: true.
    scrollDuration [NUMBER] - Время, которое должно потратиться на скроллинг страницы в ms. Работает только если smoothScroll установлен в true. По умолчанию: 1000.
    scrollTopMargin [NUMBER] - Когда страница скролится, сколько места должно быть между всплывающим окном и верхом вьюпорта? По умолчанию: 200.
    showCloseButton [BOOLEAN] - Надо ли показывать кнопку "закрыть"? По умолчанию: true.
    showPrevButton [BOOLEAN] - Надо ли показывать кнопку назад? По умолчанию: false.
    showNextButton [BOOLEAN] - Надо ли показывать кнопку далее? По умолчанию: true.
    arrowWidth [NUMBER] - Ширина стрелки по умолчанию (место между всплывающим окном и требуемым элементом). Используется для калькуляции позиции всплывающего окна. Опция пригодится, если вам потребуется изменить стрелку в вашем css. По умолчанию: 20.
    skipIfNoElement [BOOLEAN] - Если указанный элемент не найден, надо ли переходить к следующему шагу? По умолчанию: true.
    nextOnTargetClick [BOOLEAN] - Надо ли переходить к следующему шагу после клика по требуемому элементу? По умолчанию: false.
    onNext [FUNCTION] - Выполняется после каждого клика по кнопке "Далее".
    onPrev [FUNCTION] - Выполняется после каждого клика по кнопке "Назад".
    onStart [FUNCTION] - Выполняется перед началом тура.
    onEnd [FUNCTION] - Выполняется после окончания тура.
    onClose [FUNCTION] - Выполняется когда пользователь решил закрыть тур.
    onError [FUNCTION] - Выполняется когда требуемый элемент не найден на странице.
    i18n [OBJECT] - Для интернационализации. Позволяет изменять тексты кнопок и номеров шагов.
    i18n.nextBtn [STRING] - Название кнопки "Далее"
    i18n.prevBtn [STRING] - Название кнопки "Назад"
    i18n.doneBtn [STRING] - Название кнопки "Закончить"
    i18n.skipBtn [STRING] - Название кнопки "Пропустить"
    i18n.closeTooltip [STRING] - Текст для тултипа кнопки закрыть

Думаю основные моменты в этой статье я раскрыл. Если будут вопросы, пишите комментарии либо обратитесь к странице проекта за примерами.

![Example Hopscotch tour](/demo/img/screenshot.png)

Hopscotch [![Build Status](https://api.travis-ci.org/linkedin/hopscotch.png)](http://travis-ci.org/linkedin/hopscotch)
=========
Hopscotch is a framework to make it easy for developers to add product tours to their pages. Hopscotch accepts a tour JSON object as input and provides an API for the developer to control rendering the tour display and managing the tour progress.

To learn more about Hopscotch and the API, check out [linkedin.github.io/hopscotch](http://linkedin.github.io/hopscotch/).

What's Here?
------------
- `/archives` contains .zip and .tar.gz files of prior and current distributions of Hopscotch.
- `/demo` has a simple demo page with a Hopscotch tour. Much of the content duplicates what's on the github.io page.
- `/dist` includes compiled files for the current version of Hopscotch. This folder gets zipped up into an archive when a new release is published.
- `/src` contains source files for Hopscotch, including JavaScript and Less. If you're making changes to contribute back to the core repository, this is where you'll want to make them.
- `/test` is our testing suite for the core framework, written using Jasmine.

How do I get started with Hopscotch?
------------------------------------
The Hopscotch files included in `/dist` is a good starting point for working with Hopscotch. Out of the box, Hopscotch includes the core JavaScript for running and interacting with tours, a default template for rendering bubbles, and a default CSS file to provide a basic look and feel for your tours. To get started, simply include these files on your page, then use the Hopscotch API to start a tour. While Hopscotch will use YUI or jQuery if they're present, they're not required.

Check out [linkedin.github.io/hopscotch](http://linkedin.github.io/hopscotch/) for usage examples and a live sample tour. If you'd like to tweak some of the default assets included with Hopscotch to best suit your project's needs, read on for details about how to modify and rebuild a custom version of Hopscotch.

How do I build Hopscotch?
-------------------------
Hopscotch is built using Grunt.js. [Learn more about how to get started with Grunt](http://gruntjs.com/getting-started). Running `grunt` will build Hopscotch (publishing artifacts to `/tmp`) and run the test suite against the newly built artifacts.

How do I test Hopscotch?
------------------------
Testing is done as part of the build process using the [Jasmine testing framework](http://jasmine.github.io/edge/introduction.html). You can run `grunt test` to verify changes.

Continuous integration is run against every pull request using [Travis CI](https://travis-ci.org/). Please verify your changes against the test suite before submitting a pull request! We also recommend adding new tests for any new features or bugfixes as feasible.

How do I tweak Hopscotch to meet my project's requirements?
-----------------------------------------------------------
Depending on your use case, you might want to modify and/or rebuild some of the basic components included with Hopscotch. Some moddable options include...

- CSS tweaks: The Hopscotch stylesheet is written in and compiled using [LESS](http://lesscss.org/). If you make changes to your local copy of these stylesheets, they'll be recompiled when building Hopscotch.
- Bubble markup: The internal markup for Hopscotch bubbles are rendered using templates. See the README.md file in `/src/tl` for details. Any templates in `/src/tl` will be compiled into JavaScript using JST when building Hopscotch and included at the bottom of Hopscotch.js.
- Callbacks & Page Interactivity: See [linkedin.github.io/hopscotch](http://linkedin.github.io/hopscotch/) for details about the Hopscotch API and what tour/callout events you can register events with. Use callbacks to integrate Hopscotch with other libraries and/or presentational elements you might have on your page.

I want to contribute! How can I help?
-------------------------------------
See CONTRIBUTING.md for details on how to contribute back to the public Hopscotch repository on GitHub.
