---
sidebar_position: 2
---
# Произвольные кастомные поля

Для привязки полей использовать запись: 
```
 <?php echo get_field('you_custom_field', $page_id); ?>
```

Так же необходимо группировать логические блоки, использовать аккордеон, группа.

Внимательно относиться к именованию индетификаторов полей, во избежании колизии имен.

### Все поля импортируются из локальных файлов. Из папок acfe-php / acf-json.

1. Необходимо создать группу полей на локальной машине
2. Перенести на git
3. При создании полей на продакшене, при каждом пуше они будут перезаписываться ❌

#### Для создания повторителя используйте:
```
	<?php if (get_field('amazing_repeater', $page_id)) : ?>
		<?php foreach (get_field('amazing_repeater', $page_id) as $repeater) : ?>
			<div>
                <h3><?php echo $repeater['amazing_repeater_heading]; ?></h3>
				<p><?php echo $repeater['amazing_repeater_text]; ?></p>
			</div>
		<?php endforeach; ?>
	<?php endif; ?>
 ```