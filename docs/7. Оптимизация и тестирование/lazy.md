---
sidebar_position: 1
---
# Изображения и lazyload

На проекте необходимо использовать для изображений ленивую загрузку, по умолчанию 
```html
<img class="lozad" data-src="/img/prettywise.jpg">
```

Можно использовать lazy для фоновых изображений 
```html
<div class="lozad" data-background-image="/img/background.png"></div>
```

Мелкие изображения, по возможности, делать с помощью `css` или `svg`.



:::info

При загрузки изображений необходимо проверять их размер.
Для сжатия можно использовать сервис **[squoosh.app](https://squoosh.app/)**

:::