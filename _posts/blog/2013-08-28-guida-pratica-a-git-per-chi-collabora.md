---
layout: post
category : blog
tags : [git, guida, version control, software]
title: "Guida pratica a git per chi collabora"
---

Questa guida si prefigge l'obiettivo di insegnarvi ad usare git dandovi una serie di "ricette pronte" e linkandovi agli spiegoni più sintetici che ho trovato, in modo da limitare il tempo perso nei pipponi per invece iniziare ad usarlo subito.

Se non sapete che cosa sia git, ne ho scritto una approfondita e appassionata [introduzione](/blog/introduzione-a-git/) che vi invito a leggere. In breve, __se usate Dropbox per salvare il vostro codice nella cloud DOVETE LEGGERE QUESTA GUIDA__.

Questa miniguida vuole insegnarvi ad usare git per lavorare con più persone allo stesso progetto. È una sorta di "seconda parte" che dà per scontato che sappiate le basi affrontate nella [guida precedente](/blog/guida-pratica-a-git/).

#Conflitti: che fare?

I conflitti nascono quando due o più persone lavorano indipendentemente partendo dalla stessa versione e vogliono poi pushare i propri cambi (vedi la situazione che ho citato nell'[introduzione](/blog/introduzione-a-git/) quando parlavo di Dropbox).

###Caso semplice: il conflitto riguarda solo la versione, non i file. In altri termini: Tizio ha lavorato su file diversi da quelli di Caio


In questo caso, git fa il lamentoso ma poi lo risolve da sé con un merge ricorsivo. Per farlo, __git crea per voi un altro commit__ in cui fa il _merge_, cioè si occupa di sovrascrivere ogni file con la sua versione più recente (GitHub riceve in push le novità di Caio mentre Caio riceve le novità dal server di GitHub pushate precedentemente da Tizio). L'unica cosa che vi chiederà è un messaggio per questo nuovo commit, e per farlo __vi aprirà direttamente un editor di testo nel terminale__. Non panicate! Scrivete qualcosa (o anche uscite e basta, e rimane un messaggio di default). Mi raccomando: __non uscite dal terminale__, ma solo dall'editor di testo DENTRO al terminale (se avete copiato i miei comandi extra, sarà NANO). Di seguito riporto come si esce di default sui text editor in terminale più comuni e come riconoscere che cosa avete:

- NANO: Premete Ctrl-x e in basso vi chiederà se salvare o meno a cui potete rispondere con _y_ o _n_ (Nano lo riconoscete perché vi dice tutte le shortcut da tastiera in fondo).
- Vim: Premete Esc, poi scrivete :q! incluso il punto esclamativo (Se è Vim, provando a scrivere una parola che non contenga né _a_ né _i_ non ci riuscirete - dovrete prima premere uno di quei due tasti).
- EMACS: Premete Ctrl-x e poi Ctrl-c (Se è EMACS, vedrete una barra di un altro colore rispetto allo sfondo che occupa la penultima riga ma potrete scrivere fin da subito).

###Caso generale: conflitti a livello di singolo file

Basta vedere questo esempio pratico che è ottimamente commentato: <http://stackoverflow.com/questions/161813/how-do-i-fix-merge-conflicts-in-git/3407920#3407920>. (la risposta linkata e quella successiva sono super-informative e da sole bastano per praticamente tutti i casi).

Una nota sul merging: 

Notate la risposta sotto:

`git checkout --ours` vuol dire che tieni la versione DEL SERVER

`git checkout --theirs` vuol dire che tieni la versione TUA, locale

Più info sui conflitti in generale: <http://genomewiki.ucsc.edu/index.php/Resolving_merge_conflicts_in_Git>.

###'Na chicca: lo stash

Nel caso in cui steste lavorando a dei cambiamenti e il vostro collaboratore vi chiama dicendogli che c'è un bug urgentissimo da fixare siete nelle canne: il vostro progresso non può venir pushato perché non è ancora pronto e non farebbe funzionare più nulla, ma non potete tenerlo nella vostra cartella perché ora dovete lavorare a dell'altro.

La soluzione? Stash! È come avere un "posto sicuro" in cui mettere il vostro progress. Funziona come uno stack.

`git stash` vi riporta la cartella locale allo stato dell'ultimo pull (quindi in linea col server) E si salva il vostro progresso locale da parte.

A quel punto pullate, lavorate sulla patch, la pushate e tutto e quando siete pronti, basta fare un `git stash pop` per far ricomparire le vostre modifiche nella vostra cartella (occhio che questo è un vero e proprio merge quindi può causare conflitti). Fatto!