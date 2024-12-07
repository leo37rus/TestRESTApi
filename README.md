# RESTApi
_______Задание:_______
- Необходимо реализовать АРI для работы с базой данных продуктов компании. 
База размещена под управлением СУБД MySQL.
АРI должен быть реализован как RESTful API, позволяющий обращаться к системе посредством http-запросов для создания,
редактирования и удаления записей в базе.
На АРI должна быть реализована система аутентификации/авторизации.
Запрос на получения данных должен работать для любого пользователя, а запросы на создание,
редактирование или удаление — только для авторизованного.

_______Используемые инструменты:_______
- Язык программирования: PHP 8.1.31
- СУБД: MySQL на базе Open Server

_______Структура данных:_______
- Была использована простейшая структура данных из 4-x таблиц:
продукты(products), категории продукта(categories), пользователи(users), токены пользователей(tokens). 
Каждый продукт относится только к одной из категорий.
Таблицы содержат поле статуса (0 — не отображается/пользователь — заблокирован, 1 — — — опубликовано/пользователь — активен).
Неопубликованные продукты и категории не возвращаются в ответе на запрос
от неавторизованного пользователя, но показаны авторизованному.
Заблокированный пользователь не имеет возможности авторизоваться в API.
Авторизация реализована в виде создания токена авторизации для пользователя.


_______API:_______
-  _______Категории продуктов:_______
- POST /api/vl/categories Создает категорию
- GET /api/vl/categories Возвращает все категории
- GET /api/vl/categories/{id} Возвращает категорию no
переданному id, в ответе массив id продуктов, входящих в
категорию.
- РАТСН /api/vl/categories/{id} Изменяет категорию no id. Состав
продуктов в категории не редактируется этим запросом.
- DELETE /api/vl/categories/{id} Удаляет категорию по id.
- _______Продукты:_______
- POST /api/vl/products Создает продукт
- GET /api/vl/products?category={id} Возвращает список продуктов с возможностью указать категорию.
Если категория не указана, то возвращает все продукты.
- GET /api/vl/products/{id} Возвращает продукт по переданному
id.
- PATCH /api/vl/products/{id} Изменяет продукт по id.
- DELETE /api/vl/products/{id} Удаляет продукт по id.
- _______Аутентификация:_______
- POST /api/vl/auth Аутентификация пользователя. B теле
запроса передаются логин и пароль.
- DELETE /api/vl/auth Сброс аутентификации, выход из
учетной записи.
- GET /api/vl/auth Получение данных текущего
авторизованного пользователя (его логин).


_______Запуск API:_______
- Сохранить и распаковать архив с файлами.
- Переименовать файл 123.htaccess в файл вида .htaccess
- Установить СУБД MySQL, на веб-сервере Apache
- Данные для подключения к БД описаны в файле database.php
- Используя PhpMyAdmin, создать новую базу данных TestDb
- Создать 4 таблицы products,categories,users,tokens, таблица(products) должна содержать 4 столбца(id,name,category_id,status), таблица (categories) должна содержать 3 столбца(id,name,status),таблица(users) должна содержать 4 столбца(id,login,password,activ),таблица(tokens) должна содержать 3 столбца(id,login,token), заполнить столбцы данными
- Прописать данные подключения к БД в файле database.php
- При запущенном сервере обращаться к API последству URL или cURL запросов вида http://..TestRESTApi-main/api/v1/products, так же можно использовать программу Postman, при вызове методов передавать данные в формате JSON, возвращаемые данные так же в формате JSON, авторизация просходит при вызове метода POST /api/vl/auth и передаче данных login и password в формате JSON(данные пользователя должны быть описаны в таблице users).

