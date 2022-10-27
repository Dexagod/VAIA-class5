## Exercise 4.2

Using our results from the exercise 4.1, we now want find the title and date of the publications made by Ruben Verborgh, and order these titles by the date of the publication).

Use the Comunica SPARQL interface for the UGent biblio TPF endpoint:
Comunica SPARQL interface querying over the same Triple Pattern Fragments endpoint:
https://query.linkeddatafragments.org/#datasources=%2F%2Fdata.linkeddatafragments.org%2Fugent-biblio&query=%23%20Write%20your%20query%20here!


Use the following vocabularies:

| name    | prefix    | url                        | interesting properties                           | site                                                              |
|---------|-----------|----------------------------|--------------------------------------------------|-------------------------------------------------------------------|
| FOAF    | `foaf`    | http://xmlns.com/foaf/0.1/ | `foaf:name` `foaf:givenname` `foaf:surname`      | http://xmlns.com/foaf/0.1/                                        |
| DCTerms | `dcterms` | http://purl.org/dc/terms/  | `dcterms:title` `dcterms:creator` `dcterms:date` | https://www.dublincore.org/specifications/dublin-core/dcmi-terms/ |

