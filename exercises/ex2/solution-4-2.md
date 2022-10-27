## Solution 4.2


The following query results in the titles of all publications of Ruben Verborgh ordered according to their date:

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT ?title ?date WHERE {
  ?author foaf:surname "Verborgh".
  ?author foaf:givenname "Ruben".
  ?publication dcterms:creator ?author;
               dcterms:title ?title;
      		     dcterms:date ?date.
} ORDER BY (?date)
```

Or you can use the foaf:name property again:

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT ?title ?date WHERE {
  ?author foaf:name "Ruben Verborgh".
  ?publication dcterms:creator ?author;
               dcterms:title ?title;
      		     dcterms:date ?date.
} ORDER BY (?date)
```

Or you can start with the identifier found in exercise 4.1


```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT ?title WHERE {
  ?publication dcterms:creator <https://biblio.ugent.be/person/002005635351#person>;
               dcterms:title ?title;
      		     dcterms:date ?date.
} ORDER BY (?date)
```