# Requêtes wikidata
*__Devoir :__ Requêtes SPARQL sur Wikidata query service*

### Les peintures de monet :

    SELECT ?peinture WHERE {
    ?peinture wdt:P31 wd:Q3305213.
    ?peinture wdt:P170 wd:Q296.
    }

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3Fpeinture%20WHERE%20%7B%0A%20%20%3Fpeinture%20wdt%3AP31%20wd%3AQ3305213.%0A%20%20%3Fpeinture%20wdt%3AP170%20wd%3AQ296.%0A%7D%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

### Avec les labels (via le service wikibase:label) et les images associées :

    SELECT ?peinture ?peintureLabel ?image WHERE {
    ?peinture wdt:P31 wd:Q3305213;
              wdt:P170 wd:Q296.
    SERVICE wikibase:label { bd:serviceParam wikibase:language "fr". }
    OPTIONAL { ?peinture wdt:P18 ?image. }
    }

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3Fpeinture%20%3FpeintureLabel%20%3Fimage%20WHERE%20%7B%0A%20%20%3Fpeinture%20wdt%3AP170%20wd%3AQ296.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%20%7D%0A%20%20OPTIONAL%20%7B%20%3Fpeinture%20wdt%3AP18%20%3Fimage.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

#### Grille d'image :

    #defaultView:ImageGrid
    

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3AImageGrid%0ASELECT%20%3Fpeinture%20%3FpeintureLabel%20%3Fimage%20WHERE%20%7B%0A%20%20%3Fpeinture%20wdt%3AP170%20wd%3AQ296.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%20%7D%0A%20%20OPTIONAL%20%7B%20%3Fpeinture%20wdt%3AP18%20%3Fimage.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

### Avec en option (via OPTIONAL) les collections/lieux de conservation :

    SELECT ?peintureLabel ?collectionLabel ?lieuLabel WHERE {
    ?peinture wdt:P31 wd:Q3305213;
              wdt:P170 wd:Q296.
    SERVICE wikibase:label { bd:serviceParam wikibase:language "fr". }
    OPTIONAL { ?peinture wdt:P195 ?collection. }
    OPTIONAL { ?peinture wdt:P276 ?lieu. }
    }
    
    
<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3FpeintureLabel%20%3FcollectionLabel%20%3FlieuLabel%20WHERE%20%7B%0A%20%20%3Fpeinture%20wdt%3AP31%20wd%3AQ3305213%3B%0A%20%20%20%20wdt%3AP170%20wd%3AQ296.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%20%7D%0A%20%20OPTIONAL%20%7B%20%3Fpeinture%20wdt%3AP195%20%3Fcollection.%20%7D%0A%20%20OPTIONAL%20%7B%20%3Fpeinture%20wdt%3AP276%20%3Flieu.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

### Compter le nombre de Monet dans chaque collection/lieux de conservation et les afficher par odre décroissant :

    SELECT ?collectionLabel (COUNT (DISTINCT ?peinture) AS ?count) WHERE {
    ?peinture wdt:P31 wd:Q3305213;
              wdt:P170 wd:Q296.
    SERVICE wikibase:label { bd:serviceParam wikibase:language "fr". }
    OPTIONAL { ?peinture wdt:P195 ?collection. }
    } GROUP BY ?collectionLabel 
    ORDER BY DESC(?count)
    
<iframe style="width: 50vw; height: 50vh; border: 1px solid black;" src="https://query.wikidata.org/embed.html#SELECT%20%3FcollectionLabel%20(COUNT%20(DISTINCT%20%3Fpeinture)%20AS%20%3Fcount)%20WHERE%20%7B%0A%20%20%20%20%3Fpeinture%20wdt%3AP31%20wd%3AQ3305213%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20wdt%3AP170%20wd%3AQ296.%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%20%7D%0A%20%20%20%20OPTIONAL%20%7B%20%3Fpeinture%20wdt%3AP195%20%3Fcollection.%20%7D%0A%20%20%7D%20GROUP%20BY%20%3FcollectionLabel%20%0AORDER%20BY%20DESC(%3Fcount)" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

