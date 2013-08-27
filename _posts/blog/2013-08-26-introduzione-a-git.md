---
layout: post
category : blog
tags : [git, version control, software]
title: "Introduzione a git"
---

Quando nomino _"Linus Torvalds"_, tutti sanno dirmi la sua creazione più di successo - parlo ovviamente del kernel Linux.

Ciò che però molti non sanno è che nel 2005 Torvalds ha creato un altro grande progetto open source, che ha avuto uno strabiliante successo (anche social, vedere dopo) e che è un tool utilissimo per ogni informatico.

Ho quindi pensato di creare una guida per insegnarvelo. Dato che c'è tanto di cui parlare, ho diviso la guida dall'introduzione: la guida è più che altro una _cheat sheet_ con le ricette pronte in modo che possa essere un riferimento permanente, mentre questa è un'introduzione da leggere una volta nella vita solo se non si sa già che cos'è git.

Quindi, chi non conosce git continui a leggere (la faccio breve), chi invece pensa di usare questa guida solo per le recipes salti direttamente alle guide:

- [Guida base (senza collaborazione)](/blog/guida-pratica-a-git/).
- [Guida a git per chi collabora](/blog/guida-pratica-a-git-per-chi-collabora/).

#Che cos'è git?

Git è un software di _version control_, cioè un software che si preoccupa sostanzialmente di due cose:

1. Salvare il vostro lavoro nella cloud __tenendo traccia di ogni salvataggio__.
2. Se lavorate ad un progetto con altre persone, ridurre il più possibile i conflitti e soprattutto dare la garanzia che ogni conflitto verrà trovato.

Se programmate, questi due bisogni non sono né rari né comuni: sono __essenziali__ in _qualsiasi_ progetto facciate, dal progettone in C++ di migliaia di righe di codice al documento in Word[^git-word]. Che fare infatti se mi esplode il computer il giorno prima della consegna della tesi? O me lo rubano?

###Perché non Dropbox
Molte persone risolvono questo problema con Dropbox e/o Google Docs: __non fatelo!__ Ci sono tantissime ragioni per cui usare Dropbox per queste cose è una follia.

1. Se lavorate da soli, Dropbox salva solo l'ultima versione del file. Con i documenti word la cosa può anche andarvi bene, ma con il codice questo è pericoloso. La norma in un progetto è che lo sviluppo sia _incrementale_: in altri termini, voi fate del codice che funziona e fa tutto per benino e il vostro capo o supervisor vi dice che vuole che aggiungiate una nuova feature. Per fare la nuova feature, il vostro codice passerà da _funzionante_ a (si spera per poco tempo) _non funzionante_. Mettete che ci lavorate una settimana, poi non c'è più tempo oppure trovate un altro modo per farlo ma ora nel codice c'è casino e vorreste ripartire. Le cose sono semplici: con git potete, con Dropbox no[^dropbox].
2. Se lavorate con una o più altre persone, gli svantaggi che ho elencato finora vi sembreranno scherzi in rapporto ai drammi umani che affronterete voi. Intanto, dovete come minimo mettervi d'accordo prima su chi modifica quali file in un progetto e sperare che i vostri alleati possano attenersi in pieno (che non debbano cioè andare a toccare altre funzioncine in giro per poter andare avanti). Poi, il problema del non avere versioni intermedie viene amplificato: se siamo in tre, magari il codice andava finché ci ha lavorato Tizio, poi Caio ha fatto una cazzata e non va più nulla. Ancora una volta, con git in 1 secondo si torna indietro. Con Dropbox ci vuole almeno mezz'ora. Tutti questi problemi compaiono nel _caso ottimo_, quello in cui ognuno se ne sta a lavorare sui suoi file. Se per caso (succede sempre) dovete lavorare in due sullo stesso file, è la morte. Si creano situazioni tipo questa:
    - Sono le 10 del mattino. Tizio si mette a lavorare sul codice: prende l'ultima versione su Dropbox fatta da Sempronio ieri notte
    - Sono le 11 del mattino. Caio si mette a lavorare sul codice: poiché Tizio sta ancora lavorando, prende anche lui la versione di Sempronio.
    - Sono le 18. Tizio ha finito, mette la sua versioncina su Dropbox e se ne va.
    - Sono le 19. Caio ha finito, e fa altrettanto.

    Il risultato è ovviamente che __tutto il lavoro di Tizio scompare__. È vero che lui avrà ancora la sua copia locale, ma se la cosa passa inosservata (immaginate che i due abbiano lavorato su un file in comune in un progetto di 300 file), la prossima volta che Tizio torna a lavorare la cancellerà per andare avanti.

###Git contro altri software simili

Tutto il discorso fatto fin qui si applica non soltanto a git ma a tutti i software che fanno cose simili come SVN, Mercurial, CVS e tantissimi altri.

Non starò qui a fare guerre di religione, ma git è semplicemente il più veloce perché è nato per necessità: il kernel Linux è un progetto gigantesco, in cui collaborano un'infinità di persone e serviva un software adeguato. Non trovandolo, Torvalds se lo è scritto[^git-history].

Non solo: git ha il vantaggio di avere __rivoluzionato il modo in cui si fa codice__. Grazie a git sono nati siti di _social coding_ come GitHub e Bitbucket, e questo ha realmente fatto avanzare la cultura open source di un bel po' (lettura consigliata: <http://www.wired.com/opinion/2013/03/github/>). Si parla tanto di open data nella pubblica amministrazione, cosa prima impensabile, e io credo che la rivoluzione di GitHub e soci abbia realmente influito nel formare questa linea di pensiero.

Se vi ho convinti, è l'ora di iniziare a sporcarsi le mani!

[Guida base (senza collaborazione)](/blog/guida-pratica-a-git/).

[^git-history]: La storia è un po' più complicata, vedi <http://en.wikipedia.org/wiki/Git_(software)#History>.

[^dropbox]: Qualcuno di voi a questo punto starà pensando "Vabbè ma io lo faccio rinominando il progetto alla versione a cui sono arrivato così salvo due copie". Bravi! Immaginatemi con [la faccia di Willy Wonka](http://ct.fra.bz/il/fz/se/i49/5/3/24/f_461e16abac.jpg) mentre vi dico "Raccontami ancora quanti file con nomi strani hai nella cartella, da Project-1-funziona a Project-bozza-supervisor-17 passando per Project-qui-mi-pare-andasse". In git ogni cambiamento si commenta con un messaggio (obbligatorio) perciò sai sempre che cosa fa una certa versione.

[^git-word]: Va detto che i file .doc e .odt sono binari e non testuali. Non è un problema per git! Bisogna solo aggiungere un filtro in un file di configurazione, roba da 30 secondi. Più informazioni qui: <http://git-scm.com/book/ch7-2.html>, andate sotto "Diffing Binary Files" o cercate "word" con ctrl-F.