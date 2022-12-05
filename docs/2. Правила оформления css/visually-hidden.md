---
sidebar_position: 5
---
# .visually-hidden

## Скрытие элементов через .visually-hidden

Что бы визуально скрыть элемент, но при этом сохранить доступность используйте ```.visually-hidden```

```css
.visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    border: 0;
    padding: 0;
    white-space: nowrap;
    clip-path: inset(100%);
    clip: rect(0 0 0 0);
    overflow: hidden;
}
            
```