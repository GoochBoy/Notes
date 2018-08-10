---
tags:
  - CODE
  - TODO
  - REFAC
---
    -Refaire une branche avec mon code de kompano-577 (2 branches) pour prochain refac
    -Validation du nouveau Epc scanner??

    -Add tests to Operations
        -Cancel Operation after new scan was displayed    

    -Modifier Mark à Shipped pour qu'il valide que c'est same parent

Validations
    SubRoutines
        ReplaceTag (newTag, oldTag, oldtagParent, oldTag.Children)
            oldTag et newTag pas null
            oldTag et newTag are the same
            both oldTag et newTag ont un parent
            ContainerValidationService(newTag, oldTag.Children) //if oldTag has  children
            AggregateValidation(newTag, oldTag.Children) //if oldTag has children
            DeaggregateValidation(oldTag.Children) //if oldTag has children
            DeaggregateValidation(oldTag) //if oldTag has parent
            AggregateValidation(oldTagParent, newTag) //if oldTag has parent
            
        Aggregate
            parent != null
            parent is container
            children null or any null inside list
            all children Serializable
            ValidateContainer(parent, children)
            si encode => change disposition pour Active
        Deaggregate
            parent != null
            parent is container
            children null or any null inside list
            all children Serializable
        ContainerValidationService

    Same parent??