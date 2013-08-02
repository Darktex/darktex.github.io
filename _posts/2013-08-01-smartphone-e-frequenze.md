---
layout: post
category : blog
tags : []
title: "Smartphone e frequenze"
image:
  feature: frequency.jpg
---

Ultimamente ho avuto a che fare con l’annoso “problema delle frequenze" dei telefoni. “Perché dovrebbe interessarmi?" potreste chiedermi - dopotutto ogni terminale EU funziona comodamente sulle linee italiane. È vero, ma ci sono due motivi per cui vale la pena saperne qualcosa:

- L’arrivo del 4G in Italia su frequenze diverse rispetto al resto del pianeta
- La possibilità di comprarsi un telefono fuori dall’EU ed usarlo a casa.

Purtroppo rispondere da soli a queste due domande richiede un insieme di competenze che, seppur non specialistiche, non sono banali. Ho quindi pensato di raccogliere qui ciò che so sui vari standard in modo che potesse essere utile: non sono uno specialista e non è il mio campo, quindi potrebbero esserci degli errori o delle interpretazioni errate qua e là. Nonostante ciò, credo di sapermi orientare bene nel panorama smartphone e penso che al termine della lettura sarete in grado di farlo anche voi.

Ho deciso di strutturare questo post in un’ottica “storica". La scelta non è dettata da un reale interesse di storia degli standard, quanto dal fatto che questi standard si sono evoluti come conseguenza l’uno dell’altro e ha senso dare un’occhiata per capire dove sono le differenze. Chi non ne ha voglia può saltare alle conclusioni in fondo (ma non ci capirà molto, temo).

# I nonni analogici, AMPS e TACS (1G)

La telefonia mobile non ha una storia lunghissima: nasce formalmente nel 1978 con uno standard americano, AMPS, sviluppato (ovviamente) dai Bell Labs. Per chi ha fatto un corso di comunicazioni elettriche, AMPS era una tecnologia analogica FDMA (Frequency Division Multiple Access) - in altri termini, ad ogni telefonata veniva allocata una frequenza che veniva usata in esclusiva fino al termine.

La banda di frequenza originariamente assegnata all’AMPS era attorno agli 800 MHz[^com]. Non so come sia andata la procedura di scelta della banda, ma sicuramente non fu casuale: quello che so è che 800 MHz è una frequenza molto bassa per i cellulari, e questo vuol dire maggiore lunghezza d’onda e quindi possibilità di coprire il territorio con meno ripetitori, cosa essenziale per lo sviluppo di una rete ancora agli albori. In Italia AMPS è arrivato in una sua variante che forse qualcuno ricorderà: parlo di TACS, che era a sua volta un FDMA analogico, ma la frequenza era a 900 MHz, non a 800. La prima domanda è: “Perché sono diverse?". La risposta è che l’etere è di proprietà dello Stato (ricorderete che da non molto c’è stata l’asta delle frequenze LTE[^freq]) e che quindi ogni Stato lo suddivide come meglio crede tra tutti i mezzi, che includono televisione, radio pubblica e radio private (le frequenze della polizia per esempio, sulle quali ovviamente trasmettere è reato). Queste frequenze sono state assegnate quando non c’era necessità di intercompatibilità fra i Paesi e quindi la rete cellulare ha dovuto adattarsi, rendendo le cose scomode ai viaggiatori e a chi ha dovuto pensare a un modo di concepire gli standard che permettesse di fare meno casino possibile.

La vita di AMPS e TACS finisce attorno all’inizio degli anni Novanta, in cui si decide di passare al digitale. Le ragioni sono molteplici: la resistenza al rumore probabilmente è il primo.

# Il digitale: CDMA e GSM (2G)

Il passaggio dalla modulazione analogica a una digitale ha visto competere due standard: IS-95 (poi diventato famoso solo come “CDMA", anche se CDMA è solo l’accesso al mezzo) e GSM (che usa TDMA ed FDMA). Le differenze sono concettuali. in breve, GSM alloca una frequenza per ogni N chiamate (divide in frequenza), e poi fa fare alle N chiamate a turno (divide nel tempo). CDMA è totalmente diversa: manda i segnali tutti insieme, codificando ciascuno di questi con un codice pseudocasuale diverso. L’idea è che tutti sentono tutto, ma solo il destinatario del messaggio ha il codice per decrittare il messaggio originale. L’idea sembra assurda ma funziona benissimo: a parità di banda, CDMA consente di farci stare più utenti[^standards].

L’altra grande differenza un po’ strana per gli italiani è che i telefoni CDMA non hanno lo slot per la SIM card. Non c’è! La rete riconosce l’id del telefono e stabilisce se può accedervi o no, oltre a fare il billing[^cdmasim]. Nello specifico, la SIM (Subscriber Identity Module) è una prerogativa tutta del GSM e sostanzialmente è solo un chip che memorizza due ID per gli utenti (l’ICCID e l’IMSI. Il primo è per l’operatore, il secondo è internazionale - è grazie a questo che andate in roaming). In realtà oltre a ciò ci sono anche i numeri del carrier tipo il centro messaggi, il nome del provider (quel “Vodafone IT" che leggete sempre), altri dati del carrier e uno spazio a disposizione dell’utente per salvare messaggi e contatti (lo spazio varia con la memoria della SIM).

Dato che CDMA e GSM sono del tutto ortogonali, possono stare sulla stessa frequenza. A quel punto, la logica ha voluto che si prendesse la frequenza più bassa possibile: dato che sotto gli 800 MHz c’erano già televisione e radio, e a 800 MHz c’era già AMPS (che per quanto vecchio è stato dismesso solo nel 2005), la banda prescelta dagli americani è stata la più vicina disponibile: 850 MHz.

In Europa la situazione era diversa (probabilmente è stato anche più difficile trovare una banda comune fra tutti, dato che il problema del roaming era più sentito che in USA) e alla fine è emerso che l’unica banda che si poteva usare fosse la 900 MHz.

A questo punto, diciamo attorno al 1995-1998, abbiamo già i problemi di oggi: esistono due formati, CDMA e GSM, e oltretutto il GSM americano e quello europeo non sono intercompatibili perché su frequenze differenti.

# Multi-band

In seguito, il numero di utenti è cresciuto a dismisura, tanto da raggiungere (e superare) i limiti teorici di accesso alla rete. Troppi utenti, troppa poca banda. La risposta è semplice: aggiungere più bande e a più alta frequenza in città (ci sta più gente, anche se la lunghezza d’onda è inferiore - cosa che comunque in città non è un problema perché ci sono tanti utenti in poco spazio), tenendo la banda vecchia per le zone rurali e per retrocompatibilità (basta mettere di default la frequenza più alta e se non c’è si va sull’altra).

Questa seconda banda è ancora oggi la principale in città ed è di 1800 MHz in Europa e 1900 MHz in USA (avrei pensato che fosse a frequenza doppia per semplicità di adattamento dell’hw, ma in USA non è così. Le ragioni mi sfuggono, probabilmente c’era qualcos’altro in quella zona di spettro o hanno voluto più banda di guardia, boh) e i telefoni che consentono di usare entrambe le bande sono detti “dual band".

In seguito sono usciti telefoni per chi viaggiava spesso: i cosiddetti tri-band consentivano di usare entrambe le bande del proprio continente + la banda “scarsa" dell’altro. I triband americani supportano quindi 850, 900 e 1900 MHZ mentre quelli EU hanno 850, 900 e 1800 MHz. Ovviamente i quad band eliminano il problema alla radice, consentendo di andare su tutte e quattro le bande.

#GPRS ed EV-DO (2.5G)

Il GSM visto fin qui aveva un grosso limite, cioè quello di essere circuit-switched. In altri termini, un circuito andava creato fra sorgente e destinatario, quand’anche virtuale. Questo impediva, per esempio, di far passare un pezzo della comunicazione da una parte e un altro dall’altra, e soprattutto era un ostacolo (penso) all’introduzione della navigazione Internet su cellulari, dato che Internet è a pacchetti. Per questo motivo è stato introdotto un nuovo protocollo, GPRS (General Packet Radio Service) che appunto introduce il packet-switching anche nei cellulari. Da notare che l’accesso al canale segue sempre una politica TDMA e FDMA come nel GSM normale. Ciò che GPRS cambia è solo la logica con la quale viene gestito il flusso dati: se prima si diceva al singolo utente: “Ti do questo slot per k secondi, durante i quali puoi usare il tuo circuito", con GPRS la cosa diventa: “Ti do k secondi per inviare pacchetti, mandane quanti ne vuoi". Il singolo pacchetto può transitare dove gli pare, in accordo con lo standard TCP/IP che è implementato.

Non ho trovato documentazione su IS-95 o CDMA che dir si voglia, comunque mi sembra di capire che fosse già packet-switched e quindi si potessero usare i dati normalmente.

Infine, EDGE è una tecnologia che aumenta la banda a disposizione del GPRS. Alcuni lo chiamano “2.75G" per differenziarlo dal GPRS normale, che è 2.5G

# UMTS e CDMA2000/EV-DO (3G)

UMTS è l’acronimo di Universal Mobile Telecommunications System e - rullo di tamburi - non è GSM. Ebbene sì, è uno standard del tutto diverso ad ogni livello: tecnologicamente, non usa TDMA ed FDMA ma usa CDMA come il concorrente, ma in un formato diverso detto W-CDMA che non consente intercompatibilità con la rete CDMA di IS-95.

UMTS è partito su una frequenza sua in Europa, la 2100 MHz, ma è poi stato implementato su ogni altra, proprio perché ortogonale a GSM. Notate che la coesistenza sulla stessa banda dello stesso canale di GSM e UMTS non è “a costo zero": non fanno interferenza, però competono comunque per l’accesso al mezzo e quindi c’è meno disponibilità per entrambi. Per questo motivo, UMTS ha bisogno di una frequenza solo sua. Anche UMTS utilizza una cosa simile alla SIM card: si chiama USIM (la “U" sta per “Universal") e non sarebbe di per sé compatibile. Ciò che i carrier fanno è di distribuire un particolare chip integrato chiamato UICC (Universal Integrated Circuit Card) che implementa entrambi gli standard ed usa quello richiesto dalla rete in uso, cambiando se necessario.

UMTS è già packet switched “out of the box" e pensato per la navigazione dati in mobilità: si partiva da 384 kbit/s nella prima release, mentre le ultime arrivano al limite teorico di 42 Mbit/s (non male, eh?).

Dato che UMTS è CDMA richiede anche un nuovo chip per la codifica e decodifica dei dati detto Baseband processor. È questo chip che tende a scaldarsi molto e ad abbassare la vita della batteria quando navigate in 3G, a causa della quantità di dati da decodificare.

Parallelamente, lo standard CDMA ha introdotto IS-2000, che è sostanzialmente un superset di IS-95. L’idea è che, invece di fare come i carrier UMTS che mantengono due tecnologie mutualmente esclusive, si potesse mantenere IS-95 e fornire banda solo a ciò che ne aveva realmente bisogno: i dati. L’idea di per sé non pare stupida: UMTS assegna una banda molto larga anche a chi deve solo telefonare, cosa per la quale basterebbe uno standard 2G. Il nuovo standard IS-2000 mantiene IS-95 per la voce e gli SMS, ma introduce EV-DO, “Evolution-Data Optimized" che è sostanzialmente un tecnologia per il trasferimento dati (e solo quelli) lungo la rete. C’è però un forte dato negativo: a causa di questa configurazione, è impossibile fare una telefonata mentre si naviga, mentre UMTS lo permette senza problemi (perché è tutto un pacchetto e la banda comunque è sempre disponibile in quanto già allocata). Quella che una volta era un’ottimizzazione furba che permetteva di dare più banda ai clienti che la necessitavano si è trasformato in un problema: in America AT&T ha impostato una campagna pubblicitaria sul fatto che Verizon non consente di navigare mentre si telefona[^adatt].

# HSPA e EV-DO rev (3.5G in Europa, 4G in USA)

Siamo ormai giunti a pochi mesi fa: i vari standard HSPA (High-Speed Packet Access) hanno consentito un balzo gigantesco di banda per UMTS. Da quanto ho trovato, HSPA non richiede nuovo hardware al carrier, a cui basta un update del firmware dei suoi controller, mentre lo richiede per il cellulare del cliente. Suppongo che il salto sia stato fatto grazie a una codifica che permette una compressione più aggressiva lato cellulare del cliente (infatti un terminale UMTS vecchio non è compatibile HSPA) unito alla possibilità di far usare al singolo cliente più di una portante, ma non ne so di più. L’evoluzione è passata in tre fasi: prima si è migliorato il solo download (HSDPA), poi anche l’upload (HSUPA) e infine tutto con HSPA+ (detto anche “Evolved HSPA").

Parallelamente, la tecnologia CDMA ha migliorato EV-DO consentendo appunto di aggregare portanti (per questo penso che sia lo stesso trucco di HSPA) con varie “revisions". La banda è paragonabile.

Notate che per gli USA queste tecnologie sono state pubblicizzate come “4G", per cui se comprate telefoni Android americani (tipo il Samsung Infuse 4G che è un Galaxy S HSPA+) sappiate che potrebbero non essere LTE e quindi non “realmente" 4G.

# LTE (4G per tutti)

Siamo infine arrivati a oggi. Oggi il mercato converge verso LTE (Long-Term Evolution), nel senso che anche gli operatori CDMA si sono arresi e hanno smesso di supportare l’ennesima rev di EV-DO (Verizon l’aveva inizialmente proposta, poi si è arresa). LTE è una tecnologia che utilizza FDMA e TDMA e curiosamente è stata proposta da NTT-DoCoMo che è un carrier giapponese CDMA (come Verizon o Sprint insomma). LTE nella sua attuale implementazione ha un limite teorico di 100 Mbit/s in download, ma attualmente è limitato a 70 Mbit/s in tutto il mondo (almeno che io sappia).

Oltre alla velocità di navigazione blazing fast, non usa il chip CDMA come UMTS e non ha necessità di fare decodifica pesante che scalda il dispositivo e uccide la batteria: la mia esperienza personale (iPhone 5, LTE con Verizon in USA e 3G HSPA+ con Vodafone in Italia) è che LTE fa durare la batteria dalle 2 alle 3 volte di più e non scalda il dispositivo. Sembra magia!

Dato che ancora una volta la politica di accesso al mezzo per LTE è ortogonale al predecessore (UMTS), si possono usare le stesse bande - anche se non so come ci si regoli per non confliggere con GSM. Probabilmente GSM perderà canali, o verrà fatto fuori dove c’è compatibilità LTE per tenere solo UTMS / LTE. Non lo so. Comunque ciò che ormai dovrebbe essere chiaro è che un canale diviso con UMTS non può bastare ad LTE, e per questo è stato necessario che gli operatori si comprassero nuove frequenze.

Questo è l’ultimo capitolo dell’opera “Frequenze e confusione" che va in onda ormai da vent’anni.

In USA, si è scelto di non far stare LTE insieme alla rete di precedente generazione. Pertanto, AT&T continuerà usare 850 e 1900 MHz per la voce e per il 3G in UMTS, e si è comprata la banda attorno ai 700 MHz (prendendola dal DVB-H, ormai defunto), progettando di espandersi in futuro sulla AWS (AWS usa la banda da 1700 a 1750 per il download e la banda da 2100 a 2150 per l’upload, per un problema tutto americano di allocazione dello spettro). Verizon mantiene la rete CDMA per 2G e 3G e ha comprato le stesse frequenze per LTE.

In Europa, si è deciso che la banda da allocare non fosse a 700 MHz ma a 800 (sigh). L’asta frequenze 4G tenutasi poco tempo fa era appunto per queste frequenze, che erano prima appannaggio di qualche TV locale analogica. In Europa non c’è nemmeno l’AWS e non si può fare, poiché la banda da 2100 è già occupata tutta dal UMTS. Per evitare problemi, si è pensato di far stare LTE anche sulle vecchie frequenze 900 e 1800 MHz, e di passare eventualmente poi alla 2600 MHz.

# Utilità pratica di queste nozioni

La prima utilità è capire da soli se un dato modello è compatibile con il 4G implementato in casa oppure no. Potreste ricordare che l’iPad 3 fece parlare di sé in EU per il fatto che vantava la compatibiltà 4G LTE quando invece “non era vero". In realtà era vero, ma solo per le frequenze americane: andando a prendere la pagina di Wikipedia, si può leggere sulla destra sotto alla foto che è compatibile LTE a 700 e 2100 MHz. Resta comunque compatibile con HSPA+ con tutte le possibili combinazioni (850, 900, 1,900, 2,100 MHz).

In generale, Wikipedia inglese riporta sempre le frequenze di compatibilità per ogni modalità di quasi tutti i telefoni. Per alcuni le cose sono semplici, per altri meno perché esistono più versioni. Due casi emblematici sono sicuramente il Galaxy S3 e l’iPhone 5.

Il primo esiste in una pletora di versioni diverse, in cui non cambia solo la rete ma anche l’hardware (in USA monta un dual core con 2GB di RAM ed è LTE, in EU un quad core con 1GB e non lo è). Dovreste però ora avere tutti gli strumenti per capire la tabella e se deciderete di comprarne uno straniero su eBay, sapete che fare.

Anche iPhone 5 esiste in diverse versioni. Quello di AT&T, che è quello che si può comprare sbloccato in USA, non sarà mai compatibile con le reti italiane per LTE (per tutto il resto sì, ricordo che il chip UMTS è separato e compatibilissimo). Il modello europeo è il GSM A1429 (quello tedesco) e ha la 2100 americana, la 850 che qualche paese EU vuole usare per LTE e la 1800 che è quella che si potrebbe usare in Europa per partire, affiancando LTE e GSM. Notate come il 1429 CDMA sia un superset della versione GSM: va indifferentemente su CDMA, GSM, UMTS ed LTE ed è un vero world phone. Per concludere il discorso iPhone, se sentite dire che iPhone 5 non è compatibile con LTE italiano, io mi limiterò a dirvi che Vodafone, 3 e Wind in Italia hanno iniziato a mettere LTE sulla 1800 MHz ;-) Ah, con Vodafone serve una nuova SIM: non mi sembra un requisito dello standard (quantomeno io non l’ho trovato, a differenza di UMTS), quindi penso possa essere un modo loro per standardizzare le SIM ed eliminare quelle vecchie.

Facciamo un altro esempio: su eBay si trovano facilmente telefoni top di gamma non recentissimi a poco e niente. Prendiamo il caso di questa versione americana del Desire Z: [http://www.ebay.com/itm/HTC-T-Mobile-G2-4GB-Titanium-T-Mobile-Smartphone-plus-extras-/221170310274?pt=Cell_Phones&hash=item337ec71c82](http://www.ebay.com/itm/HTC-T-Mobile-G2-4GB-Titanium-T-Mobile-Smartphone-plus-extras-/221170310274?pt=Cell_Phones&hash=item337ec71c82)

"Mi girerà in Italia?". Ciò che faccio io a questo punto è guardare su Wikipedia le frequenze.

- Visitiamo Wikipedia: [http://en.wikipedia.org/wiki/T-Mobile_G2](http://en.wikipedia.org/wiki/T-Mobile_G2)
- Leggiamo sulla destra, appena sotto la foto, la voce Compatible networks che recita:
    + 900/2100 or 850/1900 MHz HSPA/WCDMA
    + 850/900/1800/1900 MHz GSM
- Ricordiamoci che la rete italiana GSM è 900/1800 MHz, quindi check
- Ricordiamoci che la rete italiana UMTS/HSPA è 900/1800/2100 MHz, quindi pseudocheck. Il telefono non può usare la banda principale da 2100, ma può andare sulle altre due. Possiamo quindi prenderlo con una certa sicurezza, a patto di non lamentarci se non va veloce come vorremmo in zone dove c’è tanta gente che telefona e che ci usa quelle bande.

Concludo lasciandovi un esercizietto: se volessi comprarmi un Nexus S in America, che cosa mi consigliereste? ;-) [suggerimento: guardate le varie varianti su Wikipedia].

[^com]: Nota per i comunicazionisti: con “attorno" intendo “centrata sugli 800 MHz", non “circa". Da qui in poi ometterò i riferimenti all’ampiezza di banda, e dicendo “800 MHz" intenderò quella banda che vai dagli 800 - x agli 800 + x, dove x dipende dallo standard e fondamentalmente non ci interessa un granché.

[^freq]: Ad esempio [http://www.businessonline.it/news/14128/Asta-frequenze-4G-Lte-chiusa-risultati-e-vincitori-Ricavi-per-Adsl.html](http://www.businessonline.it/news/14128/Asta-frequenze-4G-Lte-chiusa-risultati-e-vincitori-Ricavi-per-Adsl.html)

[^standards]: Per una trattazione più esaustiva, vedi [http://en.wikipedia.org/wiki/Comparison_of_mobile_phone_standards](http://en.wikipedia.org/wiki/Comparison_of_mobile_phone_standards)

[^cdmasim]: "Ma il mio iPhone 5/GS3/Razr HD americano ha eccome lo slot SIM!". Lo so, ma è per LTE e non per CDMA. Andate avanti fino al 4G e lo capirete.

[^adatt]: Eccolo qui: [http://www.youtube.com/watch?v=F0FL1AzCAJ8](http://www.youtube.com/watch?v=F0FL1AzCAJ8)
