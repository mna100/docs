---
sidebar_position: 1
---
# Плавный скролл

### Плавный скрол через JavaScript

```js
const anchors = document.querySelectorAll('a[href*="#"]')

for (let anchor of anchors) {
  anchor.addEventListener('click', function (e) {
    e.preventDefault()
    
    const blockID = anchor.getAttribute('href').substr(1)
    
    document.getElementById(blockID).scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    })
  })
}
```

:::tip
Альтернатива стандартному поведению браузера. ```scroll-behavior: smooth;```

Можно ставить таймауты и добавлять иные взаимодействия.
:::