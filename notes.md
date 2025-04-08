# 🎯 FINAL MISSION REPORT
**Case**: Capture of Carmen Sandiego  
**Mission**: Follow SQL clues across global databases  
**Agent**: YOU – World-class data detective 🧠  
**Status**: ✅ Mission Accomplished

---

## ✅ Clue #1: Least populated country in Southern Europe
```sql
SELECT name
FROM countries
WHERE region = 'Southern Europe'
ORDER BY population ASC
LIMIT 1;
```
**Result**: Holy See (Vatican City State)

---

## ✅ Clue #2: Official language spoken in the Holy See
```sql
SELECT language
FROM countrylanguages
WHERE countrycode = (
  SELECT code
  FROM countries
  WHERE name = 'Holy See (Vatican City State)'
)
AND isofficial = true;
```
**Result**: Italian

---

## ✅ Clue #3: Country that speaks only Italian
```sql
SELECT cl.countrycode, c.name
FROM countrylanguages cl
JOIN countries c ON cl.countrycode = c.code
WHERE cl.language = 'Italian'
  AND cl.percentage = 100;
```
**Result**: San Marino

---

## ✅ Clue #4: Other city in San Marino (besides "San Marino")
```sql
SELECT name 
FROM cities 
WHERE countrycode = 'SMR'
AND name <> 'San Marino';
```
**Result**: Serravalle

---

## ✅ Clue #5: Similar city name in South America
```sql
SELECT name, countrycode
FROM cities
WHERE name LIKE 'Serr%'
AND countrycode IN (
  SELECT code FROM countries WHERE continent = 'South America'
)
AND name <> 'Serravalle';
```
**Result**: Serrana in Brazil (BRA)

---

## ✅ Clue #6: Capital of Brazil
```sql
SELECT name
FROM cities
WHERE id = (
  SELECT capital
  FROM countries
  WHERE name = 'Brazil'
);
```
**Result**: Brasília

---

## ✅ Clue #7: City with population of 91,084
```sql
SELECT name, countrycode, population
FROM cities
WHERE population = 91084;
```
**Result**: Santa Monica, USA

---

## 🏆 Mission Summary

You chased Carmen Sandiego:
- From Vatican City 🏛️
- To San Marino 🇸🇲
- To Brazil 🇧🇷
- And finally Santa Monica, USA 🇺🇸

Your SQL skills:
- Used SELECT, JOIN, WHERE, SUBQUERIES, and PATTERN MATCHING
- Tracked foreign keys, regions, languages, and cities across multiple tables

---

**Well done, gumshoe. Carmen is behind bars thanks to you. 🕵️‍♀️📁**
