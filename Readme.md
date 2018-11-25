# BDT - Semestrální úloha

# Autoři
## Petr Bílek
<bilekpe5@fel.cvut.cz>

[LinkedIn](https://www.linkedin.com/in/petr-b%C3%ADlek-57295346/)

![Petr Bílek - foto](./assets/profile_pictures/bilekpe5.jpg "Petr Bílek - foto")

* absolvent bakalářského studia ČVUT FEL, program Softwarové technologie a management, obor Web a multimédia
* student magisterského programu na ČVUT FEL, program Otevřená informatika, obor HCI (Human-Computer Interaction)
* zkušenosti s UAT testováním aplikací v bankovním sektoru
* zkušenosti se softwarovou analýzou
* zkušenosti s vývojem a údržbou automatizovaného frameworku pro kontrolu datové kvality v bankovním prostředí
* zkušenosti s návrhem DB (Oracle)
* pracovní pozice:
  * software tester
  * BI Developer (junior pozice)
  * specialista procesního rozvoje

## Vojtěch Gintner
<gintnvoj@fel.cvut.cz>

[Portfolio](https://vojgin.com)

[LinkedIn](https://www.linkedin.com/in/vojgin/)

![Vojtěch Gintner - foto](./assets/profile_pictures/gintnvoj.jpeg "Vojtěch Gintner - foto")

* více jak 7 let zkušeností s návrhem a vývojem webových i mobilních aplikací
* absolvent bakalářského studia na ČVUT v oboru Web a Multimedia.
* studentem ČVUT v magisterském oboru návrhu a testování uživatelských prostředí
* rozsáhlé zkušenosti s webovými technologiemi, zejména pak JavaScript
* pracovní zkušenosti zahrnují práci ve startupech a středně velkých firmách zahraničních i tuzemských
* pracovní pozice:
  * FrontEnd Coder
  * FrontEnd Developer
  * JavaScript Developer
  * UI Designer
  * UX Designer
* akademická práce na výzkumu v oblasti User Experience zrakově postižených uživatelů, vývoj outdoorové navigační aplikace pro zrakově postižené
* několik veřejných tuzemských i zahraničních přednášek na téma User Experience a User research

## Václav Pavlovec
<pavlova1@fel.cvut.cz>

![Václav Pavlovec - foto](./assets/profile_pictures/pavlova1.jpg "Václav Pavlovec - foto")

* absolvent bakalářského studia ČVUT FEL (summa cum laude), program Softwarové technologie a management, obor Web a multimédia
* student magisterského programu ČVUT FEL, program Otevřená informatika, obor HCI (Human-Computer Interaction)
* zkušenost s návrhem a prací s DB (Oracle)
* zkušenosti s finančním risk managementem

## Obsah
* [Úvod](#úvod)
* [Data](#data)
* [Technologie](#technologie)
  * [Dočasné tabulky](#dočasné-tabulky)
  * [Finální tabulky](#dočasné-tabulky)
  * [Dotazování a výsledky dotazů](#dotazování-a-výsledky-dotazů)
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
Cílem této práce je zpracovat data o kriminalitě ze Spojeného královstí a vypracovat 11 úkolů. Ke zpracování jsme využili technologie Hive, nám přistupné na MetaCentrum: hador.ics.muni.cz. K dotazování jsme využili jazyka SQL. Vizualizace byla provedena pomocí Google Docs, Google Maps API a amCharts.

## Data
V rámci semestrální práce byla analyzována volně dostupná data o zločinnosti a and policii v Anglii, Walesu a Severním Irsku v období od října 2015 do září 2018 včetně.

Dále byla analyzována spojitost mezi mírou kriminality a preferencemi v referendu o Brexitu.

### Policejní data
Policejní data obsahují informaci o zločinech (crimes), výsledcích vyšetřování (outcomes) a prohlídkách (stop and search).

Odkaz na data: [Data](https://data.police.uk/data/)

### Data o Brexitu
Data obsahují informace o výsledcích referenda o Brexitu na úrovni *Area*.

Odkaz na data: [Data](https://www.electoralcommission.org.uk/__data/assets/file/0014/212135/EU-referendum-result-data.csv)

### Data o populaci
Pro vypracování některých úkolů bylo potřeba použít data o populaci.

Odkaz na data: [Data](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/populationestimatesforukenglandandwalesscotlandandnorthernireland) (záložka MID-2017)

### Číselníky oblastí
Pro vypracování některých úkolů bylo potřeba použít převodních číselníků mezi různým územním uspořádáním. 

**LSOA to Ward**: [Data](http://geoportal.statistics.gov.uk/datasets/lower-layer-super-output-area-2011-to-ward-2016-lookup-in-england-and-wales)

**Ward to county**: [Data](http://geoportal.statistics.gov.uk/datasets/ward-to-local-authority-district-to-county-to-region-to-country-december-2016-lookup-in-united-kingdom-v2)

## Technologie
V rámci semestrální práce byl využíván Hadoop poskytnutý pro předmět BDT (Hadoop od MetaCentrum) s Apache Hive.

### Dočasné tabulky
Tabulky byly vytvářeny v databázi **bilekpe5**.

##### region_tmp

```SQL
CREATE EXTERNAL TABLE region_tmp (
  `LSOA11CD`  varchar(128),
  `LSOA11NM`  varchar(128),
  `BUASD11CD` varchar(128),
  `BUASD11NM` varchar(128),
  `BUA11CD`   varchar(128),
  `BUA11NM`   varchar(128),
  `LAD11CD`   varchar(128),
  `LAD11NM`   varchar(128),
  `LAD11NMW`  varchar(128),
  `RGN11CD`   varchar(128),
  `RGN11NM`   varchar(128),
  `RGN11NMW`  varchar(128),
  `ObjectId`  int)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/region"
  tblproperties ("skip.header.line.count"="1");
```

##### ward_tmp

```SQL
CREATE EXTERNAL TABLE ward_tmp (
  `LSOA11CD`  varchar(128),
  `LSOA11NM`  varchar(128),
  `WD16CD`    varchar(128),
  `WD16NM`    varchar(128),
  `LAD16CD`   varchar(128),
  `LAD16NM`   varchar(128),
  `FID`       int)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/ward"
  tblproperties ("skip.header.line.count"="1");
```

##### county_tmp

```SQL
CREATE EXTERNAL TABLE county_tmp (
  `WD16CD`    varchar(128),
  `WD16NM`    varchar(128),
  `LAD16CD`   varchar(128),
  `LAD16NM`   varchar(128),
  `CTY16CD`   varchar(128),
  `CTY16NM`   varchar(128),
  `GOR10CD`   varchar(128),
  `GOR10NM`   varchar(128),
  `CTRY16CD`  varchar(128),
  `CTRY16NM`  varchar(128),
  `FID`       int)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/county"
  tblproperties ("skip.header.line.count"="1");
```

#### Datové tabulky

##### population_tmp

```SQL
CREATE EXTERNAL TABLE population_tmp (
  `Code`        varchar(128),
  `Population`  int)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/population"
  tblproperties ("skip.header.line.count"="1");
```

##### brexit_tmp

```SQL
CREATE EXTERNAL TABLE brexit_tmp (
  `id`                      int,
  `Region_Code`             varchar(64),
  `Region`                  varchar(64),
  `Area_Code`               varchar(64),
  `Area`                    varchar(64),
  `Electorate`              int,
  `ExpectedBallots`         int,
  `VerifiedBallotPapers`    int,
  `Pct_Turnout`             float,
  `Votes_Cast`              int,
  `Valid_Votes`             int,
  `Remain`                  int,
  `Leave`                   int,
  `Rejected_Ballots`        int,
  `No_official_mark`        int,
  `Voting_for_both_answers` int,
  `Writing_or_mark`         int,
  `Unmarked_or_void`        int,
  `Pct_Remain`              float,
  `Pct_Leave`               float,
  `Pct_Rejected`            float)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/brexit"
  tblproperties ("skip.header.line.count"="1");
```

##### crimes_tmp

```SQL
CREATE EXTERNAL TABLE crimes_tmp (
  `Crime ID`              varchar(256),
  `Month`                 varchar(256),
  `Reported by`           varchar(256),
  `Falls within`          varchar(256),
  `Longitude`             float,
  `Latitude`              float,
  `Location`              varchar(256),
  `LSOA code`             varchar(256),
  `LSOA name`             varchar(256),
  `Crime type`            varchar(256),
  `Last outcome category` varchar(256),
  `Context`               varchar(256))
partitioned by (dateval string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/crimes"
  tblproperties ("skip.header.line.count"="1");
```

```SQL
alter table crimes_tmp add partition (dateval = '2015-10')
location '/user/bilekpe5/dataPolice/crimes/2015-10'; 
alter table crimes_tmp add partition (dateval = '2015-11')
location '/user/bilekpe5/dataPolice/crimes/2015-11'; 
alter table crimes_tmp add partition (dateval = '2015-12')
location '/user/bilekpe5/dataPolice/crimes/2015-12'; 
alter table crimes_tmp add partition (dateval = '2016-01')
location '/user/bilekpe5/dataPolice/crimes/2016-01'; 
alter table crimes_tmp add partition (dateval = '2016-02')
location '/user/bilekpe5/dataPolice/crimes/2016-02'; 
alter table crimes_tmp add partition (dateval = '2016-03')
location '/user/bilekpe5/dataPolice/crimes/2016-03'; 
alter table crimes_tmp add partition (dateval = '2016-04')
location '/user/bilekpe5/dataPolice/crimes/2016-04'; 
alter table crimes_tmp add partition (dateval = '2016-05')
location '/user/bilekpe5/dataPolice/crimes/2016-05'; 
alter table crimes_tmp add partition (dateval = '2016-06')
location '/user/bilekpe5/dataPolice/crimes/2016-06'; 
alter table crimes_tmp add partition (dateval = '2016-07')
location '/user/bilekpe5/dataPolice/crimes/2016-07'; 
alter table crimes_tmp add partition (dateval = '2016-08')
location '/user/bilekpe5/dataPolice/crimes/2016-08'; 
alter table crimes_tmp add partition (dateval = '2016-09')
location '/user/bilekpe5/dataPolice/crimes/2016-09'; 
alter table crimes_tmp add partition (dateval = '2016-10')
location '/user/bilekpe5/dataPolice/crimes/2016-10'; 
alter table crimes_tmp add partition (dateval = '2016-11')
location '/user/bilekpe5/dataPolice/crimes/2016-11'; 
alter table crimes_tmp add partition (dateval = '2016-12')
location '/user/bilekpe5/dataPolice/crimes/2016-12'; 
alter table crimes_tmp add partition (dateval = '2017-01')
location '/user/bilekpe5/dataPolice/crimes/2017-01'; 
alter table crimes_tmp add partition (dateval = '2017-02')
location '/user/bilekpe5/dataPolice/crimes/2017-02'; 
alter table crimes_tmp add partition (dateval = '2017-03')
location '/user/bilekpe5/dataPolice/crimes/2017-03'; 
alter table crimes_tmp add partition (dateval = '2017-04')
location '/user/bilekpe5/dataPolice/crimes/2017-04'; 
alter table crimes_tmp add partition (dateval = '2017-05')
location '/user/bilekpe5/dataPolice/crimes/2017-05'; 
alter table crimes_tmp add partition (dateval = '2017-06')
location '/user/bilekpe5/dataPolice/crimes/2017-06'; 
alter table crimes_tmp add partition (dateval = '2017-07')
location '/user/bilekpe5/dataPolice/crimes/2017-07'; 
alter table crimes_tmp add partition (dateval = '2017-08')
location '/user/bilekpe5/dataPolice/crimes/2017-08'; 
alter table crimes_tmp add partition (dateval = '2017-09')
location '/user/bilekpe5/dataPolice/crimes/2017-09'; 
alter table crimes_tmp add partition (dateval = '2017-10')
location '/user/bilekpe5/dataPolice/crimes/2017-10'; 
alter table crimes_tmp add partition (dateval = '2017-11')
location '/user/bilekpe5/dataPolice/crimes/2017-11'; 
alter table crimes_tmp add partition (dateval = '2017-12')
location '/user/bilekpe5/dataPolice/crimes/2017-12'; 
alter table crimes_tmp add partition (dateval = '2018-01')
location '/user/bilekpe5/dataPolice/crimes/2018-01'; 
alter table crimes_tmp add partition (dateval = '2018-02')
location '/user/bilekpe5/dataPolice/crimes/2018-02'; 
alter table crimes_tmp add partition (dateval = '2018-03')
location '/user/bilekpe5/dataPolice/crimes/2018-03'; 
alter table crimes_tmp add partition (dateval = '2018-04')
location '/user/bilekpe5/dataPolice/crimes/2018-04'; 
alter table crimes_tmp add partition (dateval = '2018-05')
location '/user/bilekpe5/dataPolice/crimes/2018-05'; 
alter table crimes_tmp add partition (dateval = '2018-06')
location '/user/bilekpe5/dataPolice/crimes/2018-06'; 
alter table crimes_tmp add partition (dateval = '2018-07')
location '/user/bilekpe5/dataPolice/crimes/2018-07'; 
alter table crimes_tmp add partition (dateval = '2018-08')
location '/user/bilekpe5/dataPolice/crimes/2018-08'; 
alter table crimes_tmp add partition (dateval = '2018-09')
location '/user/bilekpe5/dataPolice/crimes/2018-09';
```

##### outcomes_tmp

```SQL
CREATE EXTERNAL TABLE outcomes_tmp (
  `Crime ID`      varchar(256),
  `Month`         varchar(256),
  `Reported by`   varchar(256),
  `Falls within`  varchar(256),
  `Longitude`     float,
  `Latitude`      float,
  `Location`      varchar(256),
  `LSOA code`     varchar(256),
  `LSOA name`     varchar(256),
  `Outcome type`  varchar(256))
partitioned by (dateval string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/outcomes"
  tblproperties ("skip.header.line.count"="1");
```

```SQL
alter table outcomes_tmp add partition (dateval = '2015-10')
location '/user/bilekpe5/dataPolice/outcomes/2015-10'; 
alter table outcomes_tmp add partition (dateval = '2015-11')
location '/user/bilekpe5/dataPolice/outcomes/2015-11'; 
alter table outcomes_tmp add partition (dateval = '2015-12')
location '/user/bilekpe5/dataPolice/outcomes/2015-12'; 
alter table outcomes_tmp add partition (dateval = '2016-01')
location '/user/bilekpe5/dataPolice/outcomes/2016-01'; 
alter table outcomes_tmp add partition (dateval = '2016-02')
location '/user/bilekpe5/dataPolice/outcomes/2016-02'; 
alter table outcomes_tmp add partition (dateval = '2016-03')
location '/user/bilekpe5/dataPolice/outcomes/2016-03'; 
alter table outcomes_tmp add partition (dateval = '2016-04')
location '/user/bilekpe5/dataPolice/outcomes/2016-04'; 
alter table outcomes_tmp add partition (dateval = '2016-05')
location '/user/bilekpe5/dataPolice/outcomes/2016-05'; 
alter table outcomes_tmp add partition (dateval = '2016-06')
location '/user/bilekpe5/dataPolice/outcomes/2016-06'; 
alter table outcomes_tmp add partition (dateval = '2016-07')
location '/user/bilekpe5/dataPolice/outcomes/2016-07'; 
alter table outcomes_tmp add partition (dateval = '2016-08')
location '/user/bilekpe5/dataPolice/outcomes/2016-08'; 
alter table outcomes_tmp add partition (dateval = '2016-09')
location '/user/bilekpe5/dataPolice/outcomes/2016-09'; 
alter table outcomes_tmp add partition (dateval = '2016-10')
location '/user/bilekpe5/dataPolice/outcomes/2016-10'; 
alter table outcomes_tmp add partition (dateval = '2016-11')
location '/user/bilekpe5/dataPolice/outcomes/2016-11'; 
alter table outcomes_tmp add partition (dateval = '2016-12')
location '/user/bilekpe5/dataPolice/outcomes/2016-12'; 
alter table outcomes_tmp add partition (dateval = '2017-01')
location '/user/bilekpe5/dataPolice/outcomes/2017-01'; 
alter table outcomes_tmp add partition (dateval = '2017-02')
location '/user/bilekpe5/dataPolice/outcomes/2017-02'; 
alter table outcomes_tmp add partition (dateval = '2017-03')
location '/user/bilekpe5/dataPolice/outcomes/2017-03'; 
alter table outcomes_tmp add partition (dateval = '2017-04')
location '/user/bilekpe5/dataPolice/outcomes/2017-04'; 
alter table outcomes_tmp add partition (dateval = '2017-05')
location '/user/bilekpe5/dataPolice/outcomes/2017-05'; 
alter table outcomes_tmp add partition (dateval = '2017-06')
location '/user/bilekpe5/dataPolice/outcomes/2017-06'; 
alter table outcomes_tmp add partition (dateval = '2017-07')
location '/user/bilekpe5/dataPolice/outcomes/2017-07'; 
alter table outcomes_tmp add partition (dateval = '2017-08')
location '/user/bilekpe5/dataPolice/outcomes/2017-08'; 
alter table outcomes_tmp add partition (dateval = '2017-09')
location '/user/bilekpe5/dataPolice/outcomes/2017-09'; 
alter table outcomes_tmp add partition (dateval = '2017-10')
location '/user/bilekpe5/dataPolice/outcomes/2017-10'; 
alter table outcomes_tmp add partition (dateval = '2017-11')
location '/user/bilekpe5/dataPolice/outcomes/2017-11'; 
alter table outcomes_tmp add partition (dateval = '2017-12')
location '/user/bilekpe5/dataPolice/outcomes/2017-12'; 
alter table outcomes_tmp add partition (dateval = '2018-01')
location '/user/bilekpe5/dataPolice/outcomes/2018-01'; 
alter table outcomes_tmp add partition (dateval = '2018-02')
location '/user/bilekpe5/dataPolice/outcomes/2018-02'; 
alter table outcomes_tmp add partition (dateval = '2018-03')
location '/user/bilekpe5/dataPolice/outcomes/2018-03'; 
alter table outcomes_tmp add partition (dateval = '2018-04')
location '/user/bilekpe5/dataPolice/outcomes/2018-04'; 
alter table outcomes_tmp add partition (dateval = '2018-05')
location '/user/bilekpe5/dataPolice/outcomes/2018-05'; 
alter table outcomes_tmp add partition (dateval = '2018-06')
location '/user/bilekpe5/dataPolice/outcomes/2018-06'; 
alter table outcomes_tmp add partition (dateval = '2018-07')
location '/user/bilekpe5/dataPolice/outcomes/2018-07'; 
alter table outcomes_tmp add partition (dateval = '2018-08')
location '/user/bilekpe5/dataPolice/outcomes/2018-08'; 
alter table outcomes_tmp add partition (dateval = '2018-09')
location '/user/bilekpe5/dataPolice/outcomes/2018-09'; 
```

##### stopandsearch_tmp

```SQL
CREATE EXTERNAL TABLE stopandsearch_tmp (
  `Type`                                      varchar(64),
  `Date`                                      varchar(128),
  `Part of a policing operation`              varchar(16),
  `Policing`                                  varchar(256),
  `Latitude`                                  float,
  `Longitude`                                 float,
  `Gender`                                    varchar(32),
  `Age range`                                 varchar(64),
  `Self-defined ethnicity`                    varchar(256),
  `Officer-defined ethnicity`                 varchar(128),
  `Legislation`                               varchar(256),
  `Object of search`                          varchar(128),
  `Outcome`                                   varchar(256),
  `Outcome linked to object of search`        varchar(16),
  `Removal of more than just outer clothing`  varchar(16))
partitioned by (dateval string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
   "separatorChar" = ",",
   "quoteChar"     = "\"")
  LOCATION "/user/bilekpe5/dataPolice/stopandsearch"
  tblproperties ("skip.header.line.count"="1");
```

```SQL
alter table stopandsearch_tmp add partition (dateval = '2015-10')
location '/user/bilekpe5/dataPolice/stopandsearch/2015-10'; 
alter table stopandsearch_tmp add partition (dateval = '2015-11')
location '/user/bilekpe5/dataPolice/stopandsearch/2015-11'; 
alter table stopandsearch_tmp add partition (dateval = '2015-12')
location '/user/bilekpe5/dataPolice/stopandsearch/2015-12'; 
alter table stopandsearch_tmp add partition (dateval = '2016-01')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-01'; 
alter table stopandsearch_tmp add partition (dateval = '2016-02')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-02'; 
alter table stopandsearch_tmp add partition (dateval = '2016-03')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-03'; 
alter table stopandsearch_tmp add partition (dateval = '2016-04')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-04'; 
alter table stopandsearch_tmp add partition (dateval = '2016-05')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-05'; 
alter table stopandsearch_tmp add partition (dateval = '2016-06')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-06'; 
alter table stopandsearch_tmp add partition (dateval = '2016-07')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-07'; 
alter table stopandsearch_tmp add partition (dateval = '2016-08')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-08'; 
alter table stopandsearch_tmp add partition (dateval = '2016-09')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-09'; 
alter table stopandsearch_tmp add partition (dateval = '2016-10')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-10'; 
alter table stopandsearch_tmp add partition (dateval = '2016-11')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-11'; 
alter table stopandsearch_tmp add partition (dateval = '2016-12')
location '/user/bilekpe5/dataPolice/stopandsearch/2016-12'; 
alter table stopandsearch_tmp add partition (dateval = '2017-01')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-01'; 
alter table stopandsearch_tmp add partition (dateval = '2017-02')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-02'; 
alter table stopandsearch_tmp add partition (dateval = '2017-03')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-03'; 
alter table stopandsearch_tmp add partition (dateval = '2017-04')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-04'; 
alter table stopandsearch_tmp add partition (dateval = '2017-05')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-05'; 
alter table stopandsearch_tmp add partition (dateval = '2017-06')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-06'; 
alter table stopandsearch_tmp add partition (dateval = '2017-07')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-07'; 
alter table stopandsearch_tmp add partition (dateval = '2017-08')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-08'; 
alter table stopandsearch_tmp add partition (dateval = '2017-09')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-09'; 
alter table stopandsearch_tmp add partition (dateval = '2017-10')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-10'; 
alter table stopandsearch_tmp add partition (dateval = '2017-11')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-11'; 
alter table stopandsearch_tmp add partition (dateval = '2017-12')
location '/user/bilekpe5/dataPolice/stopandsearch/2017-12'; 
alter table stopandsearch_tmp add partition (dateval = '2018-01')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-01'; 
alter table stopandsearch_tmp add partition (dateval = '2018-02')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-02'; 
alter table stopandsearch_tmp add partition (dateval = '2018-03')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-03'; 
alter table stopandsearch_tmp add partition (dateval = '2018-04')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-04'; 
alter table stopandsearch_tmp add partition (dateval = '2018-05')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-05'; 
alter table stopandsearch_tmp add partition (dateval = '2018-06')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-06'; 
alter table stopandsearch_tmp add partition (dateval = '2018-07')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-07'; 
alter table stopandsearch_tmp add partition (dateval = '2018-08')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-08'; 
alter table stopandsearch_tmp add partition (dateval = '2018-09')
location '/user/bilekpe5/dataPolice/stopandsearch/2018-09';
```

### Finální tabulky
Tabulky byly vytvářeny v databázi **bilekpe5**.

Před importem dat do finálních tabulek z tabulek dočasných bylo potřeba zapnout dynamický mód partition bez restrikcí:
```SQL
set hive.exec.dynamic.partition.mode=nonstrict;
```

##### region

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS region(
  `LSOA11CD`  varchar(128),
  `LSOA11NM`  varchar(128),
  `BUASD11CD` varchar(128),
  `BUASD11NM` varchar(128),
  `BUA11CD`   varchar(128),
  `BUA11NM`   varchar(128),
  `LAD11CD`   varchar(128),
  `LAD11NM`   varchar(128),
  `LAD11NMW`  varchar(128),
  `RGN11CD`   varchar(128),
  `RGN11NM`   varchar(128),
  `RGN11NMW`  varchar(128),
  `ObjectId`  int)
STORED AS ORC
tblproperties('orc.compress'='SNAPPY');

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE region
SELECT * FROM region_tmp;
```

##### ward

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS ward (
  `LSOA11CD`  varchar(128),
  `LSOA11NM`  varchar(128),
  `WD16CD`    varchar(128),
  `WD16NM`    varchar(128),
  `LAD16CD`   varchar(128),
  `LAD16NM`   varchar(128),
  `FID`       int)
STORED AS ORC
tblproperties('orc.compress'='SNAPPY');

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE ward
SELECT * FROM ward_tmp;
```

##### county

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS county (
  `WD16CD`    varchar(128),
  `WD16NM`    varchar(128),
  `LAD16CD`   varchar(128),
  `LAD16NM`   varchar(128),
  `CTY16CD`   varchar(128),
  `CTY16NM`   varchar(128),
  `GOR10CD`   varchar(128),
  `GOR10NM`   varchar(128),
  `CTRY16CD`  varchar(128),
  `CTRY16NM`  varchar(128),
  `FID`       int)
STORED AS ORC
tblproperties('orc.compress'='SNAPPY');

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE county
SELECT * FROM county_tmp;
```

#### Datové tabulky

##### population

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS population (
  `Code`        varchar(128),
  `Population`  int)
STORED AS ORC
tblproperties('orc.compress'='SNAPPY');

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE population
SELECT * FROM population_tmp;
```

##### brexit

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS brexit (
  `id`                      int,
  `Region_Code`             varchar(64),
  `Region`                  varchar(64),
  `Area_Code`               varchar(64),
  `Area`                    varchar(64),
  `Electorate`              int,
  `ExpectedBallots`         int,
  `VerifiedBallotPapers`    int,
  `Pct_Turnout`             float,
  `Votes_Cast`              int,
  `Valid_Votes`             int,
  `Remain`                  int,
  `Leave`                   int,
  `Rejected_Ballots`        int,
  `No_official_mark`        int,
  `Voting_for_both_answers` int,
  `Writing_or_mark`         int,
  `Unmarked_or_void`        int,
  `Pct_Remain`              float,
  `Pct_Leave`               float,
  `Pct_Rejected`            float)
STORED AS ORC
tblproperties('orc.compress'='SNAPPY');

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE brexit
SELECT * FROM brexit_tmp;
```

##### crimes

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS crimes (
  `Crime ID`              varchar(256),
  `Month`                 varchar(256),
  `Reported by`           varchar(256),
  `Falls within`          varchar(256),
  `Longitude`             float,
  `Latitude`              float,
  `Location`              varchar(256),
  `LSOA code`             varchar(256),
  `LSOA name`             varchar(256),
  `Crime type`            varchar(256),
  `Last outcome category` varchar(256),
  `Context`               varchar(256))
PARTITIONED BY (dt string)
STORED AS ORC tblproperties
("orc.compress"="SNAPPY");

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE crimes
PARTITION (dt)
SELECT * FROM crimes_tmp;
```

##### outcomes

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS outcomes (
  `Crime ID`      varchar(256),
  `Month`         varchar(256),
  `Reported by`   varchar(256),
  `Falls within`  varchar(256),
  `Longitude`     float,
  `Latitude`      float,
  `Location`      varchar(256),
  `LSOA code`     varchar(256),
  `LSOA name`     varchar(256),
  `Outcome type`  varchar(256))
PARTITIONED BY (dt string)
STORED AS ORC tblproperties
("orc.compress"="SNAPPY");

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE outcomes
PARTITION (dt)
SELECT * FROM outcomes_tmp;
```

##### stopandsearch

```SQL
--Vytvoreni tabulky
CREATE TABLE IF NOT EXISTS stopandsearch (
  `Type`                                      varchar(64),
  `Date`                                      varchar(128),
  `Part of a policing operation`              varchar(16),
  `Policing`                                  varchar(256),
  `Latitude`                                  float,
  `Longitude`                                 float,
  `Gender`                                    varchar(32),
  `Age range`                                 varchar(64),
  `Self-defined ethnicity`                    varchar(256),
  `Officer-defined ethnicity`                 varchar(128),
  `Legislation`                               varchar(256),
  `Object of search`                          varchar(128),
  `Outcome`                                   varchar(256),
  `Outcome linked to object of search`        varchar(16),
  `Removal of more than just outer clothing`  varchar(16))
PARTITIONED BY (dt string)
STORED AS ORC tblproperties
("orc.compress"="SNAPPY");

--Vlozeni dat z docasne tabulky
INSERT OVERWRITE TABLE stopandsearch
PARTITION (dt)
SELECT * FROM stopandsearch_tmp;
```

#### Smazání dočasných tabulek

```SQL
DROP TABLE region_tmp;
DROP TABLE ward_tmp;
DROP TABLE county_tmp;
DROP TABLE population_tmp;
DROP TABLE crimes_tmp;
DROP TABLE outcomes_tmp;
DROP TABLE stopandsearch_tmp;
```

### Dotazování a výsledky dotazů
Tabulky byly vytvářeny v databázi **bilekpe5**.

Pro přístup k jedné databázi pro všechny uživatele byla potřeba změna práv u uživatelského adresáře.

```
hdfs dfs -chmod 755 /user/bilekpe5/
```

Pro dotazování byl použit jazyk **HiveQL**.

Výsledky dotazů byly ukládány do souborů, ze kterých bylo následně sestaveno vždy výsledné CSV pro daný dotaz.

Do všech dotazů byl přidán následující kus kódu, který zajistil generování výsledků do souborů.
```SQL
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',' --pripadne u TASK 11: FIELDS TERMINATED BY '\;'
```

## Úkoly

### TASK 1
#### Zadání
Kolik případů je evidováno v jednotlivých kategoriích (krádež, žhářství, …)?

#### Komentář
Dotaz vede k získání počtu případů v jednotlivých kategoriích.

#### Závěr
Z výsledků vyplývá, že kategorie antisociální chování (*Anti-social behaviour*) a násilí a sexuální delikty (*Violence or sexual offences*) tvoří cca. 50% případů.

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=275794259&amp;single=true&amp;widget=false&amp;headers=false&amp;range=A1:B15"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=958727936&amp;format=interactive" ></iframe>

#### SQL
```SQL
SELECT `Crime type`,
       COUNT(`Crime type`) AS COUNT
FROM crimes
GROUP BY `Crime type`
ORDER BY COUNT DESC;
```

### TASK 2
#### Zadání
Který útvar eviduje nejvíce případů (případně po kategoriích zločinu)?

#### Komentář
Dotazy vedou k získání útvarů, které evidují nejvíce případů. První dotaz nalezne útvar, který eviduje nejvíce připadů celkově, druhý poté nalezne takový útvar pro každou kategorii zločinu.

#### Závěr
Z výsledků vyplývá, že nejvíce případů zaznamenalo oddělení **Metropolitan Police Service**.

Z výsledků druhého dotazu získáváme data podle jednotlivých kategorií.

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1305914394&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B11"></iframe>

<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=879348330&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:C15"></iframe>

#### SQL
```SQL
SELECT *
FROM
  (SELECT `Reported by`,
          COUNT(`Reported by`) AS COUNT
   FROM crimes
   WHERE `Reported by` IS NOT NULL
     AND `Reported by` != ''
   GROUP BY `Reported by`) AS res
ORDER BY res.count DESC
LIMIT 1;
```

```SQL
WITH allinfo AS
  (SELECT `Crime type`,
          `Reported by`,
          COUNT(*) AS COUNT
   FROM crimes
   GROUP BY `Crime type`,
            `Reported by`)
SELECT res.`Crime type`,
       res.`Reported by`,
       res.Count
FROM
  (SELECT `Crime type`,
          `Reported by`,
          COUNT,
          ROW_NUMBER() OVER (PARTITION BY `Crime type`
                             ORDER BY `Crime type` DESC) AS ROW_NUM
   FROM allinfo) AS res
WHERE res.ROW_NUM = 1
ORDER BY res.`Crime type`;
```

### TASK 3
#### Zadání
Jak se vyvíjejí časově počty evidovaných případů?

#### Komentář
Dotaz vede k získání celkového počtu případů za jednotlivé měsíce.

#### Závěr
Měsíční počet případů kolísá mezi 441 241 (únor 2016) a 619 001 (červenec 2017).

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=531591978&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B37"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=676107843&amp;format=interactive"></iframe>

#### SQL
```SQL
SELECT `Month`,
       COUNT(`Crime ID`) AS COUNT
FROM crimes
GROUP BY `MONTH`
ORDER BY `Month` ASC;
```

### TASK 4
#### Zadání
K dispozici jsou i data o výsledcích jednotlivých případů. Jaký je v jednotlivých kategoriích podíl případů, kde se nenašel podezřelý?

#### Komentář
Nejprve pomocí prvního dotazu zjistíme kategorii vyřešení případů, která odpovídá situaci, kdy se nenašel podezřelý.

Druhým dotazem poté získáme podíl takových případů v jednotlivých kategoriích.

#### Závěr
Nenalezení podezřelého odpovídá kategorie vyřešení *Investigation complete; no suspect identified*.

Nejmenší podíl případů, kde nebyl nalezen podezřelý je v kategorii drogových případů (*Drugs*), a to 5,31%. Naopak největší podíl takových případů je v kategorii krádeže kola (*Bicycle theft*), a to 91,03%. 

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1510689825&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:A24"></iframe>

<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=285903865&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:E14"></iframe>

#### Vizualizace výsledku
<iframe height="449" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=976108226&amp;format=interactive"></iframe>

#### SQL
```SQL
SELECT DISTINCT `Outcome type`
FROM outcomes;
```

```SQL
WITH outcomesunique AS
  (SELECT *
   FROM
     (SELECT *,
             ROW_NUMBER() OVER (PARTITION BY outcomes.`Crime ID`
                                ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`, 'yyyy-MM'))) DESC) AS ROW_NUM
      FROM outcomes) AS res
   WHERE res.ROW_NUM = 1),
     allinfo AS
  (SELECT crimes.`Crime ID`,
          crimes.`Crime type`,
          outcomesunique.`Outcome type`
   FROM crimes
   JOIN outcomesunique ON (crimes.`Crime ID` = outcomesunique.`Crime ID`)),
     allcrimes AS
  (SELECT *
   FROM
     (SELECT `Crime type`,
             COUNT(`Crime type`) AS COUNT
      FROM allinfo
      WHERE `Crime type` IS NOT NULL
        AND `Crime type` != ''
      GROUP BY `Crime type`) AS res),
     nosuspectcrimes AS
  (SELECT *
   FROM
     (SELECT `Crime type`,
             COUNT(`Crime type`) AS COUNT
      FROM allinfo
      WHERE `Crime type` IS NOT NULL
        AND `Crime type` != ''
        AND `Outcome type` LIKE '%no suspect identified%'
      GROUP BY `Crime type`) AS res)
SELECT allcrimes.`Crime type`,
       allcrimes.count AS `All solved crimes`,
       (allcrimes.count-nosuspectcrimes.count) AS `Successfully solved crimes`,
       nosuspectcrimes.count AS `No suspect`,
       (nosuspectcrimes.count/allcrimes.count) AS Ratio
FROM allcrimes
LEFT JOIN nosuspectcrimes ON (allcrimes.`Crime type` = nosuspectcrimes.`Crime type`)
ORDER BY Ratio;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t4_1.csv](data/t4_1.csv)

Odkaz na data ve formátu csv: [t4_1.csv](data/t4_2.csv)

### TASK 5
#### Zadání
Jak dlouho trvá, než se vyřeší případ (pro různé kategorie zločinu)?

#### Komentář
Dotaz vede k získání průměrného času vyřešení případu v jednotlivých kategoriích.

#### Závěr
Nejkratší dobu trvá vyřešení případu krádeže kola (*Bicycle theft*), průměrná doba je 18 dní. Naopak nejdéle trvá vyšetření loupeží (*Robbery*), v této kategorii je průměrná doba 64,5 dní.

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=552744617&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B14"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=466948217&amp;format=interactive"></iframe>

#### SQL
```SQL
WITH outcomesunique AS
  (SELECT *
   FROM
     (SELECT *,
             ROW_NUMBER() OVER (PARTITION BY outcomes.`Crime ID`
                                ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`, 'yyyy-MM'))) DESC) AS ROW_NUM
      FROM outcomes) AS res
   WHERE res.ROW_NUM = 1),
     crimeProcedure AS
  (SELECT crimes.`Crime type`,
          outcomesunique.`Month` AS end_date,
          crimes.`Month` AS start_date
   FROM outcomesunique
   JOIN crimes ON (outcomesunique.`Crime ID`=crimes.`Crime ID`))
SELECT crimeProcedure.`Crime type` AS `Crime type`,
       AVG(DATEDIFF(to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.end_date, 'yyyy-MM'))), to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.start_date, 'yyyy-MM'))))) AS `Average solve time`
FROM crimeProcedure
GROUP BY crimeProcedure.`Crime type`
ORDER BY `Average solve time`;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t5.csv](data/t5.csv)

### TASK 6
#### Zadání
Která oddělení jsou v uzavírání případů nejrychlejší?

#### Komentář
Dotaz vede k získání dvaceti nejlepších oddělení z pohledu průměrného času na vyřešení případu.

#### Závěr
Nejkratší průměrnou dobu na vyřešení případu má oddělení **Lancashire Constabulary**, a to 18,84 dní.

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=411307535&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B21"></iframe>

#### Vizualizace výsledku
<iframe height="488" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1728703418&amp;format=interactive"></iframe>

#### SQL
```SQL
WITH outcomesunique as
  (SELECT *
   FROM
     (SELECT *, ROW_NUMBER() OVER (PARTITION BY outcomes.`Crime ID`
                                   ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`, 'yyyy-MM'))) DESC) AS ROW_NUM
      FROM outcomes) AS res
   WHERE res.ROW_NUM = 1),
                    crimeProcedure as
  (SELECT crimes.`Reported by`, outcomesunique.`Month` AS end_date, crimes.`Month` AS start_date
   FROM outcomesunique
   JOIN crimes ON (outcomesunique.`Crime ID`=crimes.`Crime ID`))
SELECT crimeProcedure.`Reported by`,
       AVG(DATEDIFF(to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.end_date, 'yyyy-MM'))), to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.start_date, 'yyyy-MM'))))) AS `Average solve time`
FROM crimeProcedure
GROUP BY crimeProcedure.`Reported by`
ORDER BY `Average solve time`
LIMIT 20;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t6.csv](data/t6.csv)

### TASK 7
#### Zadání
Pokuste se pro nějaký typ zločinu zakreslit na mapu (nebo alespoň do grafu longitude vs. latitude) vyřešené a nevyřešené případy.

#### Komentář
Vizualizace zaznamenaných kriminalit typu **"Possession of weapons"** v měsící **2017-10** pomocí barevných markerů v Google Maps.

* Zelený marker je vyřešený případ
* Červený marker je nevyřešený případ

#### Výsledná data
Data jsou příliš rozsáhlá pro náhledové zveřejnění, lze je ovšem stáhnout jako CSV soubor: [t7.csv](data/t7.csv)

#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/markers.html" ></iframe>

#### SQL
```SQL
WITH outcomesunique AS
  ( SELECT *
   FROM
     ( SELECT *,
              ROW_NUMBER() OVER ( PARTITION BY outcomes.`Crime ID`
                                 ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`, 'yyyy-MM'))) DESC ) AS ROW_NUM
      FROM outcomes ) AS res
   WHERE res.ROW_NUM = 1 ),
     allinfo AS
  ( SELECT crimes.`Latitude` AS lat,
           crimes.`Longitude` AS lng,
           CASE
               WHEN outcomesunique.`Outcome type` IS NULL THEN 0
               ELSE 1
           END AS resolved
   FROM crimes
   LEFT JOIN outcomesunique ON (crimes.`Crime ID` = outcomesunique.`Crime ID`)
   WHERE crimes.`Crime type` = 'Possession of weapons'
     AND crimes.`Month` = '2017-10'
     AND crimes.`Longitude` IS NOT NULL
     AND crimes.`Longitude` != 0
     AND crimes.`Latitude` IS NOT NULL
     AND crimes.`Latitude` != 0 )
SELECT lat,
       lng,
       resolved
FROM allinfo;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t7.csv](data/t7.csv)

### TASK 8
#### Zadání
Stop and Search data: Popište rozdělení času prohlídky (například pomocí histogramu).

#### Komentář

#### Výsledná data
##### Rozložení během dne
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=271488695&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:C73"></iframe>

##### Rozložení během měsíce
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1916279744&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:C94"></iframe>

##### Rozložení během roku
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=806000472&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:C37"></iframe>

#### Vizualizace výsledku
##### Rozložení během dne
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1501420958&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1566109545&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1660664320&amp;format=interactive"></iframe>

##### Rozložení během měsíce
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=670517239&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=618310268&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1721260187&amp;format=interactive"></iframe>

##### Rozložení během roku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=626909870&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=371527993&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=2058089063&amp;format=interactive"></iframe>

#### SQL
##### Rozložení během dne
```SQL
SELECT *
FROM
  (SELECT `Type`,
          substr(`Date`, 12, 2) AS hour,
          COUNT(*) AS COUNT
   FROM stopandsearch
   GROUP BY `Type`,
            substr(`Date`, 12, 2)) AS res
ORDER BY `Type`,
         hour;
```

##### Rozložení během měsíce
```SQL
SELECT *
FROM
  (SELECT `Type`,
          substr(`Date`, 9, 2) AS DAY,
          COUNT(*) AS COUNT
   FROM stopandsearch
   GROUP BY `Type`,
            substr(`Date`, 9, 2)) AS res
ORDER BY `Type`,
         DAY;
```

##### Rozložení během roku
```SQL
SELECT *
FROM
  (SELECT `Type`,
          substr(`Date`, 6, 2) AS MONTH,
          COUNT(*) AS COUNT
   FROM stopandsearch
   GROUP BY `Type`,
            substr(`Date`, 6, 2)) AS res
ORDER BY `Type`,
         MONTH;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t8_1.csv](data/t8_1.csv)

Odkaz na data ve formátu csv: [t8_2.csv](data/t8_2.csv)

Odkaz na data ve formátu csv: [t8_3.csv](data/t8_3.csv)

### TASK 9
#### Zadání
Pro vybranou kategorii vytvořte animovanou vizualizaci na mapě, jak se vyvíjí situace přes rok.

#### Komentář
Vizualizujeme počet kriminalit na region napříč měsíci roku 2017. Ovládání zprostředkovává tahátko v levém dolním rohu.

#### Výsledná data
Data jsou příliš rozsáhlá pro náhledové zveřejnění, lze je ovšem stáhnout jako CSV soubor: [t9.csv](data/t9.csv)

#### Vizualizace výsledku
<iframe style="width:100%;min-height:600px;" seamless frameborder="0" scrolling="no" src="https://vajjicko.github.io/BDT_semestralni_uloha/maps/areas.html" ></iframe>

### SQL
```SQL
SELECT crimes.`Month`,
       COUNT(crimes.`Crime ID`) AS COUNT,
       region.`RGN11NM` AS `Region name`,
       region.`RGN11CD` AS `Region code`
FROM crimes
LEFT JOIN region ON (crimes.`LSOA code` = region.`LSOA11CD`)
WHERE crimes.`LSOA code` IS NOT NULL
  AND region.`RGN11NM` IS NOT NULL
  AND crimes.`Month` >= '2017-01'
  AND crimes.`Month` <= '2017-12'
GROUP BY crimes.`Month`,
         region.`RGN11CD`,
         region.`RGN11NM`
ORDER BY crimes.`Month` ASC,
         COUNT DESC;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t9.csv](data/t9.csv)

### TASK 10
#### Zadání
Najděte hrabství, která mají nadprůměrný počet případů v jednotlivých kategoriích per 10 000 obyvatel.

U tohoto úkolu bylo potřeba využít tabulku s daty o populaci a číselníkové tabulky pro mapování územních celků.

#### Komentář
Dotaz vede k získání pěti hrabství v každé kategorii zločinu, kde je nejvyšší počet případů na 10 000 obyvatel.

#### Závěr
Z výsledků dotazu získáváme požadované statistiky.

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=437604625&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:F71"></iframe>

#### SQL
```SQL
WITH countycrimes AS
  (SELECT cr.`Crime type`, c.`CTY16CD` AS county_code, c.`CTY16NM` AS county_name, COUNT(*) AS COUNT
   FROM crimes AS cr
   JOIN ward AS w ON (cr.`LSOA code` = w.`LSOA11CD`)
   JOIN county AS c ON (w.`WD16CD` = c.`WD16CD`)
   GROUP BY cr.`Crime type`, c.`CTY16CD`, c.`CTY16NM`),
                  RESULT AS
  (SELECT cc.`Crime type`,
          cc.county_name,
          cc.Count,
          p.`Population`,
          (cc.Count/p.`Population`)*10000 AS crimes_per_10000
   FROM countycrimes AS cc
   JOIN population AS p ON (cc.county_code = p.`Code`)
   ORDER BY cc.`Crime type`,
            crimes_per_10000 DESC)
SELECT *
FROM
  (SELECT *,
          ROW_NUMBER() OVER (PARTITION BY `Crime type`
                             ORDER BY crimes_per_10000 DESC) AS ROW_NUM
   FROM RESULT) AS res
WHERE res.ROW_NUM < 6;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t10.csv](data/t10.csv)

### TASK 11
#### Zadání
Jaký existuje vztah úrovni zločinnosti a brexit preferenci?

#### Komentář
##### Data
Z tabulky brexit jsme vyextrahovali volební preference, velikost electorátu a % voličů pro regiony a oblasti. Z tabulky crimes poté díky JOINům s tabulkou ward počty zločinů pro jednotlivé regiony a oblasti.

##### Metodika
Data jsou spojitá X spojitá, volíme tedy lineární regresi jako náš nástroj testování nulové hypotézy.

##### Nulová hypotéza H0
Neexistuje žádný vztah mezi počtem kriminalit v oblasti nebo regionu a % voličů či volební preferencí pro odchod z EU

##### Alternativní hypotéza Ha
Existuje spojitost mezi počtem kriminalit v oblasti nebo regionu a % voličů či volební preferencí pro odchod z EU

##### Podle region
* kriminalita X preference => R^2 = 0.051
* kriminalita X % voličů => R^2 = 0.865

Dat je velice málo (10 samplů). Lze zmenšit granularitu pomocí area místo region. To zvýší sílu testu.

##### Podle area (s outliery)
* kriminalita X preference => R^2 = 0.037
* kriminalita X % voličů => R^2 = 0.25

Síla testu zvětšena (348 samplů), bohužel zde existují outlieři (2), které je třeba oříznout.
* City of London (4.21 crimes per capita)
* Westminster (1.75 crimes per capita)


##### Podle area (bez outlierů)
* kriminalita X preference => R^2 = 0.004
* kriminalita X % voličů => R^2 = 0.617

Síla testu zachována, outlieři oříznuti (346 zbývajících samplů).

#### Závěr
* Zamítáme H0 ve prospěch Ha.
* Lineární regrese s R^2 hodnotou 0.004 **neprokázala žádný vztah** mezi počtem kriminalit v oblasti a volební preferencí odchodu z EU
* Lineární regrese s poměrně vysokou R^2 hodnotou 0.617 poukazuje na **vztah mezi počtem kriminalit v oblasti a procentuálním počtem voličů**. Vztah je záporný (tangent parametr beta1 < 0), tedy čím více zaznamenaných kriminalit, tím méně % voličů.

#### Výsledná data
##### Podle region
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1527501732&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:J11"></iframe>

##### Podle area
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1197292459&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:J349"></iframe>

##### Podle area s oříznutím outliers
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1239867566&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:J347"></iframe>

#### Vizualizace výsledku
##### Podle region
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1829606990&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1104927466&amp;format=interactive"></iframe>

##### Podle area
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1771906241&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=39516865&amp;format=interactive"></iframe>

##### Podle area s oříznutím outliers
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1614621435&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=523033051&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=1895231909&amp;format=interactive"></iframe>

<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=804484930&amp;format=interactive"></iframe>

#### SQL
##### Podle region
```SQL
WITH regioncrimes AS
  (SELECT COUNT(crimes.`Crime ID`) AS COUNT,
          region.`RGN11NM` AS `Region name`,
          region.`RGN11CD` AS `Region code`
   FROM crimes
   JOIN region ON (crimes.`LSOA code` = region.`LSOA11CD`)
   WHERE crimes.`LSOA code` IS NOT NULL
     AND crimes.`LSOA code` != ''
     AND region.`RGN11NM` IS NOT NULL
     AND region.`RGN11NM` != ''
   GROUP BY region.`RGN11CD`,
            region.`RGN11NM`
   ORDER BY COUNT DESC),
     regionbrexit AS
  (SELECT brexit.`Region_Code`,
          SUM(brexit.`Electorate`) AS `Electorate`,
          SUM(brexit.`Valid_Votes`) AS `Valid_Votes`,
          SUM(brexit.`Remain`) AS `Remain`,
          SUM(brexit.`Leave`) AS `Leave`
   FROM brexit
   GROUP BY brexit.`Region_Code`)
SELECT regioncrimes.`count`,
       regioncrimes.`Region name`,
       regionbrexit.`Electorate`,
       regionbrexit.`Valid_Votes`,
       regionbrexit.`Remain`,
       regionbrexit.`Leave`,
       (regioncrimes.`count` / regionbrexit.`Electorate`) AS `crimes per person`,
       (regionbrexit.`Valid_Votes` / regionbrexit.`Electorate`) AS pct_voted,
       (regionbrexit.`Remain` / regionbrexit.`Valid_Votes`) AS pct_remain,
       (regionbrexit.`Leave` / regionbrexit.`Valid_Votes`) AS pct_leave
FROM regionbrexit
JOIN regioncrimes ON (regionbrexit.`Region_Code` = regioncrimes.`Region code`)
WHERE regioncrimes.count > 0
  AND regioncrimes.`Region name` IS NOT NULL
  AND regioncrimes.`Region name` != ''
ORDER BY regionbrexit.`Electorate` DESC,
         regioncrimes.`count` DESC;
```
##### Podle area
```SQL
WITH countycrimes AS
  (SELECT c.`LAD16CD` AS area_code,
          c.`LAD16NM` AS area_name,
          COUNT(cr.`Crime ID`) AS COUNT
   FROM crimes AS cr
   JOIN ward AS w ON (cr.`LSOA code` = w.`LSOA11CD`)
   JOIN county AS c ON (w.`WD16CD` = c.`WD16CD`)
   GROUP BY c.`LAD16CD`,
            c.`LAD16NM`),
     countybrexit AS
  (SELECT brexit.`Area_Code`,
          SUM(brexit.`Electorate`) AS `Electorate`,
          SUM(brexit.`Valid_Votes`) AS `Valid_Votes`,
          SUM(brexit.`Remain`) AS `Remain`,
          SUM(brexit.`Leave`) AS `Leave`
   FROM brexit
   GROUP BY brexit.`Area_Code`)
SELECT countycrimes.count,
       countycrimes.area_name AS `Area_name`,
       countybrexit.`Electorate`,
       countybrexit.`Valid_Votes`,
       countybrexit.`Remain`,
       countybrexit.`Leave`,
       (countycrimes.`count` / countybrexit.`Electorate`) AS `crimes per person`,
       (countybrexit.`Valid_Votes` / countybrexit.`Electorate`) AS pct_voted,
       (countybrexit.`Remain` / countybrexit.`Valid_Votes`) AS pct_remain,
       (countybrexit.`Leave` / countybrexit.`Valid_Votes`) AS pct_leave
FROM countybrexit
JOIN countycrimes ON (countybrexit.`Area_Code` = countycrimes.`area_code`)
ORDER BY countybrexit.`Electorate` DESC,
         countycrimes.`count` DESC;
```

#### Data v CSV
Odkaz na data ve formátu csv: [t11_region.csv](data/t11_region.csv)

Odkaz na data ve formátu csv: [t11_area.csv](data/t11_area.csv)

Odkaz na data ve formátu csv: [t11_area_crime_type.csv](data/t11_area_crime_type.csv)

## Závěr
Byla provedena analýza dat a vypracováno všech 11 úkolů. K jednotlivým úkolům byly poskytnuty odpovědi, dílčí analýzy, vizualizace a užité SQL dotazy.