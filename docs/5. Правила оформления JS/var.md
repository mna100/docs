---
sidebar_position: 1
---
# Именование переменных

Запрещено объявлять переменные, имена которых совпадают с именами используемых в коде лейблов, а так же ключевыми словами, которые используются самим Javascript. Все переменные должны быть названы в верблюжьем регистре (camelCase). Исключения составляют константы которые должны именоваться прописными буквами в змеином регистре (UPPER_SNAKE_CASE)

```js
 // Неправильно
    let my_variable = 5;
    let MYVARIABLE = 5;
    let myvariable = 5;

// Правильно
    let myVariable = 5;
    const MY_VARIABLE = 5;
```