---
layout: post
category : blog
tags : [git, guida, version control, software]
title: "Guida pratica a git per chi lavora da solo"
---

Questa guida si prefigge l'obiettivo di insegnarvi ad usare git dandovi una serie di "ricette pronte" e linkandovi agli spiegoni più sintetici che ho trovato, in modo da limitare il tempo perso nei pipponi per invece iniziare ad usarlo subito.

Se non sapete che cosa sia git, ne ho scritto una approfondita e appassionata [introduzione](/blog/introduzione-a-git/) che vi invito a leggere. In breve, __se usate Dropbox per salvare il vostro codice nella cloud DOVETE LEGGERE QUESTA GUIDA__.

Questa miniguida vuole insegnarvi ad usare git per salvare il vostro progetto in cloud. È una sorta di "prima parte" che tratta le basi. Prosegue poi nella [Guida a git per chi collabora](/blog/guida-pratica-a-git-per-chi-collabora/).

#Introduzione: che mi frega di usare git da solo?

Come discusso nella [introduzione a git](/blog/introduzione-a-git/), git è valido anche se non si collabora perché tiene __tutta la storia del vostro progetto__ e potete cancellare, modificare o incasinare tutti i file che volete senza avere paura di danni.

#Fase 0: Installazione

Github ha decisamente il tutorial più rapido possibile: <https://help.github.com/articles/set-up-git>.

Già che siete su GitHub, registratevi. È gratuito e avete tutto lo spazio che volete per le vostre repo, a patto che siano __pubbliche__. Le repo private si pagano su GitHub, ma sono gratuite su <https://bitbucket.org>. Vi consiglio di fare comunque la vostra prima repo su GitHub, e poi di passare a Bitbucket per le cose che volete restino private, tipo tesi eccetera.

Non abbiamo ancora finito: bisogna impostare l'accesso via SSH invece che HTTPS. In teoria è opzionale, ma è questione di un secondo e vale la pena farlo. Una volta nella vita (del vostro computer), seguite questi step: <https://help.github.com/articles/generating-ssh-keys>. Una cosa: contrariamente a quanto vi dice lì, potete pure non mettere una passphrase alla vostra chiave ed evitarvi così sbatti extra. Fate semplicemente Invio quando vi chiede la passphrase.

Caveat: almeno per il momento, __non scaricate la loro app__. Prima imparate dal terminale, perché in caso di casino è l'unica cosa che realmente funziona. Poi, una volta che avete il terminale pronto, potete anche passare all'app grafica (io non l'ho fatto comunque).

Nota per chi ha Windows: non dimenticatevi di espandere il riquadro "Need a quick lesson about Git Bash?".

Non abbiamo ancora finito! Ora inserite questi comandi:

`git config color.ui true`

`git config format.pretty oneline`

`git config --global core.editor nano`

Adesso possiamo passare alla prossima fase :)

#Fase 1: prima infarinatura

Leggete [Git: la guida tascabile](http://rogerdudler.github.io/git-guide/index.it.html). Non c'è nulla di più veloce, richiede 5 minuti ma bisogna leggere tutto __con attenzione__. Sono tutti comandi base e sono tutti importanti!

Controllate di aver letto e capito tutti i comandi presenti nella loro pratica _cheatsheet_: <http://rogerdudler.github.io/git-guide/files/git_cheat_sheet.pdf>

#Fase 2: 'ricette' pronte

Usate questa parte della guida per sapere che cosa fare nelle varie situazioni (tornate qui e usate ctrl-F se siete bloccati). Le azioni sono ordinate in modo che le azioni più comuni siano in cima e man mano troviate quelle più rare (eccezione: "Creare una nuova repo" è in cima per aiutare chi deve iniziare). In fondo c'è un link "Più info" per i volenterosi (sempre opzionale).

Tutte queste azioni presumono che usiate il terminale e che siate già nella cartella in cui volete lavorare.

###Creare una nuova repository

`cd <percorso in cui volete creare la repo>`

Ora andate su <https://github.com/new>, date un nome e premete Create Repository (assumo che vi siate già registrati).

A questo punto, copiate i comandi sotto "Create a new repository on the command line". In alto potete scegliere tra HTTPS e SSH - se avete fatto tutto quello che c'era scritto nella fase 0, scegliete SSH.

Più informazioni sui remote: <https://help.github.com/articles/adding-a-remote>

###Variante: migrare un vostro progetto su GitHub

1. Seguite le istruzioni qui sopra per creare una nuova repository. Createla direttamente nella cartella del vostro progetto (fate cd in quella cartella e poi seguite gli stessi step).
2. Aggiornate il remoto col vostro progresso (vedi sotto)

###Aggiornare il remoto col mio progresso
 
Per prima cosa dovete aggiungere tutti i file del vostro progetto allo stage con `git add *`. Poi farete un commit (locale) con `git commit -m "<MESSAGGIO MOLTO INFORMATIVO CHE SPIEGA CHE HO FATTO>"` e infine mandare il tutto a GitHub con `git push`. Questa è di gran lunga l'azione più comune se lavorate da soli! Imparatela a memoria.

In generale, ricordate che __il commit è in locale__, finché non pushate al remoto non arriva niente!

NOTA: Il push può fallire se ci sono conflitti. Questi accadono se lavorate in tanti sullo stesso file. Vedi la sezione sui conflitti! Non abbiate comunque paura di pushare, se va a buon fine non fa casini e se non va a buon fine vi dice dove ha avuto problemi.

###Aggiornare la mia macchina col progresso da remoto

Questo serve se lavorate sul vostro progetto con più computer (che so, fisso e portatile) o se lavorate al progetto con più persone. Se la repository è stata inizializzata come scritto qui, fate semplicemente:

`git pull`

NOTA: Il pull può fallire se ci sono conflitti. Questi accadono se lavorate in tanti sullo stesso file. Vedi la sezione sui conflitti! Non abbiate comunque paura di pullare, se va a buon fine non fa casini e se non va a buon fine vi dice dove ha avuto problemi.

###Cancellare un commit (solo locale)

Se non avete ancora pushato, potete fare 

`git reset --hard <id_commit>`

e la cartella tornerà indietro nel tempo allo stato in cui era quando __quel__ commit era l'ultimo. Per scoprire l'hash del commit a cui volete tornare, fate un `git log`. Mi raccomando ricordate di aggiungere --hard o il comportamento sarà totalmente diverso (interesserà solo la staging area invece che i file nella cartella).

Sintassi alternativa:

`git reset --hard HEAD~n`

dove al posto di `n` ci va un numero. Quel numero indica di quanti commit volete andare indietro nel tempo (es: `git reset --hard HEAD~1` cancellerà l'ultimo commit).

NOTA: Se invece avete pushato è meglio non farlo in questo modo. Vedere sotto.

Vedi anche: <http://git-scm.com/book/en/Git-Basics-Undoing-Things>

###Cancellare un commit già pushato

Se il commit è già stato inviato al server, non si può usare la procedura di prima. Il motivo è che dato che voi siete tornati indietro nel tempo, il server continuerà a credere di avere una versione più recente della vostra e vi dirà che siete voi a dovervi aggiornare[^forcedpush].

Invece di far ciò, si può usare `git revert <id_commit>`. Revert è diverso perché crea un __nuovo__ commit che modifica i file in modo che il risultato sia quello di annullare il commit di cui avete dato l'id. Comodo eh? :D

Più info: <http://gitready.com/intermediate/2009/03/16/rolling-back-changes-with-revert.html>.


###Scaricare tutto un progetto su un altro computer

Andate sul vostro profilo GitHub e troverete tutte le vostre repo. Cliccate sul nome del progetto che volete importare.

A questo punto, se il computer su cui volete importarlo ha git, cliccate su SSH clone URL (in rosso nell'immagine sotto) e copiatelo (il tastino lì sulla destra lo copia già per voi).

Scegliete una cartella sul nuovo computer in cui mettere il progetto e una volta entrati scrivete `git clone <URL COPIATO>`.

Se non avete git, potete scaricare tutto il vostro progetto in .zip con il tasto evidenziato in blu nell'immagine sottostante.

![Guida](/images/blog/GithubExport.png)

###Modificare il progetto di un altro e/o ottenere un framework

GitHub è _social coding_ nel senso che è tutto open source e chiunque può modificare o adattare il codice altrui. Per farlo, c'è il __fork__.

Andate su un progetto su GitHub e premendo il pulsante "Fork" ne aggiungerete una copia al vostro account. La copia non influenza l'originale e avete tutti i permessi di farne ciò che volete. A quel punto basta scaricare il nuovo progetto con un `git clone` come già accennato prima e da lì potete continuarlo con i vostri commit (che saranno solo nel vostro progetto). Qualora vogliate aiutare il progetto originale, potete persino proporre i vostri commit all'autore facendogli una __pull request__.


 
[^forcedpush]: Per gli smartasses: sì lo so che si può fare un push forzato, ma è altamente 'diseducativo' perché se si collabora con altre persone non è saggio far tornare il server indietro nel tempo. Molto meglio imparare la cosa giusta nei fondamentali e non pensarci mai più a vita.



