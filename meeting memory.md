# Meeting Memory

Registri un incontro sul telefono. Qualche minuto dopo trovi la trascrizione testuale già salvata nella tua knowledge base. Nessun copia-incolla, nessun intervento manuale.

## The core idea

Il problema è la distanza tra il momento in cui catturi un incontro (audio sul telefono) e il momento in cui quella conoscenza diventa utile (testo cercabile, consultabile, collegabile ad altri documenti). Oggi questo gap si chiude a mano — trascrivere, correggere, incollare da qualche parte — ed è abbastanza scomodo da non farlo quasi mai.

L'intuizione è che il telefono è già il punto di raccolta naturale, e che registrazione e trascrizione possono chiudere quel gap automaticamente. Il file audio è l'unico input che l'utente deve produrre. La trascrizione testuale è l'output immediato. Tutto il resto — riassunti, estrazioni, elaborazioni — è opzionale e può essere fatto in un secondo momento, partendo dal testo accumulato.

## Examples / Applications

Chi visita musei, mostre o luoghi culturali e vuole tenere traccia delle spiegazioni delle guide, delle impressioni a caldo, delle cose da approfondire — senza distrarsi a scrivere durante la visita. Chi partecipa regolarmente a eventi (conferenze, presentazioni, incontri pubblici) e vuole un archivio consultabile di quello che ha ascoltato, non solo le slide. Chi è attivo in un'associazione — riunioni di direttivo, assemblee, gruppi di lavoro — e vuole che i verbali esistano senza che qualcuno debba farsi carico di scriverli. Chi fa colloqui, interviste o conversazioni significative e vuole poterle rileggere con calma in seguito.

## Architecture / Components

Il sistema ha due pezzi fondamentali. Come sono collegati dipende dall'implementazione — possono vivere in un'app unica, in un workflow di automazione, o in pezzi separati.

**La cattura.** L'utente registra l'audio sul telefono. Il trigger verso la trascrizione può avvenire in modi diversi: automaticamente quando il file viene salvato, manualmente con un tap, tramite sync verso uno storage intermedio. La scelta dipende dal contesto — un'app dedicata può fare tutto in locale, un'automazione può richiedere un passaggio cloud. Quello che non cambia è il contratto: entra un file audio, esce una richiesta di trascrizione.

**La trascrizione.** Il file audio viene passato a un servizio di speech-to-text. La scelta del servizio dipende dalla lingua degli incontri e dall'infrastruttura disponibile — GCP Speech-to-Text, OpenAI Whisper, Azure Speech, o qualsiasi altro motore accurato nella lingua usata. Il testo risultante viene salvato nella knowledge base dell'utente con data e titolo derivati dal file o dalla data di creazione.

## Operations

**Registra e dimentica.** L'utente registra, chiude il telefono. Entro pochi minuti il testo è disponibile. Non c'è un secondo step obbligatorio.

**Ritrova per contenuto.** La trascrizione completa è testo ricercabile. Qualsiasi tool di ricerca della knowledge base trova qualsiasi parola pronunciata — nomi, luoghi, concetti. Non serve ricordare quando era l'incontro, basta cercare cosa si è detto.

**Revisione periodica.** Una volta ogni tanto — non necessariamente subito dopo ogni incontro — l'utente passa in rassegna le trascrizioni accumulate e le elabora in blocco con un LLM: riassunti, estrazione di temi ricorrenti, connessioni tra incontri diversi, note personali. Questo momento di revisione è separato dalla cattura per design: permette di fare sintesi con più contesto, confrontando più incontri insieme invece di elaborarli uno per uno a caldo.

**Estrazione strutturata.** Dalla revisione periodica possono emergere output strutturati: una lista di luoghi da rivedere, un elenco di temi affrontati nelle riunioni di un'associazione, un diario di viaggio costruito a posteriori dalle registrazioni. La forma dipende dall'uso — il sistema fornisce la materia prima, l'utente decide cosa farne.

## Why this works

Il motivo per cui questo pattern funziona è che separa la cattura dall'elaborazione. Registrare durante un incontro è quasi a costo zero — il telefono è già in tasca. Elaborare subito dopo è costoso — sei stanco, hai altro da fare, il momento è passato. Posticipare l'elaborazione a un momento dedicato, con più trascrizioni da guardare insieme, produce output di qualità superiore con meno sforzo totale.

Il secondo motivo è che fermarsi alla trascrizione come step automatico è una scelta deliberata. Un sistema che produce automaticamente riassunti dopo ogni incontro sembra più potente, ma introduce un LLM nel path critico — con costi, latenza e possibili errori su ogni singolo file. La trascrizione testuale è deterministicamente utile: il testo è fedele all'audio, sempre. L'elaborazione LLM è più preziosa quando viene applicata in modo riflessivo, su un corpus, non in modo automatico su ogni file.

Il terzo motivo è la modularità. L'app di registrazione cambia? La trascrizione rimane. Si passa da un servizio di speech-to-text a un altro? Il resto non cambia. Si vuole aggiungere un'elaborazione automatica su ogni file in futuro? È un'estensione, non una riscrittura.

## Note

Questo documento è intenzionalmente astratto. Le scelte di implementazione — come viene triggerata la trascrizione, se passa per il cloud o rimane locale, quale servizio di speech-to-text, quale knowledge base — dipendono dal tuo stack, dal tuo budget e dalla lingua dei tuoi incontri. Dai questo file al tuo agente e digli: "Costruiscimi questo, adattato al mio contesto." Le domande che farà sono quelle giuste.
