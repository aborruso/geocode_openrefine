**NOTA BENE**: questo testo è una bozza

# Geocoding con OpenRefine da Google
Questa che che segue è una procedura basata su [OpenRefine](http://www.google.com/url?q=http%3A%2F%2Fopenrefine.org%2F&sa=D&sntz=1&usg=AFQjCNHZewmD-BM9R_3HvfK6nSRxWbfKFg).

In questo esempio, per il *geocoding*, userò le API di Google Maps, ma si tratta di qualcosa di replicabile con tutti i motori oggi disponibili; per farlo però c'è da cambiare il codice prodotto per questo esempio.

## Procedura
A seguire una delle tante procedure tipo. Sono necessarie due cose:
* che ci sia un campo denominato "2geocode" nei dati che si importeranno in OpenRefine
* che questo campo contenga gli indirizzi su cui fare il *geocoding*, e nel modo più "pulito" possibile (meglio "VIA MARCO AURELIO, 81, 80126 Napoli, Italia" e non "VIA AURELIO 81,  Napoli")

Questi i passi:

* lanciare OpenRefine - importare la tabella e creare un nuovo progetto 
* copiare il codice che si trova in [questa pagina](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Faborruso%2Fgeocode_openrefine%2Fblob%2Fmaster%2FGoogle%2Fopen_refine.json&sa=D&sntz=1&usg=AFQjCNESnPqhch2t9ANWwkb7viiJRSx3wQ) 
* incollarlo in OpenRefine (come si vede nel filmato citato sotto) 
* lanciare il processo di gecoding e aspettare che termini * fare l'export dei dati (il tasto export si trova in alto a destra)

Nell'output saranno presenti non soltanto le colonne delle coordinate, ma anche altre, tra cui "*types*". Ci sono diverse varietà di *types*, tra cui

* administrative_area_level_3 
* bus_station 
* church 
* establishment 
* locality 
* neighborhood 
* point_of_interest 
* post_office 
* premise 
* route 
* stadium 
* street_address 
* sublocality 
* ...

Conoscere il type è utile, perché restituisce in qualche modo anche informazioni sulla qualità del risultato. Se ad esempio a partire da un indirizzo si ottiene "types=locality", si tratterà di qualcosa molto genericamente posizionato nel centroide di una porzione di territorio.

L'altra proprietà interessante dell'output prodotto è "location_type":

* "**ROOFTOP**" indicates that the returned result is a precise geocode for which we have location information accurate down to street address precision. 
* "**RANGE_INTERPOLATED**" indicates that the returned result reflects an approximation (usually on a road) interpolated between two precise points (such as intersections). Interpolated results are generally returned when rooftop geocodes are unavailable for a street address. 
* "GEOMETRIC_CENTER" indicates that the returned result is the geometric center of a result such as a polyline (for example, a street) or polygon (region). 
* "APPROXIMATE" indicates that the returned result is approximate. -

In grassetto i "*location_type*" che si possono considerare corrispondenti a operazioni di geocoding, il cui è output è posizionato geograficamente in modo più appropriato.

I dati di partenza andrebbero sempre puliti e filtrati prima di eseguire la procedura descritta sopra.

Il limite di richieste possibili tramite Google Maps è di 2500 record al giorno dallo stesso IP e la licenza delle API non si presta per la produzione di dati aperti. 

Qui un video in cui tutta la procedura è replicata rapidamente: [http://youtu.be/YWHRQt8T_Ns?hd=1](http://youtu.be/YWHRQt8T_Ns?hd=1)


![geocode_openrefine_google.jpg](https://raw.githubusercontent.com/aborruso/geocode_openrefine/master/Google/imgs/geocode_openrefine_google.jpg) 
