Q# Observability in Distributed Systems

## Slide 1 - Title
- **Title:** Observability in Distributed Systems
- **Subtitle:** Microservices, Kubernetes, and Beyond
- **Author:** Fabio A. Ciraci

## Slide 3 - Microservices and Kubernetes
- What are Microservices?
- Role of Kubernetes in orchestration

## Slide 2 - Observability
- Why Observability Matters
- Monolith vs Microservices (brief comparison)

## Slide 7 - Traditional Observability Pipeline
- Data Collection
- Data Ingestion
- Insight Generation

## Slide 4 - The Three Pillars of Observability
- Logs
- Metrics
- Traces
## Slide 5 - Deep Dive into the Pillars (Optional)
- Slide per pillar (detailed explanation if needed)

## Slide 6 - eBPF: Modern Observability
- What is eBPF?
- Benefits for low-level performance and security monitoring

## Slide 8 - Advanced Observability: QoS-aware Orchestration
- Introduction to Edge Computing
- Why QoS matters at the edge

## Slide 9 - QoS Requirements
- **Functional Requirements:** FR1–FR4
- **Non-Functional Requirements:** NFR1–NFR2
- Use a table for clarity

## Slide 10 - System Architecture
- Control Plane vs Execution Plane
- Add a diagram if possible

## Slide 11 - Conclusion
- Observability is evolving
- Need for intelligent, scalable orchestration

## Slide 12 - Q&A
- Open for questions


# Discorso

## Intro
Buongiorno, sono qui per presentarvi il mio survey su ciò che ho trovato in queste settimane di ricerche e anche per proporvi quello che vorrei fosse il progetto su cui concentrare i prossimi mesi della borsa.

## Agenda
Questa è l'agenda del mio speech, ovviamente per chiarire il contesto generale ho inserito alcune sezioni molto base. Quindi Archietturea a microservizi, orchestrator, monitoring e observability, ma sarò veloce su queste.

## Architetture
Fra le architetture ho osservato prima di tutto l'aspetto strutturale, quindi con un'architettura monolitica e una a microservizi.

Le differenze maggiormente evidenziate sono sulla scalabilità, che ovviamente in architetture monolitiche è impossibile senza scalare tutta l'applicazione e quindi creando un overhead mostruoso anche se si vuole scalare un solo blocco del code. 
Cosa che nell'architettura a microservizi è molto semplice e dinamica. 

Per quanto riguarda la modularità possiamo dire che è un'altro punto a favore delle architetture a microservizi che ovviamente se hanno bisogno di aggiornare solo una parte dell'applicazione possono permetterselo velocemente e senza bloccare tutta l'applicazione. 
Nell'approccio monolitico invece questo è impossibile perchè per aggiornare o ricompilare anche solo una parte dell'applicazione si rende necessario ricompilaret tutto il codice.

## Orchestrator
Gli orchestrator sono i tool usati per la gestione di un sistema a microservizi e fra i più utilizzati spicca `Kubernetes`, che è un progetto open capace di girare su qualsiasi tipo di cluster.

## Monitoring e Observability
La differenza tra monitoring e observability sta nell'approccio e nella visione che si cerca di dare al design del software.
Il monitoring si chiede: "il sistema sta funzionando in questo momento?", se sì, non si pone il problema di quando non funzionerà.
Se invece il sistema non sta funzionando manda un'alert, potremmo dire che il sistema di monitoring non è basato sulla prevenzione del danno, ma sulla cura quando questo accade. O meglio, quando è già accaduto.

L'observability invece cerca di adottare un'approccio diverso. Con l'observability si cerca di capire se il sistema sta funzionando come aspettato. L'approccio si differenzia perchè non cerca di riparare il danno quando questo accade, cerca piuttosto di capire come evitare che il danno accada. 
Quindi l'observability si propone come una visione dove il design stesso dell'applicazione ci comunica lo stato di quest'ultimo.

## La pipeline dell'observability
L'observability si concentra sulla ricezione di informazioni da parte dei collectors che ricevono informazioni. Queste informazioni sono ingerite e con questo intendiamo parsate, commutate e tramutate in informazioni che poi possono essere graficate per comprendere come certi eventi possono essere correlati e capiti.

## Pillars of observability
Le informazioni della slide precedente sono 3 e si chiamano appunto i piloni dell'observability.

I logs:
che sono informazioni stringate e che per essere usati vanno parsati e commutati in informazioni di più alto livello

le metriche:
che sono invece valori numerici e che per essere utilizzati devono essere combinati a comporre un grafico

le tracce: 
le tracce sono un tipo di informazioni che ci dicono come è stato risolto un particolare processo, ovvero quali sono i componenti che sono stati chiamati, quanto è stato speso in termini di tempo per ogni componente.

## Observability tools
Quali sono i tool che si possono usare per l'observability:
ce ne sono di due tipi, quelli alto livello e quelli basso livello.

Quelli ad alto livello permettono di fare un'instrumentazione (che significa dotare l'applicazione di quei blocchi di codice necessari per inviare i tre pilastri) appunto ad livello, dovrebbero essere più semplici da setuppare e gestire e dovrebbero. 
Inoltre dovrebbero essere application oriented e per questo anche più. 

Quelli invece a basso livello dovrebbero essere leggermente più complessi da gestire e setuppare, però mi aspetto che siano più scalabili. Lavorando su un livello molto più in basso rispetto a quelli high level mi aspetto che siano anche più accurati nelle metriche e che possano registrare metriche non solo legate all'applicazione ma anche alla possibilità di capire come le connessioni e la rete sta comportandondosi, ovviamente essendo poi basate sul livello del kernel, mi aspetto che serva lavorare con un solo linguaggio, il C, anche se molti tool che ho visto permettono di usare strumenti proprietari invece che direttamente il C.


## QoS-aware orchestration
Durante questo periodo di ricerca ho anche cercato di avere una maggiore comprensione di sistemi QoS-aware, in particolare ho concentrato le mie forza su ricerche cloud-edge.

In sistemi cloud edge si deve cercare di incorporare l'observability su metodi che siano basati sui livelli di servizio e che facciano leva sulle negoziazioni con i livelli inferiori per avere buoni risultati. Inoltre c'è la necessita di creare livelli differenziati in base ai livelli di pagamento dell'utente.

## multi-cluster orchestratio
inoltre per avere dei buoni livelli di servizio si può scegliere di partizionare il network e in questo caso si devono creare soluzioni che supportino il multicluster.

per la gestione del multicluster si possono adottare tre modelli:

Liquid Computing: in questa strategia non ci sono cluster master e cluster slave, ma solo peer. I peer sono cluster tutti uguali fra loro che una volta entrati nella catena diventano parte del "metallo liquido di quest'ultima", tramite un processo che si chiama offloading è possibile scegliere quali namespace gestire con un cluster remoto e se qualcosa viene inserito all'interno di questo namespace viene automaticamente deployato sul cluster remoto, questa strategia sfrutta un metodo che è quello del nodo virtuale per effettuare il deploy. 
Ovviamente si può anche scambievolmente deployare un nodo virtuale su due cluster, in modo da renderli dei peers.

Hub-spoke: in questo caso c'è una struttura master-slave ma si concentra principalmente sulla gestione continua dei cluster, che non necessitano di avere contatto diretto con il master, in questo modo il master non è oberato di lavoro e può gestire in maniera autonoma anche una propria parte del workload. In ultimo va detto che i cluster slave sono molto indipendenti, quindi fanno polling con un tempo definito al master per sapere se ci sono aggiornamenti, nel caso il master crashasse non c'è un vero problema perchè continuerebbero a operare. Ovviamente per questa sua natura di polling in maniera bottom up, il sistema non è reattivo a meno di aumentare la frequenza di polling che potrebbe rendere inutile l'avere un sistema di questo tipo.

Master-slave: qui la dipendenza fra il master e gli slave è molto più forte e sentita, il master controlla gli slave in maniera continuativa e costante, notificando ogni cambiamento, questo sistema rende la struttura più reattiva ai cambiamenti impartiti, ma anche molto maggiore l'overhead. Dato che c'è una dipendenza forte tra il master e lo slave alcuni tool come rancher hanno implementato dei sistemi di fail-recovery dove se l'agent su uno dei nodi slave smette di rispondere, uno dei proxy che si trova nei namespace fa le veci di questo agent.

# Proposta
La mia proposta si concentra sullo studio dell'observabilità con tool low level e con tool high level.
E poi di studiare un'approccio ibrido di ossevabilità low level ma usando tool di exporting che solitamente utilizzerebbero metriche raccolte al livello 7.

In fine vorrei fare un confronto per capire quali sono i livelli di overhead per le due soluzioni, quale tipo di tool sono più semplici in termini di usabilità e fare un confronto generale sull'accuratezza di queste due soluzioni.