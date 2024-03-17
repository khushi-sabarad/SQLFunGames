# 🔍SQL Murder Mystery
## Can you find out whodunnit?🕵️‍♀️
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5acfdcbc-4da1-47fe-8251-a23d1e2befc3)

There's been a Murder in SQL City! The SQL Murder Mystery is designed to be both a self-directed lesson to learn SQL concepts and commands and a fun game for experienced SQL users to solve an intriguing crime.

***

## Introduction
A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. 
You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018,​ and that it took place in ​SQL City. 
Start by retrieving the corresponding crime scene report from the police department’s database.

### Schema:
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/bcf64498-83c2-4129-862e-43a8b2fab29f)

***
```sql
SELECT * FROM crime_scene_report
WHERE type = 'murder' AND date ='20180115' AND city ='SQL City';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/11698ba5-812e-4605-80ed-69be4e3c490e)

***

```sql
SELECT * FROM person 
WHERE 
    (name LIKE 'Annabel%' AND address_street_name = 'Franklin Ave') 
    OR 
    (address_street_name = 'Northwestern Dr'
	    AND address_number = (
        SELECT MAX(address_number) 
        FROM person 
        WHERE address_street_name = 'Northwestern Dr'
    ));
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/abfd4547-ddc9-4fe5-948a-3e7ad99789ae)

***

```sql
SELECT * FROM interview
WHERE person_id = 16371 OR person_id = 14887;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/84a9ee38-f1ab-4913-bbb2-5b765bf48de1)

***

```sql
SELECT * FROM get_fit_now_check_in
WHERE check_in_date = '20180109' AND membership_id LIKE '48Z%';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/01ef652e-ec22-4c5e-9056-a646e8c8e9b3)

***

```sql


```

***

```sql


```

***

```sql


```

***

```sql


```

***

```sql


```

***


