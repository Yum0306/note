```
select CONVERT(varchar(12) , day_date, 111) AS '日期',SUM(case when breakfast in ('1') then 1 ELSE 0 end) as '早餐',SUM(case when lunch in ('1') then 1 ELSE 0 end) as '午餐',SUM(case when dinner in ('1') then 1 ELSE 0 end) as '晚餐' from catering_ordering where day_date >= '2022-06-24 00:00:00' AND day_date <= '2022-06-24 23:59:59' GROUP BY day_date
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODUwOTg4MzIsLTcwMzMyNDcwNl19
-->