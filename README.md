# [CSS анімація](https://codeburst.io/learning-css-animations-with-a-touch-of-javascript-985a2404dc5e)

CSS дійсно розвивався протягом багатьох років. У минулому його можно було використовувати лише для зміни простих статичних властивостей, таких як колір, розмір та стиль рамки. Він постійно вдосконалюється , і зараз ми знаходимось в точці, де можливості css анімації конкурують з JavaScript. Влада короля мов веб розробки в області анімації захоплена. Так, це звичайно перебільшення, але використання css анімації має багато переваг. Вони прості у використанні, без використання таємничого js синтаксису (хоча API веб-анімації  повинна допомогти суровим js розробникам ). CSS використовує удосконалену підтримку браузера та інтеграцію для автоматичної оптимізації при великих навантаженнях. Одна з речей, яку я ціную - це декларативний характер CSS при створенні анімації, та можливість вказати де буде анімація на кожному ключовому кадрі. Це полегшує візуалізацію коду.

Інша річ, яка мені подобається в CSS анімації - це непогана підтримка браузерами. На даний час кожен повноцінний браузер, окрім Opera-Mini (якщо можна його вважати повноцінним браузером) має підтримку СSS анімації.


![CSS Animation MDN](https://cdn-images-1.medium.com/max/800/1*-h8ZRKUONNb5iMegkGDzXw.png)


Отже, тепер, коли ви знаєте, чому анімації CSS3 - це хороший інструмент у вашому ящику, почніть його використовувати.

Все починається з властивостей анімації для елемента. Властивість *animation* насправді є скороченням для цілого ряду інших властивостей. Синтаксис скорочень виглядає наступним чином:

```css
animation: duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name;
```

Якщо вам здається що це надто багато не хвилюйтесь. Я поясню кожну підвластивість одна за одною.

* **animation-duration:** Час тривалості анімації. За замовчуванням 0,5 секунди - не дуже швидко і не дуже повільно.
    
* **animation-timing-function:** Це те ж саме, що і функція синхронізації, яка використовується для переходів, визначає, наскільки швидко анімація рухається в   залежності від того, наскільки прогресує анімація. Наприклад  ease-in-out означає, що анімація буде повільніша на початку та в кінці анімаційної шкали часу. Щоб побачити  гарну візуалізацію функцій синхронізації відвідайте [цей сайт](http://easings.net/uk).
 
* **animation-delay:** Який часовий проміжок повинен пройти до початку анімації. Дайте браузеру про це знати, використовуючи цю властивість. Значення цієї властивості може бути вказане з секундах або мілісекундах. Це значення також може бути від’ємним, якщо ви хоче щоб анімацію почалась напівдорозі. Не знаю для чого це потрібно, але наявність такої можливості є досить крутою можливістю.

* **animation-iteration-count:** Кількість циклів (повторів) анімації. Ця  властивість переплітається **animation-direction**. Ви також можете використовувати десяткові значення: якщо ви встановили анімацію, що здійснює поворот на 360 градусів, то значення 2.5 означатиме що поворот здійсниться на 180 градусів. Поєднання **animation-direction** і **animation-iteration-count** є хорошою можливістю для розуміння анімації. Для того щоб спробувати створити власну анімацію з використанням **animation-direction** і **animation-iteration-count** властивостей перейдіть по [наступній ссилці](https://codepen.io/afrench53198/embed/preview/bLYXLR?default-tabs=css%2Cresult&embed-version=2&height=600&host=https%3A%2F%2Fcodepen.io&referrer=https%3A%2F%2Fcodeburst.io%2Fmedia%2F38f4970a90124d3303602c8e4b0e4e8c%3FpostId%3D985a2404dc5e&slug-hash=bLYXLR")
  
* **animation-direction:** Ця властивість описує поведінку анімації між циклами. Значеннями цієї властивості можуть бути: *normal*, *reverse*, *alternate*, and *alternate-reverse*. Спочатку важко зрозуміти, тому я поясню більш докладніше: *Normal* означає, що анімація починатиметься спочатку на кожному циклі або ітерації. Іншими словами анімація відтворюватиметься від початку до кінця на кожному циклі. *Reverse* - анімація відтворюватиметься в зворотньому порядку. *Alternate* - анімація буде відтворюватись спочатку в прямому, а потім зворотньому порядку, чергуючи. *Alternate-reverse*  означає, що анімація робить це перший цикл у зворотному напрямку, а потім у прямому і в подальшому чергується в такому ж порядку.

* **animation-fill-mode:** Визначає стилі, які мають застосовутись до елементу, коли анімація не виконується (якщо кількість циклів не безмежна). Дозволяє встановити стиль елементу, що відповідатиме стилю останнього ключового кадру анімації, що залежить вiд **animation-fill-mode**, **animation-direction** i **animation-iteration-count**. Зв’язок між усіма властивостями найкращще проілюстрований  [в цих маленьких приємних табличках, зроблених Mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode). В коді нижче зверніть увагу, як елемент із fill-mode forward залишається в тому ж  місці після завершення анімації.

```html
<div class="container">
  <div class="none box">No fill mode!</div>
  <div class="forwards box">Forward!</div>
  <div class="alternate-even box">Forward Alternate Even</div>
  <div class="alternate-odd box">Forward Alternate Odd</div>
</div> 
```

```css
.container {
  display: grid;
  justify-items:center;
  align-items: center;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  margin-top: 100px;
}

.box {
  width: 100px;
  height: 100px;
  background-color: blue;
  margin-bottom: 10px;
  color: white;
  animation: 2s ease-in 1 scale;
}

/*none is default fill-mode value so we only have to write css for other values  */
.forwards {
  animation-fill-mode: forwards;
}
/*The animation will end at the "from" animation state since it's an even number of iterations*/
.alternate-even {
  animation-fill-mode: forwards;
  animation-iteration-count: 2;
  animation-direction: alternate;
}
/*The animation will end at the "to" state of the animation since it's an odd number of iterations*/
.alternate-odd {
  animation-fill-mode: forwards;
  animation-iteration-count: 3;
  animation-direction: alternate;
}

@keyframes scale {
  from {
  transform: scale(1)
  } to {
    transform: scale(2.0);
  }
}
```
Поданий вище код в дії можна подивитись перейшовши по [цій ссилці](https://codepen.io/afrench53198/embed/preview/MQrgex?default-tabs=css%2Cresult&embed-version=2&height=600&host=https%3A%2F%2Fcodepen.io&referrer=https%3A%2F%2Fcodeburst.io%2Fmedia%2Fc0ed29b1497b2f067e4783c6dcd6a574%3FpostId%3D985a2404dc5e&slug-hash=MQrgex)
 
 * **animation-play-state:** Основна функція цієї властивості -  відслідковувати, чи працює анімація чи призупинена. Це дозволяє призупинити анімацію і зберігати її в поточному стані, а потім запускати її з цього стану. Це можна зробити, використовуючи ці два короткі блоки коду:
   
*CSS:*

```css
.paused {
    animation-play-state: paused;
}
```
   
*JS:*
 
```javascript
 // Get references to element and controlling button
    var element = document.querySelector(".element"),
    button = document.querySelector(".buttonForElement");
     
// toggle the paused class
   button.onclick = function () {
      element.classList.toggle("paused")
   }
 ```

Додавання класу *.paused* до відповідного елементу зупиняє та відновлює анімацію натисканням кнопки. Перейди по [ссилці](https://codepen.io/afrench53198/embed/preview/EQKyWL?default-tabs=css%2Cresult&embed-version=2&height=600&host=https%3A%2F%2Fcodepen.io&referrer=https%3A%2F%2Fcodeburst.io%2Fmedia%2F8edddeb361e2ed32080603becfb5c540%3FpostId%3D985a2404dc5e&slug-hash=EQKyWL), щоб отримати правильне уявлення про те, як це буде працювати в реальному контексті анімації. 
 
 Чудово! Тепер, коли ви знаєте всі ці властивості, перейдемо до останньої (і найважливішої) підвластивості анімації: **name**.
Назва анімації виглядає як ім'я змінної або класу; це стосується поведінки анімації. Якщо ви робите анімацію вперше то для є необхідність для початку освоїти іншу тему…

### @keyframes!

Так .. що таке правило @keyframes?

Я справді не хочу робити спроби пояснити це, тому MDN зробить це за мене:
>@keyframes CSS at-правила  керують проміжними кроками в анімаційній послідовності CSS, визначаючи стилі для ключових кадрів (або точок доступу) уздовж анімаційної послідовності. Це дає більший контроль над проміжними кроками анімаційної послідовності, ніж переходи.

Отже, ми знаємо, що основні кадри - це спосіб надати чіткий контроль над анімацією в CSS. Як точно їх використовувати?

Ну, на  початку, у вас буде щось на зразок цього:

```css
/*  From-to format */
@keyframes <animation-name> {
  from {
    <beginning-property-state>
  } to  {
    <end-property-state>
  }
}
/*  Percentage format */
@keyframes <animation-name> {
  0% {
    <beginning-property-state>
  } 
 50% {
    <transitioning-property-state>
  }
/* you can go percentage point by point - thats alot of detail!!*/
  51% {
    <transitioning-property-state>
  }
  75% {
    <transitioning-property-state>
  }
  100% {
    <end-property-state>
  }
}
```

Це досить очевидно. Ви просто вказуєте стан властивості, яку ви хочете анімувати на визначеній точці під час анімації. Так це виглядає на практиці:

```javascript
/*the element in this animation will bounce into view by changing the transform property*/
@keyframes bounceIn {
  0% {
    transform: translateY(-100%)
  }
  15% {
    transform: translateY(0%);
  }
  30% {
    transform: translateY(-30%);
  }
  40% {
    transform: translateY(0%);
  }
  50% {
    transform: translateY(-20%);
  }
  70% {
    transform: translateY(0%);
  }
  80% {
    transform: translateY(-10%)
  }
  90% {
    transform: translateY(-5%)
  }
  95% {
    transform: translateY(0%)
  }
  97% {
    transform: translateY(-2%)
  }
  100% {
    transform: translateY(0%)
  }
}
```

Дивіться цей код у дії, натиснувши [Показати](https://codepen.io/afrench53198/embed/preview/EQKyWL?default-tabs=css%2Cresult&embed-version=2&height=600&host=https%3A%2F%2Fcodepen.io&referrer=https%3A%2F%2Fcodeburst.io%2Fmedia%2F8edddeb361e2ed32080603becfb5c540%3FpostId%3D985a2404dc5e&slug-hash=EQKyWL)

Тепер, коли ви знаєте, як створювати чудові анімації за допомогою ключових кадрів CSS, як ви керуєте цими анімаціями? Саме тут Javascript корисний.

Я покажу вам метод, за допомогою якого я це роблю, але я закликаю вас експериментувати та придумати більш багаторазові та більш чисті рішення. 

**Це чотири етапи процесу:**

1. Створіть анімацію

 ```javascript
 @keyframes rotate {
  from {
    transform: rotateY(0deg)
  } to {
    transform: rotateY(360deg)
  }
}
 ```
2. Додайте доступний клас CSS для перемикання за допомогою JS

```css
.activated {
  box-shadow: 0px 0px 30px black;
  transform: perspective(500px);
  transition: all ease-out 0.5s;
  animation: rotate 1s infinite ease-in-out;
  animation-delay: 0.5s;
}
/*Don't forget the paused class if you want to be able to stop the animation to stop mid-go!*/
.paused {
  animation-play-state: paused;
}
```
3. За допомогою JS отримайте кнопку керування і/або власне елемент (однак ти хочеш керувати анімацією)

```javascript
var box1 = document.querySelector("#b1");
var buttonOne = document.querySelector("#animateOne");
```
4 .Об’єднайте це разом , міняючи клас за допомогою стану елементу/кнопки

```javascript
// Here I use the button's inner HTML to track the state of the element, as the two have a hard coded relationship
buttonOne.onclick = function() {
  if (buttonOne.innerHTML === "Play") {
    this.innerHTML = "Pause";
    box1.innerHTML = "Not So fast!";
    // for the first time clicked, add the class
    if (!box1.classList.contains("activated")) {
      box1.classList.add("activated");
    }
    box1.classList.toggle("paused");
  } else {
    buttonOne.innerHTML = "Play";
    box1.innerHTML = "Spin me!";
    box1.classList.toggle("paused");
  }
};
```

Весь необхідний код (з деяким стилями), щоб зробити вікно та кнопку наведений [тут](https://codepen.io/afrench53198/embed/preview/EQKyWL?default-tabs=css%2Cresult&embed-version=2&height=600&host=https%3A%2F%2Fcodepen.io&referrer=https%3A%2F%2Fcodeburst.io%2Fmedia%2F8edddeb361e2ed32080603becfb5c540%3FpostId%3D985a2404dc5e&slug-hash=EQKyWL).

Хоча це моє рішення в даний час, але безумовно, не найкраще. Codepen мав труднощі з методом addEventListener у Javascript, але це чудовий спосіб обробляти стан анімації, про що я міг би говорити в окремій статті. Я закликаю вас шукати більш кращі, більш модульні способи створення та управління анімаціями в CSS та Javascript. Якщо у вас є кращий спосіб, надішліть його в коментарі! Я завжди шукаю способи написання більш чистого і багаторазового використовуваного коду. Я сподіваюся, вам сподобалося читати! Якщо ця стаття допомагла вам, то кілька уподобань буде чудовою подякою:)

