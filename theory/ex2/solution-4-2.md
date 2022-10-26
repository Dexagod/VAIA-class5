## Solution 4.3

The following query will give you the wanted results:

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dc: <http://xmlns.com/foaf/0.1/>
SELECT ?title WHERE {
  ?author foaf:surname "Verborgh".
  ?author foaf:givenname "Ruben".
  ?publication dc:creator ?author;
               dc:title ?title;
      		   <http://purl.org/dc/terms/date> ?date.
} ORDER BY (?date)
```