---
tags:
  - NMVS
  - ARCHITECTURE
---
    But
        -Tester GIASS
        -Tester OSM GOVA
        -Définir qu'est ce qui arrive selon tel input
    TODO
        -voir code
        -configurer notre OSM pour parler au GIASS de test
        -Tester GIASS with Ireland
    Questions
        -si expiry pas bon, SystemMessage ==  "Selected batch designation does not exist."??
        -si mode at manual : Batchid and Expiry still needed
        -undo stolen and undo destroy doe not work
        -why 2 diff urls for verify and none verify : OSM can't be configured with 2 urls
        -why 409
        -CheckedOut, Recalled, Expired, Withdrawn        
    Tester l'api de GIASS pour comprendre résultats
        -SingleVerify
            -si connu
                http : 200
                {
                    "EpcStatus": "Destroyed",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }
                ou
                http : 200
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }                
            -si non-connu
                -si SerialNumber inconnu
                    http : 409
                    {
                        "EpcStatus": "Unknown",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "Unknown serial number."
                    } 
                -si ProductCode inconnu
                    http : 409
                    {
                        "EpcStatus": "Unknown",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "Unknown product code."
                    }   
                -si BatchId inconu
                    http : 409
                    {
                        "EpcStatus": "Unknown",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "Selected batch designation does not exist."
                    }
                -si Expiry inconu 
                    http : 409                
                    {
                        "EpcStatus": "Unknown",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "Selected batch designation does not exist."
                    }
                -si BatchId et Expiry pas présent et automatic
                    http : 400
                    {
                        "Key": "SYSTEM_ERROR",
                        "Message": "The target NMVS system encountered an error",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "The required batch ID is not supplied for the automatic operation."
                    }
                -si BatchId et Expiry pas présent et manual
                    http : 409   
                    {
                        "EpcStatus": "Unknown",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                        "NmvsSystemMessage": "NMVS_TE_XM_02: Input data does not match the XML schema definition."
                    }
                -si destroyed    
                    http : 200 
                    {
                        "EpcStatus": "Destroyed",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                           
                -si dispensed
                    http : 200 
                    {
                        "EpcStatus": "Supplied",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }
                -si exported
                    http : 200 
                    {
                        "EpcStatus": "Exported",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                
                -si sampled
                    http : 200 
                    {
                        "EpcStatus": "Sample",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                
                -si free_sampled
                    http : 200                 
                    {
                        "EpcStatus": "Freesample",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                
                -si locked
                    http : 200  
                    {
                        "EpcStatus": "Locked",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                
                -si stolen
                    http : 200  
                    {
                        "EpcStatus": "Stolen",
                        "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                    }                
            -si données non-valide 
                http : 409   
                {
                    "EpcStatus": "Unknown",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123",
                    "NmvsSystemMessage": "NMVS_TE_XM_02: Input data does not match the XML schema definition."
                }   
        -SinglePack    (from Active)       
            -dispense
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK013C4436DFA861C45",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }   
                http : 200 
                {
                    "EpcStatus": "Supplied",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }                   
            -destroy
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK0121833071C31344B",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }            
                http : 200 
                {
                    "EpcStatus": "Destroyed",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }                         
            -export
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK014C7AD8A660E9242",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }  
                http : 200  
                {
                    "EpcStatus": "Exported",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }         
            -sample
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK015DCF41DB1E73C42",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }
                http : 200      
                {
                    "EpcStatus": "Sample",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }      
            -free sample
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK01650577F105E2447",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }    
                http : 200 
                {
                    "EpcStatus": "Freesample",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }        
            -lock
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK017EFB5AE5698BE47",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }  
                http : 200  
                {
                    "EpcStatus": "Locked",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }         
            -stolen  
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK018D42DEE55D0E848",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "00000000-0000-0000-0000-000000000000",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }       
                http : 200      
                {
                    "EpcStatus": "Stolen",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789123"
                }     
        -Undo
            -undo dispense
                {
                    "Mode": "Automatic",
                    "Scheme": "GS1",
                    "ProductCode": "72471540554334",
                    "SerialNumber": "PK013C4436DFA861C45",
                    "BatchId": "TEST574CE44057",
                    "ExpiryDate": "230709",
                    "ReferenceClientTransactionId": "12345678-1234-1234-1234-123456789123",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789124"
                }
                http : 200 
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789124"
                }
            -undo destroy
                fonctionne pas
            -undo export
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK014C7AD8A660E9242",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "12345678-1234-1234-1234-123456789123",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789126"
                }          
                http : 200  
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789126"
                }
            -undo sample
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK015DCF41DB1E73C42",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "12345678-1234-1234-1234-123456789123",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789127"
                }           
                http : 200   
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789127"
                }     
            -undo free sample
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK01650577F105E2447",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "12345678-1234-1234-1234-123456789123",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789128"
                }
                http : 200 
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789128"
                }                  
            -undo lock
                {
                "Mode": "Automatic",
                "Scheme": "GS1",
                "ProductCode": "72471540554334",
                "SerialNumber": "PK017EFB5AE5698BE47",
                "BatchId": "TEST574CE44057",
                "ExpiryDate": "230709",
                "ReferenceClientTransactionId": "12345678-1234-1234-1234-123456789123",
                "ClientTransactionId": "12345678-1234-1234-1234-123456789129"
                }            
                http : 200     
                {
                    "EpcStatus": "Active",
                    "ClientTransactionId": "12345678-1234-1234-1234-123456789129"
                }
            -undo stolen
                fonctionne pas