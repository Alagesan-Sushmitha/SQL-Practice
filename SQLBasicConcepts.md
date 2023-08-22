# SQL-Practice

#### combination of 2 tables 

""" sql

select p.firstName, p.lastName, a.city,a.state from Person P left join Address A on p.personId = a.personId;
