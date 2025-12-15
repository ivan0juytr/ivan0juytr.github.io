Questo progetto è il sito statico del “Nasometro Digitale”, una piccola web app per stimare in modo indicativo la freschezza degli alimenti.

Descrizione
Nasometro Digitale è un prototipo front-end che gira interamente nel browser.
Usa HTML, CSS e JavaScript vanilla per:

registrare semplici analisi di alimenti

stimare grossolanamente il rischio in base a tempo, categoria e conservazione

visualizzare uno storico e alcune statistiche locali

Tutti i dati sono memorizzati solo nel localStorage del browser.

Struttura del progetto
index.html – Home / dashboard con:

overview del frigo (temperatura e stato sensore)

contatori “OK / da consumare / da eliminare”

ultime analisi registrate

analisi.html – Pagina per analizzare un alimento:

form (nome, categoria, data apertura, luogo, note)

calcolo di una percentuale di “sicurezza”

aggiornamento di statistiche e storico in localStorage

storico.html – Storico analisi:

lista di alimenti analizzati (nome, data, posizione, stato)

filtri (tutti / ok / da consumare / da eliminare)

pulsante per svuotare lo storico locale

impostazioni.html – Impostazioni dell’app:

temperatura frigo predefinita (slider)

flag sensore Bluetooth (on/off)

testo informativo e disclaimer

informazioni.html – Informazioni sul progetto:

spiegazione dell’idea del Nasometro Digitale

obiettivi, limiti, note tecniche e idee future

Tutte le pagine condividono la stessa navbar responsive (stile “app-like”) e un footer coerente.

Dipendenze
Non ci sono dipendenze di build.
Solo due risorse esterne via CDN:

Lucide Icons per le icone SVG (caricate con uno script <script src="https://unpkg.com/lucide@latest"></script> e inizializzate con lucide.createIcons();)

Il resto è puro HTML/CSS/JS, senza framework.

Non è necessario alcun backend: l’app è completamente statica.

Persistenza dati (localStorage)
Le pagine condividono alcune chiavi nel localStorage:

nasometro_fridge_temp – temperatura frigo predefinita (numero, es. 3.5)

nasometro_bluetooth_enabled – sensore Bluetooth attivo ("true" / "false")

nasometro_stats – oggetto con contatori globali:

{ ok: number, soon: number, bad: number }

nasometro_recent_items – array di analisi recenti:

{ name, status, date, location }[]

status: "ok" | "soon" | "bad"

Questi dati vengono letti/aggiornati da Home, Analisi, Storico e Impostazioni.

Per fare test rapidi si possono eseguire in console comandi tipo:

js
localStorage.setItem('nasometro_fridge_temp', '3.5');
localStorage.setItem('nasometro_bluetooth_enabled', 'true');

localStorage.setItem(
  'nasometro_stats',
  JSON.stringify({ ok: 8, soon: 3, bad: 2 })
);

localStorage.setItem(
  'nasometro_recent_items',
  JSON.stringify([
    { name: 'Petto di pollo', status: 'soon', date: '12/12/2025', location: 'frigo' },
    { name: 'Insalata mista', status: 'ok', date: '11/12/2025', location: 'frigo' }
  ])
);
Come eseguire in locale
Clona o copia la cartella con i file .html.

Apri index.html con un browser moderno (Chrome, Edge, Firefox, Safari).

Non serve nessun server: basta il doppio click sul file oppure un semplice static server (es. npx serve o python -m http.server).

Deploy (GitHub Pages / Netlify)
Qualsiasi hosting statico funziona. Un flusso tipico:

crea una repo Git con dentro i file HTML

attiva GitHub Pages (branch main, cartella root)

oppure collega la repo a Netlify / Vercel come “static site”

Non sono richieste build o strumenti extra: il contenuto viene servito così com’è.

Limitazioni e note
Il modello di rischio è volutamente semplice e non basato su linee guida ufficiali.

L’app ha solo scopo didattico / prototipale e non va usata come riferimento per la sicurezza alimentare reale.

Non c’è autenticazione né sincronizzazione: i dati sono legati al singolo browser/dispositivo.
