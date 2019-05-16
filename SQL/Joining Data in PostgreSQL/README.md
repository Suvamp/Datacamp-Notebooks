# Lesson 1

### Inner join

intersection of left table id with right table

```sql
select p1.country,p1.continent,
prime_ministers, president
from prime_minister as 	p1
inner join president as p2
on p1.country=p2.country;
```



```sql
select * 
from cities
inner join countries 
on cities.country_code=countries.code;
```


```sql
select cities.name as city,countries.name as country,countries.region
from cities 
inner join countries 
on (cities.country_code=countries.code);
```


