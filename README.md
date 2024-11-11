# Проектирование
Основное приложение можно разделить на несколько доменов:

1. Компонент входа и регистрации пользователя
2. Компонент галереи фотографий с функционалом лайков
3. Компонент работы с профилем пользователя (смена фотографии, имени)
4. Компонент мастер-страницы, содержащей общие компоненты (Header, Footer)

# Планирование изменений
Приложение будет разбито на микрофронтенды при помощи Module Federation.

### Приложение host
* Содержит все стили в каталоге blocks
* Перенесены общие компоненты (Footer, Header, Main, ProtectedRoute, PopupWithForm, ImagePopup)
* Перенесён модуль CurrentUserContext
* Перенесены шрифты

#### Структура файлов
![alt text](docs/image1.png)

### Приложение auth
* Перенесены компоненты (Login, Register, InfoTooltip)
* Перенесён сервис auth

#### Структура файлов
![alt text](docs/image2.png)

### Приложение cards
* Перенесены компоненты AddPlacePopup, Card
* Частично перенесён сервис API. А именно только функции для работы с карточками и лайками

#### Структура файлов
![alt text](docs/image3.png)

### Приложение profile
* Перенесены компоненты EditAvatarPopup, EditProfilePopup
* Частично перенесён сервис API. А именно только функции для работы пользователем. (getUserInfo, setUserInfo, setUserAvatar)

#### Структура файлов
![alt text](docs/image4.png)

`Так как микрофронтенд профиля содержит кнопку контрол добавления новой карточки, то для реализации этого функционала необходимо реализовать функционал взаимодействия микрофронтендов и при помощи него производить вызов метод addCard приложения "cards"`
![alt text](docs/image5.png)

# Реализация
Не выполнена