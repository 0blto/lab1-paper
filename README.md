# Использование серверного рендеринга для оптимизации производительности веб-приложений на Node.js

## Конкуренция и необходимость в оптимизации

<p>Современные веб-приложения отличаются интерактивностью, динамичностью и большим объемом данных, что заставляет создавать сложные интерфейсы со множеством компонентов и дает пользователю множество сценариев использования. Однако эта сложность заставляет прибегать к инновационным и функциональным инструментам предоставляющим лучшую производительность, SEO-оптимизацию и пользовательский опыт. В таких случаях серверный рендеринг становится незаменимым инструментом для оптимизации работы веб-приложений. </p>

> __SEO оптимизация__ включает в себя ряд практик и стратегий, направленных на улучшение различных аспектов вашего веб-сайта, которые влияют на его видимость в поисковых результатах. Эти аспекты могут включать в себя оптимизацию контента (ключевые слова, заголовки, мета-теги), техническую оптимизацию (структура сайта, скорость загрузки, мобильная дружественность), ссылочный профиль (количество и качество внешних ссылок на ваш сайт), и другие факторы.

## Как к этому пришли?

<p>Еще до прихода привычных сейчас приложений, которые генерируются полностью на Java Script в браузере разметка передавалась клиенту в ответ на HTTP-запрос при помощи какого-либо серверного языка. Подобное решение позволяло создавать отзывчивые сайты, работающие быстрее обычных, поскольку снижалось время ожидания данных в пути между сервером и клиентом. </p>

<p>При запросе приложения на React браузером будет получен ответ в виде небольшого HTML документа содержащего внутри body:</p>
<pre lang="html">
<div id='root'></div>
<script src="/app.js"></script>
</pre>
