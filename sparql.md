# SPARQL

```
 # Query. 1
 # Associate URIs with prefixes

PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

 # Example of a SELECT query, retrieving 2 variables
 # Variables selected MUST be bound in graph pattern

SELECT ?subject ?label
WHERE {

  #This is our graph pattern
  ?person rdfs:label "Wolfgang Amadeus Mozart"@de ;
          dbo:deathPlace ?place .
  ?place  dbo:populationTotal ?population 
}
```

```
 # Query. 2


PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

 # Example of a SELECT query, retrieving all variables

SELECT *
WHERE {

  ?person rdfs:label "Wolfgang Amadeus Mozart"@de ;
          dbo:deathPlace ?place .
  ?place  dbo:populationTotal ?population .
}
```

```
 # Query. 3

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT ?name ?image
WHERE {

  # This pattern must be bound
  ?person rdfs:label "Wolfgang Amadeus Mozart"@de ;
          dbo:birthPlace ?place .

  # Anything in this block doesn't have to be bound
  OPTIONAL {
	   ?place  dbo:populationTotal ?population .
  }
}
```

```
 # Query. 4

PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT ?person ?place
WHERE {
   {
		?person dbo:deathPlace ?place .
   }
   UNION
   {
		?person dbo:birthPlace ?place .
   }
}
```

```
 # Query. 5 
 # Select the URI and population of all places

PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT ?place ?population
WHERE {

	?place dbo:populationTotal ?population .

}
```

```
 # Query. 6
 # Select the URI and population of all places
 # with highest first

PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT ?place ?population
WHERE {

	?place dbo:populationTotal ?population .

}
 # Use an ORDER BY clause to apply a sort. 
 # Can be ASC or DESC
ORDER BY DESC(?population)
```

```
 # Query. 7
 # Select the URI and population of a city
 # with highest first

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbp: <http://dbpedia.org/property/>

SELECT ?place ?population
WHERE {

	?place dbo:populationTotal ?population .
   FILTER EXISTS {
      ?place dbp:countryCode [] 
   }
}
 # Use an ORDER BY clause to apply a sort. 
 # Can be ASC or DESC
ORDER BY DESC(?population)
```

```
 # Query. 8
 # Select the URI and population of the 11-20th most populated countries

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbp: <http://dbpedia.org/property/> 

SELECT ?place ?population
WHERE {
	?place dbo:populationTotal ?population .
   FILTER EXISTS {
      ?place dbp:countryCode [] 
   }
}
 # Use an ORDER BY clause to apply a sort. 
ORDER BY DESC(?population)
 # Limit to first ten results
LIMIT 10
 # Apply an offset to get next “page”
OFFSET 10
```

```
 # Query. 9
 # Select name of persons born between 1st Jan 1756 and 1st Jan 1757

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?name
WHERE {

  ?person dbo:birthDate ?date;
          foaf:name ?name.

  FILTER (?date > "1756-01-01"^^xsd:date && 
          ?date < "1757-01-01"^^xsd:date)
}
```

```
 # Query. 10
 # Select the URI and population of places with an area below 20km^2, with most populated first

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbp: <http://dbpedia.org/property/>
PREFIX dbpp: <http://dbpedia.org/ontology/PopulatedPlace/>

SELECT ?place ?population
WHERE {
	?place dbo:populationTotal ?population ;
          dbpp:areaTotal ?area .

   # Note that we have to cast the data to the right type
   # As it is not declared in the data
   FILTER( xsd:double(?area) < 20 )
}

ORDER BY DESC(?population)
```

```
 # Query. 11

 # Select persons named Wolfgang

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>

SELECT ?subject ?name
WHERE {

   ?subject foaf:name ?name ;
            dbo:deathPlace dbr:Vienna .
  
   FILTER( regex(?name, "Wolfgang", "i" ) ) 
}
```

```
 # Query. 12

 # Select list of places that gave birth to german classical composers

PREFIX space: <http://purl.org/net/schemas/space/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?place
WHERE {
  [] dbo:birthPlace ?place ;
     dct:subject dbc:German_classical_composers
}
```

```
 # Query. 13

 # Is Mozart’s date of birth 1756-1-27?

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

ASK WHERE {
  dbr:Mozart space:launched "1756-1-27"^^xsd:date .
}

 # ASK returns a boolean value
```

```
 # Query. 14

 # Describe persons born in 1757

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dbp: <http://dbpedia.org/property/>

DESCRIBE ?person  {
  ?person dbp:birthDate ?date .
  FILTER ( ?date < "1958-01-01"^^xsd:date && 
           ?date >= "1757-01-01"^^xsd:date )
} 
```


======

## Content recommendation

A large query to be execute on http://data.open.ac.uk/sparql
```
  prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
  prefix podcast: <http://data.open.ac.uk/podcast/ontology/>
  prefix yt: <http://data.open.ac.uk/youtube/ontology/>
  prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>
  prefix rkb: <http://courseware.rkbexplorer.com/ontologies/courseware#>
  prefix saou: <http://data.open.ac.uk/saou/ontology#>
  prefix dbp: <http://dbpedia.org/property/>
  prefix media: <http://purl.org/media#>
  prefix olearn: <http://data.open.ac.uk/openlearn/ontology/>
  prefix mlo: <http://purl.org/net/mlo/>
  prefix bazaar: <http://digitalbazaar.com/media/>
  prefix schema: <http://schema.org/>

 SELECT 
  distinct
  (?related as ?identifier)
  ?type
  ?label
  (str(?location) as ?link)

  FROM <http://data.open.ac.uk/context/youtube>
  FROM <http://data.open.ac.uk/context/podcast>
  FROM <http://data.open.ac.uk/context/openlearn>
  FROM <http://data.open.ac.uk/context/course>
  FROM <http://data.open.ac.uk/context/qualification>
  WHERE
  { 
 ?x schema:productID "SYry6PYsL8o" . # change the youtube id to any OU youtube video
 ?x  yt:relatesToCourse ?course .
  {
       # related video podcasts
           ?related podcast:relatesToCourse ?course .
           ?related a podcast:VideoPodcast .
       ?related rdfs:label ?label .
           optional { ?related bazaar:download ?location }
       BIND( "VideoPodcast" as ?type ) .
     } union {
       # related audio podcasts
           ?related podcast:relatesToCourse ?course . 
           ?related a podcast:AudioPodcast .
       ?related rdfs:label ?label .
           optional { ?related bazaar:download ?location }
       BIND( "AudioPodcast" as ?type ) .
     } union {
       # related openlearn units
           ?related a olearn:OpenLearnUnit .
       ?related olearn:relatesToCourse ?course  .
       BIND( "OpenLearnUnit" as ?type ) .
           ?related <http://dbpedia.org/property/url> ?location .
       ?related rdfs:label ?label .
     } union {
           # related qualifications (compulsory course)
           ?related a mlo:qualification .
           ?related saou:hasPathway/saou:hasStage/saou:includesCompulsoryCourse ?course  .
       BIND( "Qualification" as ?type ) .
       ?related rdfs:label ?label .
       ?related mlo:url ?location 
         }
 } limit 200
```