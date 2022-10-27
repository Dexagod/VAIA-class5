## Solution 4.4

### Searching for athletes

First, we search into wikidata for athletes. This will result into the following page: https://www.wikidata.org/wiki/Q2066131

Then, we can search for occupation, which results into: https://www.wikidata.org/wiki/Property:P106

We combine that to find all persons in wikidata which are athletes:

```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT ?person WHERE {
  ?person 	wdt:P106 wd:Q2066131.
} 
```

#### Birthdays

The property for date of birth can be found on wikidata as well: https://www.wikidata.org/wiki/Property:P569

So we plug that in to the query:

```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT ?person ?birth WHERE {
  ?person 	wdt:P106 wd:Q2066131;
  			wdt:P569 ?birth .
}
```

### Group athletes by their birthday month

For this, we use the aggregation function `month()`

```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT ?month WHERE {
  ?person 	wdt:P106 wd:Q2066131;
  			wdt:P569 ?birth .
} GROUP BY(month(?birth) as ?month)
```

And now we can use the function `count()` to count the athletes per month, which is the final solution.

```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT (count(?person) as ?count) ?month WHERE {
  ?person 	wdt:P106 wd:Q2066131;
  			wdt:P569 ?birth .
} GROUP BY(month(?birth) as ?month)
```

And finally, we can filter the results to contain only valid dateTime entries and order the results on their month of birth

```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT (count(?person) as ?count) ?month  WHERE {
  ?person wdt:P106 wd:Q2066131 ;
          wdt:P569 ?birth .
  FILTER (datatype(?birth) = xsd:dateTime)
}
GROUP BY (month(?birth) as ?month)
ORDER BY (?month)
```

### Solution

Following link also gives the result:

https://query.linkeddatafragments.org/#datasources=https%3A%2F%2Fquery.wikidata.org%2Fbigdata%2Fldf&query=PREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0ASELECT%20(count(%3Fperson)%20as%20%3Fcount)%20%3Fmonth%20%20WHERE%20%7B%0A%20%20%3Fperson%20wdt%3AP106%20wd%3AQ2066131%20%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP569%20%3Fbirth%20.%0A%20%20FILTER%20(datatype(%3Fbirth)%20%3D%20xsd%3AdateTime)%0A%7D%0AGROUP%20BY%20(month(%3Fbirth)%20as%20%3Fmonth)%0AORDER%20BY%20(%3Fmonth)%0A