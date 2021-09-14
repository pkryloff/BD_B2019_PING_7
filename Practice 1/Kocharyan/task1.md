# Задание №1. Кочарян Тигран БПИ197 (на ускоренном обучении из БПИ209).

---

# Условие:
Вам поручено разработать онлайн-аукцион. 
Он позволяет продавцам продавать свои товары с помощью аукциона. 
Покупатели делают ставки. Выигрывает последняя самая высокая ставка. 
После закрытия аукциона победитель оплачивает товар с помощью кредитной карты. 
Продавец отвечает за доставку товара покупателю.

* Предложите список функциональных требований для проекта.
* Определите роли пользователей и действия для каждой роли.
* Определите объекты, о которых будут храниться данные.
* Определите связи между объектами для хранения данных.
* Нарисуйте схему объектной модели (используя любые обозначения, которые вам удобны).

---

# Решение:

## Роли пользователей 
1. Администратор приложения
2. Продавец
3. Покупатель

---

## Функциональные требования:
### Требования к функционалу пользователя:
1. Доступен функционал как покупателя, так и продавца.
2. Доступно одновременное хранение информации по нескольким кредитным картам.
3. Для оплаты доступно использование Google Pay/Apply Pay/Samsung Pay.
4. Регистрация доступна с помощью:
	* электронной почты и пароля
	* google-аккаунта
5. Добавление фотографии на страницу профиля.
6. Привязка номера телефона для двухфакторной аутентификации.

### Требования к функционалу продавца:
1. Выставление на продажу одновременно нескольких товаров.

2. При выставлении товара на аукцион, продавец может указать следующую информацию:
    * Фотография товара
    * Название товара
    * Описание товара
    * Начальную цену товара
    * Дату окончания аукциона

3. В выставленном товаре продавец может редактировать следующую информацию:
    * Фотография товара
    * Описание товара

4. В проданном на аукционе товаре, продавец может добавить/редактировать следующую информацию:
    * Текущий статус доставки

5. Продавец может удалить товар с продажи в течение 10 минут после выставления на аукцион при согласовании с администратором.

### Требования к функционалу покупателя:
1. Может делать и повышать ставки на несколько товаров одновременно.
2. Либо привязано что-то из Google Pay/Apply Pay/Samsung Pay, либо привязана хотя бы одна кредитная карта.
3. Просмотр ленты выигранных товаров с информацией о текущем статусе доставки.

### Требования к функционалу администратора:
1. Удаление товаров, противоречящих закону или условиям использования, без согласования с продавцом и с возможностью блокировки аккаунта продавца и всех участников, которые сделали ставку.
2. Рассмотрение заявок продавцов на снятие своего товара с аукциона с возможностью временной блокировки продавца.

---

## Объекты 
1. Пользователь:
    * ID пользователя
    * Имя пользователя
    * Электронная почта
    * Телефон
    * Дата регистрации
    * Является ли пользователь администратором/покупателем/продавцом?

2. Кредитная карта:
    * ID карты
    * Номер карты
    * Срок действия карты
    * CVV2 или CVC2
    * Имя и фамилия владельца карты латиницей

3. Ставка:
    * ID пользователя, который сделал ставку
    * ID товара, на который делается ставка
    * ID ставки
    * Сумма ставки
    * Дата/время ставки

4. Товар:
    * ID товара
    * ID пользователя-продавца
    * ID выигрывающей ставки
    * Имя товара
    * Описание товара
    * Текущая цена товара
    * Начальная цена товара
    * Дата начала аукциона на данный товар
    * Дата конца аукциона на данный товар
    * Статус продажи
    * Статус доставки, если товар продан

5. Изображение профиля:
    * ID пользователя, к которому привязана фотография
    * ID фотографии
    * URL-ссылка на изображение

6. Изображение товара:
    * ID товара, к которому привязана фотография
    * ID фотографии
    * URL-ссылка на изображение

---

## Связи между объектами:

#### Один к многим
1. Пользователь - Ставка
2. Пользователь - Кредитная карта
3. Пользователь - Товар

#### Многие к одному:
1. Ставка - Товар
2. Изображение товара - Товар
3. Изображение профиля - Пользователь
 
---

## Диграмма:

[Ссылка на DrawSQL](https://drawsql.app/totowka/diagrams/auction-kocharyan#)

![Схема](scheme.jpg)