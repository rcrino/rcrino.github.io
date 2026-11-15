# Istruzioni per il repository

Questo repository contiene il sito accademico personale dell'utente, pubblicato tramite GitHub Pages. `index.html` gestisce il layout e carica da `research.json` i dati bibliografici degli array `publications` e `working`.

- Per gli aggiornamenti bibliografici ordinari modifica esclusivamente `research.json`; usa anche `papers/` solo quando l'utente richiede esplicitamente la gestione di PDF. Riferimento bibliografico e documento collegato sono indipendenti: conserva i campi e i PDF non interessati dalla richiesta. Non modificare `index.html`, `admin.html`, layout, fotografia, CV, altre sezioni o configurazioni senza una richiesta esplicita dell'utente.
- Prima di modificare file, verifica lo stato Git, il branch corrente e l'eventuale presenza di modifiche remote. Non sovrascrivere modifiche locali. Non eseguire operazioni Git distruttive né risolvere automaticamente conflitti.
- Non eseguire mai `git commit` senza un'autorizzazione esplicita dell'utente, richiesta dopo aver mostrato un riepilogo delle modifiche. Una richiesta generica di aggiornamento non costituisce autorizzazione.
- Non eseguire mai `git push` senza una seconda autorizzazione esplicita, distinta da quella al commit e richiesta dopo aver mostrato il riepilogo delle modifiche. Una richiesta generica di aggiornamento non costituisce autorizzazione.
- Non modificare credenziali, token o configurazioni di autenticazione.
