# Hands-On: Topicality

A piece of news from the Guardian: `https://www.theguardian.com/education/2019/jul/05/uk-universities-condemned-for-failure-to-tackle-racism`

```
Senior academics and politicians have condemned UK universities for failing to tackle endemic racism against students and staff after a Guardian investigation found widespread evidence of discrimination in the sector.
University staff from minority backgrounds said the findings showed there was “absolute resistance” to dealing with the problem. Responses to freedom of information (FoI) requests the Guardian sent to 131 universities showed that students and staff made at least 996 formal complaints of racism over the past five years.
Of these, 367 were upheld, resulting in at least 78 student suspensions or expulsions and 51 staff suspensions, dismissals and resignations.
But even these official figures are believed to underestimate the scale of racism in higher education, with two separate investigations by the Guardian and the Equality and Human Rights Commission identifying hundreds more cases that were not formally investigated by universities.
Scores of black and minority ethnic students and lecturers have told the Guardian they were dissuaded from making official complaints and either dropped their allegations or settled for an informal resolution. They said white university staff were often reluctant toaddress racism, with racial slurs treated as banter or an inevitable byproduct of freedom of speech, and institutional racism poorly recognised.

```

Named Entity Recognition with DBpedia Spotlight:
(https://www.dbpedia-spotlight.org/demo/)[https://www.dbpedia-spotlight.org/demo/]

Entities retrieved:
```
<http://dbpedia.org/resource/United_Kingdom>

<http://dbpedia.org/resource/Endemism> 

<http://dbpedia.org/resource/Racism>

<http://dbpedia.org/resource/Australian_Human_Rights_Commission>

<http://dbpedia.org/resource/Institutional_racism>
```

Generalise and find topics exploring the knowledge graph:
```
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT (count(?node) as ?sc) ?obj WHERE {
  ?node dct:subject ?cat .
  ?cat skos:broader{0,5} ?obj .
  VALUES (?node){
    (<http://dbpedia.org/resource/United_Kingdom>) 
    (<http://dbpedia.org/resource/Endemism>) 
    (<http://dbpedia.org/resource/Racism>) 
    (<http://dbpedia.org/resource/Australian_Human_Rights_Commission>) 
    (<http://dbpedia.org/resource/Institutional_racism>)
  }
} 
group by ?obj
order by desc(?sc)
limit 10

```