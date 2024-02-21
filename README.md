# Использование серверного рендеринга для оптимизации производительности веб-приложений на Node.js

## Содержание
- [Что такое серверный рендеринг?](#ssr)
- [Конкуренция и необходимость в оптимизации](#конкурентность)
- [Как к этому пришли](#пришли)
  - [Все новое - хорошо забытое старое](#старое)
  - [Повышение доступности и SEO оптимизация](#seo)
  - [Безопасность](#безопасность)
- [Использование](#использование)
  - [Оптимизации](#оптимизации)
  - [Инструменты](#инструменты)
## <a name="ssr">Что такое серверный рендеринг?</a>

Серверный рендеринг (SSR) - это процесс генерации HTML-кода на сервере и отправки его клиенту в виде готовой страницы. В отличие от клиентского рендеринга, при котором весь HTML-код формируется на стороне клиента с использованием JavaScript, при SSR исходный HTML генерируется на сервере, что позволяет отправить клиенту уже готовую страницу.

Существует и другой подход, называемый клиентский рендеринг (CSR) - это метод веб-разработки, при котором HTML контент генерируется на стороне клиента (веб-браузере), а не на сервере.

> Серверный рендеринг хоть и полезное, но не всегда необходимое решение. При выборе стека технологий важно понимать целевую аудиторию и их потребности.


## <a name="конкурентность">Конкуренция и необходимость в оптимизации</a> 

> __SEO (Search Engine Optimization) оптимизация__ включает в себя ряд практик и стратегий, направленных на улучшение различных аспектов вашего веб-сайта, которые влияют на его видимость в поисковых результатах. Эти аспекты могут включать в себя оптимизацию контента (ключевые слова, заголовки, мета-теги), техническую оптимизацию (структура сайта, скорость загрузки, мобильная дружественность), ссылочный профиль (количество и качество внешних ссылок на ваш сайт), и другие факторы.

<p>Современные веб-приложения отличаются интерактивностью, динамичностью и большим объемом данных, что заставляет создавать сложные интерфейсы со множеством компонентов и дает пользователю множество сценариев использования. Однако эта сложность заставляет прибегать к инновационным и функциональным инструментам предоставляющим лучшую производительность, SEO-оптимизацию и пользовательский опыт. В таких случаях серверный рендеринг становится незаменимым инструментом для оптимизации работы веб-приложений. </p>

## <a name="пришли">Как к этому пришли?</a>

### <a name="старое">Все новое - хорошо забытое старое</a>
<p>Еще до прихода привычных сейчас приложений, которые генерируются полностью на Java Script в браузере разметка передавалась клиенту в ответ на HTTP-запрос при помощи какого-либо серверного языка. Подобное решение позволяло создавать отзывчивые сайты, работающие быстрее обычных, поскольку снижалось время ожидания данных в пути между сервером и клиентом. </p>

### <a name="seo">Повышение доступности и SEO оптимизация</a>
<p>При запросе приложения на React браузером будет получен ответ в виде небольшого HTML документа вида:</p>
<pre lang="html">
&lt;html&gt;
  &lt;head&gt;
    &lt;!----- Some meta tags -----&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id="root"&gt;&lt;/div&gt;
    &lt;script src="/app.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

<p>Так происходит потому что страницы генерируются на клиенте. Все что необходимо браузеру - HTML страница с выделенным блоком для подстановки контента и скрипт, который его рендерит. Это значит, что все страницы будут содержаться в нем (для нашего примера это app.js).</p>

<p align="center">
  <img src="./Server-side-rendering-benefits-node-js/ssr_csr.png" alt="CSR vs SSR" width="70%" />
</p>


<p>То есть по мимо небольшого HTML файла браузер получает зачастую очень большой скрипт, что негативно скажется на владельцев маломощных устройств или устройств со слабым интернет-соединением так как им придется достаточно долго ждать загрузку, а если речь идет о маркетплейсах, образовательных порталах и других приложениях, оперирующих большими массивами данных, то даже клиенту с очень мощным устройством и быстрым интернетом придется подождать. Контент приложений использующих серверный рендеринг предоставляется клиенту в виде готовых HTML-страниц по запросу, что дает большое преимущество в скорости загрузки. Это так же позволяет браузерам легко индексировать контент страниц. (В случае простых SPA приложений большинство браузеров не может это сделать т.к. не поддерживают просмотр JavaScript файлов до отображения страницы). Такой подход обеспечивает им доступность для поисковых систем и улучшает позиции в результатах поиска, а так же приложение будет работать у клиентов с отключенным JavaScript.</p>

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

### <a name="оптимизации">Оптимизации</a>

<p>SSR уже из коробки обладает достоинствами, однако его отличия от приложений, генерирующих HTML разметку при помощи скрипта на клиенте дают разработчикам большое количество возможностей дополнительной оптимизации скорости доступности и безопасности.</p>

При разработке приложения очень важно правильно __манипулировать данными__. SSR удобен для этого, т.к. есть возможность загрузить их заранее на сервере, но ничего не мешает запросить их на клиенте. Как можно больше информации должно загружаться во время рендеринга страницы на сервере. В таком случае пропадет необходимость запрашивать их с клиента, это ускорит загрузку страницы, что как следствие учлучшит пользовательский опыт. Предварительная загрузка данных так же обеспечит их видимость поисковыми роботами, что улучшит SEO-показатели приложения. Конечно, это не касается конфиденциальных данных.


<p>Вообще поисковая система сложна и смотрит на большое количество характеристик сайта. Генерация страниц на сервере помогает провести некоторые оптимизации:</p>

- META теги
  <p>SSR приложения позволяют на каждой странице использовать уникальные <br>META теги<br>
  <pre lang="html">&lt;title&gt;, &lt;meta name="description"&gt;</pre>
  это способствует лучшей индексации</p>
- URL-адреса
  <p>Создавайте читаемые и информативные URL-адреса для каждой страницы вашего приложения. Это поможет поисковым системам лучше понять содержание вашего сайта и повысит его рейтинг.</p>
- Теги со смыслом
  <p>Таким тегами является например заголовок. Используйте их для выделения контента и структуры. Это поможет поисковым системам.</p>
<p>Так же стоит постоянно проводить мониторинг (например с помощью Google Analytics). Это поможет отследить эффективность SEO стратегии.</p>

<p>В случае оптимизации производительности SSR уже благодаря своим принципам дает сильный прирост "из коробки". Однако силить его так же можно усилить:</p>

- Сжатие изображений и выбор формата
- Оптимизация запросов к серверу и количества передаваемых данных
- Кэширование ресурсов
  <p>Используйте HTTP-кэширование для хранения копий ресурсов на стороне клиента или на сервере. Это позволяет браузеру избежать повторной загрузки ресурсов, которые не изменились с предыдущего запроса.</p>
- Ленивая загрузка ресурсов
  <p>Применяйте ленивую загрузку изображений, скриптов и стилей, чтобы отложить загрузку ресурсов, которые не отображаются сразу при загрузке страницы. Например, используйте атрибут loading="lazy" для изображений, если они запрашиваются на клиенте.</p>
- Найти узкие места можно так же при помощи средств мониторинга.

### <a name="инструменты">Инструменты</a>

<p>SSR можно написать на любом серверном языке (Java, Pytho, PHP и т.д.), как это и происходило раньшеб ведь принцип довольно простой. Но даже при условиях наличия большого количества backend фреймворков, которые облегчают эту задачу. Не всегда в команде есть fullstack специалисты, либо стоит задача написать клиент для уже существующего API. Это привело к появлению современных фреймворков на которые легко перейти фронтенд программистам. Одними из самых популярных сейчас являются Next.js использующий React.js под капотом и Nuxt.js, который основан на Vue.js, являющимися одими из самых популярных JS фреймворков.</p>

<p align="center">
  <img src="./Server-side-rendering-benefits-node-js/frame-charts.png" alt="CSR vs SSR" width="70%" />
</p>

<p>Написание SSR приложений с использованием этих инструментов сильно облегчит написание кода, ведь используется тот же синтаксис и принцип написания компонентов как в уже знакомых библиотеках. Необходимо будет разобраться только в создании, структуре и оптимизации приложения.</p>

### <a name="next">Next.js</a>

<p>Структура Next.js приложения такая же как и у приложения на React.js. Можно писать те же клиентские компоненты и стили, однако добавляется особенность работы со страницами и серверной частью приложения. Для его создания можно написать в консоль:</p>

<pre>npx create-next-app@latest</pre>

<p>Страницы в проекте находятся в отдельной папке в виде js файлов. Чтобы создать страницу доступную по стандартному URL создается файл Index.js.</p>

<pre lang="js">
import React from 'react';

function HomePage({ data }) {
  return (
    <div>
      <h1>Hello, SSR in Next.js!</h1>
      <p>Data from server: {data}</p>
    </div>
  );
}

export async function getServerSideProps() {
  // Логика для получения данных с сервера
  const data = 'Some data from server';
  
  return {
    props: { data }
  };
}

export default HomePage;
</pre>

<p>Функция getServerSideProps используется для выполнения кода на сервере и предварительного заполнения данных перед тем, как компонент будет отрендерен на стороне клиента. Этот метод должен вернуть объект с props, который будет передан компоненту.</p>

<p>Навигация по страницам происходит по тем же адресам, по которым они распологаются в файловой системе относительно папки со страницами.</p>

<p align="center">
  <img src="./Server-side-rendering-benefits-node-js/next-routing.png" alt="CSR vs SSR" width="70%" />
</p>

<p>Next.js позволяет создавать страницы по динамическому URL. Для этого нужно заключить названиие аргумета в квадратные скобки в имени файла, как показано на картинке. Так же можно использовать альтернативную структуру, где вместо файлов создаются папки с названиями адресов, а внутри них index.js с разметкой и логикой, error.js и loading.js для отображения ошибок и загрузки. Index.js для пути '/' заменяется на папку (site).</p>

<p>Запуск осуществляется командой</p>
<pre>npm run dev</pre>
