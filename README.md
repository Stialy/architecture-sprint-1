Задание 1, разделение на микрофронты портала Mesto

Уровень 1. Проектирование
Выбран фреймворк Module Federation, т.к. используется единая среда React. 

Уровень 2. Планирование изменений
Решение разделено на 4 микрофронта:
app - является базовым компонентом, содержит общий шаблон страницы и связывает между собой другие микрофронты;
auth-microfrontend - подключаемый микрофронт, отвечает за авторизацию, регистрацию и логаут пользователя.
card-microfrontend - подключаемый микрофронт, отвечает за работу с каталогом фотографий;
profile-microfrontend - подключаемый микрофронт, отвечает за работу с профилем пользователя;

Задание 2, разделение на микросервисы монолита сервиса Аукционов

В рамках разделения были выделены следующие микросервисы:
   1. Сервис авторизации - аутентификация, авторизация (ролевая модель).
   2. Сервис профиля пользователя - регистрация пользователя, редактирование данных пользователя, отчетность активности.
   3. Сервис каталога товаров - управление товарами.
   4. Сервис каталога услуг - управление услугами.
   5. Сервис Корзины - управление заказами, отчетность по продажам.
   6. Сервис аукционов - управление аукционами.
   7. Сервис поддержки - управление заявками на поддержку.
   8. Сервис платежей - управление платежами, взаимодействие с платежными агрегаторами.
   9. Сервис уведомлений - управление уведомлениями пользователей через почту и SMS, взаимодействие с SMS провайдерами.