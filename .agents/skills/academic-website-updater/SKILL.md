---
name: academic-website-updater
description: Aggiorna le pubblicazioni e i working papers del sito accademico da istruzioni in linguaggio naturale, preservando struttura, stile e controlli di pubblicazione.
---

# Academic website updater

Usa questa skill, anche tramite `$academic-website-updater`, per aggiungere, modificare, rimuovere o riordinare voci di Publications e Working Papers. Rispetta anche le istruzioni di `AGENTS.md` nella radice del repository.

## Preparazione

1. Prima di modificare file, verifica branch corrente, stato Git, eventuali conflitti e stato del remoto e del branch di tracciamento. Recupera le informazioni remote con `git fetch` e confronta i commit locali e remoti. Se il remoto non è raggiungibile o il branch di tracciamento non è configurato, interrompi e chiedi istruzioni.
2. Se esistono modifiche locali non salvate, commit locali non pubblicati, aggiornamenti remoti, divergenze o conflitti, interrompi e chiedi istruzioni. Non eseguire automaticamente `reset`, `clean`, `stash`, `rebase` o merge; non sovrascrivere modifiche locali. Riprendi soltanto dopo istruzioni dell'utente e dopo aver verificato nuovamente lo stato.
3. Leggi `research.json` e verifica che `publications` e `working` siano array e che le voci abbiano la struttura esistente. Non introdurre campi non necessari.

## Aggiornamento bibliografico

- Interpreta titolo, autori, rivista o serie, anno, DOI, URL del paper e URL VoxEU forniti dall'utente. Verifica riferimenti e link tramite fonti affidabili quando disponibili; segnala ciò che non è verificabile e non inventare dati. Non chiedere token GitHub nella conversazione e non modificare credenziali o autenticazione.
- Confronta la voce con entrambe le liste usando titoli normalizzati, DOI e URL disponibili. Segnala possibili duplicati e chiarisci le corrispondenze ambigue. Un link VoxEU condiviso da più lavori non è, da solo, prova di duplicazione.
- Se un working paper viene pubblicato su una rivista, chiedi all'utente se trasferirlo in Publications o mantenerlo anche in Working Papers, prima di applicare la scelta. Conserva gli ID delle voci esistenti; per ogni nuova voce assegna un ID univoco coerente con le convenzioni presenti, senza riutilizzare ID esistenti.
- Mantieni i campi `id`, `title`, `citation`, `paperUrl` e `voxeuUrl`, lo stile bibliografico e la formattazione esistenti. Usa stringhe vuote per i link non disponibili; non inserire DOI in un nuovo campo. Mantieni l'ordine cronologico inverso, preservando l'ordine manuale delle voci dello stesso anno, salvo istruzioni diverse. Per i working papers usa la data originaria anziché quella della versione; se la data o la posizione è incerta, chiedi chiarimenti.
- Modifica soltanto `research.json`, salvo autorizzazione esplicita a intervenire su altri file. Non modificare il comportamento di `admin.html`, il layout o le altre sezioni.

## Verifica e pubblicazione

1. Valida il JSON, gli array, i campi e l'unicità degli ID; controlla possibili duplicati e integrità delle informazioni, distinguendo eventuali anomalie preesistenti dalle modifiche introdotte. Controlla il diff pertinente e che non siano stati modificati altri file senza autorizzazione.
2. Mostra all'utente un riepilogo delle modifiche, il diff pertinente e le eventuali verifiche non riuscite. Chiedi un'autorizzazione esplicita prima di eseguire `git commit`; una richiesta generica di aggiornamento non è sufficiente. Non includere nel commit modifiche estranee.
3. Dopo il commit, verifica nuovamente lo stato del remoto e confrontalo con il commit locale. Se il remoto è cambiato o non è verificabile, fermati e chiedi istruzioni senza integrare automaticamente. Mostra il riepilogo e chiedi una seconda autorizzazione esplicita, distinta da quella al commit, prima di `git push`.
4. Dopo il push, comunica l'esito e, se possibile, verifica che GitHub Pages abbia pubblicato le modifiche. Distingui una pubblicazione ancora in corso da un errore verificato.

In caso di errore, interrompi la procedura, spiega il problema e come risolverlo senza alterare i file esistenti. Non eseguire operazioni correttive distruttive o risoluzioni automatiche di conflitti.
