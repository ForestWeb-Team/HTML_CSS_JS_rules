# HTML_CSS_JS_rules

> Мы рекомендуем придерживаться этих правил верстки
> для проектов студии Forestweb, 
> которые разрабатываются на базе ModX.

### Использование иконок и изображений
1. Аккуратно используйте иконочные шрифты в проектах. Если экспортируете иконку
из макета Figma, то при наличии в иконке обводки генератор шрифта ее может отбросить.
И иконка не будет соответствовать макету. Лучше вставлять SVG, можно подумать над
добавлением иконок через ShadowDOM (руководство по нему напишем позднее);
   
> Для генерации иконочных шрифтов можно использовать [Fontello](https://fontello.com/)

2. При добавлении картинок через тег img указывайте как минимум параметр width.
Если указываете только ширину, то высоту ставьте auto
   
```html
<img src="../path/name.jpg" alt="" width="320px" height="320px">
<img src="../path/name.jpg" alt="" width="320px" height="auto">
```

> Это поможет бэкендеру правильно указать ширину картинки при натяжке на 
> ModX, и на выходе мы не получим разбабаханные картинки.
> Для слайдеров лучше указывать и ширину, и высоту картинки!

### Правильная структура элементов сайтов

1. При верстке корзины нежелательно использовать таблицы 

> Из-за этого могут не работать кнопки удаления товаров из корзины

2. Если какие-то элементы на сайте подразумевают обработку клика на них,
то их лучше заворачиват в div, не оставлять голый svg или span. И, если клик навешиваете,
то делайте это на div
   
3. Следующие элементы при верстке карточки товара (если это предусмотрено макетом) нужно обязательно
завернуть внутрь формы (особенность работы ModX)
   
> + поле для изменения количества элементов
> + кнопка добавления товара в корзину, она должна сабмитить форму, внутри которой
> находится
> + поля для выбора параметров товаров, например, для выбора начинки или вкуса

4. Никаким образом не нужно стилизовать формы (не применять для формы display:flex, 
   например), вы так создадите кучу проблем в будущем себе или коллегам
   
5. Мы используем плагин поиска, который помещает результаты поиска в определенный блок,
поэтому можно результаты быстрого поиска можно завернуть вот в такой контейнер и
его стилизовать
   
```html
<ul class="ui-menu ui-widget ui-widget-content ui-autocomplete ui-front">
  ...результаты поиска...
</ul>
```

6. Ссылки на подкатегории каталога нужно верстать именно как ссылки (см. скриншоты)

![Скриншот блока подкатегорий 1][screenshot1]

[screenshot1]: ./screenshots/002.png


![Скриншот блока подкатегорий 2][screenshot2]

[screenshot2]: ./screenshots/001.png

7. Структура меню должна быть примерно такая, не стоит использовать
классы для подкатегорий
   
```html
<ul class="catalog-nav">
  <li class="catalog-nav__item">
    <i class="icon-menu"></i>
    <a href="#">Пункт основного меню</a>
    <ul>
      <li>
        <a href="#">Пункт подменю</a>
        <ul>
          <li><a href="#">Третий уровень меню</a></li>
          <li><a href="#">Третий уровень меню</a></li>
          <li><a href="#">Третий уровень меню</a></li>
        </ul>
      </li>
      <li><a href="#">Пункт подменю</a></li>
    </ul>
  </li>
</ul>
```

8. На текстовых страницах (см скриншот ниже) внутри самого контента не используйте
классы для элементов. Подразумевается, что эти страницы будут наполнять из админки,
там нельзя добавить классы

![Текстовая страница][screenshot3]

[screenshot3]: ./screenshots/003.jpg

На скриншоте оранжевым обозначили контент. Примерно делаем вот это

```html
<div class="content-block">
  
  <!-- Это картинка -->
  <img src="" alt="">

  <!-- Абзац текста -->
  <p>Текст</p>

  <!-- Заголовки -->
  <h1>1 уровень</h1>
  <h2>2 уровень</h2>
  <h3>3 уровень</h3>

  <!-- Списки -->
  <ol>
    <li></li>
    <li></li>
    <li></li>
  </ol>
  
  <ul>
    <li></li>
    <li></li>
    <li></li>
  </ul>

  <!-- Цитата -->
  <blockquote>Цитата</blockquote>
</div>
```

На самом деле, для фотогалереи это правило не работает, там можете ставить классы, 
галерея, скорее всего, заполнится из TV-полей

9. При верстке корзины заголовок, кнопки и список товаров размещать в отдельных DIV.
Если все слепить в один блок, то могут слетать кастомные обработчики с кнопок

Вот какие отдельные блоки в корзине

> + Заголовок
> + Список товаров, общая цена
> + Промокод
> + Кнопка оформления заказов
> + Кнопки открытия/закрытия корзины, если она в форме выпадашки/попапа

10. Все, что надо знать о ссылках на наших проектах
    
> + Для ссылок делаем aria-label, где прописываем осмысленные описания ссылки.
Это для доступности интерфейса людям с ограниченными возможностями
> + Если ссылка ведет на сторонний сайт - делаем ее target=_blank
> + hreflang, ping, rel, download тоже очень полезные атрибуты, советую изучить и
продвигать в массы
> + Для номеров телефона href="tel: "
> + Если используете mailto, можете посмотреть заодно, как тему и тело письма
подставить сразу автоматом
> + Логотип нашей студии всегда заворачивайте в ссылку
> + Логотип клиента где бы он ни был, тоже - ссылка всегда. Ведет на главную. Ну если забыли))
> + Кнопка удаления товара из корзины - всегда ссылка
> + Кнопка очистки корзины - ссылка. Обработчики на эту и предыдущую кнопки
сами не пишем, их добавит бэкендер
    
11. Если есть фильтр по типу минимальной и максимальной цены (когда подразумеваются
цифровые значения, но в input есть еще и текст) - см скриншот, там пример

![Range filter][screenshot4]

[screenshot4]: ./screenshots/003.png

То бэкендер скажет вам спасибо, если ниже фильтра добавите что-то такое

```html
<input type="hidden" class="min-price" name="min-price" value="">
<input type="hidden" class="max-price" name="max-price" value="">
```

И в эти поля при помощи JS будете подставлять текущие значения в фильтре

12. Сортировку лучше заворачивать в форму, делать выпадающий список и при изменении
значения отправлять форму на сервер
    
```html
<form>
  <select name="" id="">
    <option value=""></option>
  </select>
</form>
```

13. Лучше будет, если при перезагрузке страницы оформления заказа будут сохраняться
значения полей формы. Если Вы читаете это руководство, а в репозиториях компании
еще не появился скрипт для этого от автора данного руководства, то берите
sisyphus с какого-то из очень старых проектов. Ну или можете сами этот скрипт
написать, велком
    
14. Количество товара в карточке товара, в корзине лучше писать так

```html
<div class="count">
  <span class="dec">-</span>
  <input type="text" name="count">
  <span class="inc">+</span>
</div>
```

Мы часто используем этот шаблон, тут можно не мудрить

### JAVASCRIPT

1. При обработке форм нельзя привязываться к name у полей формы и тем более к value.
Используем class / id

### Прочие рабочие моменты
1. При именовании папок, файлов, классов и ID не использовать следующие слова
+ banner
+ adv

> Если пользователь включит ADBLOCK или похожий на него плагин, то у него
> просто не отобразятся все ваши блоки, картинки и все такое, не ходите
> по нашему многострадальному пути

2. Убедитесь, что все ваши картинки, использованные в макете, оптимизированы.
Мы стремимся, чтобы наши картинки не весили больше 150кб. Но смотрите, чтобы качество
сильно тоже не ухудшилось, а то за пикселизированное фото вас покусает ПМ

> Для оптимизации JPG, PNG - [TinyPNG](https://tinypng.com/)

3. Вы можете использовать (даже желательно) формат изображений WEBP

4. Все векторные картинки добавляйте в SVG (например, логотипы)

5. Если предполагается использование разных картинок для разного размера
экрана, то используйте тег picture для этого, пример ниже

```html
<picture>
    <source srcset="" media="(max-width: 768px)">
    <source srcset="" media="(max-width: 1300px)">
    <source srcset="">
    <img srcset="" alt="Slider image">
</picture>
```

> Для слайдера на главной странице сайта, если он есть,
> использовать это обязательно!

6. БЭМ и все такое - очень классно и круто, но покрывать весь код классами не нужно здесь,
правда. В случае с ModX это сильно усложняет натяжку на CMS, если сомневаетесь,
спросите бэкендера
   
7. Мы верим в семантику, поэтому используйте, пожалуйста, теги осмысленно. Изучите,
где и какие теги можно использовать и вперед. Разберитесь в разнице между
ссылками и кнопками, когда что нужно использовать

## Самое главное правило для верстальщика

> Если не согласны с чем-то из этого руководства, можете предложить лучшее решение
> и аргументировать его, если знаете, что добавить - предлагайте улучшения, мы всегда
> любим инициативных и заботливых людей. Мы сами такие же, ну =)
