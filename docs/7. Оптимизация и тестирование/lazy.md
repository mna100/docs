---
sidebar_position: 1
---
# Изображения

При загрузки изображений необходимо придерживаться следующих рекомендаций.

Контент - `.jpeg`   
Оформление - `.png`  
Иконки, навигация и тд - `.svg .ico`


## Отзывчивый макет

Это понятная методика позволяет изображению занимать доступное горизонтальное пространство с сохранением соотношения сторон. В 2020-м браузеры научились резервировать корректное количество вертикального пространства под изображение до его загрузки, если в элементе `<img>` указаны атрибуты `width` и `height`. Это позволяет избежать накопительного сдвига макета (cumulative layout shift).

```html
<style>
 img {
   max-width: 100%;
   height: auto;
 }
</style>
<!-- Providing width and height is more important than ever. -->
<img height="853" width="1280" src="/img/prettywise.jpg" />
```

## Ленивая отрисовка

Вторая методика сложнее. Новый CSS-атрибут `content-visibility: auto` говорит браузеру не думать о размещении изображения, пока оно не будет готово. У этого подхода несколько достоинств, главное из которых в том, что пока браузер не получит размытое изображение-заглушку или само изображение, он не будет его декодировать, экономя ресурсы процессора.

## Ленивая загрузка

Добавив `loading="lazy"` в элемент `<img>` мы говорим браузеру начать извлекать изображение лишь тогда, когда оно готово быть отрисовано.

```html
<img loading="lazy" src="/img/prettywise.jpg" />
```

В шаблоне есть зависимость для реализации lazy load через фреймворк


```html
<img class="lozad" data-src="/img/prettywise.jpg">
```

Код lazy load для фоновых изображений

```html
<div class="lozad" data-background-image="/img/background.png"></div>
```

## Асинхронная расшифровка

Добавив `decoding="async"` в элемент `<img>` мы разрешаем браузеру расшифровывать изображение вне основного потока, чтобы эта процедура не помешала пользователю. Заметных недостатков у этого решения быть не должно, за исключением того, что оно не всегда применима по умолчанию в старых браузерах.

```html
<img decoding="async" src="/img/prettywise.jpg" />
```

## Размытая заглушка

Размытая заглушка — это инлайненное изображение, дающее пользователю какое-то представление о полноценной картинке, которая будет позднее загружена, без передачи данных по сети.

Заглушка инлайнится как `background-image` изображения. Эта методика позволяет отказаться от второго HTML-элемента буквально прячет заглушку, когда загружается основное изображение, для этого не нужен JavaScript.
URI данных основного изображения обёртывается в URI данных SVG-картинки. Это делается потому, что размытие выполняется на уровне SVG, а не с помощью CSS-фильтра. То есть размытие выполняется однократно для каждого изображения при растеризации SVG, а не для каждого макета. Это экономит ресурсы процессора.


<kbd>
  <img src="https://habrastorage.org/r/w1560/getpro/habr/post_images/c8e/7f8/2eb/c8e7f82eb52f7b1da723413ee213b136.jpg" data-src="https://habrastorage.org/getpro/habr/post_images/c8e/7f8/2eb/c8e7f82eb52f7b1da723413ee213b136.jpg" />
</kbd>



```html
<img
 style="
     …
     background-size: cover;
     background-image:
       url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=\'http%3A//www.w3.org/2000/svg\'
        xmlns%3Axlink=\'http%3A//www.w3.org/1999/xlink\' viewBox=\'0 0 1280 853\'%3E%3Cfilter id=\'b\' color-interpolation-filters=\'sRGB\'%3E%3CfeGaussianBlur stdDeviation=\'.5\'%3E%3C/feGaussianBlur%3E%3CfeComponentTransfer%3E%3CfeFuncA type=\'discrete\' tableValues=\'1 1\'%3E%3C/feFuncA%3E%3C/feComponentTransfer%3E%3C/filter%3E%3Cimage filter=\'url(%23b)\' x=\'0\' y=\'0\' height=\'100%25\' width=\'100%25\'
        xlink%3Ahref=\'data%3Aimage/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAkAAAAGCAIAAACepSOSAAAACXBIWXMAAC4jAAAuIwF4pT92AAAAs0lEQVQI1wGoAFf/AImSoJSer5yjs52ktp2luJuluKOpuJefsoCNowB+kKaOm66grL+krsCnsMGrt8m1u8mzt8OVoLIAhJqzjZ2tnLLLnLHJp7fNmpyjqbPCqLrRjqO7AIeUn5ultaWtt56msaSnroZyY4mBgLq7wY6TmwCRfk2Pf1uzm2WulV+xmV6rmGyQfFm3nWSBcEIAfm46jX1FkH5Djn5AmodGo49MopBLlIRBfG8yj/dfjF5frTUAAAAASUVORK5CYII=\'%3E%3C/image%3E%3C/svg%3E');"

        src="/img/prettywise.jpg"
/>
```

Так же смотрите статью скелетная загрузка

## (Опциональная) JavaScript-оптимизация

Браузеры могут быть вынуждены растеризовать размытую заглушку, даже если изображение уже загружено. Проблему можно решить, убрав растеризацию при загрузке. Кроме того, если у вашего изображения есть прозрачные области, то эта оптимизация становится обязательной, иначе сквозь картинку будет просвечивать заглушка.

```js

 document.body.addEventListener(
   "load",
   (e) => {
     if (e.target.tagName != "IMG") {
       return;
     }
     // Remove the blurry placeholder.
     e.target.style.backgroundImage = "none";
   },
   /* capture */ true
 );

```


## Используйте современные форматы изображений WebP, AVIF.

:::info
#### Обязательно проверяйте на предмет кроссбраузерности  **[caniuse.com](https://caniuse.com/)**  
В случае если сайт на CMS, учитывайте особенности платформ и оформления админ. панели
:::

При необходимости пользуйтесь тегом `<picture>`

```html
<picture>
  <source srcset="mdn-logo-wide.png" media="(min-width: 600px)" />
  <img src="mdn-logo-narrow.png" alt="MDN" />
</picture>
```

**habr (https://habr.com/ru/post/594211/)**




:::danger

## Очень важно!     
### При загрузки изображений необходимо проверять их размер и разрешение.

#### `extrahugepic.jpeg 8000x8000 size: 320GB` - плохо
#### `normal.jpeg 300x400 size: 420KB` - хорошо

:::

#### Для сжатия можно использовать сервис **[squoosh.app](https://squoosh.app/)**