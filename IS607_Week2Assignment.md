#SAM RIVERA
##WEEK #2 Assignment



##1) Which destination in the flights database is the furthest distance away?

SELECT avg(distance), origin, dest
from flights
GROUP BY origin, dest
ORDER BY avg(distance) desc;
--JFK to HNL 4983
--EWR to HNL 4963

##2) What are the different numbers of engines in the planes table? For each number of engines, which aircraft have the most number of seats?

SELECT distinct engines
from planes

SELECT model, engines, seats
from planes

GROUP by model, engines, seats
ORDER by seats desc


##3) What weather conditions are associated with New York City departure delays?


SELECT f.origin AS origin, f.dep_delay AS dep_delay, w.wind_speed, w.visib, w.precip
from flights AS f

INNER JOIN weather AS w
ON f.origin = w.origin

WHERE f.dep_delay >0
AND (f.origin = 'JFK' OR f.origin = 'LGA' OR f.origin = 'EWR')

GROUP BY f.origin, f.dep_delay, w.wind_speed, w.visib, w.precip
ORDER BY f.dep_delay desc, w.wind_speed desc, w.visib asc, w.precip desc
--delays occur when high wind and/or low visibility and/or high precipitation


##4) Are older planes more likely to be delayed?

SELECT p.year AS Year, sum(f.dep_delay)/count(f.flight) AS Avg_Delay
from flights f
INNER JOIN planes p

ON f.tailnum = p.tailnum
WHERE dep_delay >0
AND p.year IS NOT NULL

GROUP BY p.year, f.flight, f.dep_delay
ORDER BY Avg_Delay desc
--Older planes are not more likely to be delayed, neither are newer planes. However, asking the person inquiring this to define "newer" into clusters could give better answer because 


##5) What airlines with 4 engines travel quicker on average from JFK-MIA?
