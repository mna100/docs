---
sidebar_position: 1
---

# Карта с множеством точек

### Яндекс Карта с множеством точек, и переключением табами.

```html
<button data-coords="<?php echo $contact['coords']; ?"></button>
<div class="map_container" id="map_contacts" style="width: 100%; height:500px"></div>
```

```js
/**
* Yandex Map init
*/
if (document.querySelector("#map_contacts")) {
  let countriesMap,
  objectManager,
  countriesData = [];

  document.querySelectorAll(".contacts__btn").forEach((country) => {
    countriesData.push({
    type: "FeatureCollection",
    features: [
    {
      type: "Feature",
        id: country.dataset.id,
          geometry: {
            type: "Point",
            coordinates: country.dataset.coords.split(","),
            },
            options: {
            iconLayout: "default#image",
            iconImageHref:
            "http://.....",
            iconImageSize: [130, 70],
            },
    },
            ],
            });
  });

            // инициализация карты
  ymaps
    .load(
      "https://api-maps.yandex.ru/2.1/?lang=ru_RU&amp;apikey=YOU_API_KEY"
        )
        .then((maps) => {
        countriesMap = new maps.Map("map_contacts", {
          center: [53.677713, 23.829215],
            zoom: 5,
            controls: ["fullscreenControl", "zoomControl"],
            });
            countriesMap.behaviors.disable("scrollZoom");
            objectManager = new maps.ObjectManager({
              clusterize: true,
              gridSize: 64,
            });
            objectManager.clusters.options.set(
              "preset",
              "islands#invertedRedClusterIcons"
              );
            countriesMap.geoObjects.add(objectManager);
            countriesData.forEach((country) => objectManager.add(country));
            })
            .catch((error) => console.log("Failed to load Yandex Maps", error));

            // центрирование карты по клику
            document.querySelectorAll(".contacts__btn").forEach((btn) => {
                btn.addEventListener("click", (evt) => {
                evt.preventDefault();

                let id = evt.currentTarget.dataset.id,
                    coords = evt.currentTarget.dataset.coords;

                countriesMap.setCenter(coords.split(","), 16);
          });
      });
  }
```

:::info
Подробная документация: **[Яндекс.Карты API](https://yandex.ru/dev/maps/jsapi/doc/2.1/quick-start/index.html?from=techmapsmain)**
:::