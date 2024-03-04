# 🏝️ SQL Island 
<img width="500" alt="sql_island" src="https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/bf9eb234-f1f1-4f6d-95b6-44a4e27859a9">


Note: The default language on [SQL Island](https://sql-island.informatik.uni-kl.de/) is German. To play in English, you can manually adjust the game language through the menu.

 ***

## Introduction
After a plane crash, you realize that you are the only survivor. You land on SQL Island where there are a few villages. The goal of the game is to escape from this island.

## Datasets
- VILLAGE (village number, name, chief)
- RESIDENTS (resident number, name, village number, gender, profession, gold, status)
- SUBJECT (object, owner)


 ***

1. List all village names
   ```sql
   SELECT * FROM VILLAGE;
   ```
2. A few people are living in these villages. List of all inhabitants.
   ```sql
   SELECT * FROM INHABITANT;
   ```
3. Find a butcher to ask for some free sausages.
   ```sql
   SELECT * FROM inhabitant WHERE job = 'butcher'
   ```
Butcher (Edward): There you are! Enjoy your meal! But take care of yourself. As long as you are unarmed, stay away from villains. Not everyone on this island is friendly.

4. Let's see who is friendly on this island...
```sql
SELECT * FROM inhabitant WHERE state = 'friendly';
```
5. There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one.
```sql
SELECT * FROM inhabitant
WHERE state = "friendly"
AND job = "weaponsmith";
```
6. Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. Try out: job LIKE '%smith' to find all inhabitants whose job ends with 'smith' (% is a wildcard for any number of characters).
   
```sql
SELECT * FROM inhabitant
WHERE state = "friendly"
AND job LIKE "%smith";
```
That looks better! I will go and visit those smiths.

7. 
