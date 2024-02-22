# Проект A/B--тестирования новой платежной системы 
## Стек:
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-blue?logo=seaborn&logoColor=white&style=for-the-badge)
![Clickhouse](https://camo.githubusercontent.com/317deacab8b76427e3055c39199ac23c1d09699098327690178ff9af3611d0f6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d436c69636b686f7573652d4646463f7374796c653d666f722d7468652d6261646765266c6f676f3d436c69636b686f757365)
![API](https://camo.githubusercontent.com/baaf5e1a9158523784ea96088085eeb4b44ac2932739d1dfa4eee337ee7977af/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d4150492d4646363630303f7374796c653d666f722d7468652d6261646765266c6f676f3d415049)

## Для удобства блоки задач были разделены на 3 части: задание 1,задание 2 и задание 3. 
-В первом блоке-A/B-тестирование данных, подключенных через Яндекс.Диск 
-Во втором блоке-анализ БД SQL, ETL(Python+SQL),расчет ключевых метрик 
-В третьем блоке- построение графиков по метрикам в зависимости от изменения данных датафрейма groups_add, а также написание функции, которая перестраивала графики по определенным в 1 задании метрикам. 
______
Задачами первого раздела исследования являются:
*1.Изучение распределений данных 
*2.Определение ключевых метрик для A/B-тестирования, а также наличие статистически значимых различий между группами 
*3.Принятие решения о запуске новой механики работы платежной системы на всех пользователей сайта компании. 
## Задачами второго раздела исследования являются : 
*1. Написать оптимальный запрос, который даст информацию о количестве очень усердных студентов. ###Под усердным
студентом мы понимаем студента, который правильно решил 20 задач за текущий месяц. 
* 2.В одном запросе выгрузить следующую информацию о группах пользователей:
  -ARPU
  -ARPAU
  -CR в покупку
  -СR активного пользователя в покупку
  -CR пользователя из активности по математике в покупку курса по математике
## Задачами третьего раздела исследования являются : 
*1. Реализовать функцию, которая будет автоматически подгружать информацию из дополнительного файла groups_add.csv и на
основании дополнительных параметров пересчитывать метрики. 
*2. Реализовать функцию, которая будет строить графики по получаемым метрикам.
_______
## **Входные данные** 
_____
## Первый раздел исследования 
*groups.csv - файл с информацией о принадлежности пользователя к контрольной или экспериментальной группе (А -контроль, B - целевая группа) 
*groups_add.csv - дополнительный файл спользователями, который вам прислали спустя 2 дня после передачи данных
*active_studs.csv - файл с информацией о пользователях, которые зашли на платформу в дни проведения эксперимента. \*checks.csv - файл с
информацией об оплатах пользователей в дни проведения эксперимента.
_____
## Второй раздел исследования 
Образовательные курсы состоят из различных уроков, каждый из которых состоит из нескольких маленьких заданий. Каждое такое маленькое задание называется "горошиной".
Назовём очень усердным учеником того пользователя, который хотя бы раз
за текущий месяц правильно решил 20 горошин.
## Таблица default.peas:
| Название атрибута| Тип атрибута| Смысловое значение|
|:------------- |:---------------:| -------------:|
| st_id         | int          | ID ученика        |
| timest         | timestamp          | Время решения карточки        |
| correct         | bool          | Правильно ли решена горошина?        |
| subject         | text          | Дисциплина, в которой находится горошина        |
_____
##Таблица default.studs:
| Название атрибута| Тип атрибута| Смысловое значение|
|:------------- |:---------------:| -------------:|
| st_id         | int          | ID ученика        |
| test_grp         | text          | Метка ученика в данном эксперименте        |
_____
##Таблица default.final_project_check:
| Название атрибута| Тип атрибута| Смысловое значение|
|:------------- |:---------------:| -------------:|
| st_id         | int          | ID ученика        |
| sale_time         | timestamp          | Время покупки        |
| money         | int          | Цена, по которой приобрели данный курс        |
| subject         | text          | Изучаемый предмет        |

## Выводы по итогам исследования 
  ## По первому этапу 
    -По 1 заданию я использовала следующие метрики:конверсия со входа на сайт в покупку, поскольку если бы она статистически значимо различалась с контрольной группой, это говорило бы о прямом влиянии новой механики оплаты услуг на сайте. Также я использовала ARPU(средний чек на пользователей в период тестирования) и ARPPU(средний чек среди уже оплативших клиентов), поскольку возможно новая система оплаты на сайте связана с выпадающими рекомендациями в корзине+ если было неудобно покупать что-то на сайте, вероятно, клиент уже второй раз не вернулся бы и ушел к конкуренту.
    -Конверсия в покупку на сайте статистически значимо не отличается в зависимости от выбранной группы.Различия ARPU и ARPPU являются статистически значимыми(т.е. нулевые гипотезы 2, 3 опроверглись), больше всего новая механика оплаты услуг на сайте положительно влияет на средний чек среди что-то купивших клиентов сайта(ARPPU), чуть меньше на ARPU(средний чек среди пользователей), вероятность что последний при работе нового алгоритма будет хуже составляет (10.37%). 
   **Подводя итог, стоит запускать новую механику работы на всех пользователей, поскольку она увеличивает ARPU, ARPPU.**
  ## По второму этапу
    *Количество очень усердных студентов составляет 136 человек 
  ## Изменение метрик 
  *CR в покупку у относительно контрольной группы вырост в 2 раза,
  *CR в покупку среди активных студентов вырос в 2.36 раза, 
  *CR среди активных студентов по математике вырос на 41%
  *ARPAU вырос в 2.86 раза 
  *ARPAU для активных по математике 2.01 
  *ARPU вырос в 2.4 раза
  *ARPPU вырос на 20% 
**Таким образом, новый экран оплаты, разработанный командой, можно раскатывать на всех пользователей** 
  ## По третьему этапу 
**Если удалить 80% данных из файла groups_add, метрики статистически значимо не отличаются**
