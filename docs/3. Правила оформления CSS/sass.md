---
sidebar_position: 2
---
# Синтаксис sass, вложенность

На проектах используется препроцессор sass. Обязательно группировать классы и использовать вложенность.

На проектах рекомендовано пользоваться переменными и миксинами.

Допускается использовать теги в качестве селектора.

```css
/* Хороший пример */
    main {
    .header {
        h1 {
        font-size: 2rem;
        font-weight: 700;
        }

        &__nav {
        display: flex;

            &__item {
            max-width: 20%;
                &--red {
                color: red;
                }
            }
        }
    }    
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/Mrq2ora_p0o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>