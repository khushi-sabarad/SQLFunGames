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
WHERE type = 'murder' AND date = 20180115 AND city = 'SQL City';
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
WHERE check_in_date = 20180109 AND membership_id LIKE '48Z%';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/01ef652e-ec22-4c5e-9056-a646e8c8e9b3)

***
For the witness to see the killer at the gym, they should both be checked in around the same time. 

```sql
SELECT * FROM get_fit_now_check_in
WHERE check_in_date = 20180109 ORDER BY check_in_time;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/8953e44b-2576-4c0d-abd7-097c82cbc35b)

The witness' membership_id is among these three.

***

For all we know, the witness could be the killer too.
```sql
SELECT * FROM get_fit_now_member
WHERE person_id = 16371;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/cfd22259-7fc6-4f2d-a456-940da8393fbf)

Now, we can rule out the possibility that the witness is the killer as her membership ID does not start with 48Z.

***
To find information about the other two people who were at the gym when the witness was there.

```sql
SELECT * FROM get_fit_now_member
WHERE membership_status = 'gold' AND (id = '48Z55' OR id = '48Z7A');
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/55e8a803-57a9-496b-8125-5aad3cdebaa6)

***

```sql
SELECT * FROM person
WHERE id = 67318 OR id = 28819;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/ec0aaf0c-ab16-4f6c-ae6d-6cd415ab5bbd)

***

```sql
SELECT * FROM drivers_license
WHERE id = 173289 OR id = 423327;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5d7a4900-dd86-462f-ad6a-e4d640942c7b)

***
The plate number contains H42W. We found the killer !!!
Killer: Jeremy Bowers (id: 67318)

***
```sql
INSERT INTO solution VALUES (1, 'Jeremy Bowers');
SELECT value FROM solution;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/4139361e-4c91-4b42-9374-d9d307ae6ce0)

***
## Let's find the real villain behind the murder

```sql
SELECT * FROM interview WHERE person_id = 67318;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/32d61d68-6df6-40b2-ae74-2126a208f4a7)

***
### Beginner friendly step-by-step version:

```sql
SELECT * FROM drivers_license
WHERE 	gender = 'female' AND hair_color = 'red'
	AND car_make = 'Tesla' AND car_model = 'Model S'
	AND height > 64 AND height < 68;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/f834853f-5f7f-4017-9df7-46a718fc3720)

***

```sql
SELECT * FROM person
WHERE license_id = 202298 OR license_id = 291182 OR license_id = 918773;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/291bd1df-50fb-407b-9e85-6bc27583a0a6)

***
```sql
SELECT * FROM facebook_event_checkin
WHERE 	event_name = 'SQL Symphony Concert'
	AND `date` LIKE '201712%'
GROUP BY person_id
HAVING COUNT(*) = 3; 
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/4a2911e6-6e97-4c5b-a7c4-e99ffe3e3eb2)

We found the real villain behind the murder !!!
Real Villain: Miranda Priestly (99716)

The killer mentioned that the one who hired him has a lot of money, let's find out how much.
```sql
SELECT * FROM income WHERE ssn = 987756388;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/2f11344b-0ba7-4344-a48b-8b9fd7d57417)

***
### Single query version:
```sql
SELECT name, annual_income
FROM (
    SELECT person.id AS person_id, name, annual_income
    FROM (
        SELECT id AS license_id
        FROM drivers_license
        WHERE gender = 'female' AND hair_color = 'red' 
          AND car_make = 'Tesla' AND car_model = 'Model S' 
          AND height >= 64 AND height <= 68
    ) AS person_described
    LEFT JOIN person ON person_described.license_id = person.license_id
    LEFT JOIN income ON person.ssn = income.ssn
) AS rich_suspects

JOIN (
    SELECT person_id
    FROM (
        SELECT person_id
        FROM facebook_event_checkin
		WHERE event_name = 'SQL Symphony Concert'
		AND `date` LIKE '201712%'
		GROUP BY person_id
		HAVING COUNT (*) = 3
    ) AS concert_attenders    
) AS concert_attenders ON rich_suspects.person_id = concert_attenders.person_id;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/09ea3108-6594-4531-80ed-064525a36500)

```sql
INSERT INTO solution VALUES (1, 'Miranda Priestly');
SELECT value FROM solution;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/2adeea08-1212-42e0-8fdd-06ec2a453c22)

🍾🍾🍾🍾

***
Let's connect on [LinkedIn!](https://www.linkedin.com/in/khushi-sabarad/)🤝
***

