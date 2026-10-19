# ads-sdk-lamboos

Локальная сборка Ads SDK API v0.2 для Lomboos, конфиг `blombo-io`.
Имя файла намеренно: `ads-sdk-lamboos.js`.

## Установка

Разместите `ads-sdk-lamboos.js` и каталог `static/` рядом, сохраняя структуру.
Подключайте SDK по HTTP(S). Асинхронные чанки загружаются относительно URL скрипта.
На странице должна быть одна копия SDK.

```html
<script src="/lamboos/ads-sdk-lamboos.js"></script>
<script>
  window.pgAds.init({
    clid: "p_5bab71de-0cc6-42a9-be28-4ce95eaf42bd",
    // gameId: "your-game-id"
  }).then(function (status) {
    console.log("Ads SDK status:", status);
  });
</script>
```

## Shared GPT и PPID

Страница партнёра должна сама загрузить GPT и вызвать `googletag.enableServices()`.
Для `gam-h5` и `gam-banner-interstitial` принудительно задан `gptSharedMode: true`.
Они ждут готовности GPT до 10 секунд и не вызывают `setPublisherProvidedId`,
не заменяют PPID партнёра, не загружают свой GPT и не включают его сервисы.
Это относится к GPT: стандартные instream-запросы и аналитика SDK сохранены.

## Форматы и порядок провайдеров

- `interstitial`, `rewarded`: gam-h5 → gam-instream → gam-banner-interstitial → prebid-direct.
- `interstitial_preroll`: gam-instream → gam-instream (no_floor).
- Группа обычных баннеров `banner_1…4` удалена из конфига.
- Отдельные `interstitial_midroll` и `video_banner` не настроены.
- Полный список ad units сохранён в `partner-config.json`; desktop и mobile одинаковы.
- Публичный API v0.2 сохранён; методы page/video рекламы присутствуют в SDK, но соответствующих placements в этом пакете нет.

## Сетевые зависимости

Это пакет для самостоятельного размещения JS и assets, а не режим без интернета.
Актуальные domain/MCM overrides (`/ads/sdk-config`), страна, consent,
аналитика, аукционы, рекламные библиотеки и креативы продолжают использовать
стандартные внешние сервисы SDK. `sdk_origin` — `https://playgama.com`.

## Проверки

Проверены сборка, конфиг на desktop/Android/iOS, 68 существующих unit-тестов
и загрузка готового JS в jsdom. Реальные показы в браузере партнёра не проверялись.
Проведено локальное ревью сборки; независимое ревью не проводилось.
`build-info.json` содержит исходный коммит и SHA-256 файлов.
