## Таймер обратного отсчета с настройкой по дате
НЕТ ЗАВИСИМОСТЕЙ JQUERY\
Очень часто на страницы (лендинги акционные страницы) которые нужны очень срочно 
просят поставить таймеры обратного отсчета с нестандартной логикой. 

Например:\
На странице есть таймер обратного отщета который повышает цену на товар после окончания выделеного времени.\
Таймер отображается на странице в нескольких местах.\
Цену нужно повышать в конкретные дни и фиксированое время.\
Пример бизнес логики таймера:
- 10.11.2018 9 00  - первое повышение цены
- 10.12.2018 11 00  - вотрое повышение цены
- 10.12.2018 19 00  - третее повышение цены
- 10.12.2018 23 00  - четвертое повышение цены
- 10.13.2018 23 00  - пятое повышение цены
- 10.13.2018 24 00  - скидка заканчивается
## Быстрый старт

```html
<div style="display: none;" id="myTimer1">
  <div>
    <strong>[days2]</strong>[days1][days0] :
    <strong>[hours1]</strong>[hours0] : <strong>[mins1]</strong>[mins0] :
    <strong>[secs1]</strong>[secs0]
  </div>
</div>
<div style="display: none;" id="myTimer2">
  <div>[days] : [hours] : [mins] : [secs]</div>
</div>

```
```html
<script src="DPTimerData.js"></script>
<script>
var timer = new DPTimerData({ 
  htmLayoutIds: ['myTimer1','myTimer2'], // масив id контейнеров верстки таймера
  // показываем верстки таймера сss свойством 'display: block,inline-block,flex и тд'
  displays: ['block','block'], // показываем верстки таймера
  // timeZone 'если ваш (GMT-3) то timeZone: -3'
  timeZone: 3, // для времени по которому вам удобно заводить таймер
  //timers[] - завести таймер на определенное время когда он отработает начнет
  //работать следующий таймер в масиве
  timers: [
    {
      stopDate: { // Дата когда заканчивается таймер. (счет с текущего дня)
        day: 10, month: 8, year: 2017, hour: 3, minute: 33, sec: 0
      },
      timerStarted: function () { // хук для бизнеслогики
        console.log("таймер 1 начал работу!!");
      },
      timerFinished: function () { // хук для бизнеслогики
        console.log("Таймер 1 закончил работу!!");
      }
    },
    {
      stopDate: { // Дата когда заканчивается таймер. (счет с текущего дня)
        day: 10, month: 8, year: 2017, hour: 3, minute: 34, sec: 0
      },
      timerStarted: function () { // хук для бизнеслогики
        console.log("таймер 2 начал работу!!");
      },
      timerFinished: function () { // хук для бизнеслогики
        console.log("Таймер 2 закончил работу!!");
      }
    }
    // ... любое количество промежутков
  ]
});
timer.start();
</script>

```
## Важно!
DPTimerData представляет собой один обьект который будет 
показывать одинаковое время во всех верстках с id прописаных в htmLayoutIds
согласно логике с конфигурированой в timers.\
На одной странице может быть несколько обьектов DPTimerData.

## Построение верстки таймера
[days2][days1][days0] : [hours1][hours0] : [mins1][mins0] : [secs1][secs0]

365: 02: 15: 33\
[days] = 365; [hours] = 2;  [mins] = 15;  [secs] = 33;\
[days2] = 3; [hours1] = 0;  [mins1] = 1;  [secs1] = 3;\
[days1] = 6; [hours0] = 2;  [mins0] = 5;  [secs0] = 3;\
[days0] = 5;\
Когда скрипт запустится переменные [days2], [days1], [days0], [hours1], [hours0], [mins1], [mins0], [secs1], [secs0] 
заменятся на числа от 0 - 9.\
```html
<div style="display: none;" id="TIMER_ID1">
  <div>[days2][days1][days0] : [hours1][hours0] : [mins1][mins0] : [secs1][secs0]</div>
</div>

```
Таймер на странице может быть уже сверстан. Вы можете подставить замисть цифр [values] а обертке таймера назначить id.
Если [values] подставить в имена класов то будут генерироваться нужные класы и дизайн таймера может быт абсолютно любым.
```html
<div style="display: none;" id="TIMER_ID1">
  <div class="days_img_number_[days2]"></div>
  <div class="days_img_number_[days1]"></div>
  <div class="days_img_number_[days0]"></div>

  <div class="hours_img_number_[hours1]"></div>
  <div class="hours_img_number_[hours0]"></div>

  <div class="mins_img_number_[mins1]"></div>
  <div class="mins_img_number_[mins0]"></div>

  <div class="secs_img_number_[secs1]"></div>
  <div class="secs_img_number_[secs0]"></div>
</div>

```
Внутри обертки таймера может быть ЛЮБАЯ HTML верстка главно правельно подставить [values] в квадратных скобках.

## Start demo
- скачиваем репозиторий
- открываем demo.html в редакторе
- редактируем даты (если дни которые описывают даты прошли то таймеры покажут 0)
- открываем demo.html в браузере
