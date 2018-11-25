# BDT - Semestrální úloha

## Obsah
* [Úvod](#úvod)
* [Data](#data)
* [Technologie](#technologie)
* [Úkoly](#úkoly)
  * [Task 1](#task-1)
  * [Task 2](#task-2)
  * [Task 3](#task-3)
  * [Task 4](#task-4)
  * [Task 5](#task-5)
  * [Task 6](#task-6)
  * [Task 7](#task-7)
  * [Task 8](#task-8)
  * [Task 9](#task-9)
  * [Task 10](#task-10)
  * [Task 11](#task-11)
* [Závěr](#závěr)

## Úvod

## Data

## Technologie

Dočasné tabulky: https://vajjicko.github.io/BDT_semestralni_uloha/docs/temporary_tables.html
Finální tabulky: https://vajjicko.github.io/BDT_semestralni_uloha/docs/final_tables.html

## Úkoly

### TASK 1
#### Zadání
Kolik případů je evidováno v jednotlivých kategoriích (krádež, žhářství, …)?

#### Informace

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=275794259&amp;single=true&amp;widget=false&amp;headers=false&amp;range=A1:B15"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=958727936&amp;format=interactive" ></iframe>

#### SQL
```SQL
SELECT `Crime type`, COUNT(`Crime type`) as Count FROM crimes GROUP BY `Crime type` ORDER BY Count DESC;
```

### TASK 2
#### Zadání
Který útvar eviduje nejvíce případů (případně po kategoriích zločinu)?

#### Informace

### TASK 3
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 4
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 5
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 6
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 7
#### Zadání
Pokuste se pro nějaký typ zločinu zakreslit na mapu (nebo alespoň do grafu longitude vs. latitude) vyřešené a nevyřešené případy.

#### Informace
#### Výsledná data
#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/markers.html" ></iframe>

#### SQL
```SQL
WITH outcomesunique as
(
  SELECT * FROM (
    SELECT *, ROW_NUMBER() OVER (
      PARTITION BY outcomes.`Crime ID` ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`,'yyyy-MM'))) DESC
    ) AS ROW_NUM FROM outcomes
  ) AS res WHERE res.ROW_NUM = 1
),
allinfo as
(
  SELECT 
    crimes.`Latitude` AS lat,
    crimes.`Longitude` AS lng,
    CASE
      WHEN outcomesunique.`Outcome type` IS NULL THEN 0
      ELSE 1
    END
    AS resolved
    FROM crimes
    LEFT JOIN outcomesunique ON
      (crimes.`Crime ID` = outcomesunique.`Crime ID`)
    WHERE crimes.`Crime type` = 'Possession of weapons'
      AND crimes.`Month` = '2017-10'
      AND crimes.`Longitude` IS NOT NULL
      AND crimes.`Longitude` != 0
      AND crimes.`Latitude` IS NOT NULL
      AND crimes.`Latitude` != 0
)
INSERT OVERWRITE DIRECTORY '/user/vojgin/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT lat, lng, resolved
FROM allinfo;
```

### TASK 8
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 9
#### Zadání
Pro vybranou kategorii vytvořte animovanou vizualizaci na mapě, jak se vyvíjí situace přes rok.
#### Informace
#### Výsledná data
#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/areas.html" ></iframe>

### SQL
```SQL
INSERT OVERWRITE DIRECTORY '/user/vojgin/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT crimes.`Month`, COUNT(crimes.`Crime ID`) AS count, region.`RGN11NM` AS `Region name`, region.`RGN11CD` AS `Region code`
FROM crimes
LEFT JOIN region ON (crimes.`LSOA code` = region.`LSOA11CD`)
WHERE crimes.`LSOA code` IS NOT NULL
AND region.`RGN11NM` IS NOT NULL
AND crimes.`Month` >= '2017-01'
AND crimes.`Month` <= '2017-12'
GROUP BY crimes.`Month`, region.`RGN11CD`, region.`RGN11NM`
ORDER BY crimes.`Month` ASC, count DESC;
```

### TASK 10
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 11
#### Zadání
#### Informace
#### Výsledná data
#### Vizualizace výsledku
#### SQL

## Závěr
