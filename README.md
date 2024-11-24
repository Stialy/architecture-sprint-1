Применим стратегию вертикальной нарезки и выделим 2 домена:
* управление профилями пользователей;
* управление фотографиями и учет лайков.

Приложение, разбитое на микрофронтенды, располагается на адерсу ./microfrontend

Ввиду отсуствия спецефических требований, в частности - возможности реализовывать приложения на разных языках, выбран подход Module Federation.
Модуль может разрабатываться и тестироваться независимо от других, что упрощает внесение изменений и исправление ошибок без влияния на остальную часть приложения.
Ленивую загрузку предполагают оба подхода (MF, SPA).  

Таким образом, структура приложения следующая:
* ./microfrontend/host - основное приложение;
* ./microfrontend/auth-microfrontend - удаленный модуль (Remote) аутентификации;
* ./microfrontend/user-microfrontend - удаленный модуль (Remote) для управление профилями пользователей;
* ./microfrontend/card-microfrontend - удаленный модуль (Remote) для управления фотографиями.

Приложения запускаются на портах 8080, 8081, 8082.

Выполнено разделение компонентов (**/src/components), вызовов API( **/src/utils), изображений ( **/src/images), стилей (**/src/index.css, **/src/blocks) и зависимостей (package.json). 
