---
sidebar_position: 1
---

# YouTube с превью

### Встроеное видео YouTube с изображением - заглушкой.

В случае, когда необходимо сделать превью - картинку используйте следующий код

```html
<script src="https://www.youtube.com/iframe_api"></script>

<div class="common__video-presentation">
  <img id="<?php echo get_field('video_present_embed'); ?>" 
  class="video__frame lozad" 
  data-src="<?php echo get_field('video_present_img'); ?>" 
  alt="Видео">
</div>
````

:::tip
```
<?php echo get_field('video_present_img'); ?> - ссылка на изображение-заглушку.

<?php echo get_field('video_present_embed'); ?> - id для рендера видео YouTube.
 https://www.youtube.com/embed/dQw4w9WgXcQ - пример. 
  Где dQw4w9WgXcQ - является индетификатором видео. Прописывается в полях админ панели.
```
:::

```js
if (document.querySelector("img.video__frame")) {
  let players = {};
    document.querySelectorAll("img.video__frame").forEach((img) => {
      img.addEventListener("click", () => {
        function onYouTubeIframeAPIReady() {
          players[img.id] = new YT.Player(img.id, {
            height: "250",
            width: "100%",
            videoId: img.id,
              events: {
                onReady: onPlayerReady,
                  onStateChange: onPlayerStateChange,
                  },
              });
            }
            function onPlayerReady(event) {
              event.target.playVideo();
              }
            function onPlayerStateChange(event) {
              }
            onYouTubeIframeAPIReady();
              });
          });
      }
```

:::tip
Важно учитывать, что для ```<img>``` и ```<iframe>``` необходимо задавать одинаковые размеры.
:::

:::info
Подробная документация: **[YouTube API](https://developers.google.com/youtube/iframe_api_reference)**
:::