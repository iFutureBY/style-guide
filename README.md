# Codeworks style guides

- [HTML](#1)
  - [Правила] (#1.1)
  - [Рекомендуемый порядок атрибутов] (#1.2)
  - [Методология] (#1.3)
- [CSS](#2)
  - [Правила] (#2.1)
- [Angular](#3)
  - [Структура](#3.1)
  - [Правила](#3.2)
  - [Модули](#3.3)
  - [Контроллеры](#3.4)
  - [Директивы](#3.5)
  - [Сервисы](#3.6)
  - [Фабрики](#3.7)
  - [Фильтры](#3.8)


<a id="1"></a>
## HTML

<a id="1.1"></a>
### Правила:
- Использовать табуляцию с расстоянием в 2-пробела;
- По возможности использовать семантику тегов HTML5;
- Прописывать обязательные атрибуты title и alt для соотвествующих тегов `<a>` и `<img>`;
- Для аннулирования float использовать `clearfix`;
- Теги, классы и идентификаторы писать строчными буквами;
- Правильное написание названий классов и идентификаторов;
  - если названия классов состоят из нескольких слов, то они пишутся через дефис "-" `.header-content`;
- Названия класса должны описывать то, чем является элемент, а не как он выглядит  `.read-more-link` вместо `.red-button`

<a id="1.2"></a>
### Рекомендуемый порядок атрибутов:
1. class;
2. id, name;
3. data-*;
4. src, for, type, href, value;
5. title, alt;
6. role, aria-*;
7. angular directives.

<a id="1.3"></a>
### Методология:
БЭМ = Б__Э_М

#### 1. Что есть блок?
Блок - часть страницы, являющаяся логически независимой от остального наполнения. Представляет собой "строительную единицу" для сайта

Блок не отвечает за свое расположение. Он задает внутренние своства (размеры, шрифты и т.д.)

Разработчик сам выбирает, что есть блок, а что элемент.

Если кусок кода не имеет смысла без родителя - это скорее всего элемент.

Исключением может быть ситуация, когда у такого элемента оказывается слишком богатый внутренний мир.

Стили для каждого блока находятся в отдельном файле.

#### 2. Не бывает элементов вложенных в элементы?
Так делать нельзя.
```
.block__elem1__elem2__ ...
```
Как надо?
```
<div class="block">
  <div class="block__elem1">
  
    <div class="block__elem2">
    </div> <!-- end block__elem2 -->
    
  </div> <!-- end block__elem1 -->
  
  <div class="block__elem3">
  </div> <!-- end block__elem3 -->
</div>
```

#### 3. Глобальные модификаторы
В проекте **евровеб** вводим понятие глобального модификатора (ГМ), позволяет быстро применять некоторые стили, такие как upper-case, text-center и т.д.  
Класс ГМ начинается с '_' `._upper`

Стили для ГМ записываются в файл global-modifiers.less в папке components.


<a id="2"></a>
## CSS

<a id="2.1"></a>
### Правила:
- Использовать табуляцию с расстоянием в 2-пробела;
- Использовать пробел после “ : “  и перед  “ { ";
```
.sector {
  display: block;
  margin: 0;
}
```
- Использовать перевод на новую строку для каждого последующего CSS правила;
- Использовать пробел после запятых `rgba(0, 0, 0, 1)`;
- Всегда использовать “;” в конце CSS правила;
- Использовать перевод на новую строку при перечислении селекторов:
```
.sector_1,
.sector_2,
.sector_3 {
  display: block;
  margin: 0;
}
```
- Использовать hex код #000 (не rgb(0,0,0) или ‘black’ ). За исключением случаев `rgba(0, 0, 0, 1)`;
- Не использовать px для нулевого значения - `margin: 0` вместо `margin: 0px`;
- Минимизировать использование сокращенных деклараций по возможности;
- Использовать только lowercase символы при записи hex кода (`#dadada` вместо `#DADADA`).
- Использовать переменные CSS (LESS/SASS/SCSS) для инициализации color/size/fonts;
- Не минимизировать CSS файлы для удобного последующего редактирования/чтения.  
**Минимизация проходит во время завершения проекта при его сборке**
- Использовать общепринятый normalize файл для нормализации стандартных стилей;
- Подключать все less файлы с помощью @import в основной файл less;

<a id="3"></a>
## Angular

<a id="3.1"></a>
### Структура

Разделение по типам компонентов, затем по функциональности.
```
├── app
│   ├── app.js
│   ├── controllers
│   │   ├── home
│   │   │   ├── FirstCtrl.js
│   │   │   └── SecondCtrl.js
│   │   └── about
│   │       └── ThirdCtrl.js
│   ├── directives
│   │   ├── home
│   │   │   └── directive1.js
│   │   └── about
│   │       ├── directive2.js
│   │       └── directive3.js
│   ├── filters
│   │   ├── home
│   │   └── about
│   └── services
│       ├── CommonService.js
│       ├── cache
│       │   ├── Cache1.js
│       │   └── Cache2.js
│       └── models
│           ├── Model1.js
│           └── Model2.js
├── partials
├── lib
```
<a id="3.2"></a>
### Правила

- Если имя каталога состоит из нескольких слов, используйте разделение в стиле lisp:
```
app
 ├── app.js
 └── my-complex-module
     ├── controllers
     ├── directives
     ├── filters
     └── services
```
- Файл `app.js` должен содержать определения маршрутов, конфигурацию и/или начальную инициализацию (если требуется);
- Каждый JavaScript файл должен содержать только один компонент. Имя файла должно соответствовать названию компонента;
- Расположение скриптов в самом конце файла:
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>App</title>
    </head>
  <body>
    <div ng-app="myApp">
      <div ng-view></div>
    </div>
    <script src="angular.js"></script>
    <script src="app.js"></script>
  </body>
</html>
```
- Указывайте атрибуты AngularJS (директивы) после стандартных:  
`<input class="input" type="text" placeholder="name" require ng-model="user.name">`  

*Почему?*  
*Так будет проще отделить элементы фреймворка от HTML-разметки (что, в свою очередь, сильно облегчит
поддержку).*

- Используйте:
  - `$timeout` вместо setTimeout
  - `$interval` вместо setInterval
  - `$window` вместо window
  - `$document` вместо document
  - `$http` вместо $.ajax

- Автоматизируйте ваши процессы с помощью следующих инструментов:
  - Yeoman
  - Gulp
  - Grunt
  - Bower

- Используйте промисы (`$q`) взамен callback'ов;

*Почему?*  
*Это сделает ваш код более элегантным и чистым, а также спасет от "callback hell"*

- Используйте `$resource` вместо `$http` где это возможно;

*Почему?*  
*Более высокий уровень абстракций убережет вас от избыточного кода.*

- Не используйте глобальное пространство имён, используйте анонимные самовызывающиеся функции;
```
(function() {
  "use strict";
  
  ...
  
})();
```

- Разрешайте все зависимости с помощью Dependency Injection;

*Почему?*  
*Это уменьшит количество ошибок и убережёт от обезьяньей работы при тестировании.*

- Не захламляйте ваш $scope. Добавляйте только те переменные и функции, который будут использованы в шаблонах.

- Не используйте префикс $ при определении переменных, свойств и методов.

*Почему?*  
*Этот префикс зарезервирован для AngularJS.*

- При перечислении зависимостей сперва указывайте встроенные, потом дополнительные:
```
module.factory('Service', ['$rootScope', '$timeout', 'MyCustomDependency1', 'MyCustomDependency2',
function ($rootScope, $timeout, MyCustomDependency1, MyCustomDependency2) {
  return {
    // Something
  };
})];
```

<a id="3.3"></a>
### Модули

#### Шаблон
```
(function() {
  "use strict";
  
  angular.module('myApp', [])
    .config(function() {
    
    });
  
})();
```

- Названия модулей должны соответстовать подходу lowerCamelCase:

- Для определения иерархии:
например, что модуль `b` является подмодулем `a`, используйте пространства имён: `a.b`.


<a id="3.4"></a>
### Контроллеры

#### Шаблон
```
(function() {
  "use strict";
  
  angular
    .module('myApp')
    .controller('MainController', ['dependencies',
    function(dependencies) {
      var self = this;
    }]);
  
})();
```

- Не изменяйте DOM из контроллеров;

*Почему?*  
*Это усложнит их тестирование, а также нарушит "Принцип разделения ответственности". Используйте для этого директивы*

- Именовать контроллер следует так, чтобы его имя состояло из части, описывающей то, чем он занимается (для примера: корзина, домашняя страница, админ-панель) и постфикса Controller;

-  Контроллеры - это стандартные конструкторы, соответвенно их имена записываются в UpperCamelCase (HomePageCtrl, ShoppingCartCtrl, AdminPanelCtrl, и т.д.);

- Контроллеры не должны быть объявлены в глобальном пространстве;

- Использовать синтаксис `controller as`:
```
<div ng-controller="MainController as main">
 {{ main.title }}
</div>
```
- Держите контроллеры настолько маленькими на сколько это возможно. Вынесите общие функции в сервисы;

- Не помещайте бизнес-логику в контроллеры. Вынесите её в сервис, как model;

- Организовывайте коммуникацию между контроллерами используя вызовы методов (например когда дети хотят связаться с родителями) или методы `$emit`, `$broadcast` и `$on`;

- Количество `$emit` и `$broadcast` сообщений должно быть сведено к минимуму;

- Если вам нужно отформатировать данные, перенесите логику форматирования в фильтр и укажите его как зависимость:


<a id="3.5"></a>
### Директивы

#### Шаблон
```
(function() {
  "use strict";
  
  angular
    .module('myApp')
    .directive('prefix-myDirective',
    function() {
      var directive = {
        restrict: 'EA',
        templateUrl: 'templateUrl',
        link: linkFunc,
        controller: ['dependencies', Controller]
      }
      
      return directive;
      
      function linkFunc(scope, el, attr) {

      }

      function Controller(dependencies) {
        var self = this;
      }
    });

})();
```

- Называйте ваши директивы используя `lowerCamelCase`;

- Используйте `scope` вместо `$scope` в функции link;

*Почему?*  
*При использовании функций compile, post/pre link им будут переданы предопределённые аргументы, которые нельзя будет
изменить, используя DI. Такой стиль используется и внутри самого AngularJS*

- Используйте кастомные префиксы для ваших директив во избежание коллизий со сторонними библиотеками. (две первые буквы имени приложения);

- Не используйте префиксы `ng` или `ui`, так как они зарезервированы для использования в `AngularJS` и `AngularJS UI`;

- Манипуляции с DOM должны производиться только с помощью директив;

- Определяйте директивы через атрибуты или элементы, не используйте для этого классы или комментарии;

- Не забывайте про `$sce`, когда работаете с непроверенным контентом.


<a id="3.6"></a>
### Сервисы

#### Шаблон
```
(function() {
  "use strict";
  
  angular
    .module('myApp')
    .service('Service', ['dependencies',
    function(dependencies) {
      var self = this;
      self.func = func;

      function func() {
      
      }
    }]);
    
})();
```

<a id="3.7"></a>
### Фабрики

#### Шаблон
```
(function() {
  "use strict";
  
  angular
    .module('myApp')
    .factory('factory', ['dependencies',
    function(dependencies) {
      var service = {
        func: func
      };
      
      return service;
      
      function func() {
      
      }
    }]);
    
})();
```

<a id="3.8"></a>
### Фильтры

#### Шаблон
```
(function() {
  "use strict";
  
  angular
    .module('myApp')
    .filter('filter', function() {
      return filter

      function filter(params) {
        return params;
      }
    }]);
    
})();
```
