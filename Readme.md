# BDT - Semestrální úloha

## Obsah
* [Úvod](#úvod)
* [Data](#data)
* [Technologie](#technologie)
  * [Dočasné tabulky](#dočasné-tabulky)
  * [Finální tabulky](#dočasné-tabulky)
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

### Dočasné tabulky

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

```SQL
--Zapnuti dynamickeho partition
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

## Úkoly

### TASK 1
#### Zadání
Kolik případů je evidováno v jednotlivých kategoriích (krádež, žhářství, …)?

#### Komentář

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

#### Komentář

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1305914394&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B11"></iframe>

<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=879348330&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:C11"></iframe>

#### SQL

```SQL
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT * FROM (SELECT `LSOA name`, COUNT(`LSOA name`) as count FROM crimes WHERE `LSOA name` IS NOT NULL AND `LSOA name` != '' GROUP BY `LSOA name`) as res ORDER BY res.count DESC LIMIT 10;

```

```SQL
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT * FROM (SELECT `LSOA name`, `Crime type`, COUNT(*) as count FROM 
crimes WHERE `LSOA name` IS NOT NULL AND `LSOA Name` != '' GROUP BY `LSOA name`, `Crime type`) as res ORDER BY res.count DESC LIMIT 10;
```

### TASK 3
#### Zadání
Jak se vyvíjejí časově počty evidovaných případů?

#### Komentář

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=531591978&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B37"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=676107843&amp;format=interactive"></iframe>

#### SQL
```SQL
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT `Month`, COUNT(`Crime ID`) AS Count FROM crimes GROUP BY `MONTH` ORDER BY `Month` ASC;
```

### TASK 4
#### Zadání
K dispozici jsou i data o výsledcích jednotlivých případů. Jaký je v jednotlivých kategoriích podíl případů, kde se nenašel podezřelý?

#### Komentář

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=1510689825&amp;single=true&amp;widget=true&amp;headers=falserange=A1:A24"></iframe>

<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=285903865&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:E14"></iframe>

#### Vizualizace výsledku
<iframe height="449" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=976108226&amp;format=interactive"></iframe>

#### SQL
```SQL
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT DISTINCT `Outcome type` from outcomes;
```

```SQL
WITH outcomesunique as(SELECT * FROM (SELECT *,ROW_NUMBER() OVER (PARTITION BY outcomes.`Crime ID` ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`,'yyyy-MM'))) DESC) AS ROW_NUM FROM outcomes) AS res WHERE res.ROW_NUM = 1),
allinfo as( SELECT crimes.`Crime ID`, crimes.`Crime type`, outcomesunique.`Outcome type` FROM crimes JOIN outcomesunique ON (crimes.`Crime ID` = outcomesunique.`Crime ID`)),
allcrimes as( SELECT * FROM (SELECT `Crime type`, COUNT(`Crime type`) as count FROM allinfo WHERE `Crime type` IS NOT NULL AND `Crime type` != '' GROUP BY `Crime type`) as res),
nosuspectcrimes as( SELECT * FROM (SELECT `Crime type`, COUNT(`Crime type`) as count FROM allinfo WHERE `Crime type` IS NOT NULL AND `Crime type` != '' AND `Outcome type` LIKE '%no suspect identified%' GROUP BY `Crime type`) as res)
INSERT OVERWRITE DIRECTORY '/user/bilekpe5/results'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
SELECT allcrimes.`Crime type`, allcrimes.count as `All solved crimes`, (allcrimes.count-nosuspectcrimes.count) as `Successfully solved crimes`, nosuspectcrimes.count as `No suspect`, (nosuspectcrimes.count/allcrimes.count) AS Ratio FROM allcrimes LEFT JOIN nosuspectcrimes ON (allcrimes.`Crime type` = nosuspectcrimes.`Crime type`) ORDER BY Ratio;
```

### TASK 5
#### Zadání
Jak dlouho trvá, než se vyřeší případ (pro různé kategorie zločinu)?

#### Komentář

#### Výsledná data
<iframe height="450" style="width:100%;" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=552744617&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B14"></iframe>

#### Vizualizace výsledku
<iframe height="371" style="width:100%;" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=466948217&amp;format=interactive"></iframe>

#### SQL
```SQL
WITH outcomesunique as(SELECT * FROM (SELECT *,ROW_NUMBER() OVER (PARTITION BY outcomes.`Crime ID` ORDER BY to_date(from_unixtime(UNIX_TIMESTAMP(outcomes.`Month`,'yyyy-MM'))) DESC) AS ROW_NUM FROM outcomes) AS res WHERE res.ROW_NUM = 1),
crimeProcedure as(SELECT crimes.`Crime type`, outcomesunique.`Month` as end_date, crimes.`Month` as start_date FROM outcomesunique
JOIN crimes ON (outcomesunique.`Crime ID`=crimes.`Crime ID`))
SELECT crimeProcedure.`Crime type` as `Crime type`, AVG(DATEDIFF(to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.end_date,'yyyy-MM'))),to_date(from_unixtime(UNIX_TIMESTAMP(crimeProcedure.start_date,'yyyy-MM'))))) AS `Average solve time` FROM crimeProcedure GROUP BY crimeProcedure.`Crime type` ORDER BY `Average solve time`;
```

### TASK 6
#### Zadání
#### Komentář
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 7
#### Zadání
Pokuste se pro nějaký typ zločinu zakreslit na mapu (nebo alespoň do grafu longitude vs. latitude) vyřešené a nevyřešené případy.

#### Komentář
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
#### Komentář
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 9
#### Zadání
Pro vybranou kategorii vytvořte animovanou vizualizaci na mapě, jak se vyvíjí situace přes rok.
#### Komentář
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
#### Komentář
#### Výsledná data
#### Vizualizace výsledku
#### SQL

### TASK 11
#### Zadání
#### Komentář
#### Výsledná data
#### Vizualizace výsledku
#### SQL

## Závěr
