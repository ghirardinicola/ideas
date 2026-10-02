# Raindrop Crawler — crawling pagine salvate per sintesi accurata

Crawlare i bookmark salvati su Raindrop.io per creare sintesi/riassunti accurati dei contenuti.

## The core idea

Raindrop.io è usato come bookmark manager. L'idea è fare crawling automatico di tutte le pagine salvate (o di una selezione), estrarne il contenuto testuale, e produrre una sintesi ragionata — per tenere traccia di cosa si è letto, cosa è ancora rilevante, e collegare fonti diverse sullo stesso tema.

Esiste già un progetto su GitHub (salvato su Raindrop) per accedere a Reddit via API — potrebbe essere un modello per come interfacciarsi con piattaforme specifiche.

## Esempi / Applicazioni

- Sintesi settimanale di tutti gli articoli/bookmark della settimana
- Collegamento automatico tra pagine che parlano dello stesso argomento
- Generazione di una knowledge base personale partendo dai propri bookmark
- Integrazione con Hermes: su richiesta, «riassumi cosa ho salvato su X» cercando nei bookmark

## Architettura / Componenti

- **Raindrop API** per leggere la lista dei bookmark (collezioni, tag, date)
- **Crawler** HTTP per scaricare il contenuto di ogni pagina
- **Estrattore testo** (trafilatura, readability, o direttamente web_extract)
- **LLM** per sintesi, collegamento tematico, estrazione entità
- **Cache** per non ricrawlare pagine già processate

## Note

Salvata il 1 ottobre 2026. Ci sono progetti su btab/GitHub che mostrano pattern simili (es. accesso a Reddit).
