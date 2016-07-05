# poster
one mounth posts with email notification

ТЗ от компании ІSky

ЗАДАНИЕ:
Реализовать крон-задачу выполняющую отправку email уведомлений о завершении срока публикации объявлений.


Есть таблица объявлений:
CREATE TABLE IF NOT EXISTS `items` (
  id int(11) unsigned NOT NULL auto_increment, -- ID объявления
  user_id int(11) unsigned NOT NULL default 0, -- ID пользователя
  status tinyint(1) unsigned NOT NULL default 1, -- статус объявления
  title varchar(150) NOT NULL default '', -- заголовок объявления
  link text, -- ссылка на страницу просмотра объявления
  descr text, -- описание объявления
  publicated_to timestamp NOT NULL default '0000-00-00 00:00:00', -- срок окончания публикации объявления
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1;


И таблица пользователей:
CREATE TABLE IF NOT EXISTS `users` (
  id int(11) unsigned NOT NULL auto_increment, -- ID пользователя
  email text, -- Email пользователя
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1;


Цикл публикации объявления:
Пользователь заходит на сайт объявлений и размещает свое объявление на сайте.
После размещения оно публикуется на период в 30 дней, по истечению срока снимается с публикации.
1) Неопубликовано: status = 1, publicated_to = не указана
2) Опубликовано: status = 2, publicated_to = дата завершения срока публикации
3) Снято с публикации: status = 3, publicated_to = дата снятия с публикации


Необходимо реализовать функцию вызываемую по крону:
- Выполняющую рассылку email-уведомления о скором завершении срока публикации объявления на email-адрес пользователя (владельца объявления).
- Уведомление должно отправляться за 1,2,5 дней до завершения срока публикации, с возможностью расширить до 10 и более дней.
- Одно выполнение функции должно отправлять не более 100 писем за раз.
- Вызов функции выполняется каждые 15 минут (по крону).
- В шаблоне отправляемого письма кроме прочего (id / link / title объявления)
  предполагается наличие макроса {days} с кол-вом дней до завершения публикации: "1 день", "2 дня", ...
- Отправка письма может быть абстрактной (схематичной).
- Если двух таблиц или полей в них будет недостаточно, можно добавить.


В конечном итоге это должен быть 1 php файл без использования фреймворков/cms + SQL выгрузка.
=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=