---
tags:
  - ARCHITECTURE
  - CODE
  - TODO
---

Implémenter
K-server
      //structure VB pour sdk (faire comme ...)
      //checker le csproj de certaweb api (versions)
        netcoreapp2.0 et Include="Microsoft.AspNetCore.All" Version="2.0.6"
      //TODO : écrire stories 
        -osmService
        -enlever les fakes
        -trail
        -API key pour parler à GOVA
        -spike : comment poller GOVA
        -notifier something 
      //TODO : bouger les dtos et mapper pour que kompano le sache
      //TODO : verif same url, diffe parameters : route bien
      //TODO : crée POC GOVA
      //TODO : GET TOKEN FROM HEADER
      //TODO : CREATE osmsERVICE
      //TODO : Validate token

  -dépendances avec Business (Workflow), Nmvs
    -messages d'erreur => vers des code d'erreur, comment REST porpage les erreur?
  -Authentication : qui a accès à K-Server, avec quel Token K-Server s'authentifie à l'OSM et à GOVA
  -proxy vers gova
  -proxy vers OSM

GOVA
  -créer service avec un api
    -verify
    -singlePack
    -singleUndo
    -bulkPack
    -bulkUndo
  -Authentication : qui a accès à GOVA, comment GOVA reçoit sa API key pour GI
  -Implémenter une Q qui va permettre l'asynchone
    -task todo
    -task inprogress
    -task completed
  -Implémenter un system de polling vers GI pour recevoir les résultats du bulk
  -Avoir un API pour que K-Server puisse poller GOVA pour avoir les résultats (url par Task genre...)

GI
  -définir l'API bulk
  -connecteur bulk arvato
  -connecteur bulk solidsoft
  
TODO :
  -Estelle : vacances (compiler toutes mes vacances)
  -Estelle dentiste
  -Estelle temps accumulé (Hour bank vs Accumulated) (verif le truc quelle m'avait dit)
  -GOVA preuve concept
  -K-SERVER preuve concept
  -GI
  -Chercher sur comment faire des callback avec un api REST
  -mail Sven
    -why is undo not an url sent back to caller that would be valid the amount of time the NMVS has specified (10 days)
  -ména
  -API GI
  -K-Server : définitions besoin et todos
    -branch avec un esquisse
  -GOVA : définitions besoin et todos
  -GI-Bulk interface
  -bonifier story de Mathieu
  -connect to NMVS Irland
  -Connect to NMVS UK
  -branch avec code legacy 577
  -Test GI
    -uk
    -ie
  -Notes dans mon cahier
  -Dev Python dans VS code
  -Sync vs code
    -put in git Notes
  -plan pour kompano services
    -gi bulk api
    -
  -questions sven

  -test api gi

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

