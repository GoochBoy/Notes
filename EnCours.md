---
tags:
  - ARCHITECTURE
  - CODE
  - TODO
---

TODO :
  -written exercice
  -Notes dans mon cahier
  -Dev Python dans VS code
  -Sync vs code
  -Code review / merge
  -plan pour kompano services
    -gi bulk api
    -
  -questions sven
  -code de refac remove user interactions
    -refaire une branche avec mon code de kompano-577 (2 branches) pour prochain refac
  -clone repo de GI
  -Add tests to Operations
    -Cancel Operation after new scan was displayed
  -test api gi
  -test api Ireland
  -demander à Mathieu si c'est toujours vrai que MarkAsShipped peut demander à l'utilisateur de scanner plusieurs nouveau parent
    ça devrait pu, assumer que ça va changer
  -check mail de Sven
  -test Bulk Arvato bulk API
    -action post workflow
      -destroy tag (tag needed)
      -replace tag 
  -sync api
    -test verify de OSM
      -modif de code ??
        -si pas là en mode verify => 409, 404 ou 200
        -liste des epc state possible
    -test Dispense de OSM
  -sync api : Admin??
  -async api
    -voir code sync
    -comprendre besoins

ARCHITECTURE suivi
  -2 urls pour GASS
  -offline mode
  -pourquoi 409 si not found
  -NMVS async (Bulk api)
  -Trail api
  -Kompano Mvc Core server
    -api OSM data access
  -OsmService SeesionState avec Login et machin
