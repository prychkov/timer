# timer
Timer in native JavaScript
Этот скрипт позволяет установить счётчик обратного отсчёта на сайт.

Использование:

1. Базовая разметка для HTML:
  
	<div class="timer-numbers" id="timer">

		<span class="hours">18</span>
		<span>:</span>
		<span class="minutes">20</span>

		<span>:</span>

		<span class="seconds">11</span>
	</div>

2. JS скрипт:

	1) переменная let deadline = '2020-08-27'; это дата окончания отсчёта (например дата конца акции '2020-08-27');

	2) далее следует функция getTimeRemaining, которая вычисляет отсавшееся врямя от текущего момента до конца акции;
	3) Date.parse(endtime) это дата окончания в миллесекундах
	4) Date.parse(new Date()) это текущая дана в миллесекундах
	5) let t = Date.parse(endtime) - Date.parse(new Date()), итого получаем оставшееся время в милесекундах
	6) seconds = Math.floor((t/1000) % 60), записываем в переменную значене в секундах
	7) minutes = Math.floor((t/1000/60) % 60), записываем в переменную значене в минутах
	8) hours = Math.floor((t/(1000*60*60))), записываем в переменную значене в часах
		// если необходимо отразить отсавщееся количество часов в формате 24 часа с днями
		// hours = Math.floor((t/1000/60/60) % 24); 
		// days = Math.floor((t/(1000*60*60*24)));
	9) return возвращает обект, в который записываем полученные выше значения, для дальнейшего использования
	
	Функция setClock принимает два значения id, endtime:
	1) получаем и записываем в переменные элементы вёрстки которые будем менять:
	
	let timer = document.getElementById(id), // принимает аргумент id, ниже мы передадим его значение
            hours = timer.querySelector('.hours'), // ищет в блоке который получили выше (id), элемент с классом hours и записывает его в переменную, ниже тоже самое 
            minutes = timer.querySelector('.minutes'),
            seconds = timer.querySelector('.seconds'),
            

	2) timeInterval = setInterval(updateClock, 1000); // запускает функцию updateClock каждую секунду (1000 миллесекунд);
	3) функция updateClock обнавляет данные по времени и записывает их в верстку
	4) let t = getTimeRemaining(endtime); // запускает функцию getTimeRemaining и записывает в переменную объект возвращаемый функцией getTimeRemaining
	5) функция addZero подставляет 0 перед числами если число меньше или равно 9 (например 09:05:13, а не 9:5:13);
	6) hours.textContent = addZero(t.hours); // всавляет в вёрстку обновлённое число часов с переменной t, которая содержит объект, ниже minutes и seconds,
	то же самое
	7) if (t.total <= 0) {
                clearInterval(timeInterval);
                hours.textContent = '00';
                minutes.textContent = '00';
                seconds.textContent ='00';
            }	// если занчение времени меньше 0 (т.е. уже прошла дата акции) останавливается переменная timeInterval, в которой есть метод setInterval и в ввёрстку
	подставляются значения '00'
	
	setClock('timer', deadline); // запускает функцию setClock и передает два аргумента 'timer' (это id элемента вёрстки где установлены часы) и deadline это время
	когда закончиться акция
