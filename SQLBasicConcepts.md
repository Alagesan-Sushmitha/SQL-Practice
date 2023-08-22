# SQL-Practice

#### combination of 2 tables 

``` SQL

select p.firstName, p.lastName, a.city,a.state from Person P
left join Address A on p.personId = a.personId;
```

#### Comparision of attribute within same table

``` SQL
select e.name as Employee from Employee e
inner join Employee m on m.id = e.managerId where e.salary > m.salary;
```

#### Detecting duplicates

```SQL
select email as Email from Person
group by email having count(email)>1;
```

#### Detecting exceptions acroos 2 tables
``` SQL
select name as Customers from Customers 
where id not in 
(select c.id from Customers c 
inner join Orders o 
on c.id = o.customerId);
```

#### Detecting and deleting duplicate records within same table
``` SQL
Delete p1 from person p1, Person p2 
where p1.id > p2.id and p1.email = p2.email;
```

#### Comparision of records within same tables
##### Scenario: Find all dates' Id with higher temperatures compared to its previous dates (yesterday)

``` SQL
select w1.id from Weather w1, Weather w2
where datediff(w1.recordDate, w2.recordDate) = 1 
and w1.temperature > w2.temperature;
```

#### concentration on joins

``` SQL
select e.name , b.bonus from Employee e left join Bonus b 
on e.empId = b.empId where b.bonus < 1000 or b.bonus is NULL;
```

#### Finding maximum acroos groups 
``` SQL 
select customer_number from Orders 
group by customer_number order by count(customer_number) desc
limit 1;
```

#### Scenario Question
##### Scenario:
* Find the overall acceptance rate of requests, which is the number of acceptance divided by the number of requests. Return the answer rounded to 2 decimals places.

###### Note that:

* The accepted requests are not necessarily from the table friend_request. In this case, Count the total accepted requests (no matter whether they are in the original requests), and divide it by the number of requests to get the acceptance rate.
* It is possible that a sender sends multiple requests to the same receiver, and a request could be accepted more than once. In this case, the ‘duplicated’ requests or acceptances are only counted once.
If there are no requests at all, you should return 0.00 as the accept_rate.

![image](https://github.com/Alagesan-Sushmitha/SQL-Practice/assets/137837229/0cb621e9-19e0-4ee3-9da7-8f61db58fe6b)


``` SQL
select ifnull(round((count(distinct requester_id,accepter_id)/count(distinct sender_id,send_to_id)),2),0.00) as accept_rate
 from FriendRequest, RequestAccepted;
```



