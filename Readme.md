# BDT - Semestrální úloha

## Úvod

## Data

## Technologie

## Úkoly

### T1: Kolik případů je evidováno v jednotlivých kategoriích (krádež, žhářství, …)?

#### Výsledná data
<iframe height="450" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=275794259&amp;single=true&amp;widget=false&amp;headers=false&amp;range=A1:B15">
</iframe>

#### Vizualizace výsledku
<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=958727936&amp;format=interactive" >
</iframe>

#### SQL
```SQL
SELECT `Crime type`, COUNT(`Crime type`) as Count FROM crimes GROUP BY `Crime type` ORDER BY Count DESC;
```

### T2: Který útvar eviduje nejvíce případů (případně po kategoriích zločinu)?

### T7: Pokuste se pro nějaký typ zločinu zakreslit na mapu (nebo alespoň do grafu longitude vs. latitude) vyřešené a nevyřešené případy.

### SQL
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

#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/markers.html" >
</iframe>

### T9: Pro vybranou kategorii vytvořte animovanou vizualizaci na mapě, jak se vyvíjí situace přes rok.

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

#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/areas.html" >
</iframe>