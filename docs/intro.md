---
sidebar_position: 1
---

# Подключение

Подключение **Маркетинг на 100 меньше чем за 5 минут**.

## Инициализация

Скопируйте код.

```js
(function(m){
  var s  = document.getElementsByTagName(m)[0],
      ms = document.createElement(m);
  ms.async = 1;
  ms.src='https://api.mna100.ru/mna100.js';
  s.parentNode.insertBefore(ms,s);
})('script');
```

Вставьте перед закрывающим тегом &lt;/head&gt;