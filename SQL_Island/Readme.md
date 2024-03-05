# 🏝️ SQL Island 
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/c4b2e354-f709-46c4-81f9-114cb1920641)


Note: The default language on [SQL Island](https://sql-island.informatik.uni-kl.de/) is German. To play in English, you can manually adjust the game language through the menu.

 ***

## Introduction
After a plane crash, you realize that you are the only survivor. You land on SQL Island where there are a few villages. The goal of the game is to escape from this island.

## Datasets
- VILLAGE (villageid, name, chief)
- INHABITANT (personid, name, villageid, gender, job, gold, state)
- ITEM (item, owner)

 ***

Oh dear, what happened? It seems that I am the only survivor of the air crash. Wow, there are some villages on this island. List all village names.
```sql
SELECT * FROM village
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/4e838e66-9830-4172-bd5e-77bb7578c849)

***
    
1. A few people are living in these villages. List of all inhabitants.
   ```sql
   SELECT * FROM INHABITANT
   ```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/c6a23210-bed8-4aa5-9a9c-74eb410e879a)

Woah, so many people!

***   
2. Man! I'm hungry. I will go and find a butcher to ask for some free sausages.
   ```sql
   SELECT * FROM inhabitant WHERE job = 'butcher'
   ```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/063ead22-8e52-4ae5-9530-b1a6a20698fe)

Butcher (Edward): There you are! Enjoy your meal! But take care of yourself. As long as you are unarmed, stay away from villains. Not everyone on this island is friendly.

***

3. Let's see who is friendly on this island...
```sql
SELECT * FROM inhabitant WHERE state = 'friendly';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/30cd98db-1d6a-45e4-ace0-f812c03cb476)

***

4. There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one.
```sql
SELECT * FROM inhabitant
WHERE state = "friendly"
AND job = "weaponsmith";
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/3c02fbb4-6424-4788-b8e8-a15f5566c476)

***

5. Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. Try out: job LIKE '%smith' to find all inhabitants whose job ends with 'smith' (% is a wildcard for any number of characters).
   
```sql
SELECT * FROM inhabitant
WHERE state = "friendly"
AND job LIKE "%smith";
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/934ea485-bf52-474c-a2d4-bb0b3aae8192)

That looks better! I will go and visit those smiths.

***
6. Hi stranger! Where are you going? I'm Paul, I'm the mayor of Monkeycity. I will go ahead and register you as a citizen.
```sql
INSERT INTO inhabitant (name, villageid, gender, job, gold, state) VALUES ('Stranger', 1, '?', '?', 0, '?')
```

No need to call me a stranger! What's my personid?
```sql
SELECT personid 
FROM INHABITANT 
WHERE name = "Stranger";
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/f31de0d1-c017-4d5a-92f3-587fc5ba5d0d)

***
7. Hi Ernest! How much is a sword?
Ernest: I can offer to make you a sword for 150 gold. That's the cheapest you will find! How much gold do you have?
```sql
SELECT gold 
FROM INHABITANT 
WHERE name = "Stranger";
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/dbb43c4d-47db-44db-92cd-42e0a0e9b482)

Damn! No mon, no fun. 

***
8. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don't belong to anyone?
    
```sql
SELECT * 
FROM ITEM 
WHERE owner IS null;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/cd836d24-cffc-435b-9985-b0af7e247213)

So much cool stuff!

***
9. Yay, a coffee cup. Let's collect it!
```sql
UPDATE item SET owner = 20 WHERE item = 'coffee cup'
```
Do you know a trick how to collect all the ownerless items?
```sql
UPDATE item SET owner = 20 WHERE owner IS NULL;
```
Now list all of the items I have!

```sql
SELECT * FROM ITEM WHERE owner = 20;
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/c49bdcd9-f30a-424e-9c4f-6ed74c0f7f9a)

***
10. Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items. (Hint: When you use both AND and OR, don't forget to put brackets correctly!)

```sql
SELECT * FROM INHABITANT 
WHERE state = "friendly" 
AND (job = "dealer" OR job = "merchant");
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/1384b431-4ea6-4b1c-b9c6-57acb3f15f07)

***

11. My personid is 15. I'd like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. 
```sql
UPDATE item SET owner = 15 
WHERE item = "ring" OR item = "teapot"
```
personid 15: Thank you! Here, some gold!

```sql
UPDATE inhabitant SET gold = gold + 120 WHERE personid = 20
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5a73b60c-0d2f-498d-a963-11dcad5602db)

Unfortunately, that's not enough gold to buy a sword :( 
***

12. Seems like I do have to work after all. It's not a bad idea to change my name from Stranger to my real name before I apply for a job.
```sql
UPDATE inhabitant SET name = "Khushi" 
WHERE personid = 20
```
***
13. Since baking is one of my hobbies, why not find a baker who I can work for? (Hint: List all bakers and use 'ORDER BY gold' to sort the results. 'ORDER BY gold DESC' is even better because then the richest baker is on top.)
```sql
SELECT * FROM inhabitant 
WHERE job = "baker" 
ORDER BY gold DESC
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5d1f766f-3657-4f5e-aa1c-54e8d0e0aa36)

Aha, Paul! I know him!
***

Paul: Hi! So, Khushi is your name. I saw you want to work as a baker. Okay! You will be paid 1 gold for 100 bread rolls.

(8 hours later...) Here, I made ten thousand bread rolls! I quit! This should be enough money to buy a sword. Let's see what happens with my gold balance.
```sql
UPDATE inhabitant SET gold = gold + 100 - 150
WHERE personid = 20
```
Here's your new sword! Now you can go everywhere.
```sql
INSERT INTO item (item, owner) VALUES ('sword', 20)
```
***
14. Is there a pilot on this island by any chance? He could fly me home.
```sql
SELECT * 
FROM inhabitant 
WHERE job = "pilot"
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5975fa3c-8e64-4535-95d3-3554ee6e6526)

Oh no, his state is 'kidnapped'.
***
Horrible, the pilot is held captive by Dirty Dieter! I will show you a trick how to find out the name of the village where Dirty Dieter lives.
```sql
SELECT village.name
FROM village, inhabitant
WHERE village.villageid = inhabitant.villageid
AND inhabitant.name = 'Dirty Dieter'
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/5060d0b4-261d-4d29-8c5c-cc440b38baa8)

The expression presented here is called a join. It combines the information from the inhabitant table with information from the village table by matching villageid values.

***
15. Use joins to find out the chief's name of the village Onionville.
```sql
SELECT i.name 
FROM village v
JOIN inhabitant i ON v.chief = i.personid
WHERE v.name = 'Onionville';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/8b43c3b6-1cdc-4f98-825d-500b3826c802)

I've got it! I will visit Fred and ask him about Dirty Dieter and the pilot.

***

Um, how many inhabitants does Onionville have? 
```sql
SELECT COUNT(*) FROM inhabitant, village
WHERE village.villageid = inhabitant.villageid AND village.name = 'Onionville'
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/a60ef6c1-5b11-41a1-a9c8-051319617b27)

***
16. Chief: Hello Khushi, the pilot is held captive by Dirty Dieter in his sister's house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself! (Hint: Women show up as gender = 'f')

```sql
SELECT COUNT(*)
FROM inhabitant i
JOIN village v ON i.villageid = v.villageid 
WHERE v.name = 'Onionville' AND i.gender = 'f';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/024aa0f9-3994-42c4-9d73-b99154d88419)

Only one? What's her name?
```sql
SELECT i.name
FROM inhabitant i
JOIN village v ON i.villageid = v.villageid 
WHERE v.name = 'Onionville' AND i.gender = 'f';
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/741df426-4a47-4ed3-aaf8-e9332bf7d863)

***
Dirty Dieter: Khushi, if you hand me over the entire property of our nearby village Cucumbertown, I will release the pilot. I will show you now what this property consists of.
```sql
SELECT SUM(inhabitant.gold) FROM inhabitant, village
WHERE village.villageid = inhabitant.villageid AND village.name = 'Cucumbertown'
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/97bf2156-20df-4588-ac08-c21ea6f4353a)

***
17. Oh no, baking bread alone can't solve my problems. If I continue working and selling items though, I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?
```sql
SELECT SUM(gold) 
FROM inhabitant 
WHERE job = "baker" 
OR job = "dealer" 
OR job = "merchant"
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/c13332f7-60e9-48b2-9165-bb0187f18a00)


That's not enough :(


Let's have a look at how much average gold people own, depending on their job.
```sql
SELECT job, SUM(gold),
AVG(gold)
FROM inhabitant
GROUP BY job
ORDER BY AVG(gold)
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/38efaf89-af74-42d5-956a-343e93b6b3fe)

Very interesting: For some reason, butchers own the most gold.
***
18. How much gold do different inhabitants have on average, depending on their state (friendly, ...)?
```sql
SELECT state, AVG(gold) 
FROM inhabitant 
GROUP BY state 
ORDER BY AVG(gold)
```
![image](https://github.com/khushi-sabarad/SQLFunGames/assets/71957748/de4b43ed-91e4-4e45-9d7c-148bd38cf26a)

Ok, so the only way is to mug the villains.

Or I might as well go ahead and just kill Dirty Dieter with my sword!
```sql
DELETE FROM inhabitant WHERE name = 'Dirty Dieter'
```
Dirty Diane: Heeeey! Now I'm very angry!
```sql
DELETE FROM inhabitant WHERE name = 'Dirty Diane'
```
***
19. Yeah! Now I can release the pilot!
```sql
UPDATE inhabitant SET state = 'friendly'
WHERE state = 'kidnapped'
```

Pilot: Thanks for releasing me, Khushi! I will fly you home!

I take my sword, some gold and lots of useless items with me as a souvenir. What a big adventure!
```sql
UPDATE inhabitant SET state = 'emigrated' WHERE personid = 20
```
***
The game is over. Get your certificate of completion now! If you want to change the name on the certificate, use an UPDATE command on the inhabitants table.

***
Let's connect on [LinkedIn!](https://www.linkedin.com/in/khushi-sabarad/)🤝
***
