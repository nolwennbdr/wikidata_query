# Requêtes wikidata
*__Devoir :__ Requêtes SPARQL sur Wikidata query service*

### Les peintures de monet :

    SELECT ?peinture ?peintureLabel WHERE {
    ?peinture wdt:P31 wd:Q3305213.
    ?peinture wdt:P170 wd:Q296.
    } 

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3Fpeinture%20%3FpeintureLabel%20WHERE%20%7B%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%20%20%0A%20%20%3Fpeinture%20wdt%3AP170%20wd%3AQ296.%0A%20%20%3Fpeinture%20wdt%3AP31%20wd%3AQ3305213.%0A%7D%0ALIMIT%20100" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

### Avec les labels (via le service wikibase:label) et les images associées :

### Avec en option (via OPTIONAL) les collections/lieux de conservation :

### Compter le nombre de Monet dans chaque collection/lieux de conservation et les afficher par odre décroissant :
