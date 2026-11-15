---
name: academic-website-updater
description: Aggiorna riferimenti bibliografici e documenti collegati di pubblicazioni e working papers del sito accademico, preservando struttura e controlli di pubblicazione.
---

# Academic website updater

Usa questa skill, anche tramite `$academic-website-updater`, per gestire voci e documenti di Publications e Working Papers. Rispetta anche le istruzioni di `AGENTS.md` nella radice del repository. Usa percorsi relativi alla radice del repository, senza introdurre percorsi assoluti specifici di un PC.

## Preparazione

1. Prima di modificare file, verifica branch corrente, stato Git, eventuali conflitti e stato del remoto e del branch di tracciamento. Recupera le informazioni remote con `git fetch` e confronta i commit locali e remoti. Se il remoto non è raggiungibile o il branch di tracciamento non è configurato, interrompi e chiedi istruzioni.
2. Se esistono modifiche locali non salvate, commit locali non pubblicati, aggiornamenti remoti, divergenze o conflitti, interrompi e chiedi istruzioni. Non eseguire automaticamente `reset`, `clean`, `stash`, `rebase` o merge; non sovrascrivere modifiche locali. Riprendi soltanto dopo istruzioni dell'utente e dopo aver verificato nuovamente lo stato.
3. Leggi `research.json` e verifica che `publications` e `working` siano array e che le voci abbiano la struttura esistente. Non introdurre campi non necessari.

## Aggiornamento bibliografico

- Interpreta titolo, autori, rivista o serie, anno, DOI, URL del paper e URL VoxEU forniti dall'utente. Verifica riferimenti e link tramite fonti affidabili quando disponibili; segnala ciò che non è verificabile e non inventare dati. Non chiedere token GitHub nella conversazione e non modificare credenziali o autenticazione.
- Confronta la voce con entrambe le liste usando titoli normalizzati, DOI e URL disponibili. Segnala possibili duplicati e chiarisci le corrispondenze ambigue. Un link VoxEU condiviso da più lavori non è, da solo, prova di duplicazione.
- Se un working paper viene pubblicato su una rivista, chiedi all'utente se trasferirlo in Publications, mantenerlo in Working Papers o farlo comparire in entrambe le sezioni, prima di applicare la scelta. Conserva gli ID delle voci esistenti; per ogni nuova voce assegna un ID univoco coerente con le convenzioni presenti, senza riutilizzare ID esistenti.
- Mantieni i campi `id`, `title`, `citation`, `paperUrl` e `voxeuUrl`, lo stile bibliografico e la formattazione esistenti. Usa stringhe vuote per i link non disponibili; non inserire DOI in un nuovo campo. Mantieni l'ordine cronologico inverso, preservando l'ordine manuale delle voci dello stesso anno, salvo istruzioni diverse. Per i working papers usa la data originaria anziché quella della versione; se la data o la posizione è incerta, chiedi chiarimenti.
- Applica la modifica minima necessaria: conserva `voxeuUrl` e gli altri campi non interessati, salvo richiesta esplicita. Gli aggiornamenti ordinari interessano solo `research.json` e, quando la gestione di PDF è esplicitamente richiesta, `papers/`. Non modificare `index.html`, `admin.html`, il layout, il CV, la fotografia o altre sezioni senza richiesta esplicita.

## Documenti collegati

- `citation` contiene il riferimento bibliografico, compresi collana, numero e data della versione quando pertinenti; `paperUrl` identifica il documento apribile dal titolo. Sono indipendenti: una citazione CEPR può collegare una versione degli autori ospitata sul sito. Non dedurre modifiche a un campo dall'altro o dai metadati del PDF. Se è richiesto solo un aggiornamento bibliografico, conserva esattamente `paperUrl` e non modificare, sostituire, rinominare o eliminare PDF; se è richiesta solo la sostituzione del PDF, conserva `citation`.
- Per un PDF locale, usa esclusivamente un file fornito dall'utente: verifica che esista, sia leggibile e non vuoto e chiedi conferma che possa essere reso pubblico prima di copiarlo. Usa `papers/`, creandola se necessario, e un nome descrittivo, stabile, minuscolo e senza spazi; inserisci in `paperUrl` un percorso relativo come `papers/nome-paper.pdf`. Il sito supporta questi percorsi e gli URL HTTP(S) assoluti; verifica che il collegamento sia cliccabile e funzioni su GitHub Pages.
- Non scaricare e ripubblicare automaticamente PDF di editori o collane, né presumere che un file fornito sia la versione ufficiale della collana citata. Non rimuovere o alterare copertine, copyright notice, watermark o informazioni editoriali. Se i diritti sono incerti, chiedi chiarimenti prima della pubblicazione.
- Per un URL esterno fornito, verifica la sintassi e, quando possibile, la raggiungibilità, quindi inseriscilo in `paperUrl`; non scaricare automaticamente il documento e non modificare `citation` senza autorizzazione. Distingui link non raggiungibili da verifiche impedite dalle restrizioni del sito remoto.
- Se non è disponibile un documento, conserva il riferimento e usa una stringa vuota per `paperUrl`, come nello schema attuale. Verifica che il titolo sia visualizzato senza link non funzionanti; se non supportato, proponi la modifica minima senza implementarla automaticamente. L'assenza di un nuovo documento in una richiesta di aggiornamento non autorizza a cancellare un collegamento esistente.
- Per sostituire un PDF esistente, identifica il file e il relativo `paperUrl`, verifica il nuovo file e, se possibile, conserva il nome stabile. Non sovrascrivere senza autorizzazione esplicita; segnala differenze rilevanti di titolo, autori o data rispetto alla citazione e chiedi conferma prima di modificare dati bibliografici non richiesti. Non eliminare automaticamente PDF non più utilizzati: segnala gli eventuali orfani e chiedi istruzioni.

## Verifica e pubblicazione

1. Valida il JSON, gli array, i campi e l'unicità degli ID; controlla possibili duplicati e integrità delle informazioni, distinguendo eventuali anomalie preesistenti dalle modifiche introdotte. Verifica che i percorsi locali corrispondano a file presenti e che i PDF aggiunti siano leggibili e non vuoti; verifica i link esterni quando possibile. Controlla che i campi non interessati siano invariati, `index.html` non sia stato modificato e non vi siano variazioni indesiderate al layout o altri file modificati senza autorizzazione.
2. Mostra le voci e i campi aggiunti o modificati, con valori precedenti e nuovi ove applicabile, i PDF aggiunti, sostituiti o invariati, il diff pertinente e problemi, verifiche non riuscite o informazioni da confermare. Chiedi un'autorizzazione esplicita prima di eseguire `git commit`; una richiesta generica di aggiornamento non è sufficiente. Non includere nel commit modifiche estranee.
3. Dopo il commit, verifica nuovamente lo stato del remoto e confrontalo con il commit locale. Se il remoto è cambiato o non è verificabile, fermati e chiedi istruzioni senza integrare automaticamente. Mostra il riepilogo e chiedi una seconda autorizzazione esplicita, distinta da quella al commit, prima di `git push`.
4. Dopo il push, comunica l'esito e, se possibile, verifica che GitHub Pages abbia pubblicato le modifiche. Distingui una pubblicazione ancora in corso da un errore verificato.

In caso di errore, interrompi la procedura, spiega il problema e come risolverlo senza alterare i file esistenti. Non eseguire operazioni correttive distruttive o risoluzioni automatiche di conflitti.
