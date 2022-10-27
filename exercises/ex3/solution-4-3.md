## Solution 4.3

### Location model

An example of a location observation is the following:

```turtle
@prefix dct: <http://purl.org/dc/terms/>.
@prefix sosa: <http://www.w3.org/ns/sosa/>.
@prefix wgs: <http://www.w3.org/2003/01/geo/wgs84_pos#>.
@prefix ex: <http://example.org/>.
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>.
@prefix geo: <http://www.opengis.net/ont/geosparql#>.
@prefix loc: <http://location.example.com/>.

<http://location.example.com/tracks/observation/2022-08-07T08%3A08%3A36Z> sosa:hasFeatureOfInterest <https://data.knows.idlab.ugent.be/person/woslabbi/#me>;
    sosa:resultTime "2022-08-07T08:08:36Z"^^<http://www.w3.org/2001/XMLSchema#dateTime>;
    a sosa:Observation;
    sosa:hasResult <http://location.example.com/tracks/observation/result/2022-08-07T08%3A08%3A36Z>;
    sosa:observedProperty loc:location;
    sosa:hasSimpleResult "POINT(3.611652000 50.960230000)"^^geo:wktLiteral;
    dct:isVersionOf ex:location;
    sosa:madeBySensor <http://sensor.be>.
<http://location.example.com/tracks/observation/result/2022-08-07T08%3A08%3A36Z> a sosa:Result;
    wgs:latitude "50.960230000";
    wgs:longitude "3.611652000";
    wgs:elevation "6.1";
    <https://w3id.org/transportmode#transportMode> <https://w3id.org/transportmode#Walking>.
```

### A SPARQL query for location data

In this observation, we are interested in the fact that it is an observation, the point in the simple result and the time at which it has happened.

So first we build a query that can find all the observations:
```
PREFIX sosa: <http://www.w3.org/ns/sosa/>
SELECT * WHERE {   
  ?s a sosa:Observation;
}
```
Using the model, we can now bind the location point and the timestamp:

```
PREFIX sosa: <http://www.w3.org/ns/sosa/>
SELECT * WHERE {   
  ?s a sosa:Observation;
  sosa:hasSimpleResult ?loc ;  
  sosa:resultTime ?datetime
}
```

### Ordering the results

Executing the previous query, results in retrieving all the location points.
However, we are interested in the current location, which is the most recent one.

To create ordering in the result of a SPARQL query, we can use the [ORDER BY](https://www.w3.org/TR/rdf-sparql-query/#modOrderBy) modifier.

The following query orders the results chronologically, using the timestamp within the observation:

```
PREFIX sosa: <http://www.w3.org/ns/sosa/>
SELECT * WHERE {   
  ?s a sosa:Observation;
  sosa:hasSimpleResult ?loc ;  
  sosa:resultTime ?datetime
}
ORDER BY ?datetime
```

We want to reverse the order, which results in retrieving the most recent observation first:

```
PREFIX sosa: <http://www.w3.org/ns/sosa/>
SELECT * WHERE {   
  ?s a sosa:Observation;
  sosa:hasSimpleResult ?loc ;  
  sosa:resultTime ?datetime
}
ORDER BY DESC(?datetime)
```

### Limiting the results

Currently, we are retrieving all the location observations.
We can single out only 1 observation by using the [LIMIT](https://www.w3.org/TR/rdf-sparql-query/#modResultLimit) modifier.


Thus the solution to discover our current location using the Comunica SPARQL interface is the following query:

```
PREFIX sosa: <http://www.w3.org/ns/sosa/>
SELECT * WHERE {   
  ?s a sosa:Observation;
  sosa:hasSimpleResult ?loc ;  
  sosa:resultTime ?datetime
}
ORDER BY DESC(?datetime) LIMIT 1
```

Filled into Comunica, this it the following query:

https://query.linkeddatafragments.org/#datasources=https%3A%2F%2Fwoutslabbinck.solidcommunity.net%2Flocation.ttl&query=PREFIX%20sosa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0ASELECT%20*%20WHERE%20%7B%20%20%20%0A%20%20%3Fs%20a%20sosa%3AObservation%3B%0A%20%20sosa%3AhasSimpleResult%20%3Floc%20%3B%20%20%0A%20%20sosa%3AresultTime%20%3Fdatetime%0A%7D%0AORDER%20BY%20DESC(%3Fdatetime)%20%20LIMIT%201%0A