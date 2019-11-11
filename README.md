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

## Serve una Dashboard
Partiamo dallo scenario più semplice possibile, graficando le esigenze di entrambi. 
Mettendo insieme le esigenze di Analisti e Manager potrebbe verificarsi che il minimo comun denominatore tra questi due ruoli sia rappresentabile dalle informazioni di:
- Microservizio Chiamante
- Microservizio Chiamato
- Numero di chiamate
- Tempo medio di request-response (per i colloqui sincroni)  
 
Supponiamo di dover governare un parco applicativo composto da 3 applicazioni che comunicano tra loro utilizzando chiamate sincrone. L'app A utilizza i servizi esposti dall'app B e in alcuni casi quest'ultima applicazione utilizza i servizi dell'app C.  
![esempio dashboard](/img/dashboard_example_sync.PNG)  
L'esempio basilare di dashboard vede allora sui nodi le informazioni di Microservizi/applicazioni chiamenti e chiamati, mentre sugli archi le informazioni relative al numero di chiamate e tempi che le applicazioni effettuano tra loro.  
  
l'interrogativo fondamentale è:
> La responsabilità del passaggio delle informazioni con cui popolare la dashboard è delle factory applicative o può essere delegata all'infrastruttura?
  
Una gestione puramente applicativa potrebbe lasciar spazio ad un'ampia eterogeneità di implementazioni. Ciascun team di sviluppo potrebbe scegliere (dal momento che ne ha facoltà) di affidarsi alla composizione di un log più o meno completo, altri alla composizione di header http custom, altri ancora ad un misto delle due implementazioni appena enumerate e così via.  
Per ridurre il numero di casistiche la scelta più scontata è quella di affidarsi alla composizione di un framework di sviluppo di riferimento in modo tale da indirizzare le scelte.
Si traterebbe sempre e comunque della definizione di una linea guida e non di una soluzione implementativa univoca.  
  
Una gestione delegata all'infrastruttura, invece, metterebbe le carte in chiaro una volta per tutte. Sarebbe sicuramente una soluzione che limita il concetto di *Governo Distribuito*, ma parliamoci chiaro, stiamo cercando di evitare che Manager, Analisti e Architetti passino la maggior parte del loro tempo ad inseguire i team di sviluppo per comprendere e uniformare la soluzione da implementare.  
Personalmente credo che la gestione infrastrutturale, tuttosommato, non tolga un così importante grado di libertà allo sviluppo. Certo che se si sta immaginando di rendere *trasparente* allo sviluppo una scelta del genere, lo deve essere per davvero e non può costringere i team di infrastruttura a sincronizzarsi con quelli applicativi.  
  
## Come realizzare una vista di Governo
> Quali sono le informazioni grezze da reperire per costruire una *Vista di Governance*?
>
> Sono sufficienti informazioni dichiarative a design-time o sono necessarie informazioni di run-time?  

Proviamo a partire con la risposta alla seconda domanda. Supponiamo di aver intrapreso lo sviluppo di una applicazione che necessita di intergrarsi con 3 differenti applicazioni.
Tuttavia, il committente cambia lo scenario funzionale, eliminando la necessità di integrazione con una delle tre applicazioni. Il team dev scrive un software allineato con la richiesta, ma non aggiorna la documentazione. 
Il risultato è una applicazione che dichiara una cosa e ne implementa una diversa (sembra fantascenza e invece succede spesso!).
Una ipotetica applicazione di Governance registrerebbe l'indicazione che la nostra applicazione si integra con un numero ed una lista di altre applicazioni errato, quindi potrebbe portare a scelte non corrette, quindi non sarebbe utilizzabile.  
  
Per esclusione siamo arrivati a definire che le informazioni utili alla nostra piattaforma di Governo derivano da misurazioni di Run-Time, ma di cosa?
Esistono due tipologie di informazioni da poter osservare i Log e le Trace.  
  
- **Log**: rappresentano eventi discreti. Ad esempio il debug dell'applicazione o messaggi di errore emessi durante l'esecuzione di una applicazione.
- **Trace**: si riferiscono ad informazioni crelative ad una richiesta/chiamata, cioè un qualsiasi bit di dati o metadati che possono essere associati al ciclo di vita di un singolo oggetto transazionale nel sistema. Ad esempio il testo di una query SQL effettiva inviata a un database o l'ID di correlazione di una richiesta HTTP in entrata.  

Tra le due la scelta migliore in funzione di quanto vogliamo ottenere potrebbe essere quelle delle Trace.  
Ora che ci è più chiaro cosa intercettare come informazioni grezze e dove reperirirle, ci resta solo da definire il come.  
Riprendendo quanto emerso nel paragrafo precedenete, non vogliamo chiedere ai team di sviluppo di pensare anche a questo e al contempo vogliamo rendere la gestione, la raccolta e la propagazione di tali Trace il più possibile uniforme e standard.
La rappresentazione di seguito potrebbe dare uno spunto interessante:  
![](/img/infra_sidecar.PNG)  
  
Aggiungendo un componente di infrastruttura (sidecar) a ciascun microservizio applicativo permette di:
- lasciare inalterato il perimetro applicativo, no extra effort al team dev
- uniformare il comportamento della gestione delle Trace e delle informazioni utili da osservare (ad esempio: **Transaction-Id**, **Applicazione chiamante**, **Applicazione chiamata**, servizio chiamato, **timestamp della richiesta**)
- il comportamento del sidecar può essere esteso per implementare anche altre funzioni come ad esempio lo stato di salute di una applicazione (circuit-braker, che tratteremo in una articolo dedicato)
- iniettare il componente stesso durante la fase di deploy dell'applicazione
  
L'ultimo punto menziona proprio una delle pratiche e metodologie che sta prendendo piede maggiormente nelle architetture a microservizi, ossia il *Service-Meshing*.  
Con gli stessi razionali, il pattern implementativo si adatta anche a scenari asincroni, in cui due o più applicazioni si scambiano eventi.
![](/img/sidecar_async.PNG) 

## Conclusione
Il governo di un parco applicativo progettato secondo lo stile architetturale a Microservizi si fonda sulla possibilità di raccolta e analisi di informazioni che evidenziano sia lo stato di salute di ciascuna applicazione che le relazioni che intercorrono tra applicazioni differenti. Risulta naturale intendere che tali informazioni hanno valore solo se estrapolate dalla misurazione di quanto avviene effettivamente a run-time all'interno di ambienti produttivi. In particolare si pone l'accento sull'importanza dell'analisi delle tracciature e sulla necessaria standardizzazione della loro emissione.  
L'utilizzo e la responsabilità di componenti infrastrutturali, iniettati durante il processo di composizione dell'intero oggetto scalabile, permette ai team applicativi di delegare completamente l'intera gestione dell'*Observability*.
Infine tale comportamento e approcio è adottabile sia in contesti sincroni (http request - response) che asincroni (event messaging/streaming) ed è quindi considerabile come una buona base per aumentare il governo dell'architettura e allo stesso tempo il livello complessivo di maturità nella gestione di applicazioni sempre più distribuite. 
