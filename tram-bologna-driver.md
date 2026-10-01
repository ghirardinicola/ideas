# Tram Bologna Driver — Simulatore 3D realistico

Replicare il concetto di *Tokyo Metro Driver* (Steam) applicato al nuovo tram di Bologna (Linea Rossa/Line 1).

## The core idea

Un simulatore 3D realistico dove guidi il tram lungo la linea tranviaria di Bologna. Come nei simulatori di guida ferroviaria giapponesi: cruscotto funzionante, accelerazione/frenata realistica, segnali da rispettare, fermate da centrare, orari da mantenere.

## Esempi / Applicazioni

- Modalità libera: guida senza vincoli, esplorando la linea
- Modalità scenario: rispettare orario, condizioni meteo variabili, gestione anomalie (passaggio a livello, pedoni)
- Percorso didattico: spiegazione del tracciato, delle fermate, della storia della linea
- Supporto per chiunque voglia «provare» la linea senza essere un macchinista

## Architettura / Componenti

- **Motore 3D**: Unity o Godot (l'importante è la scena tranviaria con binari, fermate, città riconoscibile)
- **Fisica del tram**: accelerazione, frenata elettrica/freno di emergenza, inerzia, pendenza
- **Percorso fedele**: mappa della Linea Rossa con tutte le fermate, distanze, tempi di percorrenza
- **HUD cruscotto**: velocità, orario, prossima fermata, segnali
- **Suoni ambiente**: rumore del tram, campanella fermate, annunci stazioni (in bolognese?)

## Note

Idea salvata il 1 ottobre 2026. Riferimento: discussione su Hermes dopo la conversazione sulla frame theory. Da valutare se usare dati OSM per il tracciato preciso.
