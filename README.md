## Задание № 1

Сделано 1 и 2ой пункты

### Предварительный анализ и разбиение на бизнес функции.

- Авторизация
- Остальное по сути профиль. В текущей реализации мы отображаем только свой профиль, если разлогинимся, то нас перебрасывает на экран авторизации.
	Внутри у нас есть функционал:
	- Лента фоток пользователя
	- Возможность добавлять фотки
	- Возможность редактировать профиль: данные и аватар
	- Возможность ставить лайки на свои фотки

### Выбор метода реализации

Я бы попробовал объединить два метода Single SPA и Module Federation

Авторизацию и Основной модуль (Main) я бы выделил как Single SPA сущности т.к:
 - обеспечит маршрутизацию по путям "/" , "/signup", "/signin"
 - эти сущности более независимы, команда авторизация может быть вообще командой для многих продуктов
 - может спокойно отлаживаться, добавлять новые механизмы без влияния на все систему
 - модуль авторации нужен не так часто - тянуть его каждый раз не стоит

Сам модуль Main более тесно переплетен, тут я бы использовал Module Federation для создания логических  частей с единой ответственностью:
- Profile info - где мы можем обновить данные о пользователе, изменить аватар
- Card list - отображение списка изображений (карточек), удаление, добавление, лайки

```md
/auth-microfrontend         // Микрофронтенд авторизации
  /src
    /components
      InfoTooltip.js        // Подсказка при регистрации  
      Login.js              // Компонент входа пользователя
      Register.js           // Компонент регистрации пользователя
    /styles
      login.css             // Стили для компонента входа
      auth-form.css         // Стили для компонента регистрации
    /utils
      auth.js                // Утилиты для аутентификации
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  
/main-host-microfrontend    // host микрофронтенд - по сути главный модуль и точка входа
    /src
        /components
            App.js          // Главный компонент - точка сборки главного экрана
            Footer.js       // Компонент нижней подписи
            Header.js       // Компонент заголовка/лого + вход логин/регистрацию
            Main.js         // Компонент с отображением тела сайта использует компоненты профиля и карточек
        /styles
            conents.css     // Стили главного экрана
            footer.css
            header.css
            page.css
        /utils
/main-profile-microfrontend // микрофронтенд информации о профиле
    /src
        /components
            CurrentUserContext.js   // Компонента профиля пользователя
            EditAvatarPopup.js      // Всплывающее окно изменения аватара
            EditProfilePopup.js     // Всплывающее окно изменения информации о профиле
            PopupWithForm.js        // Базовая реализация всплывающего окна
        /styles
            popup.css
            profile.css
        /utils
            api.js                  // Апи микрофронтенда с методами связанными только с профилем и автаром
/main-cadrs-microfrontend           // Микрофронтенд списка карточек с возможностью удаления, добавления, лайка
    /src
        /components
            AddPlacePopup.js        // Всплывающее окно добавления карточки-изображения
            Card.js                 // Элемент изображения
            ImagePopup.js           // Всплывающее окно изображения
            PopupWithForm.js        // Базовая реализация всплывающего окна
        /styles
            card.css
            places.css
        /utils
            api.js                  // Апи связанное только с карточками и изображениями: дать список карточек, добавить, удалить, поставить лайк

```

Комментарии:

PopupWithForm.js - Это элемент будет используется в нескольких местах, есть некоторое дублривание кода, что плохо, как вариант, вынести общие компонет в отдельный модуль/либу 

## Задание №2

Схема: https://app.diagrams.net/#G1TUX6Lx2IzCeh8i_OrVAxTXddexRRR3iJ#%7B%22pageId%22%3A%22S9S3dTGNHZGxb8ddAdWJ%22%7D

