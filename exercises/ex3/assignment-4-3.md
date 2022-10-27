## Exercise 4.3

Discover our current location using the Comunica SPARQL interface, which is stored as a data dump on the Solid Pod of Wout: [https://woutslabbinck.solidcommunity.net/location.ttl](https://woutslabbinck.solidcommunity.net/location.ttl).

To model the location, the [Semantic Sensor Network Ontology (SSN/SOSA)](https://www.w3.org/TR/vocab-ssn/) is used.
The location can be found as a result of a `sosa:Observation`.

To retrieve the current observation, [modifiers](https://www.w3.org/TR/rdf-sparql-query/#solutionModifiers) will be required.

Comunica SPARQL interface querying over the data dump in the solid Pod: 
https://query.linkeddatafragments.org/#datasources=https%3A%2F%2Fwoutslabbinck.solidcommunity.net%2Flocation.ttl&query=%23%20Write%20your%20query%20here

Use the following vocabularies: 

| name    | prefix    | url                        | interesting properties                      | site                                                              |
|---------|-----------|----------------------------|---------------------------------------------|-------------------------------------------------------------------|
| SOSA    | `sosa`    | http://www.w3.org/ns/sosa/ | `sosa:Observation` `sosa:hasSimpleResult` `sosa:resultTime` | https://www.w3.org/TR/vocab-ssn/                           |


