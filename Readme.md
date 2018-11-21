# BDT - Semestrální úloha

## Úvod

## Data

## Technologie

## Úkoly

### T1: Kolik případů je evidováno v jednotlivých kategoriích (krádež, žhářství, …)?

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubhtml?gid=275794259&amp;single=true&amp;widget=true&amp;headers=false&amp;range=A1:B15"></iframe>

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT8kFoVB6TB8-bQCMInVBvB2l2HuElhyXmWn8kBtQ2BRCGmejcSKpZU_zNOJaqtfrT98rQPWC0tOn7Y/pubchart?oid=958727936&amp;format=interactive"></iframe>

```sql
SELECT `Crime type`, COUNT(`Crime type`) as Count FROM crimes GROUP BY `Crime type` ORDER BY Count DESC;
```
