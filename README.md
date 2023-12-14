# SQl-Mystery-Murder
**Hello friends, I want to show you the solution to the quest.**

**The first step is to request a crime scene report. Here you will find screenshots of the execution and the necessary code**

select * from crime_scene_report


WHERE date = 20180115 AND type = 'murder' AND city = 'SQL City'

![1 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/160b0898-92a2-4a03-98ad-b39393984281)

**The second step is to look for information about Annabelle who lives on Franklin Street.** 


select * from person 

WHERE name LIKE 'Annabel%' AND address_street_name  = 'Franklin Ave'

![2 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/b0a89a0b-ab49-49a3-9a9e-1b1b3c8a47c8)

**The third step is to look for information about the person who lives in the last house on Northwestern Dr.**


<code>
SELECT * FROM person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC;

-- The first witness lives at the last house on "Northwestern Dr".
-- The second witness, named Annabel, lives somewhere on "Franklin Ave".
-- id = 16371 Annabel
</code>

![3 st](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/851e8b19-fd01-4988-81e0-08002c0a76bb)

**The fourth step is to look for information on their reports.**


-- 2 witnesses.

-- 1st - lives at the last house on "Northwestern Dr". 14887Morty Schapiro

-- 2nd - Annabel, lives somewhere on "Franklin Ave". 16371 Annabel Miller

SELECT *
FROM person
WHERE id IN (14887,16371)

![4 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/049dcff8-ad2e-41b3-a4d7-b4e96eabe7bc)

**5-6 steps.  We are looking for a car using the data from the reports.**


-- "Get Fit Now Gym" bag started with "48Z" gold member

-- car with a plate that included "H42W"

-- my gym last week on January the 9th


select p.* from drivers_license as dl

INNER JOIN person as p ON  p.license_id = dl.id

WHERE plate_number Like '%H42W%'

![5-6 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/036ab023-b1ed-4a49-9f31-9109d9f7d7a9)

**7 steps.  I find this person thanks to the reports, making the necessary joins under certain conditions.**


-- "Get Fit Now Gym" bag started with "48Z" gold member

-- car with a plate that included "H42W"

-- my gym last week on January the 9th

SELECT p.* , gc.*

FROM drivers_license AS dl

INNER JOIN person AS p ON p.license_id = dl.id

INNER JOIN get_fit_now_member AS gf ON p.id = gf.person_id

INNER JOIN get_fit_now_check_in AS gc ON gf.id = gc.membership_id

WHERE dl.plate_number LIKE '%H42W%'

AND gf.membership_status = 'gold'

AND gc.check_in_date = 20180109;

![7 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/b6155497-657f-4fe0-ada1-f20627ce216d)

**8 steps. I check this person as he fits, and you can see that not everything is as easy as we thought**

![check result 7 s](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/26c35735-ec39-44d5-8847-76ffc489b86d)

**9 step. Checking this person's report.** 


select * from interview
WHERE person_id = 67318

![8 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/2415beb1-ada3-44f4-8075-7ac5ce3dded5)

**10 step. I take the necessary actions to search for a car and a person by its parameters.**


-- hired by a woman with a lot of money

-- around 5'5" (65"') or 5'7" (67"'), red hair, drives a Tesla Model s

-- attended the SQL Symphony Concert 3 times in December 2017

select * from drivers_license

WHERE hair_color = 'red'

AND height >=65

AND height <=67

and car_make = 'Tesla'

AND car_model = 'Model S'

AND gender = 'female'

![9 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/dcea881b-999b-4ca8-8f77-84a9dacd47f8)

**11 Step. I do the necessary joins to find the concert. I use CTE/ in the final code.**


-- hired by a woman with a lot of money

-- around 5'5" (65"') or 5'7" (67"'), red hair, drives a Tesla Model s

-- attended the SQL Symphony Concert 3 times in December 2017

select p.* ,fb.* from drivers_license as dl

INNER JOIN person as p ON p.license_id = dl.id

INNER JOIN facebook_event_checkin as fb ON fb.person_id =p.id

WHERE hair_color = 'red'

AND height >=65

AND height <=67

and car_make = 'Tesla'

AND car_model = 'Model S'

AND gender = 'female'





-- hired by a woman with a lot of money

-- around 5'5" (65"') or 5'7" (67"'), red hair, drives a Tesla Model s

-- attended the SQL Symphony Concert 3 times in December 2017

with CTE as (
SELECT

person_id,

COUNT (*) as visits

FROM facebook_event_checkin

WHERE date BETWEEN 20171201 AND 20171231

AND event_name = 'SQL Symphony Concert'

GROUP BY person_id,

event_name

HAVING COUNT (*)
)



select p.* , fb.* from drivers_license as dl

INNER JOIN person as p ON p.license_id = dl.id

INNER JOIN CTE as fb ON fb.person_id =p.id

WHERE hair_color = 'red'

AND height >=65

AND height <=67

and car_make = 'Tesla'

AND car_model = 'Model S'

AND gender = 'female'

![10 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/de535e63-b831-4bc5-b56b-8f78ff4c76b7)

![11 step](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/794844fe-e3a5-4d58-a952-42afd7d3d49a)


**12 step. Found the real killer**
![result](https://github.com/Hordiychuk-Radion/SQl-Mystery-Murder/assets/139583782/cb4b2f62-e87e-4f3e-96fb-170762f1f20b)



