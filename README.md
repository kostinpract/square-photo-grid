# Резиновая сетка с квадратными картинками

Предположим, у нас есть вот такие исходные фотографии:

![Исходные картинки с разными соотношениями сторон](./images/source-photos.png "Исходные картинки с разными соотношениями сторон")

Как видите, они с разным соотношением сторон: вертикальные, горизонтальные, квадратные (или «почти квадратные»).

Нужно получить вот такой результат:

![Карточки с квадратными картинками](./images/target.png "Карточки с квадратными картинками")

При этом картинки должны остаться картинками (```img```): потому что так семантически верно и чтобы им можно было задать alt-атрибуты. В общем, вариант с выводом картинок через фон — не подходит.

Поскольку карточки резиновые, то мы заранее не знаем, какая высота и ширина должна быть у каждой картинки (она будет меняться в зависимости от размеров вьюпорта). Если высоту/ширину можно было задать жёстко в пикселях, то проблема стала бы тривиальной и решалась бы через задание примерно таких свойств для элемента-картинки (```img```):

```css
.gallery-item__photo {
  ...
  width: 200px;
  height: 200px;
  object-fit: cover;
}
```

Если мы попытаемся установить для картинок ширину в 100%, то получим вот такой вариант:

![Карточки с картинками в оригинальном соотношении сторон](./images/problem-1.png "Карточки с картинками в оригинальном соотношении сторон")

А если ещё и высоту сделаем 100%, то получим такое:

![Картинки отмасштабировались по картинке с наибольшей высотой в ряду](./images/problem-2.png "Картинки отмасштабировались по картинке с наибольшей высотой в ряду")

Картинки отмасштабировались по картинке с наибольшей высотой в ряду. Красиво. Но нам нужно, чтоб они были квадратными, а не вытянутыми по вертикали. К тому же, может получиться так, что в в каком-то ряду попадутся только горизонтальные картинки, и тогда от ряда к ряду высота карточек будет очень сильно меняться.

Красивым решением является использование свойства ```aspect-ratio``` (даже ```object-fit: cover``` больше не потребуется):

```css
.gallery-item__photo {
  ...
  width: 100%;
  aspect-ratio: 1/1;
}
```

Но беда в том, что автотесты Яндекс.Практикума это свойство не принимают. Слишком свежее. Хотя по данным https://caniuse.com/mdn-css_properties_aspect-ratio все современные браузеры его уже поддерживают.




