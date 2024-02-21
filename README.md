# Использование серверного рендеринга для оптимизации производительности веб-приложений на Node.js

## Содержание
- [Что такое серверный рендеринг?](#ssr)
- [Конкуренция и необходимость в оптимизации](#оптимизации)
- [Как к этому пришли](#пришли)
  - [Все новое - хорошо забытое старое](#старое)
  - [Повышение доступности и SEO оптимизация](#seo)
  - [Безопасность](#безопасность)
- [Использование](#использование)

## <a name="ssr">Что такое серверный рендеринг?</a>
Серверный рендеринг (SSR) - это процесс генерации HTML-кода на сервере и отправки его клиенту в виде готовой страницы. В отличие от клиентского рендеринга, при котором весь HTML-код формируется на стороне клиента с использованием JavaScript, при SSR исходный HTML генерируется на сервере, что позволяет отправить клиенту уже готовую страницу.

> Серверный рендеринг хоть и полезное, но не всегда необходимое решение. При выборе стека технологий важно понимать целевую аудиторию и их потребности.


## <a name="оптимизации">Конкуренция и необходимость в оптимизации</a> 

> __SEO (Search Engine Optimization) оптимизация__ включает в себя ряд практик и стратегий, направленных на улучшение различных аспектов вашего веб-сайта, которые влияют на его видимость в поисковых результатах. Эти аспекты могут включать в себя оптимизацию контента (ключевые слова, заголовки, мета-теги), техническую оптимизацию (структура сайта, скорость загрузки, мобильная дружественность), ссылочный профиль (количество и качество внешних ссылок на ваш сайт), и другие факторы.

<p>Современные веб-приложения отличаются интерактивностью, динамичностью и большим объемом данных, что заставляет создавать сложные интерфейсы со множеством компонентов и дает пользователю множество сценариев использования. Однако эта сложность заставляет прибегать к инновационным и функциональным инструментам предоставляющим лучшую производительность, SEO-оптимизацию и пользовательский опыт. В таких случаях серверный рендеринг становится незаменимым инструментом для оптимизации работы веб-приложений. </p>

## <a name="пришли">Как к этому пришли?</a>

### <a name="старое">Все новое - хорошо забытое старое</a>
<p>Еще до прихода привычных сейчас приложений, которые генерируются полностью на Java Script в браузере разметка передавалась клиенту в ответ на HTTP-запрос при помощи какого-либо серверного языка. Подобное решение позволяло создавать отзывчивые сайты, работающие быстрее обычных, поскольку снижалось время ожидания данных в пути между сервером и клиентом. </p>

### <a name="seo">Повышение доступности и SEO оптимизация</a>
<p>При запросе приложения на React браузером будет получен ответ в виде небольшого HTML документа содержащего внутри body:</p>
<pre lang="html">
&lt;div id="root"&gt;&lt;/div&gt;
<script src="/app.js"></script>
</pre>

<p>То есть по мимо небольшого HTML файла браузер получает зачастую очень большой app.js, что негативно скажется на владельцев маломощных устройств или устройств со слабым интернет-соединением так как им придется достаточно долго ждать загрузку. Помимо этого приложение смогут увидеть пользователи с отключенным или неподдерживаемым JavaScript в браузере. Контент приложений использующих серверный рендеринг предоставляется клиенту в виде готовых HTML-страниц, что дает большое преимущество. Это так же позволяет браузерам легко индексировать контент страниц. (В случае простых SPA приложений большинство браузеров не может это сделать т.к. не поддерживают просмотр JavaScript файлов до отображения страницы). Такой подход обеспечивает им доступность для поисковых систем и улучшает позиции в результатах поиска.</p>

> Веб-скрейпинг (web scraping) - это процесс автоматического извлечения данных с веб-сайтов. Обычно скрейпинг используется для извлечения структурированных данных с веб-страниц, таких как цены товаров, контактная информация, новости и т. д. Эти данные затем могут быть сохранены, обработаны и использованы для различных целей, таких как анализ, сравнение цен, агрегация информации и многое другое.

<p>Часто для продвижения своих продуктов и услуг используются социальные сети. Для улучшения качества рекламы в них был придуман веб‑скрейпинг. Многие социальные сети, такие как Facebook и Twitter, используют его для получения информации о веб-сайтах, которыми пользователи хотят поделиться. Серверный рендеринг обеспечивает более надежное представление контента на странице по выше указанным причинам. Этот процесс позволяет социальным сетям автоматически извлекать заголовки, изображения и другие данные с веб-сайтов, чтобы создавать привлекательные карточки предварительного просмотра (preview cards) для отображения на платформе.</p>

### <a name="безопасность">Безопасность</a>

<p>Серверный рендеринг помогает предотвратить некоторые виды атак, такие как XSS (межсайтовый скриптинг — уязвимость системы безопасности, которая позволяет злоумышленнику размещать клиентские скрипты на веб-страницах). Поскольку контент рендерится на сервере и отправляется клиенту в виде готовой HTML-страницы, а не динамически создается на клиенте с использованием JavaScript, возможности для внедрения вредоносного кода снижаются. По мимо этого разработчикам в целом легче контролировать доступность данных получаемых клиентом, в том числе управление авторизацией.</p>

__Итак, получается преимущество в:__
- __Доступности__
- __Видимости__
- __Инструментах продвижения__
- __Безопасности__

## <a name="использование">Использование</a>


