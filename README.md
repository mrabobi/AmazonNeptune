 <h3 align="center">Practical usages of Amazon Neptune with SPARQL</h3>

## Check if status of Database is healthy


```python
%status
```




    {'status': 'healthy',
     'startTime': 'Thu Dec 09 00:06:24 UTC 2021',
     'dbEngineVersion': '1.0.5.1.R2',
     'role': 'writer',
     'gremlin': {'version': 'tinkerpop-3.4.11'},
     'sparql': {'version': 'sparql-1.1'},
     'labMode': {'ObjectIndex': 'disabled',
      'DFEQueryEngine': 'viaQueryHint',
      'ReadWriteConflictDetection': 'enabled'},
     'features': {'ResultCache': {'status': 'disabled'},
      'IAMAuthentication': 'disabled',
      'Streams': 'disabled',
      'AuditLog': 'disabled'},
     'settings': {'clusterQueryTimeoutInMs': '120000'}}



## Load data in database


```python
%load
```

<img src="pics/load.png" alt="Load" width="500" height="150">


# SELECT FIRST 100 ITEMS FROM DATASET



```python
%%sparql 
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
SELECT ?s ?p ?o {?s ?p ?o} LIMIT 100
```


   <img src="pics/first100.png" alt="First100" width="500" height="150">


## Select all clases from cars dataset


```python
%%sparql

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>  
SELECT ?clasa  WHERE { ?clasa rdf:type rdfs:Class } ORDER BY ?clasa
```


    Tab(children=(Output(layout=Layout(max_height='600px', overflow='scroll', width='100%')), Output(layout=Layout…


## Select Subject and object where predicate contains prefLabel. Order by eng column


```python
%%sparql

PREFIX rdf:<http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX skos:<http://www.w3.org/2004/02/skos/core#> 
SELECT * {?url skos:prefLabel ?eng;skos:prefLabel ?de FILTER(lang(?eng)='en' && lang(?de)='de')}  ORDER BY ASC(?eng)
```


   <img src="pics/prefLabel.png" alt="PrefLabel" width="500" height="150">


## We can store the result and reuse it 


```python
%%sparql --store-to result

PREFIX rdf:<http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX skos:<http://www.w3.org/2004/02/skos/core#> 
SELECT * {?url skos:prefLabel ?eng;skos:prefLabel ?de FILTER(lang(?eng)='en' && lang(?de)='de')} ORDER BY ASC(?eng)
```


    <img src="pics/store1.png" alt="Store1" width="500" height="150">
    
    <img src="pics/store2.png" alt="Store2" width="500" height="150">

