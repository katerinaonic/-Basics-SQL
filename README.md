# -Basics-SQL
Проект выполняется в интерактивном тренажере на платформе Яндекс.Практикума

Состоит из 23 заданий на составление запросов к БД (PostgreSQL) на основе датасета Startup Investments с Kaggle (https://www.kaggle.com/justinas/startup-investments)

ER-диаграмма базы данных:
![ER-диаграмма проекта Базовый SQL](https://user-images.githubusercontent.com/117563470/206789888-280635f0-758a-42b4-9bf8-f0e7ff8a41b3.png)

***

Описание данных, которые хранят таблицы:

Таблица `acquisition`

Содержит информацию о покупках одних компаний другими.
Таблица включает такие поля:
* первичный ключ id — идентификатор или уникальный номер покупки;
* внешний ключ acquiring_company_id — ссылается на таблицу company — идентификатор компании-покупателя, то есть той, что покупает другую компанию;
* внешний ключ acquired_company_id — ссылается на таблицу company — идентификатор компании, которую покупают;
* term_code — способ оплаты сделки:
* cash — наличными;
* stock — акциями компании;
* cash_and_stock — смешанный тип оплаты: наличные и акции.
* price_amount — сумма покупки в долларах;
* acquired_at — дата совершения сделки;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `company`

Содержит информацию о компаниях-стартапах.
* первичный ключ id — идентификатор, или уникальный номер компании;
* name — название компании;
* category_code — категория деятельности компании, например:
* news — специализируется на работе с новостями;
* social — специализируется на социальной работе.
* status — статус компании:
* acquired — приобретена;
* operating — действует;
* ipo — вышла на IPO;
* closed — перестала существовать.
* founded_at — дата основания компании;
* closed_at — дата закрытия компании, которую указывают в том случае, если компании больше не существует;
* domain — домен сайта компании;
* twitter_username — название профиля компании в твиттере;
* country_code — код страны, например, USA для США, GBR для Великобритании;
* investment_rounds — число раундов, в которых компания участвовала как инвестор;
* funding_rounds — число раундов, в которых компания привлекала инвестиции;
* funding_total — сумма привлечённых инвестиций в долларах;
* milestones — количество важных этапов в истории компании;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `education`

Хранит информацию об уровне образования сотрудников компаний.
* первичный ключ id — уникальный номер записи с информацией об образовании;
* внешний ключ person_id — ссылается на таблицу people — идентификатор человека, информация о котором представлена в записи;
* degree_type — учебная степень, например:
* BA — Bachelor of Arts — бакалавр гуманитарных наук;
* MS — Master of Science — магистр естественных наук.
* instituition — учебное заведение, название университета;
* graduated_at — дата завершения обучения, выпуска;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `fund`

Хранит информацию о венчурных фондах.
* первичный ключ id — уникальный номер венчурного фонда;
* name — название венчурного фонда;
* founded_at — дата основания фонда;
* domain — домен сайта фонда;
* twitter_username — профиль фонда в твиттере;
* country_code — код страны фонда;
* investment_rounds — число инвестиционных раундов, в которых фонд принимал участие;
* invested_companies — число компаний, в которые инвестировал фонд;
* milestones — количество важных этапов в истории фонда;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `funding_round`

Содержит информацию о раундах инвестиций.
* первичный ключ id — уникальный номер инвестиционного раунда;
* внешний ключ company_id — ссылается на таблицу company — уникальный номер компании, участвовавшей в инвестиционном раунде;
* funded_at — дата проведения раунда;
* funding_round_type — тип инвестиционного раунда, например:
* venture — венчурный раунд;
* angel — ангельский раунд;
* series_a — раунд А.
* raised_amount — сумма инвестиций, которую привлекла компания в этом раунде в долларах;
* pre_money_valuation — предварительная, проведённая до инвестиций оценка стоимости компании в долларах;
* participants — количество участников инвестиционного раунда;
* is_first_round — является ли этот раунд первым для компании;
* is_last_round — является ли этот раунд последним для компании;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `investment`

Содержит информацию об инвестициях венчурных фондов в компании-стартапы.
* первичный ключ id — уникальный номер инвестиции;
* внешний ключ funding_round_id — ссылается на таблицу funding_round — уникальный номер раунда инвестиции;
* внешний ключ company_id — ссылается на таблицу company — уникальный номер компании-стартапа, в которую инвестируют;
* внешний ключ fund_id — ссылается на таблицу fund — уникальный номер фонда, инвестирующего в компанию-стартап;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

Таблица `people`

Содержит информацию о сотрудниках компаний-стартапов.
* первичный ключ id — уникальный номер сотрудника;
* first_name — имя сотрудника;
* last_name — фамилия сотрудника;
* внешний ключ company_id — ссылается на таблицу company — уникальный номер компании-стартапа;
* twitter_username — профиль сотрудника в твиттере;
* created_at — дата и время создания записи в таблице;
* updated_at — дата и время обновления записи в таблице.

***

## Задания и решения

**1. Отобразите все записи из таблицы company по компаниям, которые закрылись.**

````sql
SELECT *
FROM company
WHERE status = 'closed';
````

**2. Отобразите количество привлечённых средств для новостных компаний США. Используйте данные из таблицы company. Отсортируйте таблицу по убыванию значений в поле funding_total.**

````sql
SELECT funding_total
FROM company
WHERE category_code = 'news' AND country_code = 'USA'
ORDER BY funding_total DESC;
````

**3. Найдите общую сумму сделок по покупке одних компаний другими в долларах. Отберите сделки, которые осуществлялись только за наличные с 2011 по 2013 год включительно.**

````sql
SELECT SUM(price_amount)
FROM acquisition
WHERE term_code = 'cash'
      AND EXTRACT(YEAR FROM CAST(acquired_at AS date)) BETWEEN 2011 AND 2013;
````

**4. Отобразите имя, фамилию и названия аккаунтов людей в поле network_username, у которых названия аккаунтов начинаются на 'Silver'.**

````sql
SELECT first_name,
       last_name,
       network_username
FROM people
WHERE network_username LIKE 'Silver%';
````

**5. Выведите на экран всю информацию о людях, у которых названия аккаунтов в поле network_username содержат подстроку 'money', а фамилия начинается на 'K'.**

````sql
SELECT *
FROM people
WHERE network_username LIKE '%money%'
      AND last_name LIKE 'K%';
````

**6. Для каждой страны отобразите общую сумму привлечённых инвестиций, которые получили компании, зарегистрированные в этой стране. Страну, в которой зарегистрирована компания, можно определить по коду страны. Отсортируйте данные по убыванию суммы.**

````sql
SELECT SUM(funding_total) AS total,
       country_code
FROM company
GROUP BY country_code
ORDER BY total DESC;
````

**7. Составьте таблицу, в которую войдёт дата проведения раунда, а также минимальное и максимальное значения суммы инвестиций, привлечённых в эту дату.
     Оставьте в итоговой таблице только те записи, в которых минимальное значение суммы инвестиций не равно нулю и не равно максимальному значению.**

````sql
SELECT funded_at,
       MAX(raised_amount) AS max,
       MIN(raised_amount) AS min
FROM funding_round
GROUP BY funded_at
HAVING MIN(raised_amount) != 0 AND MIN(raised_amount) !=  MAX(raised_amount);
````

**8. Создайте поле с категориями:
                                 Для фондов, которые инвестируют в 100 и более компаний, назначьте категорию high_activity.
                                 Для фондов, которые инвестируют в 20 и более компаний до 100, назначьте категорию middle_activity.
                                 Если количество инвестируемых компаний фонда не достигает 20, назначьте категорию low_activity.
                                 Отобразите все поля таблицы fund и новое поле с категориями.**

````sql
SELECT *,
       CASE
           WHEN invested_companies>=100 THEN 'high_activity'
           WHEN invested_companies>=20 THEN 'middle_activity'
           ELSE 'low_activity'
       END AS activity
FROM fund;
````

**9. Для каждой из категорий, назначенных в предыдущем задании, посчитайте округлённое до ближайшего целого числа среднее количество инвестиционных раундов, в которых фонд принимал участие. Выведите на экран категории и среднее число инвестиционных раундов. Отсортируйте таблицу по возрастанию среднего.**

````sql
SELECT CASE
           WHEN invested_companies>=100 THEN 'high_activity'
           WHEN invested_companies>=20 THEN 'middle_activity'
           ELSE 'low_activity'
       END AS activity,
       ROUND(AVG(investment_rounds))
FROM fund
GROUP BY activity
ORDER BY ROUND(AVG(investment_rounds));
````

**10. Проанализируйте, в каких странах находятся фонды, которые чаще всего инвестируют в стартапы. 
Для каждой страны посчитайте минимальное, максимальное и среднее число компаний, в которые инвестировали фонды этой страны, основанные с 2010 по 2012 год включительно. Исключите страны с фондами, у которых минимальное число компаний, получивших инвестиции, равно нулю. 
Выгрузите десять самых активных стран-инвесторов: отсортируйте таблицу по среднему количеству компаний от большего к меньшему. Затем добавьте сортировку по коду страны в лексикографическом порядке.**

````sql
SELECT country_code,
       MIN(invested_companies),
       MAX(invested_companies),
       AVG(invested_companies)
FROM fund
WHERE EXTRACT(YEAR FROM CAST(founded_at AS date)) BETWEEN 2010 AND 2012
GROUP BY country_code
HAVING MIN(invested_companies) != 0
ORDER BY AVG(invested_companies) DESC, country_code
LIMIT 10;
````

**11. Отобразите имя и фамилию всех сотрудников стартапов. Добавьте поле с названием учебного заведения, которое окончил сотрудник, если эта информация известна.**

````sql
SELECT p.first_name,
       p.last_name,
       e.instituition
FROM people AS p
LEFT OUTER JOIN education AS e ON p.id=e.person_id;
````

**12. Для каждой компании найдите количество учебных заведений, которые окончили её сотрудники. Выведите название компании и число уникальных названий учебных заведений. Составьте топ-5 компаний по количеству университетов.**

````sql
SELECT c.name,
       COUNT(DISTINCT e.instituition)
FROM company AS c
LEFT OUTER JOIN people AS p ON c.id=p.company_id
LEFT OUTER JOIN education AS e ON p.id=e.person_id
GROUP BY c.id
ORDER BY COUNT(DISTINCT e.instituition) DESC
LIMIT 5;
````

**13. Составьте список с уникальными названиями закрытых компаний, для которых первый раунд финансирования оказался последним.**

````sql
SELECT DISTINCT(c.name)
FROM company AS c
LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
WHERE status = 'closed' 
      AND is_first_round = 1 AND is_last_round = 1
GROUP BY c.id;
````

**14. Составьте список уникальных номеров сотрудников, которые работают в компаниях, отобранных в предыдущем задании.**

````sql
WITH 
n AS (SELECT (c.id)
      FROM company AS c
      LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
      WHERE status = 'closed' 
            AND is_first_round = 1 AND is_last_round = 1
       GROUP BY c.id)

SELECT DISTINCT(p.id)
FROM people AS p
INNER JOIN n ON n.id=p.company_id;
````

**15. Составьте таблицу, куда войдут уникальные пары с номерами сотрудников из предыдущей задачи и учебным заведением, которое окончил сотрудник.**

````sql
WITH 
n AS (SELECT (c.id)
      FROM company AS c
      LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
      WHERE status = 'closed' 
            AND is_first_round = 1 AND is_last_round = 1
       GROUP BY c.id),
nc AS (SELECT DISTINCT(p.id)
       FROM people AS p
       INNER JOIN n ON n.id=p.company_id)

SELECT DISTINCT(nc.id),
       e.instituition
FROM nc
INNER JOIN education AS e ON nc.id=e.person_id;
````

**16. Посчитайте количество учебных заведений для каждого сотрудника из предыдущего задания. При подсчёте учитывайте, что некоторые сотрудники могли окончить одно и то же заведение дважды.**

````sql
WITH 
n AS (SELECT (c.id)
      FROM company AS c
      LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
      WHERE status = 'closed' 
            AND is_first_round = 1 AND is_last_round = 1
       GROUP BY c.id),
nc AS (SELECT DISTINCT(p.id)
       FROM people AS p
       INNER JOIN n ON n.id=p.company_id)

SELECT DISTINCT(nc.id),
       COUNT(e.instituition)
FROM nc
INNER JOIN education AS e ON nc.id=e.person_id
GROUP BY nc.id;
````

**17. Дополните предыдущий запрос и выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники разных компаний. Нужно вывести только одну запись, группировка здесь не понадобится.**

````sql
WITH 
n AS (SELECT (c.id)
      FROM company AS c
      LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
      WHERE status = 'closed' 
            AND is_first_round = 1 AND is_last_round = 1
       GROUP BY c.id),
nc AS (SELECT DISTINCT(p.id)
       FROM people AS p
       INNER JOIN n ON n.id=p.company_id),
ncp AS (SELECT DISTINCT(nc.id),
              COUNT(e.instituition) AS cnt
         FROM nc
         INNER JOIN education AS e ON nc.id=e.person_id
         GROUP BY nc.id)

SELECT AVG(cnt)
FROM ncp;
````

**18. Напишите похожий запрос: выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники Socialnet.**

````sql
WITH 
n AS (SELECT (c.id)
      FROM company AS c
      LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
      WHERE name LIKE 'Socialnet'
       GROUP BY c.id),
nc AS (SELECT DISTINCT(p.id)
       FROM people AS p
       INNER JOIN n ON n.id=p.company_id),
ncp AS (SELECT DISTINCT(nc.id),
              COUNT(e.instituition) AS cnt
         FROM nc
         INNER JOIN education AS e ON nc.id=e.person_id
         GROUP BY nc.id)

SELECT AVG(cnt)
FROM ncp;
````

**19. Составьте таблицу из полей:
                                 name_of_fund — название фонда;
                                 name_of_company — название компании;
                                 amount — сумма инвестиций, которую привлекла компания в раунде.
      В таблицу войдут данные о компаниях, в истории которых было больше шести важных этапов, а раунды финансирования проходили с 2012 по 2013 год включительно.**

````sql
SELECT f.name AS name_of_fund,
       c.name AS name_of_company,
       fr.raised_amount AS amount
FROM investment AS i 
LEFT OUTER JOIN company AS c ON i.company_id=c.id
LEFT OUTER JOIN fund AS f ON i.fund_id=f.id 
LEFT OUTER JOIN funding_round AS fr ON i.funding_round_id=fr.id 
WHERE c.milestones > 6 
      AND fr.funded_at BETWEEN '01.01.2012' AND '31.12.2013';
````

**20. Выгрузите таблицу, в которой будут такие поля:
                  название компании-покупателя;
                  сумма сделки;
                  название компании, которую купили;
                  сумма инвестиций, вложенных в купленную компанию;
                  доля, которая отображает, во сколько раз сумма покупки превысила сумму вложенных в компанию инвестиций, округлённая до ближайшего целого числа.
Не учитывайте те сделки, в которых сумма покупки равна нулю. Если сумма инвестиций в компанию равна нулю, исключите такую компанию из таблицы. 
Отсортируйте таблицу по сумме сделки от большей к меньшей, а затем по названию купленной компании в лексикографическом порядке. Ограничьте таблицу первыми десятью записями.**

````sql
SELECT c_1.name AS acquiring_company,
       a.price_amount AS transaction_amount,
       c.name AS acquired_company,
       c.funding_total AS total_amount,
       ROUND(a.price_amount / c.funding_total) AS share
FROM acquisition AS a 
LEFT OUTER JOIN company AS c_1 ON a.acquiring_company_id=c_1.id 
LEFT OUTER JOIN company AS c ON a.acquired_company_id=c.id
WHERE a.price_amount > 0 AND c.funding_total > 0
ORDER BY transaction_amount DESC, acquired_company
LIMIT 10;
````

**21. Выгрузите таблицу, в которую войдут названия компаний из категории social, получившие финансирование с 2010 по 2013 год включительно. Проверьте, что сумма инвестиций не равна нулю. Выведите также номер месяца, в котором проходил раунд финансирования.** 

````sql
SELECT name,
       EXTRACT(MONTH FROM CAST(fr.funded_at AS date))
FROM company AS c
LEFT OUTER JOIN funding_round AS fr ON c.id=fr.company_id
WHERE c.category_code = 'social' AND fr.raised_amount > 0
      AND EXTRACT(YEAR FROM CAST(fr.funded_at AS date)) BETWEEN 2010 AND 2013;
````

**22. Отберите данные по месяцам с 2010 по 2013 год, когда проходили инвестиционные раунды. Сгруппируйте данные по номеру месяца и получите таблицу, в которой будут поля:
      номер месяца, в котором проходили раунды;
      количество уникальных названий фондов из США, которые инвестировали в этом месяце;
      количество компаний, купленных за этот месяц;
      общая сумма сделок по покупкам в этом месяце.**

````sql
with acq as (
    select count(a.acquired_company_id) as acquired_companies,
           sum(a.price_amount) as total_price,
           extract(month from cast(a.acquired_at as timestamp)) as month
    from acquisition as a
    where cast(acquired_at as date) between '2010-01-01' and '2013-12-31'
    group by month
),    
fnd as (
    select extract(month from cast(fr.funded_at as timestamp)) as month,
           count(distinct f.name) as fund_cnt
    from fund as f
    left join investment as i on i.fund_id = f.id
    left join funding_round as fr on i.funding_round_id = fr.id
    where country_code = 'USA'
    and cast(fr.funded_at as date) between '2010-01-01' and '2013-12-31'
    group by month
)
select fnd.month, fnd.fund_cnt, acq.acquired_companies, acq.total_price
from fnd
join acq on acq.month = fnd.month
````

**23. Составьте сводную таблицу и выведите среднюю сумму инвестиций для стран, в которых есть стартапы, зарегистрированные в 2011, 2012 и 2013 годах. Данные за каждый год должны быть в отдельном поле. Отсортируйте таблицу по среднему значению инвестиций за 2011 год от большего к меньшему.**

````sql
WITH
inv_2011 AS (SELECT AVG(funding_total) AS avg_funding_total,
                    country_code
              FROM company 
              WHERE EXTRACT(YEAR FROM CAST(founded_at AS date)) = 2011
              GROUP BY country_code),
inv_2012 AS (SELECT AVG(funding_total) AS avg_funding_total,
                    country_code
              FROM company 
              WHERE EXTRACT(YEAR FROM CAST(founded_at AS date)) = 2012
              GROUP BY country_code),
inv_2013 AS (SELECT AVG(funding_total) AS avg_funding_total,
                    country_code
              FROM company 
              WHERE EXTRACT(YEAR FROM CAST(founded_at AS date)) = 2013
              GROUP BY country_code)

SELECT inv_2011.country_code,
       inv_2011.avg_funding_total,
       inv_2012.avg_funding_total,
       inv_2013.avg_funding_total
FROM inv_2011 
INNER JOIN inv_2012 ON inv_2011.country_code=inv_2012.country_code
INNER JOIN inv_2013 ON inv_2012.country_code=inv_2013.country_code
ORDER BY inv_2011.avg_funding_total DESC;
````
***

