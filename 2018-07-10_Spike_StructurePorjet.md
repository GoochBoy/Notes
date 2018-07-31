---
tags:
  - SPIKE
---
	Spike: Structure de projet
	CERTA-359
	
	-But : Savoir sans se poser de question où mettre notre code

	Lignes directrices
		-avoir le moins de niveau de dossier possible
		-se faire une liste de nom de domain et toujours utiliser les mêmes lorsqu'on parle de la même chose

	Liste de nom de dossiers possible 
		*Pour aider à la clarté, on peut avoir plusieurs dossiers du même type au même niveau dans un projet, il faut juste ajouter un suffix, ex : XamarinHelper, ErrorHelper, ValidationHelper, ...
		-"NomDeDomain" genre Nmvs, Trail, Serialisation, ...
			-dans un projet on peut avoir un dossier avec comme nom un nom de domain, c'est comme un mini projet dans le projet courant; on y retrouvera les mêmes types de dossiers que à la racine d'un projet
		-Helpers
			-pas de state
			-Converters : StringToVisibilityConverter.cs, ...
			-Mappers : permet de transformer un type externe en type du projet
			-...
		-Exceptions 
		-Extentions 
		-Factories
		-Operations
			-code qui va modifier les données (dans notre cas OSM ou NMVS)
			-les interface et les classes sont à côté, pas de sous dossier
		-Services
			-code qui va chercher des données 
			-les interface et les classes sont à côté, pas de sous dossier
		-"NomDeDomain"Models ex : NmvsModels, BarcodeModels, ...
			-enum
			-classes qui contiennent très peu ou pas de logique
			-exemple : NmvsModels, Barcode, 
		-Requirements
			-interfaces qui sont injectées dans des classes du projet courant, donc les dépendances inversées du projet courant
		-View (seulement dans un projet Xamarin)
		-Viewmodel (seulement dans un projet Xamarin)
		-Autres dossiers seulement dans un projet de type Xamarin : Behaviors, Controls, Images, Styles
