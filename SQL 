
# 1. Create a View called “forestation” by joining all three tables - forest_area, land_area and regions in the workspace.

DROP  VIEW  IF  EXISTS forestation;
CREATE OR REPLACE  VIEW  forestation  AS
SELECT
fa.country_code,
fa.country_name,
r.region,
fa.year,
fa.forest_area_sqkm,
la.total_area_sq_mi *  2.59  AS total_area_sqkm,
ROUND((fa.forest_area_sqkm / (la.total_area_sq_mi *  2.59))::numeric  *  100, 1) AS forestation_percentage
FROM
forest_area AS fa
JOIN land_area AS la
ON fa.country_code = la.country_code
AND fa.year = la.year
JOIN regions AS r
ON fa.country_code = r.country_code
WHERE
fa.forest_area_sqkm IS NOT NULL
AND la.total_area_sq_mi IS NOT NULL

  
  
  
  
  

# 1. GLOBAL SITUATION

  

# a. What was the total forest area (in sq km) of the world in  1990? Please keep  in mind that you can use the country record denoted as “World" in the region table.

select forest_area_sqkm
from forest_area
where country_name = 'World' and year = 1990

  
  
# b. What was the total forest area (in sq km) of the world in 2016? Please keep in mind that you can use the country record in the table is denoted as “World.”select forest_area_sqkm

  

select forest_area_sqkm
from forest_area
where country_name = 'World' and year = 2016

  
  

# c. What was the change (in sq km) in the forest area of the world from 1990 to 2016?

  

select forest_area_sqkm_1990 - forest_area_sqkm_2016
from base_country
where country_name = 'World'



  

# d.What was the percent change in forest area of the world between 1990 and 2016?

  

select ((forest_area_sqkm_1990 - forest_area_sqkm_2016)/forest_area_sqkm_1990)*100 as percent_change
from base_country
where country_name = 'World'

  
  

# e. If you compare the amount of forest area lost between 1990 and 2016, to which country's total area in 2016 is it closest to

SELECT f.country_name, 1324449 -total_area_sqkm_2016 as diff_total_forest ,
SUM(total_area_sqkm) AS total_area_of_land
FROM forestation f
join base_country bc
on f.country_code = bc.country_code
WHERE YEAR = 2016
AND total_area_sqkm <= 1324449
GROUP BY 1,2
ORDER BY total_area_of_land DESC
LIMIT 1

  
  

# 2.Regional Outlook

  

# Create a table that shows the Regions and their percent forest area (sum of forest area divided by sum of land area) in 1990 and 2016. (Note that 1 sq mi = 2.59 sq km).

CREATE OR REPLACE VIEW base_region AS
WITH forestation_1990 AS (
SELECT
region,
SUM(forest_area_sqkm) AS forest_area_sqkm,
SUM(total_area_sqkm) AS total_area_sqkm
FROM
forestation
WHERE
year = 1990
GROUP BY 1
),

forestation_2016 AS (
SELECT
region,
SUM(forest_area_sqkm) AS forest_area_sqkm,
SUM(total_area_sqkm) AS total_area_sqkm
FROM
forestation
WHERE
year = 2016
GROUP BY 1
)

SELECT
f90.region,
f90.forest_area_sqkm AS forest_area_sqkm_1990,
f90.total_area_sqkm AS total_area_sqkm_1990,
f16.forest_area_sqkm AS forest_area_sqkm_2016,
f16.total_area_sqkm AS total_area_sqkm_2016,
ROUND((f90.forest_area_sqkm / f90.total_area_sqkm)::numeric * 100, 2) AS forestation_percentage_1990,
ROUND((f16.forest_area_sqkm / f16.total_area_sqkm)::numeric * 100, 2) AS forestation_percentage_2016
FROM
forestation_1990 f90
JOIN forestation_2016 f16
ON f90.region = f16.region


select r.country_name, (sum(fa.forest_area_sqkm)/sum(la.total_area_sq_mi*2.59))*100 as prc_forest_area
from forest_area fa
join regions r
using(country_code)
join land_area la
on fa.country_code=la.country_code and la.year=fa.year
group by 1

# a. What was the percent forest of the entire world in 2016? Which region had the HIGHEST percent forest in 2016, and which had the LOWEST, to 2 decimal placesrest_area_sqkm

select region, forestation_percentage_2016
from base_region
where region = 'World'

  

# Highest and Lowest

  

select region, forestation_percentage_2016

from base_region

order by 2 desc

  
  

#b. What was the percent forest of the entire world in 1990? Which region had the HIGHEST percent forest in 1990, and which had the LOWEST, to 2 decimal places?

select region, forestation_percentage_1990

from base_region

where region = 'World'

  
  

# Highest and Lowest
select region, forestation_percentage_1990
from base_region
order by 2 desc


# c. Based on the table you created, which regions of the world DECREASED in forest area from 1990 to 2016?

select region, forestation_percentage_1990, forestation_percentage_2016
from base_region
where forestation_percentage_2016 <= forestation_percentage_1990


# 3. COUNTRY-LEVEL DETAIL

# a. Which 5 countries saw the largest amount decrease in forest area from 1990 to 2016? What was the difference in forest area for each?

  

WITH T1 AS
(SELECT country_name, Round(SUM(forest_area_sqkm)) AS Forest_Area1990
FROM forestation
WHERE YEAR = 1990
GROUP BY country_name, forest_area_sqkm
ORDER BY Forest_Area1990 DESC),
T2 AS
(SELECT country_name, Round(SUM(forest_area_sqkm)) AS Forest_Area2016
FROM forestation
WHERE YEAR = 2016
GROUP BY country_name, forest_area_sqkm
ORDER BY Forest_Area2016 DESC)
SELECT fra.country_name, fra.Forest_Area1990, tra. Forest_Area2016,
(tra.Forest_Area2016-fra.Forest_Area1990) AS Difference_Land_Area
FROM T1 AS fra
JOIN T2 AS tra
ON fra.country_name = tra.country_name
WHERE fra.country_name != 'World'
GROUP BY fra.country_name, tra.Forest_Area2016, fra.Forest_Area1990
ORDER BY Difference_Land_Area
limit 5

  
  

# b. Which 5 countries saw the largest percent decrease in forest area from 1990 to 2016? What was the percent change to 2 decimal places for each?

  

with T1 as
(select country_name, region, round((forest_area_sqkm)::numeric, 2) as percent_forest_area1990
from forestation
where year=1990
group by country_name,region, forest_area_sqkm),
T2 as
(select country_name, region, round((forest_area_sqkm)::numeric, 2) as percent_forest_area2016
from forestation
where year=2016
group by country_name,region, forest_area_sqkm)

select T1.country_name, T1.region, T1.percent_forest_area1990, T2.percent_forest_area2016, (T1.percent_forest_area1990 - T2.percent_forest_area2016) as diff_land_area, round((((T1.percent_forest_area1990 - T2.percent_forest_area2016)/T1.percent_forest_area1990)*100),2) AS
diff_Prc_land_area
from T1
join T2
on T1.country_name = T2.country_name
where T2.percent_forest_area2016 is not null
and T1.percent_forest_area1990 is not null
and T1.country_name <>'World'
group by T1.country_name, T1.region, T1.percent_forest_area1990, T2.percent_forest_area2016
order by diff_Prc_land_area desc
limit 5


# c. If countries were grouped by percent forestation in quartiles, which group had the most countries in it in 2016?

  
with table_1 as (
SELECT
f.country_code,
f.country_name,
f.year,
f.forest_area_sqkm,
l.total_area_sq_mi*2.59 total_area_sqkm,
(f.forest_area_sqkm/(l.total_area_sq_mi*2.59))*100 AS forest_percent
FROM forest_area AS f
JOIN land_area AS l
ON f.country_code = l.country_code
and( f.forest_area_sqkm is not null and l.total_area_sq_mi is not null and f.country_name <> 'World' )
and(f.year = 2016 and l.year=2016)
order BY 6 desc),
table_2 as (
select table_1.country_code,
table_1.country_name,
table_1.year,
table_1.forest_percent,
case when table_1.forest_percent >= 75 then '75-100%'
when table_1.forest_percent <75 and table_1.forest_percent >= 50 then '50-75%'
when table_1.forest_percent < 50 and table_1.forest_percent >= 25 then '25-50%'
else '0-25%'
end as percentile
from table_1
order by 5 desc)
select
table_2.percentile,
count(table_2.percentile) as total_percentile
from
table_2
group by table_2.percentile
order by total_percentile desc


  

# d. List all of the countries that were in the 4th quartile (percent forest > 75%) in 2016.


with table_1 as (
SELECT
f.country_code,
f.country_name,
f.year,
f.forest_area_sqkm,
l.total_area_sq_mi*2.59 total_area_sqkm,
(f.forest_area_sqkm/(l.total_area_sq_mi*2.59))*100 AS forest_percent
FROM forest_area AS f
JOIN land_area AS l
ON f.country_code = l.country_code
and( f.forest_area_sqkm is not null and l.total_area_sq_mi is not null and f.country_name <> 'World' )
and(f.year = 2016 and l.year=2016)
order BY 6 desc),
table_2 as (
select table_1.country_code,
table_1.country_name,
table_1.year,
table_1.forest_percent,
case when table_1.forest_percent >= 75 then '75-100%'
when table_1.forest_percent <75 and table_1.forest_percent >= 50 then '50-75%'
when table_1.forest_percent < 50 and table_1.forest_percent >= 25 then '25-50%'
else '0-25%'
end as percentile
from table_1
order by 5 desc)
select
table_2.country_name,
r.region,
round(cast(table_2.forest_percent as numeric),2) as Pct_Designated ,
table_2.percentile
from
table_2
join regions r
on table_2.country_code = r.country_code
where table_2.percentile = '75-100%'
order by Pct_Designated desc


# e. How many countries had a percent forestation higher than the United States in 2016?

With table1 AS (SELECT f.country_code,
f.country_name,
f.year,
f.forest_area_sqkm,
l.total_area_sq_mi*2.59 AS total_area_sqkm,
(f.forest_area_sqkm/(l.total_area_sq_mi*2.59))*100 AS perc_fa
FROM forest_area f
JOIN land_area l
ON f.country_code = l.country_code
AND (f.country_name != 'World' AND f.forest_area_sqkm IS NOT NULL AND l.total_area_sq_mi IS NOT NULL)
AND (f.year=2016 AND l.year = 2016)
ORDER BY 6 DESC
)
SELECT COUNT(table1.country_name)
FROM table1
WHERE table1.perc_fa > (SELECT table1.perc_fa
FROM table1
WHERE table1.country_name = 'United States'
)