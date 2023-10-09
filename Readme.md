# SQL Query Questions and Answers

## Hackerrank SQL preparation Questions and answers

### 1. Query all columns for all American cities in the CITY table with populations larger than 100000.
The CountryCode for America is USA.

```
select * from city where countrycode = 'USA' and population>100000;
```

### 2. Query the NAME field for all American cities in the CITY table with populations larger than 120000.
The CountryCode for America is USA.

```
select name from city where countrycode = 'USA' and population>120000;
```

### 3. Query all columns (attributes) for every row in the CITY table.

```
select * from city;
```

### 4. Query all columns for a city in CITY with the ID 1661.

```
select * from city where id = 1661;
```

### 5. Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

```
select * from city where countrycode = 'JPN';
```

### 6. Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

```
select name from city where countrycode = 'JPN';
```

### 7. Query a list of CITY and STATE from the STATION table.

```
select city,state from station;
```

### 8. Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.

```
select distinct city from station where mod(id,2)=0;
```

### 9. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

```
select count(city) - count(distinct city) from station;
```

### 10. Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```
select city,length(city) from station order by length(city),city limit 1;
select city,length(city) from station
 order by length(city) desc,city limit 1;
```

### 11. Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

```
select distinct city from station
 where city like 'A%' or city like 'E%' or
  city like 'I%' or city like 'O%' or city like 'U%';
```
or
```
select distinct city from customers 
where city regexp '[AEIOUaeiou].+';
```

### 12. Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

```
select distinct city from station
 where city like '%a' or city like '%e' or
  city like '%i' or city like '%o' or city like '%u';
```

### 13. Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

```
select distinct city from station 
where city not rlike '^[aeiouAEIOU].*$';
```

### 14. Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

```
select distinct city from station
 where upper(substr(city, length(city), 1)) not in ('A','E','I','O','U') 
 and lower(substr(city, length(city),1)) not in ('a','e','i','o','u');
```

### 15. Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

```
select distinct city from station
 where lower(substr(city,1,1)) not in ('a','e','i','o','u')
  or lower(substr(city,length(city),1)) not in ('a','e','i','o','u');
```

### 16. Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

```
select distinct city from station
 where lower(substr(city,1,1)) not in ('a','e','i','o','u')
  and lower(substr(city,length(city),1)) not in ('a','e','i','o','u');
```

### 17. [Sales Analysis III Leetcode](https://leetcode.com/problems/sales-analysis-iii/description/) - Write a solution to report the products that were only sold in the first quarter of 2019. That is, between 2019-01-01 and 2019-03-31 inclusive.

```
select product_id,product_name from product inner join sales using(product_id)
 group by product_id  having min(sale_date) >= '2019-01-01' and max(sale_Date) <= '2019-03-31';
```

### 18. [Article Views I Leetcode](https://leetcode.com/problems/article-views-i/description/) - Write an SQL query to find all the authors that viewed at least one of their own articles. Return the result table sorted by id in ascending order.

```
select distinct author_id as id from views 
where author_id=viewer_id order by id;
```

### 19. [Immediate food delivery I Leetcode](https://leetcode.com/problems/immediate-food-delivery-i/) - Write an SQL query to find the percentage of immediate orders in the 

```
select round(avg(order_date = customer_pref_delivery_date)*100,2) 
as immediate_percentage from delivery;
```

### 20. [Ads performance Leetcode](https://leetcode.com/problems/ads-performance/) - Write an SQL query to find the ctr of each Ad. Round ctr to two decimal points. Return the result table ordered by ctr in descending order and by ad_id in ascending order in case of a tie.

```
select ad_id,
round(avg(case when action="Clicked" then 1 else 0 end)*100,2) as ctr from Ads group by ad_id order by ctr desc,ad_id;
```

### 21. [Find the team size Leetcode](https://leetcode.com/problems/find-the-team-size/) - Write an SQL query to find the team size of each of the employees. Return result table in any order.

```
select e1.employee_id,count(*) from employee e1 left join employee e2 using(team_id) group by e1.employee_id;
```

### 22. [Weather Type Leetcode](https://leetcode.com/problems/weather-type-in-each-country/) - Write an SQL query to find the type of weather in each country for November 2019. The type of weather is: ● Cold if the average weather_state is less than or equal 15, ● Hot if the average weather_state is greater than or equal to 25, and ● Warm otherwise. Return result table in any order.

```
select country_name,(
case when avg(weather_state)<=15 then 'Cold'
when avg(weather_state)>=25 then 'Hot'
else 'Warm' end
)as weather_type from country left join
 weather using(country_id) where day between '2019-11-01' and 
 '2019-11-30' group by country_name;
```