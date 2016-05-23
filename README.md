# paste.js

`paste.js` это интерфейс для чтения информации (текст / изображение) из буфера обмена в различных браузерах. Он также содержит немного браузерных хаков.

В этом репозитории находится глубокая переработка исходной функции. Эта не требует `jQuery`, имеет другой интерфейс и возвращает в случае изображений только `blob`.


## Совместимость

|                              | IE11 | Firefox 33 | Chrome 38 | Safari | Opera |
|------------------------------|------|------------|-----------|--------|-------|
| pasteText (non-inputable)    | ok   | ok         | ok        | ok     | ok    |
| pasteText (textarea)         | ok   | ok         | ok        | ok     | ok    |
| pasteText (contenteditable)  | ok   | ok         | ok        | ok     | ok    |
| pasteImage (non-inputable)   | ok   | ok         | ok        |        |       |
| pasteImage (textarea)        | ok   | ok         | ok        |        |       |
| pasteImage (contenteditable) | ok   | ok         | ok        |        |       |

## Использование

```js

// инициализация
// в init можно передавать массив элементов или селектор
// init возвращает массив элементов, к которым применён
[].forEach.call(Paste.init('.example'), function (example) {
	
	// обработчик события вставки изображения
	example.addEventListener('pasteImage', function (e) {
		var resultItem = document.createElement('div');
		var i = document.createElement('img');

		// изображение передаётся в виде blob
		i.src = URL.createObjectURL(e.detail.blob);
		resultItem.appendChild(i);
		result.appendChild(resultItem);
	});

	// обработчик события вставки текста
	example.addEventListener('pasteText', function (e) {
		var resultItem = document.createElement('div');

		resultItem.innerHTML = e.detail.text;
		result.appendChild(resultItem);
	});
});
```
