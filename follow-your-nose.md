# Follow your nose

Tools:

 - CURL: https://curl.haxx.se/
 - wURL: http://purl.org/ld4dh/wurl
 - http://prefix.cc

## Mozart
An HTTP resource: `http://dbpedia.org/resource/Wolfgang_Amadeus_Mozart`

```
curl -v http://dbpedia.org/resource/Wolfgang_Amadeus_Mozart
```

```
curl -v http://dbpedia.org/resource/Wolfgang_Amadeus_Mozart -H “Accept: text/turtle”
```

```
curl -v http://dbpedia.org/data/Wolfgang_Amadeus_Mozart.ttl
```

```
curl -v http://dbpedia.org/resource/Wolfgang_Amadeus_Mozart -H “Accept: text/turtle” -L
```

Find the answer to the following questions:

- In what formats is Mozart available? Try: text/html, application/rdf+xml, text/n-triples, text/turtle
- Find Mozart's image (it’s a jpg)
- When Mozart was born?
- Where Mozart died?
- How many inhabitants has the city today?

## A listening experience
```
http://data.open.ac.uk/led/lexp/1446304716352
```

Find the answer to the following questions:

- Find the location of the experience
- When did it happened?
- Who is the listener?
- What musical opera was performed?
- What is the author of the listened music?
- Who is the performer?
- What is the genre?
- *Find* other operas of the same genre.

```
http://dbpedia.org/sparql
```

```
SELECT * WHERE {
  ?entity 
  <http://purl.org/dc/terms/subject> 
  <http://dbpedia.org/resource/Category:Grand_operas> .
}
```
