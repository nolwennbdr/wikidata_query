# Wikidata requests
Devoir : requête sparql sur wikidata query service

Les peintures de monet :

'''SELECT ?peinture ?peintureLabel WHERE {
  ?peinture wdt:P31 wd:Q3305213.
  ?peinture wdt:P170 wd:Q296.
}'''

Avec les labels (via le service wikibase:label) et les images associées :

Avec en option (via OPTIONAL) les collections/lieux de conservation :

Compter le nombre de Monet dans chaque collection/lieux de conservation et les afficher par odre décroissant :
