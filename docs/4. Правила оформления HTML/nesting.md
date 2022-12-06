---
sidebar_position: 2
---

# Вложенность тегов
Не допускается использование стилей из библиотек (bootstrap) вместе со стилями проекта. (возможны проблемы с переопределением стилей)

```html
    <!-- хороший пример -->
    <div class="main">
        <div class="container">
            <h1>Heading</h1>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. A, ad?</p>
        </div>
    </div>

    <!-- плохой пример -->
    <div class="main container">
        <h1>Heading</h1>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. A, ad?</p>
    </div>
```