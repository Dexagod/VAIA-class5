## Exercise 4.4

There is the claim that top athletes are mostly born in the first quarter of the year due to the **“relative age effect”**.

In this exercise we will try to verify that claim by creating a SPARQL query using the wikidata.

We want to query athletes, group them by birth month and then count those groups.

As a starting point, you can use the Comunica SPARQL interface with [wikidata](https://query.wikidata.org/bigdata/ldf) as source: 
https://query.linkeddatafragments.org/#datasources=https%3A%2F%2Fquery.wikidata.org%2Fbigdata%2Fldf&query=%23%20Write%20your%20query%20here!

### Grouping with SPARQL

In [SPARQL 1.1 Aggregates](https://www.w3.org/TR/2013/REC-sparql11-query-20130321/#aggregates), there is information about how to group in SPARQL and which operations we can use.

* Grouping is done via [GROUP BY](https://www.w3.org/TR/2013/REC-sparql11-query-20130321/#groupby) syntax.
* Useful aggregation functions
  * Count: counts the number of patterns
  * month: extracts the month of an `xsd:dateTime` Literal

As a pointer, you can check out the [slide on aggregations in SPARQL](https://dexagod.github.io/VAIA-class5/#sparql-aggregators-example).

### Prefixes
Use the following vocabularies: 

| name       | prefix | url                                  | interesting properties | site                                                   |
| ---------- | ------ | ------------------------------------ | ---------------------- | ------------------------------------------------------ |
| Entity     | `wd`   | http://www.wikidata.org/entity/      | `wd:Q2066131`          | https://www.wikidata.org/wiki/Wikidata:SPARQL_tutorial |
| Properties | `wdt`  | http://www.wikidata.org/prop/direct/ | `wdt:P106` `wdt:P569`  | https://www.wikidata.org/wiki/Wikidata:SPARQL_tutorial |