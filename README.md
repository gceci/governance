# Governance di applicazioni a Microservizi
## Introduzione
Non é più un mistero, lo stile architetturale a Microservizi porta inevitabilmente al proliferare di applicazioni.
Tali applicazioni sono implementate sulla base del principio della singola responsabilità, ciascuna applicazione esegue i propri processi e comunica con altre applicazioni prediligendo l'utilizzo di protocolli leggeri.
A dire la verità questo stile architetturale sottolinea con forza l'importanza dell'indipendenza, sia a livello di codice che a livello organizzativo e di processo.
Indipendenza significa anche velocità, abbattimento del time-to-market e l'implementazione di componenti fortemente focalizzati sul "fare una sola cosa", seppur garantendo il massimo della sua ottimizzazione.
Anche la strategia di delivery cambia, l'organizzazione aziendale cambia (seppur non sempre alla stessa velocità della tecnica), cambiano i processi e il modo in cui i team di progetto si organizzano e comunicano tra loro.  
  
Nelle organizzazioni più piccole tutti questi cambiamenti non sono un problema, anzi l'esatto opposto.
É in quelle più grandi che si sente la differenza, quelle che gestiscono un portafoglio di applicazioni costituito da centinaia se non migliaia di applicazioni, dove tali applicazioni sono il frutto di anni di evoluzione e stratificazione e dove i processi sono difficili da cambiare perché richiedono un cambio culturale ad un numero molto elevato di persone.  

In accordo con i principi fondamentali dello stile architetturale a microservizi, anche il governo di tali applicazioni è caratterizzato da uno spinto livello di decentralizzazione, dal momento che ciascun team di sviluppo ha la possibilità di risolvere in autonomia i propri problemi di implementazione in maniera indipendente e massimizzando la velocità di risoluzione e rilascio.  
Tuttavia, se per gli Sviluppatori è diventato quasi indispensabile mantenere tale livello di auto-governo, cosa può significare per Analisti e Manager il concetto di governo di una Architettura a Microservizi? Cosa possiamo fare, come sviluppatori, per fargli dormire sonni tranquilli?  

## Il punto di vista di un Manager
Solitamente i Manager richiedono ai propri team di  avere un senso di conformità e maturità dei componenti dell'ecosistema. In pratica, sempre più spesso vogliono limitare leggermente quella libertà conquistata dagli sviluppatori per evitare l'*anarchia* più completa. Accade sempre più spesso che manager *(e architetti)* impongano una serie di scelte tra cui gli sviluppatori possono scegliere e gli obiettivi che i team devono raggiungere. 
  
Tuttavia accade ancora spesso che i manager restano incerti su quanto sforzo è necessario per far maturare ed uniformare l'architettura e su quali team investire per far si che ciò accada.  
Avere a disposizione una dashboard che indichi loro dove è necessario intervenire potrebbe sicuramente aiutare a garantire che il budget e le priorità siano in linea con gli obiettivi dell'architettura e del business.  

## Il punto di vista di un Analista
Per gli Analisti, il vantaggio fondamentale potrebbe derivare dalla conoscenza, istante per istante, di quali microservizi sono disponibili nei vari ambienti *(sia produttivi che non-produttivi)*, oppure quali risorse sono esposte dai differenti microservizi, in modo da riutilizzare il più possibile quanto già sviluppato ed evitare duplicazioni.  
Inoltre, l'analisi dell'impatto può migliorare in modo significativo quando agli analisti è disponibile una panoramica dei componenti e del modo in cui sono collegati tra loro. Non solo incoraggia gli analisti a identificare e informare i consumatori in merito a un servizio in evoluzione, ma può anche aiutare a evitare di introdurre cambiamenti di rottura dovuti a negligenza o ignoranza.  
  
Proprio come i manager, gli analisti funzionali sono interessati alle funzionalità e alle versioni in arrivo in modo da definire lo stato futuro dell'ecosistema. Soprattutto quando più team stanno lavorando su funzionalità simili, può essere notoriamente difficile evitare duplicazioni e violazioni di contesti limitati. L'uso di una dashboard per definire ciò che sta per accadere, può aiutare a dare loro una visione inequivocabile del panorama attuale e futuro.  

## La Dashboard
Partiamo dallo scenario più semplice possibile, graficando le esigenze di entrambi.  
![esempio dashboard](dashboard_example_sync.PNG)
Mettendo insieme le esigenze di Analisti e Manager potrebbe verificarsi che il minimo comun denominatore tra questi due ruoli sia rappresentabile dalle informazioni di:
- Microservizio Chiamante
- Microservizio Chiamato
- Numero di chiamate
- Tempo medio di request-response (per i colloqui sincroni)
