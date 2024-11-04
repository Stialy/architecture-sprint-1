МИКРОФРОНТЕНДЫ

Если проходить по чек-листу "когда переходить на фронтенды", то, учитывя размер приложения и его простоту, можно с большой долей вероятности утверждать, что никакого разбиения на микрофронтенды не требуется.
Однако, результаты прохождения чер-листа перевешиваются желанием заказчика произвести такое разбиение

1. Вертикальная нарезка:

В постановке указаны следующие функциональности:
    1. работа с профилем (создание, редактирование)
    2. работа с галереей (создание, удалерие фотографий)
    3. работа с лайками фотографий (проставление, удаление)
    4. регистрация/вход на сайт

1 и 2 функциональности могут существовать отдельно друг от друга, поэтому их возможно вынести в отдельные микрофронтенд.
Лайки имеют отношения только к фотографиям, а не к галерее в целом. Скорее-всего, это будет самая часто используемая функциональность. Возможно она потребует обновления в реальном времени, а так же какого-то механизма предотвращения накруток. Если функциональность с какой-то момент времени перестанет рабоать - это не должно остановить работу остальной части приложения. Очень подозрительная функциональность. Лучше вынести в отедьный микрофронтенд, однако, она слишком сильно завязана на микрофронтенд галереии. Поэтому стоит оставить его там.
Вход на сайте и регистрация - функциональности, обеспечивающие возможность создания и управление собственными галереями различным пользователям. Можно объеденить с профилем пользователя

2. Автономность команд

Т.к. функциональности, описанные в разделе 1 автономны, то над каждой из них возможно работать отедьной команде

3. Изоляция

Наименее изменчивая функциональность - это регисрация и вход. Функциональность, обычно, подверженная изменениям меньше всего.
Затем - профиль. Не основная функциональность. Скорее-всего будет изменяться реже чем основная
Затем - галерея. Т.к. скорее-всего, основная функциональность приложения - это работа с фотографиями, то она будет меняться чаще остальных.

4. Интеграция

Если предпололжить, что приложение будет развиваться и:
    1. развитие микрофронтендов происходит с разной скорость
    2. они слабо связанны
    3. требования к производительности отсутствуют

, то лучше выбрать интеграцию времени выполнения (runtime), что позволит:
    1. работать командам независимо над разными микрофронтендами
    2. поставлять пользователю обновленные/новые функциональности независимо друг от друга

5. Композиция

Т.к:
    1. серверная композиция дает большую нагрузку на бекед-разработчиков
    2. скорее-всего на сайте необходим сбор аналитический данных для зарабатывания на рекламе
    3. большая часть сервисов с фотографиями рассчитана на мобильные устройства, а чрезмерные вычисления на сторое клиента приводят к быстрой разрядки аккумулятора, а значит к уменьшению времени, которое пользователь проведет на сайте
Лучше выбрать или runtime или гибридный вариант композиции

6. Инструменты
Т.к. разницы между Webpack Module Federation и Single SPA почти нет (судя по данным из курса), то стоит выбрать наиболее знакомый пакет. А это Webpack Module Federation, иначе разработка затянется. Более того для Webpack Module Federation есть примеры использования. 
В Webpack Module Federation есть мозможность динамического подключения микрофронтендов. Т.к. код пишется в виде строки, то скорее-всего, достатоно слабо проверяется, что может порождать огромное количеств ошибок. Лучше такой возможностью не пользоваться. 
Судя по этой статье, разрабатывать под sigle-spa сложнее: https://habr.com/ru/companies/sportmaster_lab/articles/724314/

В результате получилось три микрофронтенда:
- галерея (gallery)
- пользватели (users)
- хост (host)

Галерея содержит формы и методы АПИ для радботы с картинками
Пользователи содержат формы и методы АПИ для работы с входом и выходом из приложения, регисррацией и редактированием профиля
Хост содержит основные элементы сайта: шапку, подвал, тело в виде списка картинок
Некоторые общие формы продублированы в каждом сервисе, т.к. способа вынести это в отдельный модуль я не знаю. Такую работу желательно проверсти силами разработчиков: вынести общие элементы в отдельные модули

Некоторые наблюдения:
Проект состояит из следующих элементов:
- Всплывающее окно с элементами стилей. Т.е. это общий элемент для несокльких микрофронтов, то его придется скопировать. По хорошему общие элементы необходимо сложить в общую библиотеку
- шапка сайта. Шапка содержит элементы для входа на сайт, регистрации и выхода с сайта. Она будет перенесена в главный микрофронтенд
- подвал сайта с некоторой текстовой информацией. Он будет перенесен в главный микрофронтенд
- карточка места, форма добавления карточки, кнопки удаления, добавлвения редактирования карточки
- методы для работы с АПИ, которые находятся в одном файле. Метды будут разнесены по разным фроентендам. Методы регистрации, входа, выхода и работы с пользовательским профилем - в микрофронтенд users. Методы добавлвения, удаления, изменения, получения картинки - в gallery. Остальные методы (только проверка токена) будут перенесены в host. 
- наборы стилей css. Большая часть папок стилей будет разнесена в соотвествующие фронтенды. Часть придется скопировать. Но при наличии возможности их необходим перенести в общую сборку
- файлы картинок GUI. Тоже что со css - большую часть можно перенести в соотвествующие сервисы. Части придется скопировать за неимением времени разбираться как сделать общую библиотеку
- входи регистрацию пользователя можно было бы вынести в отдельный микрофронтенд, но эти функциональности сильно завязаны на редактирование профиля. Сделать этого не получилось, но такую работу лучше запланировать, т.к., например, список соцсетей, которые пользователь может захотеть добавить в профиль, не связан ни с регистрацией ни с входом на сайт

В проекте есть одна функция закрытия всех окон. Ее можно разбить на части и разнести по разным микрофронтендам. Но для того, чтобы host мог реагировать на действия пользователя с окном, можно добавить события нажатия на кнопки в окне, если в этом будет необходимость.




