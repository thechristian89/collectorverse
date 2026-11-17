# CollectorVerse Blueprint v1.0 FINAL

# Indice

1. Vision e Fondamenta
2. Utenti e Privacy
3. Abbonamenti e Monetizzazione
4. Catalogo Universale
5. Sistema Scansione
6. Catalogo Collaborativo
7. Marketplace e Matching
8. Gamification
9. Esperienza Utente
10. Dashboard Amministratore
11. Strategia di Lancio e Crescita


---

# Parte 1 - Vision e Fondamenta

---

# Parte 2 - Utenti • Privacy • Sicurezza • Recensioni • Gestione Account • Ruoli • Profili

---

# Parte 3 - Abbonamenti • Monetizzazione • Pubblicità • Scansioni • Bundle • Pacchetti

# Modello Economico

CollectorVerse utilizza un modello **Freemium**.

L'accesso alle funzionalità fondamentali di catalogazione deve essere gratuito, mentre le funzionalità avanzate possono essere abilitate tramite piani di abbonamento.

La monetizzazione non deve compromettere l'utilizzo essenziale della piattaforma da parte dei collezionisti.

---

# Piani Disponibili

CollectorVerse supporta i seguenti piani:

```text
Free

Premium

Premium Plus

Commerciante
```

Ogni account può possedere un solo Piano attivo alla volta.

---

# Piano Free

Il Piano Free consente l'utilizzo delle funzionalità fondamentali della piattaforma.

## Funzionalità Incluse

- Catalogo Universale
- Collezioni Personali
- Wishlist
- Ricerca Utenti
- Visualizzazione Profili Pubblici
- Visualizzazione Collezioni Pubbliche
- Visualizzazione Wishlist Pubbliche
- Follow Categorie
- Follow Collezioni
- Follow Serie
- Follow Oggetti
- Follow Utenti
- Follow Commercianti
- Mappa Commercianti
- Scansioni giornaliere
- Catalogo Collaborativo
- Ricezione Richieste di Contatto
- Ricezione Messaggi
- Risposta alle Conversazioni ricevute

## Limitazioni

Non può:

```text
❌ avviare nuove Conversazioni

❌ pubblicare Annunci Marketplace

❌ utilizzare il Matching

❌ comparire nella Mappa Utenti
```

---

# Piano Premium

Include tutte le funzionalità del Piano Free.

## Funzionalità Aggiuntive

```text
✅ avviare Conversazioni

✅ utilizzare la Chat completa

✅ creare Annunci Marketplace

✅ utilizzare il Matching
```

---

# Piano Premium Plus

Include tutte le funzionalità del Piano Premium.

## Funzionalità Aggiuntive

```text
✅ Mappa Utenti

✅ Geolocalizzazione avanzata

✅ Matching avanzato

✅ Filtri geografici avanzati

✅ Ricerca geografica avanzata
```

---

# Piano Commerciante

Il Piano Commerciante è destinato a:

- negozi
- fumetterie
- card shop
- rivenditori professionali
- attività commerciali specializzate nel collezionismo

Include tutte le funzionalità del Piano Premium Plus.

---

## Profilo Negozio

Ogni account Commerciante dispone di una pagina negozio dedicata.

Il Profilo Negozio può mostrare:

- Logo
- Banner
- Descrizione attività
- Sito Web
- Indirizzo
- Orari di apertura
- Recapiti pubblici
- Categorie trattate

---

## Mappa Commercianti

I Commercianti possono apparire nella Mappa Commercianti.

La presenza sulla mappa è controllata dal titolare dell'attività e soggetta alle impostazioni Privacy.

---

## Statistiche Professionali

I Commercianti possono accedere a statistiche dedicate.

Esempi:

- visualizzazioni profilo
- visualizzazioni annunci
- click sui recapiti
- richieste ricevute
- conversioni marketplace

---

## Commerciante Verificato

Gli Amministratori possono assegnare lo stato:

```text
✅ Commerciante Verificato
```

La verifica può richiedere:

- documentazione aziendale
- partita IVA
- sito web
- presenza commerciale verificabile

La perdita della verifica non modifica il Piano Commerciante.

---

# Durata Abbonamenti

CollectorVerse supporta inizialmente:

```text
Mensile

Trimestrale

Annuale
```

Le durate disponibili sono configurabili tramite Dashboard Admin.

È possibile aggiungere nuove durate senza modificare il codice dell'applicazione.

---

# Periodo di Prova Gratuito

CollectorVerse supporta un periodo di prova gratuito.

Valore iniziale consigliato:

```text
7 giorni
```

La durata deve essere configurabile tramite Dashboard Admin.

---

## Funzionamento

Durante il periodo di prova l'utente può accedere alle funzionalità del piano associato alla prova.

Alla scadenza:

```text
✅ nessuna perdita dati

✅ ritorno automatico al piano posseduto

✅ conservazione completa dell'account
```

---

# Sistema di Pagamento

CollectorVerse non gestisce direttamente:

- carte di credito
- IBAN
- conti bancari
- dati di pagamento degli utenti

I pagamenti devono essere effettuati tramite i sistemi ufficiali degli Store supportati.

---

## Implementazione Iniziale

```text
Google Play Billing
```

per:

- Premium
- Premium Plus
- Commerciante

Lo stato degli abbonamenti viene verificato tramite i servizi ufficiali dello Store.

---

# Scansioni

CollectorVerse utilizza un sistema di scansioni giornaliere.

Tutti i valori devono essere configurabili tramite Dashboard Admin.

---

## Quantità Scansioni Iniziali

### Free

```text
3 scansioni al giorno
```

### Premium

```text
20 scansioni al giorno
```

### Premium Plus

```text
40 scansioni al giorno
```

### Commerciante

```text
100 scansioni al giorno
```

---

# Consumo Scansione

La scansione viene consumata immediatamente dopo l'acquisizione dell'immagine.

Flusso:

```text
Foto

↓

Consumo di 1 scansione

↓

Analisi
```

---

# Area Scansioni

L'utente deve poter visualizzare:

```text
Scansioni disponibili

Scansioni utilizzate

Scansioni ottenute tramite Reward

Video disponibili

Reset giornaliero
```

---

# Pubblicità

CollectorVerse può utilizzare sistemi pubblicitari esterni.

Implementazione iniziale prevista:

```text
Google AdMob
```

---

## Tipologie Supportate

```text
Banner

Rewarded Video
```

---

# Banner

I Banner devono essere mostrati in modo discreto e non invasivo.

La frequenza è configurabile dalla Dashboard Admin.

Gli utenti Free possono visualizzare Banner.

Premium, Premium Plus e Commerciante possono essere esclusi dalla pubblicità secondo le configurazioni amministrative.

---

# Rewarded Video

Gli utenti possono ottenere benefici guardando volontariamente video pubblicitari.

---

## Ricompensa Iniziale Consigliata

```text
+3 scansioni
```

---

## Limite Giornaliero Consigliato

```text
5 video al giorno
```

---

## Cooldown Consigliato

```text
15 minuti
```

---

Tutti i valori devono essere configurabili tramite Dashboard Admin.

---

# Marketplace

L'accesso al Marketplace dipende dal Piano attivo.

---

# Disponibilità Oggetti

Ogni oggetto presente nella Collezione Personale può essere marcato come:

```text
In Vendita

In Scambio
```

Le due opzioni possono coesistere.

---

# Utente Free

Può:

```text
✅ contrassegnare oggetti In Vendita

✅ contrassegnare oggetti In Scambio
```

Può inoltre mostrare tali disponibilità nel proprio profilo pubblico.

Non può:

```text
❌ creare Annunci Marketplace
```

---

# Utente Premium

Può:

```text
✅ creare Annunci Marketplace

✅ creare annunci di vendita

✅ creare annunci di scambio
```

---

# Utente Premium Plus

Può utilizzare tutte le funzionalità Marketplace del Piano Premium.

---

# Utente Commerciante

Può utilizzare tutte le funzionalità Marketplace del Piano Premium Plus.

Dispone inoltre di limiti annunci dedicati.

Valore iniziale consigliato:

```text
100 annunci attivi
```

---

# Annunci Marketplace

Ogni annuncio può contenere:

```text
Oggetto

Versione

Variante

Condizione

Prezzo

Valuta

Descrizione
```

---

# Condizione

La Condizione appartiene esclusivamente alla copia posseduta dall'utente.

Non appartiene:

```text
❌ all'Oggetto

❌ alla Versione

❌ alla Variante

❌ al Catalogo Universale
```

---

# Valuta

Ogni utente possiede una Valuta Preferita configurabile nel profilo.

Esempi:

```text
EUR €

USD $

GBP £

JPY ¥

CHF
```

---

## Utilizzo

Tutti i prezzi vengono registrati nella valuta scelta dall'utente.

---

## Visualizzazione

Gli altri utenti visualizzano sempre:

```text
Prezzo originale

+

Valuta originale
```

Esempio:

```text
120 €

150 USD

20.000 JPY
```

CollectorVerse non effettua conversioni automatiche tra valute.

---

# Stati Annuncio

Ogni annuncio può assumere uno dei seguenti stati.

---

## Attivo

Visibile nel Marketplace.

---

## Sospeso

Non visibile ma conservato.

---

## Chiuso

Venduto, scambiato o rimosso.

---

# Scadenza Abbonamento

Se il Piano Premium, Premium Plus o Commerciante termina:

```text
Gli annunci vengono automaticamente sospesi.
```

---

## Effetti

```text
✅ annunci conservati

✅ annunci recuperabili

❌ annunci visibili

❌ annunci inclusi nel Matching
```

---

# Riattivazione

Al rinnovo di un piano compatibile:

```text
Gli annunci vengono riattivati automaticamente.
```

---

# Limiti Annunci

Configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

### Premium

```text
10 annunci
```

### Premium Plus

```text
30 annunci
```

### Commerciante

```text
100 annunci
```

---

# Superamento Limite

Se un utente supera il numero massimo di annunci consentiti:

mostrare un Wizard di selezione.

Esempio:

```text
Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona gli annunci da mantenere attivi.
```

---

# Pacchetti

CollectorVerse supporta Pacchetti opzionali acquistabili separatamente.

---

## Esempi

```text
Scansioni Extra

Annunci Extra
```

---

# Stato Pacchetti

## Attivo

Utilizzabile.

---

## Congelato

Temporaneamente sospeso.

---

## Scaduto

Terminato.

---

# Congelamento Pacchetti

Se un utente perde i requisiti necessari all'utilizzo del pacchetto:

```text
Il pacchetto viene congelato.

Il tempo residuo viene conservato.
```

---

## Esempio

```text
Premium

+

Pacchetto 100 Annunci

↓

Scadenza Premium

↓

Pacchetto Congelato
```

---

# Riattivazione Pacchetto

Quando l'utente torna ad avere un piano compatibile:

```text
Il pacchetto riprende dal tempo residuo rimanente.
```

---

# Bundle

CollectorVerse supporta Bundle commerciali.

---

## Premium Collector

```text
Premium Annuale

+

250 Scansioni

+

50 Annunci
```

---

## Premium Plus Collector

```text
Premium Plus Annuale

+

1000 Scansioni

+

100 Annunci
```

---

# Fonti di Monetizzazione

CollectorVerse prevede:

```text
Abbonamenti

Bundle

Pacchetti

Banner Pubblicitari

Rewarded Video
```

---

# Gestione Admin

Tutti i valori devono essere configurabili senza modificare il codice.

---

## Configurazioni Abbonamenti

- piani
- prezzi
- durate
- periodo di prova
- vantaggi

---

## Configurazioni Provider

- provider pagamenti
- provider pubblicitari
- reward video

---

## Configurazioni Scansioni

- scansioni giornaliere
- scansioni reward
- cooldown
- limiti giornalieri

---

## Configurazioni Marketplace

- limiti annunci
- durata annunci
- visibilità annunci

---

## Configurazioni Pubblicità

- banner
- rewarded video
- frequenza

---

## Configurazioni Bundle

- contenuto
- durata
- prezzo

---

## Configurazioni Pacchetti

- quantità
- durata
- prezzo

---

# Obiettivo della Monetizzazione

L'obiettivo della monetizzazione di CollectorVerse è:

- sostenere i costi operativi della piattaforma
- finanziare l'evoluzione del Catalogo Universale
- mantenere accessibili gratuitamente le funzionalità fondamentali per l'intera community dei collezionisti

# Parte 4 - Catalogo Universale • Categorie • Collezioni • Serie • Oggetti • Versioni • Varianti

# Catalogo Universale

Il Catalogo Universale rappresenta il cuore di CollectorVerse.

Tutte le funzionalità della piattaforma si basano sulla struttura del Catalogo Universale.

Il Catalogo Universale costituisce la fonte ufficiale e centralizzata dei dati utilizzati da:

- Catalogazione Personale
- Wishlist
- Marketplace
- Matching
- Scanner AI
- Catalogo Collaborativo
- Gamification
- Dashboard Amministratore

---

# Obiettivo

Consentire la catalogazione di qualsiasi tipologia di oggetto collezionabile utilizzando una struttura unica, coerente e scalabile.

Esempi:

- Carte Collezionabili
- Monete
- Banconote
- Francobolli
- Fumetti
- Manga
- Libri
- LEGO
- Action Figure
- Videogiochi
- Vinili
- CD
- Modellismo
- Orologi
- Antiquariato
- Vini e Distillati

---

# Principi Fondamentali

Il Catalogo Universale deve essere:

- Scalabile
- Estensibile
- Multicategoria
- Collaborativo
- Verificabile
- Normalizzato
- Compatibile con Scanner AI
- Compatibile con Marketplace
- Compatibile con Matching

---

# Regola Fondamentale

Il Catalogo Universale NON contiene:

- proprietà degli utenti
- quantità possedute
- prezzi personali
- condizioni personali
- wishlist utente
- annunci marketplace
- dati commerciali personali

Questi dati appartengono alle aree personali degli utenti.

---

# Struttura Ufficiale

Ogni elemento del Catalogo Universale deve rispettare la seguente struttura.

```text
Categoria
↓
Collezione
↓
Serie
↓
Oggetto
↓
Versione
↓
Variante
```

---

# Regole Gerarchiche

## Regola 1

Una Collezione appartiene ad una sola Categoria.

---

## Regola 2

Una Serie appartiene ad una sola Collezione.

---

## Regola 3

Un Oggetto appartiene ad una sola Serie.

---

## Regola 4

Una Versione appartiene ad un solo Oggetto.

---

## Regola 5

Una Variante appartiene ad una sola Versione.

---

## Regola 6

Ogni Oggetto possiede almeno una Versione.

---

## Regola 7

Se una Collezione non utilizza realmente le Versioni, il sistema crea automaticamente:

```text
Versione Generica
```

---

## Regola 8

Le Varianti sono opzionali.

Una Versione può non possedere Varianti.

---

# Categoria

La Categoria rappresenta il livello più alto della classificazione.

---

## Esempi

- Carte Collezionabili
- Numismatica
- Filatelia
- Fumetti e Libri
- LEGO e Costruzioni
- Action Figure e Toys
- Videogiochi
- Musica e Media
- Orologi e Gioielli
- Militaria e Storico
- Modellismo
- Antiquariato e Arte
- Enologia e Spirits

---

# Stati Categoria

Ogni Categoria deve possedere uno stato.

---

## In Sviluppo

Categoria in preparazione.

Visibile esclusivamente agli amministratori.

---

## Attiva

Categoria disponibile agli utenti.

---

## Nascosta

Categoria temporaneamente non visibile.

---

## Archiviata

Categoria conservata ma non più utilizzabile.

---

# Regola Visibilità Categoria

Le categorie che non si trovano nello stato:

```text
Attiva
```

non devono comparire in:

- Catalogo
- Scanner
- Marketplace
- Matching
- Ricerca
- Importazione
- Catalogazione Personale
- Wishlist

---

# Informazioni Categoria

Per ogni Categoria visualizzare:

- Nome
- Logo
- Banner
- Stato
- Numero Collezioni
- Numero Serie
- Numero Oggetti
- Percentuale Completamento Utente

---

# Collezione

Una Collezione rappresenta un insieme coerente di Serie appartenenti alla stessa Categoria.

---

## Esempi

Categoria:

Carte Collezionabili

↓

Collezioni:

- Pokémon
- Yu-Gi-Oh!
- Magic The Gathering
- Disney Lorcana
- One Piece

---

Categoria:

Videogiochi

↓

Collezioni:

- Nintendo
- PlayStation
- Xbox

---

# Informazioni Collezione

Visualizzare:

- Nome
- Logo
- Banner
- Numero Serie
- Numero Oggetti
- Percentuale Completamento Utente

---

# Sistema Rarità

Ogni Collezione può utilizzare il proprio sistema di rarità.

Le rarità non sono condivise globalmente.

---

# Rarità

Le rarità appartengono alla Collezione.

---

## Esempio Pokémon

```text
Common
Uncommon
Rare
Ultra Rare
Illustration Rare
Secret Rare
```

---

## Esempio Magic

```text
Common
Uncommon
Rare
Mythic Rare
```

---

## Esempio Funko

```text
Common
Exclusive
Limited Edition
Chase
Grail
```

---

# Creazione Oggetto

Quando un utente crea un nuovo Oggetto il sistema deve mostrare:

- tutte le rarità esistenti della Collezione
- la voce "Altro..."

---

## Esempio

```text
Common
Uncommon
Rare
Ultra Rare

Altro...
```

---

# Caso "Altro..."

Se l'utente seleziona:

```text
Altro...
```

significa che la rarità desiderata non esiste ancora.

---

# Comportamento Sistema

Il Catalogo deve considerare l'elemento come non riconosciuto.

Il sistema deve avviare il workflow:

```text
Nuova Rarità
↓
Catalogo Collaborativo
↓
Revisione
↓
Approvazione Amministratore
```

---

# Serie

Una Serie rappresenta un insieme di Oggetti appartenenti alla stessa Collezione.

---

## Esempio

Pokémon

↓

Serie:

- Set Base
- Jungle
- Fossil
- Team Rocket
- Neo Genesis

---

# Data Uscita Serie

Ogni Serie possiede una data ufficiale di uscita.

---

## Formato

```text
gg/mm/aaaa
```

---

## Gestione

La data viene gestita dagli Amministratori del Catalogo.

---

## Regola Fondamentale

La data di uscita della Serie rappresenta l'unica fonte ufficiale utilizzata per l'ordinamento cronologico.

---

# Ordinamento Serie

Le Serie devono essere ordinate cronologicamente utilizzando:

```text
release_date
```

---

## Esempio

```text
Set Base
09/01/1999

↓

Jungle
16/06/1999

↓

Fossil
10/10/1999

↓

Team Rocket
24/04/2000
```

---

# Informazioni Serie

Visualizzare:

- Nome
- Data Uscita
- Numero Oggetti
- Percentuale Completamento Utente

---

# Oggetto

L'Oggetto rappresenta l'entità collezionabile principale.

È il centro logico del Catalogo Universale.

---

## Esempio

Serie:

Set Base

↓

Oggetto:

```text
Charizard 4/102
```

---

# Informazioni Oggetto

Visualizzare:

- Nome
- Codice
- Numero Catalogo
- Rarità
- Numero Versioni
- Numero Varianti Totali
- Statistiche

---

# Rarità Oggetto

La rarità appartiene sempre all'Oggetto.

---

## Regola Fondamentale

La rarità NON appartiene:

```text
❌ alla Versione

❌ alla Variante
```

---

## Esempio

```text
Charizard
↓
Ultra Rare
↓
Versione Inglese
↓
Holo
```

---

```text
Charizard
↓
Ultra Rare
↓
Versione Inglese
↓
Reverse Holo
```

La rarità rimane:

```text
Ultra Rare
```

---

# Versione

Le Versioni rappresentano differenti lingue, edizioni, distribuzioni o pubblicazioni dello stesso Oggetto.

Le Versioni NON sono nuovi Oggetti.

---

## Esempi Linguistici

```text
Italiano
Inglese
Francese
Tedesco
Giapponese
Spagnolo
```

---

## Esempi Editoriali

```text
First Edition
Unlimited
Collector Edition
Launch Edition
Reprint
```

---

# Versione Generica

Quando una Collezione non utilizza realmente Versioni:

il sistema crea automaticamente:

```text
Versione Generica
```

---

# Regola Fondamentale

Ogni Oggetto possiede almeno una Versione.

---

# Progressione Versioni

Le Versioni possiedono una progressione indipendente.

---

## Esempio

```text
Italiano ✅

Inglese ✅

Francese ❌

Tedesco ❌
```

Progressione:

```text
2 / 4 Versioni
```

---

# Possesso Oggetto

Un Oggetto viene considerato posseduto quando l'utente possiede almeno una Versione.

---

## Esempio

```text
Charizard

Italiano ✅

Inglese ❌

Giapponese ❌
```

Risultato:

```text
Oggetto Posseduto
```

---

# Variante

Una Variante appartiene sempre ad una specifica Versione.

Le Varianti NON rappresentano nuovi Oggetti.

Le Varianti NON rappresentano nuove Versioni.

---

## Esempi

Versione Inglese

↓

```text
Holo
Reverse Holo
Gold
Promo Stamp
Error Print
```

---

## Esempi Funko

```text
Glow In The Dark
Metallic
Signed
```

---

# Progressione Varianti

Le Varianti possiedono una progressione indipendente.

---

## Esempio

```text
Holo ✅

Reverse Holo ✅

Gold ❌

Promo Stamp ❌
```

Progressione:

```text
2 / 4 Varianti
```

---

# Regole Completamento

Versioni e Varianti NON incrementano:

- numero Oggetti
- completamento Serie
- completamento Collezione
- completamento Categoria

---

# Immagini Catalogo

Le immagini del Catalogo rappresentano elementi reali utilizzati da utenti e Scanner.

---

# Regola Fondamentale

Le immagini NON appartengono direttamente agli Oggetti.

Le immagini possono appartenere esclusivamente a:

```text
ItemVersion

oppure

ItemVariant
```

---

# Motivazione

L'Oggetto rappresenta un'entità logica.

Le immagini rappresentano invece una specifica manifestazione reale dell'oggetto.

---

## Esempio

```text
Charizard
```

possiede:

```text
Versione Italiana
↓
Immagine Italiana
```

---

```text
Charizard
```

possiede:

```text
Versione Inglese
↓
Immagine Inglese
```

---

```text
Charizard
```

possiede:

```text
Versione Giapponese
↓
Immagine Giapponese
```

---

# Esempio Variante

```text
Charizard
↓
Versione Inglese
↓
Gold
↓
Immagine Gold
```

---

# Tipologie Immagine

Esempi:

- Fronte
- Retro
- Confezione
- Dettaglio
- Immagine Versione
- Immagine Variante

---

# Benefici

Questo approccio:

- migliora la precisione Scanner
- migliora il Matching
- migliora il Marketplace
- evita immagini errate
- supporta cataloghi multilingua
- supporta promo speciali
- supporta versioni regionali
- supporta error print

---

# Scheda Oggetto

Ogni Oggetto possiede una scheda dedicata.

---

## Sezioni

- Dettagli
- Versioni
- Varianti
- Marketplace
- Statistiche

---

# Statistiche Oggetto

Visualizzare:

- utenti che possiedono l'Oggetto
- utenti che desiderano l'Oggetto
- scansioni effettuate
- annunci attivi
- annunci di scambio

---

# Condizione

La condizione appartiene esclusivamente alla copia posseduta dall'utente.

---

## Regola Fondamentale

La condizione NON appartiene:

```text
❌ all'Oggetto

❌ alla Versione

❌ alla Variante

❌ al Catalogo Universale
```

---

# Catalogo Collaborativo

Le modifiche non vengono applicate direttamente.

Ogni modifica segue il flusso:

```text
Proposta
↓
Revisione Community
↓
Decisione Amministratore
↓
Pubblicazione
```

---

# Creazione Nuovi Elementi

CollectorVerse supporta:

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante
- Nuova Rarità
- Nuova Immagine

---

# Stato Iniziale

Ogni elemento creato dalla community assume inizialmente lo stato:

```text
Provvisorio
```

---

# Stati Disponibili

```text
Provvisorio
In Revisione
Verificato
Rifiutato
Unificato
```

---

# Controllo Duplicati

Prima della creazione di qualsiasi elemento il sistema deve effettuare verifiche automatiche.

---

# Verifiche Disponibili

- nome
- codice identificativo
- OCR
- immagini
- hash immagini
- rarità esistenti

---

# Follow Categoria

Gli utenti possono seguire una Categoria.

---

## Eventi Notificabili

- Nuove Collezioni
- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

# Follow Collezione

Eventi notificabili:

- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

# Follow Serie

Eventi notificabili:

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

# Follow Oggetto

Eventi notificabili:

- Nuove Versioni
- Nuove Varianti
- Nuove Immagini
- Nuovi Annunci

---

# Collezioni Preferite

Le Collezioni possono essere salvate come preferite.

---

# Differenza rispetto al Follow

Follow:

```text
Riceve notifiche
```

---

Preferita:

```text
Funziona come segnalibro rapido
```

---

# Collezioni Pubbliche

Ogni Collezione pubblica possiede:

- Link pubblico
- QR Code dedicato

---

# Regola Privacy

Se una Collezione pubblica viene:

- eliminata
- resa privata

deve essere automaticamente rimossa dai preferiti degli altri utenti.

---

# Obiettivo del Catalogo Universale

Fornire una struttura unica, consistente e scalabile in grado di rappresentare qualsiasi tipologia di collezionabile supportando contemporaneamente Catalogazione Personale, Scanner AI, Marketplace, Matching, Gamification e crescita collaborativa del Catalogo senza richiedere modifiche strutturali future.

---

# Parte 5 - Sistema Scansione • OCR • Hash • AI • Wizard Catalogo • Cronologia Scansioni

# Sistema Scansione

Il Sistema Scansione rappresenta una delle funzionalità principali di CollectorVerse.

L'obiettivo è permettere il riconoscimento rapido degli oggetti catalogati e semplificare la catalogazione delle collezioni personali.

Il sistema deve essere progettato per supportare milioni di scansioni mantenendo elevata accuratezza, velocità e semplicità d'uso.

---

# Obiettivi

Il Sistema Scansione deve:

- riconoscere Oggetti esistenti
- riconoscere Versioni esistenti
- riconoscere Varianti esistenti
- ridurre l'inserimento manuale
- velocizzare la catalogazione
- migliorare la qualità del Catalogo Universale
- aiutare nella scoperta di nuovi elementi non catalogati
- alimentare il Catalogo Collaborativo
- supportare il Matching
- supportare la crescita della Community

---

# Principio Fondamentale

La scansione non modifica direttamente il Catalogo Universale.

La scansione può:

```text
Riconoscere

oppure

Suggerire
```

Le modifiche al Catalogo Universale seguono sempre il workflow ufficiale di revisione.

---

# Gerarchia di Riconoscimento

Lo Scanner deve sempre rispettare la gerarchia ufficiale del Catalogo.

```text
Categoria
↓
Collezione
↓
Serie
↓
Oggetto
↓
Versione
↓
Variante
```

---

# Flusso Ufficiale Scansione

```text
Selezione Categoria
↓
Selezione Collezione
↓
Selezione Versione (se applicabile)
↓
Acquisizione Immagine
↓
Consumo Scansione
↓
Analisi
↓
Risultato
↓
Conferma Utente
↓
Catalogazione
```

---

# Selezione Categoria

Prima della scansione l'utente deve selezionare una Categoria.

---

## Regola

Possono essere selezionate esclusivamente:

```text
Categorie Attive
```

---

# Selezione Collezione

Dopo la Categoria viene selezionata la Collezione.

---

## Esempio

```text
Categoria

Carte Collezionabili

↓

Collezione

Pokémon
```

---

# Selezione Versione

Dopo la Collezione.

La selezione della Versione è facoltativa se la Collezione utilizza esclusivamente una Versione Generica.

---

## Esempio

```text
Italiano

Inglese

Francese

Tedesco

Giapponese

Spagnolo
```

---

# Obiettivo

Ridurre gli errori di riconoscimento.

Migliorare la precisione dell'analisi.

Velocizzare il matching catalografico.

---

# Versione Generica

Se la Collezione utilizza esclusivamente:

```text
Versione Generica
```

il selettore della Versione non deve essere mostrato.

---

# Acquisizione Immagine

L'utente può:

- scattare una foto
- caricare una foto esistente dalla galleria

---

# Requisiti Minimi

L'immagine deve essere:

- sufficientemente nitida
- leggibile
- centrata
- supportata dal sistema

---

# Formati Supportati

Valori iniziali consigliati:

```text
JPG

JPEG

PNG

WEBP
```

Nuovi formati possono essere aggiunti dalla Dashboard Admin.

---

# Consumo Scansione

La scansione viene consumata immediatamente dopo l'acquisizione della foto.

---

## Flusso

```text
Foto
↓
Consumo Scansione
↓
Analisi
```

---

# Regola Anti-Abuso

Una scansione consumata non viene restituita automaticamente.

Eccezioni e compensazioni possono essere configurate dagli Amministratori.

---

# Pipeline di Analisi

CollectorVerse utilizza una pipeline multilivello.

Ogni livello aumenta la precisione del riconoscimento e riduce il carico computazionale.

---

# Livello 1 - Hash Immagini

Confronto dell'immagine con quelle già presenti nel Catalogo Universale.

---

## Obiettivo

Identificare rapidamente immagini già conosciute.

---

## Benefici

- elevata velocità
- basso costo computazionale
- elevata precisione

---

# Livello 2 - OCR

Estrazione automatica del testo presente nell'immagine.

---

## Informazioni Ricercate

- nome oggetto
- numero catalogo
- codici identificativi
- numerazioni
- sigle
- testi stampati

---

## Esempi

```text
4/102

SV3

Charizard

English

EN
```

---

# Livello 3 - Matching Catalogo

Le informazioni ottenute da:

- Hash
- OCR

vengono confrontate con il Catalogo Universale.

---

## Obiettivo

Individuare:

```text
Oggetto
↓
Versione
↓
Variante
```

più compatibili.

---

# Livello 4 - Analisi AI

L'Intelligenza Artificiale viene utilizzata esclusivamente come fallback.

---

## Attivazione

L'AI interviene quando:

```text
Hash
+
OCR
+
Matching Catalogo

non raggiungono
una soglia di affidabilità sufficiente
```

---

## Utilizzo

L'AI supporta:

- identificazione oggetti
- identificazione versioni
- identificazione varianti
- classificazione immagini
- suggerimenti catalografici

---

# Utilizzo Immagini Catalogo

Lo Scanner utilizza esclusivamente immagini associate a:

```text
ItemVersion

oppure

ItemVariant
```

---

# Regola Fondamentale

Le immagini NON appartengono direttamente all'Oggetto.

---

# Motivazione

L'Oggetto rappresenta una entità logica.

Le immagini rappresentano una manifestazione reale e specifica dell'oggetto.

---

## Esempio

```text
Charizard
↓
Versione Italiana
↓
Immagine Italiana
```

---

```text
Charizard
↓
Versione Inglese
↓
Immagine Inglese
```

---

```text
Charizard
↓
Versione Giapponese
↓
Immagine Giapponese
```

---

# Esempio Variante

```text
Charizard
↓
Versione Inglese
↓
Gold
↓
Immagine Gold
```

---

# Benefici

Questa struttura:

- migliora la precisione dello Scanner
- evita immagini errate
- supporta cataloghi multilingua
- supporta promo speciali
- supporta versioni regionali
- supporta Error Print
- supporta Varianti rare

---

# Priorità Immagini

La visualizzazione delle immagini deve rispettare il seguente ordine:

```text
Immagine Variante
↓
Immagine Versione
↓
Placeholder
```

---

## Regola

Se esiste una immagine associata alla Variante:

```text
utilizzare immagine Variante
```

Altrimenti:

```text
utilizzare immagine Versione
```

Se nessuna immagine è disponibile:

```text
utilizzare Placeholder
```

---

# Risultati Scansione

Al termine dell'analisi mostrare:

- risultato suggerito
- livello di affidabilità
- Versione individuata
- Variante individuata
- risultati alternativi

---

## Esempio

```text
Charizard 4/102

Versione:
Inglese

Variante:
Holo

Affidabilità:
98%
```

---

# Risultati Alternativi

Mostrare soluzioni alternative ordinate per affidabilità.

---

## Esempio

```text
Charizard Holo
98%
```

---

```text
Charizard Reverse Holo
82%
```

---

```text
Charmander Holo
71%
```

---

# Livelli Affidabilità

## Alta

```text
90% - 100%
```

---

## Media

```text
70% - 89%
```

---

## Bassa

```text
0% - 69%
```

---

# Conferma Risultato

Prima della catalogazione definitiva l'utente deve confermare il risultato proposto.

---

# Azioni Disponibili

- Conferma
- Correggi
- Cerca Manualmente
- Segnala Errore

---

# Nessun Risultato

Quando non viene trovato alcun risultato sufficientemente affidabile.

---

## Comportamento

Mostrare il Wizard Catalogo.

---

# Wizard Catalogo

Sistema guidato per la creazione di nuovi elementi.

---

# Operazioni Disponibili

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante
- Nuova Rarità
- Nuova Immagine

---

# Nuovo Oggetto

Utilizzato quando l'Oggetto non esiste.

---

## Informazioni Richieste

- Categoria
- Collezione
- Serie
- Nome
- Codice
- Numero Catalogo
- Rarità
- Prima Versione
- Immagine della Versione
- Descrizione

---

# Nuova Versione

Utilizzata quando:

```text
Oggetto esistente
+
Versione mancante
```

---

## Esempio

```text
Charizard esiste

↓

Versione Spagnola assente

↓

Nuova Versione
```

---

# Nuova Variante

Utilizzata quando:

```text
Oggetto esistente
↓
Versione esistente
↓
Variante mancante
```

---

## Esempio

```text
Charizard
↓
Inglese
↓
Gold non presente
↓
Nuova Variante
```

---

# Nuova Rarità

Utilizzata quando l'utente seleziona:

```text
Altro...
```

durante la scelta della rarità.

---

## Workflow

```text
Nuova Rarità
↓
Catalogo Collaborativo
↓
Revisione
↓
Approvazione
```

---

# Nuova Immagine

Utilizzata per migliorare il Catalogo Universale.

---

## Associazioni Consentite

Le immagini possono essere associate esclusivamente a:

```text
ItemVersion

oppure

ItemVariant
```

---

# Controlli Automatici

Prima della creazione di una proposta il sistema deve verificare:

- duplicati
- OCR simili
- nomi simili
- codici identici
- hash immagini
- immagini simili
- rarità esistenti

---

# Stato Iniziale

Ogni proposta assume automaticamente lo stato:

```text
Provvisorio
```

---

# Utilizzo Immediato

Gli elementi Provvisori possono essere:

- cercati
- catalogati
- aggiunti alle collezioni
- aggiunti alle wishlist
- utilizzati nel Marketplace

fino a decisione amministrativa.

---

# Catalogazione Diretta

Dopo il riconoscimento l'utente può:

- aggiungere alla Collezione
- aggiungere alla Wishlist
- impostare quantità
- segnare come disponibile alla vendita
- segnare come disponibile allo scambio

---

# Cronologia Scansioni

Ogni utente possiede una cronologia personale.

---

# Percorso

```text
Profilo
↓
Cronologia Scansioni
```

---

# Informazioni Visualizzate

Per ogni scansione mostrare:

- Data
- Immagine
- Categoria
- Collezione
- Serie
- Oggetto
- Versione
- Variante
- Affidabilità
- Risultato

---

# Conservazione

Valore iniziale consigliato:

```text
50 scansioni
```

Configurabile dalla Dashboard Admin.

---

# Errori di Scansione

Quando la scansione fallisce devono essere mostrati messaggi comprensibili.

---

## Esempi

```text
Immagine troppo sfocata
```

---

```text
Immagine troppo scura
```

---

```text
Oggetto non riconosciuto
```

---

```text
Formato non supportato
```

---

```text
Versione non selezionata
```

---

```text
Nessuna scansione disponibile
```

---

# Statistiche Scansione

CollectorVerse deve registrare:

- scansioni effettuate
- scansioni riuscite
- scansioni fallite
- scansioni AI
- nuove proposte generate
- nuove Versioni suggerite
- nuove Varianti suggerite
- nuove Rarità suggerite

---

# Utilizzo Statistiche

Le statistiche possono essere utilizzate da:

- Dashboard Utente
- Gamification
- Dashboard Merchant
- Dashboard Admin

---

# Importazione Collezioni

CollectorVerse supporta l'importazione tramite:

```text
Excel

CSV
```

---

# Obiettivo

Popolare rapidamente le Collezioni Personali.

---

# Regola Fondamentale

L'importazione:

```text
❌ NON crea Oggetti

❌ NON crea Versioni

❌ NON crea Varianti

❌ NON crea Rarità

❌ NON modifica il Catalogo Universale
```

---

# Flusso Importazione

```text
Categoria
↓
Caricamento File
↓
Mapping Colonne
↓
Simulazione
↓
Correzione Guidata
↓
Conferma
↓
Importazione
```

---

# Mapping Colonne

L'utente associa i campi del file ai campi CollectorVerse.

---

## Esempio

```text
Product Name
↓
Oggetto
```

```text
Language
↓
Versione
```

```text
Series
↓
Serie
```

---

# Simulazione

Mostrare:

- elementi riconosciuti
- elementi non riconosciuti
- duplicati
- incongruenze
- errori

---

## Esempio

```text
1200 righe analizzate

1180 riconosciute

20 non riconosciute
```

---

# Elementi Non Riconosciuti

Gli elementi non riconosciuti:

```text
NON vengono importati

NON creano automaticamente
Oggetti

Versioni

Varianti

Rarità
```

---

# Azioni Disponibili

```text
Importa Elementi Riconosciuti

Esporta Elementi Non Riconosciuti
```

---

# Dashboard Admin

Tutte le configurazioni devono essere modificabili senza aggiornare il codice.

---

# Configurazioni Scansione

- scansioni giornaliere
- scansioni reward
- cooldown
- limiti AI
- soglia affidabilità

---

# Configurazioni Cronologia

- numero scansioni conservate

---

# Configurazioni AI

- attivazione AI
- provider AI
- soglia utilizzo
- limiti consumo

---

# Configurazioni Importazione

- formati consentiti
- limiti file
- limiti righe
- soglie simulazione

---

# Configurazioni Errori

Tutti i messaggi di errore devono poter essere personalizzati dalla Dashboard Admin.

---

# Obiettivo del Sistema Scansione

Il Sistema Scansione deve consentire il riconoscimento rapido e affidabile di Oggetti, Versioni e Varianti presenti nel Catalogo Universale, semplificare la catalogazione delle collezioni personali, migliorare la qualità del Catalogo Universale e favorire la crescita collaborativa dell'intero ecosistema CollectorVerse.

---

# Parte 6 - Catalogo Collaborativo • Contributori Catalogo • Votazioni • Reputazione • Immagini

# Catalogo Collaborativo

CollectorVerse utilizza un sistema di crescita collaborativa del Catalogo Universale.

La community può contribuire alla creazione, correzione e miglioramento del Catalogo Universale.

---

# Obiettivo

Consentire una crescita rapida del catalogo mantenendo elevata qualità dei dati, coerenza strutturale e controllo amministrativo.

---

# Principio Fondamentale

La community contribuisce al Catalogo.

La community NON approva direttamente il Catalogo.

La decisione finale appartiene sempre agli Amministratori.

---

# Contenuti Contribuibili

Gli utenti possono proporre:

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuove Rarità
- Nuove Immagini
- Correzioni Catalogo

---

# Workflow Ufficiale

Tutte le proposte seguono il seguente flusso:

```text
Proposta
↓
Revisione Community
↓
Valutazione Amministrativa
↓
Decisione Finale
```

---

# Contributori Catalogo

I Contributori Catalogo sono utenti autorizzati a partecipare al processo di revisione.

---

# Accesso Commercianti

I Commercianti diventano automaticamente Contributori Catalogo.

---

## Limitazioni

Possono revisionare esclusivamente le categorie dichiarate nel proprio Profilo Negozio.

---

# Accesso Utenti

Gli utenti possono essere invitati a partecipare al programma Contributori Catalogo.

---

## Requisito Minimo

Valore iniziale consigliato:

```text
30 giorni di iscrizione
```

Configurabile dalla Dashboard Admin.

---

# Invito

Quando l'utente raggiunge i requisiti stabiliti riceve una notifica.

---

## Messaggio Esempio

```text
Vuoi aiutare CollectorVerse
a migliorare il Catalogo Universale?
```

---

# Accettazione

Quando l'utente accetta:

entra ufficialmente nel programma Contributori Catalogo.

---

# Ambito di Revisione

Gli utenti possono revisionare solo collezioni effettivamente presenti nelle proprie Collezioni Personali.

---

## Esempio

Possiede:

```text
Pokémon
LEGO
Euro Italia
```

---

Può revisionare:

```text
Pokémon
LEGO
Euro Italia
```

---

Non può revisionare:

```text
Magic
Lorcana
Francobolli
```

se non presenti nelle sue Collezioni Personali.

---

# Area Contributori Catalogo

Sezione dedicata ai revisori.

---

## Percorso

```text
Profilo
↓
Contributori Catalogo
```

---

# Sezioni Disponibili

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuove Rarità
- Nuove Immagini
- Correzioni Catalogo

---

# Informazioni Visualizzate

Ogni proposta deve mostrare:

- Categoria
- Collezione
- Serie
- Oggetto
- Versione
- Variante (se presente)
- Rarità (se presente)
- Immagine
- Data Proposta
- Utente Proponente

---

# Sistema di Votazione

Ogni revisore può votare una sola volta per ogni proposta.

---

# Voti Disponibili

```text
✅ Corretta

❌ Non Corretta

❓ Non So
```

---

# Motivazione

Quando viene selezionato:

```text
❌ Non Corretta
```

deve essere possibile inserire:

```text
Motivazione (facoltativa)
```

---

# Visibilità Andamento

I revisori possono visualizzare l'andamento della revisione.

---

## Informazioni Mostrate

```text
Corretta

Non Corretta

Non So

Totale Voti
```

---

# Reputazione Contributore

Ogni Contributore possiede una reputazione.

---

# Formula Iniziale

```text
Correzioni Approvate

-

Correzioni Respinte
```

---

# Valore Minimo

La reputazione non può mai essere negativa.

---

## Valore Minimo

```text
0
```

---

# Peso del Voto

Non tutti i voti hanno lo stesso peso.

Gli utenti più affidabili influenzano maggiormente la revisione.

---

# Configurazione Iniziale Consigliata

Reputazione:

```text
0 - 9
```

↓

Peso:

```text
1
```

---

Reputazione:

```text
10 - 29
```

↓

Peso:

```text
2
```

---

Reputazione:

```text
30 - 99
```

↓

Peso:

```text
3
```

---

Reputazione:

```text
100+
```

↓

Peso:

```text
5
```

---

# Applicazione Peso

Il peso viene applicato a:

- Utenti
- Commercianti

---

# Statistiche Contributore

Ogni Contributore deve visualizzare:

- Correzioni Approvate
- Correzioni Respinte
- Reputazione
- Peso Voto Attuale

---

# Revisione Community

La Community non approva direttamente gli elementi.

La Community fornisce indicazioni agli Amministratori.

---

# Stati Revisione

---

## Revisione Positiva

Valori configurabili.

Esempio:

```text
Almeno 20 voti

+

Almeno 85% Corretta
```

---

## Revisione Negativa

Valori configurabili.

Esempio:

```text
Almeno 20 voti

+

Almeno 85% Non Corretta
```

---

## Revisione Incerta

Tutti gli altri casi.

---

# Utilizzo Revisioni

Lo stato della revisione viene utilizzato esclusivamente per stabilire la priorità di revisione amministrativa.

---

# Decisione Finale

La decisione finale appartiene sempre ad un Amministratore.

---

# Azioni Amministratore

```text
✅ Verifica

✏️ Correggi

❌ Rifiuta

🔀 Unifica
```

---

# Nuove Collezioni

Quando una nuova Collezione non possiede ancora una base utenti sufficientemente ampia:

le revisioni vengono affidate principalmente a:

- Commercianti
- Moderatori
- Amministratori

---

# Immagini Collaborative

CollectorVerse supporta un sistema di miglioramento continuo delle immagini del Catalogo Universale.

---

# Obiettivo

Permettere alla Community di migliorare progressivamente la qualità visiva del Catalogo.

---

# Regola Fondamentale

Le immagini NON appartengono direttamente agli Oggetti.

Le immagini possono appartenere esclusivamente a:

```text
ItemVersion

oppure

ItemVariant
```

---

# Immagini Candidate

Ogni Versione o Variante può possedere più immagini candidate.

Le immagini non appartengono direttamente agli Oggetti.

---

# Valutazione Immagini

Formula completamente configurabile.

---

## Valori Iniziali Consigliati

```text
Qualità Tecnica = 50%

Voti Community = 40%

Utilizzo = 10%
```

---

# Immagine Ufficiale

L'immagine con il punteggio più elevato diventa:

```text
Immagine Ufficiale
```

---

# Soglia Minima

Valore iniziale consigliato:

```text
80 / 100
```

Configurabile tramite Dashboard Admin.

---

# Priorità Visualizzazione Immagini

La piattaforma deve utilizzare il seguente ordine:

```text
Immagine Variante
↓
Immagine Versione
↓
Placeholder
```

---

# Regola

Se una Variante possiede una propria Immagine Ufficiale:

```text
utilizzare immagine Variante
```

---

Altrimenti:

```text
utilizzare immagine Versione
```

---

Se nessuna immagine è disponibile:

```text
utilizzare Placeholder
```

---

# Nuova Immagine

Ogni nuova immagine entra nel sistema come:

```text
Immagine Candidata
```

---

# Prime Fasi

Se un'immagine non possiede ancora:

- voti
- utilizzi

la valutazione deve basarsi principalmente sulla qualità tecnica.

---

# Gestione Immagini

Gli Amministratori possono:

- eliminare immagini errate
- eliminare immagini inappropriate
- bloccare immagini
- sostituire immagini
- forzare immagine ufficiale

---

# Controllo Duplicati

Le immagini candidate devono essere sottoposte a controlli automatici.

---

## Verifiche Disponibili

- Hash Immagine
- Similarità Immagine
- OCR
- Duplicati Catalogo
- Duplicati Variante
- Duplicati Versione

---

# Proprietà dei Contributi

I contributi approvati diventano parte permanente del Catalogo Universale.

---

# Contenuti Coinvolti

- Oggetti
- Versioni
- Varianti
- Rarità
- Immagini

---

# Eliminazione Account

Se l'autore elimina il proprio account:

```text
I contributi approvati rimangono nel Catalogo.
```

---

# Effetti

```text
✅ contenuti conservati

✅ catalogo preservato

✅ autore anonimizzato
```

---

# Dashboard Admin

Tutte le configurazioni devono essere modificabili senza aggiornare il codice.

---

# Configurazioni Contributori

- giorni minimi iscrizione
- attivazione programma
- requisiti accesso
- limiti operativi

---

# Configurazioni Reputazione

- soglie reputazione
- peso voto
- formule reputazione

---

# Configurazioni Revisioni

- voti minimi
- soglia revisione positiva
- soglia revisione negativa
- gestione revisione incerta

---

# Configurazioni Immagini

- peso qualità tecnica
- peso voti community
- peso utilizzo
- soglia immagine ufficiale

---

# Configurazione Programma

Il Programma Contributori può essere:

```text
Attivo

Disattivato
```

tramite Dashboard Admin.

---

# Obiettivo del Catalogo Collaborativo

Il Catalogo Collaborativo deve consentire alla Community di contribuire alla crescita e al miglioramento continuo del Catalogo Universale mantenendo elevati standard qualitativi grazie ad un sistema di revisione, reputazione, controllo amministrativo e validazione progressiva dei contenuti.

---

# Parte 7 - Marketplace • Chat • Matching • Geolocalizzazione • Commercianti

# Marketplace

CollectorVerse include un Marketplace dedicato all'incontro tra collezionisti e commercianti.

La piattaforma non gestisce direttamente:

- pagamenti
- spedizioni
- incassi
- rimborsi
- controversie commerciali

Le transazioni avvengono direttamente tra gli utenti.

CollectorVerse opera esclusivamente come piattaforma di incontro tra domanda e offerta.

---

# Obiettivi Marketplace

Il Marketplace deve:

- facilitare la compravendita tra collezionisti
- facilitare gli scambi
- valorizzare le collezioni personali
- favorire il completamento delle collezioni
- generare opportunità tramite il Matching
- supportare commercianti professionali

---

# Principio Fondamentale

Un Annuncio Marketplace può essere creato esclusivamente a partire da un elemento realmente presente nella Collezione Personale dell'utente.

Non è consentita la creazione di annunci per oggetti non posseduti.

---

# Chat

CollectorVerse utilizza un sistema di messaggistica privata.

---

# Regola Fondamentale

Una Conversazione non può essere aperta direttamente.

Il flusso obbligatorio è:

```text
Richiesta di Contatto
↓
Accettazione
↓
Conversazione
↓
Messaggi
```

---

# Richieste di Contatto

Le Richieste di Contatto rappresentano il punto di accesso alle comunicazioni private.

---

# Informazioni Mostrate

Una Richiesta di Contatto può mostrare:

- Username
- Display Name
- Piano Attivo
- Affidabilità
- Media Recensioni
- Numero Recensioni
- CollectorScore
- Badge Principali

---

# Stati Richiesta

```text
In Attesa
Accettata
Rifiutata
Bloccata
Scaduta
```

---

# Regole

Solo una richiesta Accettata genera una Conversazione.

Non possono esistere richieste duplicate in stato pendente tra la stessa coppia di utenti.

Può esistere una sola Conversazione attiva per la stessa coppia di utenti.

---

# Conversazioni

Le Conversazioni sono private.

Devono rispettare:

- Privacy
- Blocchi Utente
- Moderazione
- Segnalazioni

---

# Messaggi

I Messaggi appartengono sempre ad una Conversazione.

---

# Stato Lettura

Lo stato di lettura è riferito al destinatario del messaggio.

Valori disponibili:

```text
Inviato
Letto
```

---

# Utenti Free

Possono:

```text
✅ ricevere richieste di contatto
✅ rispondere a richieste ricevute
✅ partecipare a conversazioni avviate da altri
```

Non possono:

```text
❌ avviare nuove richieste di contatto
```

---

# Utenti Premium

Possono:

```text
✅ inviare richieste di contatto
✅ avviare nuove conversazioni
✅ utilizzare la chat completa
```

---

# Recensioni

Gli utenti possono rilasciare recensioni dopo un'interazione avvenuta tramite CollectorVerse.

---

# Utilizzo delle Recensioni

Le recensioni contribuiscono a:

- Affidabilità
- Matching
- Profilo Utente
- Profilo Commerciante

---

# Regola Fondamentale

Ogni utente può lasciare una sola recensione per un altro utente.

---

# Modifica Recensione

La recensione può essere modificata.

La modifica aggiorna la recensione esistente.

Non viene creata una nuova recensione.

---

# Segnalazioni

Le recensioni possono essere:

- segnalate
- analizzate
- moderate

dagli Amministratori.

---

# Disponibilità Oggetti

Ogni elemento della Collezione Personale può essere contrassegnato come:

```text
In Vendita
In Scambio
```

Le due opzioni possono coesistere.

---

# Disponibilità e Marketplace

La semplice disponibilità NON genera automaticamente un annuncio Marketplace.

Disponibilità e Annuncio Marketplace sono due concetti distinti.

---

# In Vendita

L'utente è disposto a vendere l'oggetto posseduto.

---

# In Scambio

L'utente è disposto a scambiare l'oggetto posseduto.

---

# Accesso Marketplace

Dipende dal Piano attivo.

---

# Piano Free

Può:

```text
✅ contrassegnare elementi come In Vendita
✅ contrassegnare elementi come In Scambio
✅ mostrare tali disponibilità nel profilo
✅ consultare il Marketplace
✅ consultare gli annunci pubblici
```

Non può:

```text
❌ creare Annunci Marketplace
```

---

# Piano Premium

Può:

```text
✅ creare Annunci Marketplace
✅ creare annunci vendita
✅ creare annunci scambio
✅ creare annunci vendita e scambio
```

---

# Piano Premium Plus

Può utilizzare tutte le funzionalità del Piano Premium.

---

# Piano Commerciante

Può utilizzare tutte le funzionalità del Piano Premium Plus.

Dispone inoltre di:

- Profilo Negozio
- Dashboard Professionale
- Mappa Commercianti
- Statistiche Professionali
- Opportunità Commerciali
- Commerciante Verificato

---

# Tipologie Annuncio

CollectorVerse supporta tre tipologie di annuncio.

---

## Vendita

L'oggetto viene proposto esclusivamente per la vendita.

---

## Scambio

L'oggetto viene proposto esclusivamente per lo scambio.

---

## Vendita e Scambio

L'utente accetta entrambe le possibilità.

---

# Contenuto Annuncio

Ogni annuncio può contenere:

```text
Oggetto
Versione
Variante
Condizione
Prezzo
Valuta
Descrizione
Immagini
```

---

# Identificazione Elemento

Ogni annuncio deve identificare in modo preciso:

```text
Oggetto
↓
Versione
↓
Variante
```

quando disponibili.

---

# Esempio

```text
Charizard

↓

Versione Inglese

↓

Variante Holo
```

---

# Prezzo

Gli annunci di vendita richiedono un prezzo.

Gli annunci di scambio possono non avere alcun prezzo.

---

# Valute

Ogni prezzo viene registrato nella valuta originale scelta dall'utente.

---

# Esempi

```text
120 EUR

250 USD

20.000 JPY
```

---

# Regola Fondamentale

CollectorVerse non effettua conversioni automatiche tra valute.

Gli utenti visualizzano sempre:

```text
Prezzo originale
+
Valuta originale
```

---

# Condizione

La condizione appartiene esclusivamente alla copia posseduta.

Non appartiene:

```text
❌ all'Oggetto
❌ alla Versione
❌ alla Variante
❌ al Catalogo Universale
```

---

# Stati Annuncio

Ogni annuncio può assumere uno dei seguenti stati.

---

## Attivo

Visibile nel Marketplace.

Incluso nel Matching.

---

## Sospeso

Non visibile.

Conservato nel sistema.

Escluso dal Matching.

---

## Chiuso

Venduto.

Scambiato.

Ritirato.

Concluso.

---

# Limiti Annunci

Configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

### Premium

```text
10 annunci attivi
```

### Premium Plus

```text
30 annunci attivi
```

### Commerciante

```text
100 annunci attivi
```

---

# Superamento Limite

Quando il numero di annunci supera il limite del Piano:

mostrare un Wizard di selezione.

---

# Esempio

```text
Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona gli annunci da mantenere attivi.
```

---

# Scadenza Piano

Quando Premium, Premium Plus o Commerciante scadono:

```text
Gli annunci vengono sospesi automaticamente.
```

---

# Effetti

```text
✅ dati conservati
✅ annunci recuperabili

❌ annunci visibili
❌ matching attivo
```

---

# Riattivazione

Al rinnovo di un Piano compatibile:

```text
Gli annunci vengono riattivati automaticamente.
```

---

# Ricerca Marketplace

Il Marketplace deve supportare:

- ricerca testuale
- ricerca catalografica
- filtri dinamici
- ordinamenti personalizzabili

---

# Filtri Base

- Categoria
- Collezione
- Serie
- Oggetto
- Versione
- Variante

---

# Filtri Avanzati

- Prezzo
- Condizione
- Distanza
- Tipo Annuncio
- Tipo Account
- Affidabilità
- Commerciante Verificato

---

# Ordinamenti

Valori iniziali consigliati:

- Compatibilità
- Data Pubblicazione
- Prezzo
- Distanza
- Affidabilità
- CollectorScore
- Recensioni

---

# Matching

Il Matching rappresenta il sistema automatico di individuazione opportunità.

---

# Obiettivo

Individuare automaticamente:

- opportunità di acquisto
- opportunità di vendita
- opportunità di scambio
- opportunità commerciali
- completamenti collezione

---

# Accesso Matching

Disponibile per:

```text
Premium
Premium Plus
Commerciante
```

Non disponibile per utenti Free.

---

# Dati Utilizzati

Il Matching può utilizzare:

- Wishlist
- Collezioni Personali
- Disponibilità Vendita
- Disponibilità Scambio
- Annunci Marketplace
- Affidabilità
- Recensioni
- CollectorScore
- Geolocalizzazione
- Piano Utente

---

# Precisione Matching

Il Matching deve supportare:

```text
Oggetto
↓
Versione
↓
Variante
```

---

# Esempio

Richiesta:

```text
Charizard
↓
Inglese
↓
Holo
```

Non è equivalente a:

```text
Charizard
↓
Giapponese
↓
Holo
```

---

# Matching Acquisto

Individua:

```text
Wishlist
↓
Disponibilità compatibili
```

---

# Matching Vendita

Individua:

```text
Oggetti disponibili
↓
Utenti interessati
```

---

# Matching Scambio

Identifica situazioni in cui:

```text
Utente A possiede ciò che vuole Utente B

↓

Utente B possiede ciò che vuole Utente A
```

---

# Matching Completamento Collezione

Individua elementi mancanti.

---

# Esempio

```text
Serie:
102 elementi

Utente:
101 posseduti

↓

Manca 1 elemento
```

---

# Opportunità Commercianti

Il sistema può individuare:

- wishlist compatibili
- domanda geografica
- utenti interessati
- opportunità ad alta conversione

---

# Geolocalizzazione

Il Matching può utilizzare la distanza geografica.

---

# Distanza Predefinita Consigliata

```text
25 km
```

---

# Estensioni Possibili

```text
50 km
100 km
250 km
500 km
Nazionale
Europa
Mondo
```

---

# Filtri Geografici

Supportati:

- Regione
- Nazione
- Continente

---

# Ranking Matching

Il ranking può considerare:

- compatibilità
- distanza
- affidabilità
- recensioni
- CollectorScore
- attività recente

---

# Blocchi Utente

Gli utenti bloccati non devono comparire nei risultati reciproci.

---

# Effetti

Non devono essere generati:

- Match
- Suggerimenti
- Opportunità
- Contatti

tra utenti coinvolti da un blocco.

---

# Conversione Match

Quando un Match viene considerato interessante:

l'utente può inviare una Richiesta di Contatto.

---

# Flusso

```text
Match
↓
Richiesta di Contatto
↓
Accettazione
↓
Conversazione
↓
Interazione
```

---

# Notifiche Matching

CollectorVerse può generare notifiche per:

- nuovi Match Acquisto
- nuovi Match Vendita
- nuovi Match Scambio
- nuovi annunci compatibili
- nuove opportunità commerciali
- opportunità completamento collezione

---

# Statistiche Matching

CollectorVerse può registrare:

- Match generati
- Match visualizzati
- Match aperti
- Match convertiti in contatto
- Match convertiti in recensione
- Match convertiti in transazione

---

# Merchant Profile

I Commercianti dispongono di un Profilo Professionale dedicato.

---

# Merchant Verification

Ogni Merchant può possedere una sola verifica.

---

# Stato Verifica

```text
Pending
Approved
Rejected
Suspended
```

---

# Commerciante Verificato

Visualizza il badge:

```text
✅ Commerciante Verificato
```

---

# Regola Fondamentale

La verifica:

- non scade automaticamente
- rimane valida fino a modifica amministrativa
- può essere sospesa
- può essere revocata

---

# Google Business

I Merchant possono collegare un profilo Google Business.

---

# Informazioni Visualizzabili

- Rating Medio
- Numero Recensioni
- Recensioni Pubbliche
- Informazioni Business

---

# Dashboard Professionale

I Merchant possono visualizzare:

- visualizzazioni profilo
- visualizzazioni annunci
- click recapiti
- follower
- conversioni marketplace
- opportunità matching
- recensioni Google

---

# Obiettivo del Marketplace e del Matching

L'obiettivo del Marketplace e del Matching è facilitare l'incontro tra collezionisti e commercianti, aumentare la probabilità di completamento delle collezioni, migliorare la scoperta di opportunità rilevanti e favorire vendite e scambi senza che CollectorVerse intervenga direttamente nelle transazioni economiche.

---

# Parte 8 - Gamification • CollectorScore • Livelli • Badge • Cornici Profilo • Obiettivi

# Gamification

CollectorVerse utilizza un sistema di gamification per incentivare la partecipazione degli utenti.

L'obiettivo non è creare competizione aggressiva ma premiare:

- partecipazione
- qualità
- contributo alla community
- crescita delle collezioni

---

# CollectorScore

Il CollectorScore rappresenta il punteggio generale dell'utente.

Ogni attività può generare punti.

---

# Utilizzo

Il CollectorScore viene utilizzato per:

- Livelli
- Progressione
- Badge
- Matching
- Affidabilità interna

---

# Configurazione

Tutti i punteggi sono configurabili tramite Dashboard Admin.

---

# Esempi Attività

- Profilo completato
- Oggetto aggiunto alla collezione
- Collezione completata
- Badge ottenuto
- Correzione approvata
- Attività giornaliera
- Partecipazione alla community

---

# Livelli

Ogni utente possiede un livello.

Il livello viene determinato dal CollectorScore.

---

# Livelli Iniziali

Valori iniziali consigliati.

---

## Novizio

Livello iniziale.

---

## Collezionista

Primo livello avanzato.

---

## Esperto

Utente con esperienza significativa.

---

## Master Collector

Utente molto attivo.

---

## Leggenda

Utente storico e autorevole.

---

## Mito

Livello estremamente elevato.

---

## CollectorVerse Hero

Livello speciale assegnabile dagli amministratori.

---

# Configurazione Livelli

Le soglie di avanzamento sono completamente configurabili tramite Dashboard Admin.

---

# Cornici Profilo

Ogni livello può possedere una cornice dedicata.

---

## Novizio

Cornice Grigia

---

## Collezionista

Cornice Verde

---

## Esperto

Cornice Blu

---

## Master Collector

Cornice Viola

---

## Leggenda

Cornice Oro

---

## Mito

Cornice Animata

---

## CollectorVerse Hero

Cornice Speciale

---

# Visibilità Cornici

Le cornici devono essere visibili in:

- Profilo Utente
- Collezioni Pubbliche
- Wishlist Pubbliche
- Chat
- Marketplace
- Commenti
- Revisioni Catalogo

---

# Badge

CollectorVerse utilizza un sistema di badge per riconoscere risultati, esperienza e contributi.

---

# Informazioni Badge

Ogni badge deve contenere:

- Nome
- Descrizione
- Icona
- Requisiti
- Data ottenimento

---

# Categorie Badge

---

## Profilo

Esempi:

- Profilo Completo
- Profilo Avanzato

---

## Collezionista

Esempi:

- 100 Oggetti
- 500 Oggetti
- 1000 Oggetti
- 5000 Oggetti

---

## Completamento

Esempi:

- Prima Serie Completata
- Prima Collezione Completata
- 100% Categoria

---

## Fedeltà

Esempi:

- 30 Giorni
- 180 Giorni
- 365 Giorni
- 3 Anni

---

## Marketplace

Esempi:

- Primo Annuncio
- Primo Scambio
- Primo Contatto

---

## Community

Esempi:

- Primo Follow
- Prima Collezione Pubblica
- Prima Wishlist Pubblica

---

## Contributori Catalogo

Badge dedicati ai revisori del catalogo.

---

# Livelli Contributore Catalogo

---

## Contributore Catalogo

Livello iniziale.

---

## Contributore Esperto

Utente con esperienza nelle revisioni.

---

## Curatore Catalogo

Contributore altamente affidabile.

---

# Esperto Serie

CollectorVerse riconosce gli utenti particolarmente esperti di una determinata serie.

---

## Esempio

```text
Pokémon

↓

Set Base

↓

Completamento Elevato

↓

Badge Esperto Set Base
```

---

# Soglia Esperto Serie

Configurabile tramite Dashboard Admin.

Valori iniziali consigliati:

```text
90%

95%

100%
```

---

# Visualizzazione

Il badge deve essere mostrato pubblicamente nel profilo utente.

---

# Progressione Badge

Ogni badge deve mostrare:

- stato attuale
- progresso
- requisiti mancanti

---

## Esempio

Badge:

```text
500 Oggetti
```

---

Progressione:

```text
322 / 500
```

---

# Obiettivi Giornalieri

CollectorVerse supporta obiettivi giornalieri.

---

# Esempi

- Effettua 3 scansioni
- Aggiungi un oggetto
- Aggiorna la wishlist
- Effettua una revisione
- Segui una nuova collezione

---

# Ricompense

Configurabili tramite Dashboard Admin.

---

## Esempi

- CollectorScore
- Badge speciali
- Bonus temporanei
- Scansioni aggiuntive

---

# Schermata Badge

Ogni utente possiede una sezione dedicata ai badge.

---

# Filtri Disponibili

- Tutti
- Ottenuti
- Non Ottenuti
- In Progressione

---

# Affidabilità Visiva

L'indice di affidabilità interno non viene mostrato numericamente.

---

# Rappresentazione

Visualizzare solamente:

```text
🟢 Alta

🟡 Media

🔴 Bassa
```

---

# Profilo Utente

Nel profilo devono essere mostrati:

- CollectorScore
- Livello
- Cornice
- Badge
- Affidabilità
- Data iscrizione

---

# Dashboard Admin

Configurazioni modificabili senza aggiornare il codice.

---

## CollectorScore

- punteggi attività
- bonus
- moltiplicatori

---

## Livelli

- soglie
- nomi
- progressione

---

## Badge

- attivazione/disattivazione
- icone
- descrizioni
- requisiti

---

## Cornici

- immagini
- animazioni
- requisiti

---

## Obiettivi Giornalieri

- attivazione
- quantità
- premi

---

## Affidabilità

- parametri utilizzati
- peso dei parametri

---

## Esperto Serie

- soglie percentuali
- categorie abilitate
- serie abilitate

# Parte 9 - Esperienza Utente • Home • Profilo • Attività • Notifiche • Tutorial • Assistenza • Importazione • Esportazione

# Esperienza Utente

L'interfaccia di CollectorVerse deve essere semplice, intuitiva e personalizzabile.

Ogni utente deve poter adattare la propria esperienza alle proprie esigenze senza richiedere competenze tecniche.

---

# Obiettivi

L'esperienza utente deve:

- essere semplice da apprendere
- essere veloce da utilizzare
- richiedere pochi passaggi operativi
- valorizzare le collezioni personali
- facilitare la scoperta di nuovi contenuti
- incentivare la partecipazione alla community
- rendere immediatamente accessibili le funzionalità principali

---

# Primo Accesso

Alla prima apertura dell'applicazione l'utente deve completare una configurazione guidata iniziale.

---

# Interessi Iniziali

L'utente può selezionare le categorie di maggior interesse.

---

## Esempi

- Carte Collezionabili
- Numismatica
- Fumetti e Libri
- LEGO e Costruzioni
- Videogiochi

---

# Utilizzo Interessi

Le categorie selezionate vengono utilizzate per:

- Home Personalizzata
- Suggerimenti
- Matching
- Notifiche
- Contenuti in Evidenza

---

# Tutorial Iniziale

Durante il primo accesso deve essere disponibile un tutorial guidato.

---

## Argomenti

- Catalogo Universale
- Collezioni Personali
- Wishlist
- Scanner
- Marketplace
- Matching
- Catalogo Collaborativo

---

# Home

La Home rappresenta il punto di accesso principale dell'applicazione.

---

# Obiettivi Home

Fornire una panoramica immediata di:

- Collezioni
- Wishlist
- Scanner
- Marketplace
- Matching
- Notifiche
- Badge
- Attività Recenti

---

# Home Personalizzata

La Home deve essere composta da widget configurabili.

---

# Widget Base

Disponibili per tutti gli utenti.

---

## Widget

- Le Mie Collezioni
- Wishlist
- Scansioni Disponibili
- Badge
- Attività Recenti
- Notifiche Recenti

---

# Widget Premium

Disponibili per Premium, Premium Plus e Commercianti.

---

## Widget

- Scambi Consigliati
- Utenti Consigliati
- Opportunità Marketplace

---

# Widget Premium Plus

Disponibili per Premium Plus e Commercianti.

---

## Widget

- Match Vicini
- Utenti Vicini
- Opportunità Locali
- Attività Geolocalizzate

---

# Personalizzazione Home

L'utente può:

- mostrare widget
- nascondere widget
- riordinare widget

---

# Obiettivi Giornalieri

La Home può mostrare gli obiettivi giornalieri.

---

## Informazioni Mostrate

- obiettivi disponibili
- avanzamento
- premi ottenibili
- tempo rimanente

---

# Profilo Utente

Ogni utente possiede una schermata Profilo dedicata.

---

# Informazioni Principali

Visualizzare:

- Avatar
- Cover
- Cornice Profilo
- Username
- Display Name
- Piano Attivo
- Ruolo
- CollectorScore
- Livello
- Affidabilità
- Data Iscrizione

---

# Badge Profilo

Possibili valori:

```text
👤 Collezionista

⭐ Collezionista Premium

💎 Collezionista Premium Plus

🏪 Commerciante

✅🏪 Commerciante Verificato

🛡️ Moderatore

⚙️ Amministratore
```

---

# Indicatore Affidabilità

L'affidabilità non viene mostrata con un valore numerico.

---

## Rappresentazione

```text
🟢 Alta

🟡 Media

🔴 Bassa
```

---

# Indicatori Funzionalità

Mostrare chiaramente le funzionalità disponibili all'utente.

---

## Chat

```text
💬 Chat Disponibile
```

oppure

```text
🚫 Non può avviare nuove conversazioni
```

---

## Marketplace

```text
🟢 Marketplace Attivo
```

oppure

```text
⚪ Marketplace Non Attivo
```

---

# Sezioni Profilo

- Collezioni
- Wishlist
- Disponibili per Vendita
- Disponibili per Scambio
- Annunci
- Recensioni
- Badge
- Contributori Catalogo
- Le Mie Attività
- Cronologia Scansioni
- Importazione
- Esportazione
- Tutorial
- Centro Assistenza
- Abbonamenti e Pacchetti

---

# Collezioni

Visualizzare:

- Collezioni Pubbliche
- Collezioni Private
- Percentuali di Completamento
- Numero Oggetti
- Numero Versioni Possedute
- Numero Varianti Possedute

---

# Wishlist

Ogni Wishlist può essere:

```text
Pubblica

Privata
```

---

# Disponibili per Vendita

Visualizzare:

- Oggetto
- Versione
- Variante
- Condizione
- Prezzo
- Valuta

---

# Disponibili per Scambio

Visualizzare:

- Oggetto
- Versione
- Variante
- Condizione

---

# Annunci

Mostrare tutti gli annunci creati dall'utente.

---

## Informazioni Visualizzate

- Oggetto
- Versione
- Variante
- Prezzo
- Valuta
- Stato Annuncio
- Data Pubblicazione

---

# Recensioni

Visualizzare:

- Media Recensioni
- Numero Recensioni
- Ultime Recensioni Ricevute

---

# Le Mie Attività

Storico delle attività dell'utente.

---

## Eventi Visualizzati

- Oggetti creati
- Versioni create
- Varianti create
- Rarità proposte
- Correzioni proposte
- Correzioni approvate
- Badge ottenuti
- Livelli ottenuti
- Scansioni effettuate

---

# Cronologia Scansioni

Area dedicata alle ultime scansioni effettuate.

---

## Informazioni Mostrate

- Data
- Immagine
- Categoria
- Collezione
- Serie
- Oggetto
- Versione
- Variante
- Affidabilità
- Risultato

---

# Abbonamenti e Pacchetti

Sezione dedicata alla situazione commerciale dell'account.

---

## Informazioni Visualizzate

- Piano Attivo
- Data Scadenza
- Bundle Attivi
- Pacchetti Attivi
- Pacchetti Congelati
- Pacchetti Scaduti

---

## Esempio

```text
Pacchetto +100 Annunci

Stato:
Congelato

Tempo Residuo:
8 mesi e 12 giorni
```

---

# Valuta Preferita

Ogni utente può modificare la propria valuta preferita.

---

## Utilizzo

La valuta selezionata viene proposta automaticamente durante la pubblicazione degli annunci.

---

# Profilo Pubblico

Ogni utente può condividere il proprio profilo pubblico.

---

# Informazioni Visibili

- Avatar
- Cornice
- CollectorScore
- Livello
- Badge
- Affidabilità
- Recensioni
- Collezioni Pubbliche
- Wishlist Pubbliche
- Disponibili per Vendita
- Disponibili per Scambio

---

# Condivisione Profilo

Disponibile tramite:

- Link Pubblico
- QR Code Profilo

---

# QR Code Profilo

Il QR Code deve essere collegato all'identificativo interno dell'utente.

---

# Regola Fondamentale

La modifica di Username o Display Name non deve invalidare il QR Code.

---

# Notifiche

CollectorVerse utilizza un sistema notifiche centralizzato.

---

# Canali Disponibili

## Push

Inviate tramite:

```text
Firebase Cloud Messaging (FCM)
```

---

## Email

Inviate tramite:

```text
Brevo
```

---

## In-App

Disponibili all'interno del Centro Notifiche.

---

# Preferenze Notifiche

Ogni categoria può essere configurata separatamente.

---

## Esempio

```text
Push ✅

Email ❌

In-App ✅
```

---

# Centro Notifiche

Le notifiche devono essere facilmente consultabili.

---

## Filtri Disponibili

- Tutte
- Non Lette
- Sistema

---

# Tipologie Notifiche

---

## Marketplace

- Nuovi Annunci Compatibili
- Nuove Opportunità
- Interesse per i propri Oggetti

---

## Chat

- Nuove Richieste di Contatto
- Nuovi Messaggi

---

## Matching

- Nuovi Match
- Nuove Opportunità di Scambio
- Opportunità di Completamento

---

## Catalogo

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuove Rarità

---

## Follow Categoria

- Nuove Collezioni
- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

## Follow Collezione

- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuovi Commercianti

---

## Follow Serie

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

## Follow Oggetto

- Nuove Versioni
- Nuove Varianti
- Nuove Immagini
- Nuovi Annunci

---

## Follow Utente

- Nuovi Annunci
- Nuove Collezioni Pubbliche

---

## Follow Commerciante

- Nuovi Annunci
- Aggiornamenti Profilo
- Nuove Recensioni Google

---

## Gamification

- Nuovi Badge
- Passaggio Livello
- Obiettivi Completati

---

## Abbonamenti

- Scadenza Imminente
- Pacchetti Congelati
- Bundle in Scadenza

---

# Promemoria Scadenze

Configurabili tramite Dashboard Admin.

---

## Valori Iniziali Consigliati

- 7 giorni prima
- 3 giorni prima
- giorno di scadenza

---

# Tutorial

CollectorVerse include un sistema tutorial integrato.

---

# Tutorial Iniziale

Visualizzato durante il primo accesso.

---

# Argomenti

- Collezioni
- Catalogo
- Scanner
- Marketplace
- Matching
- Community

---

# Tutorial Successivi

Consultabili in qualsiasi momento.

---

## Percorso

```text
Profilo
↓
Tutorial
```

---

# Centro Assistenza

Area dedicata al supporto utenti.

---

# Contenuti

- FAQ
- Guide
- Tutorial
- Contatti
- Segnalazioni

---

# Segnalazioni

Gli utenti possono segnalare:

- Problemi Tecnici
- Errori Catalogo
- Immagini
- Recensioni
- Utenti
- Annunci Marketplace

---

# Importazione

CollectorVerse supporta l'importazione delle Collezioni Personali.

---

# Formati Supportati

- Excel
- CSV

---

# Simulazione Importazione

Prima dell'importazione definitiva deve essere mostrata una simulazione.

---

## Esempio

```text
Oggetti trovati: 1200

Oggetti riconosciuti: 1180

Oggetti non riconosciuti: 20
```

---

# Correzione Guidata

Gli elementi non riconosciuti non vengono importati automaticamente.

---

## Azioni Disponibili

- Importa Elementi Riconosciuti
- Esporta Elementi Non Riconosciuti

---

# Esportazione

Gli utenti possono esportare i propri dati.

---

# Formati Supportati

- PDF
- Excel

---

# Ricerca Globale

CollectorVerse dispone di una ricerca globale.

---

# Ricerca

Consentire la ricerca di:

- Categorie
- Collezioni
- Serie
- Oggetti
- Versioni
- Varianti
- Utenti
- Commercianti

---

# Dashboard Admin

Tutte le configurazioni devono essere modificabili senza aggiornare il codice.

---

# Configurazioni Home

- Widget Disponibili
- Widget Premium
- Widget Premium Plus

---

# Configurazioni Profilo

- Sezioni abilitate
- Informazioni visibili
- Layout profilo

---

# Configurazioni Notifiche

- Template
- Categorie
- Priorità
- Attivazione

---

# Configurazioni Tutorial

- Step
- Ordine
- Obbligatorietà

---

# Configurazioni Importazione

- Formati Consentiti
- Dimensione Massima File
- Limiti Importazione

---

# Configurazioni Esportazione

- Formati Disponibili
- Limiti Esportazione

---

# Obiettivo dell'Esperienza Utente

L'Esperienza Utente deve consentire ad ogni collezionista di accedere rapidamente alle proprie collezioni, utilizzare in modo semplice le funzionalità principali della piattaforma, ricevere informazioni rilevanti e personalizzare il proprio percorso all'interno dell'ecosistema CollectorVerse mantenendo semplicità, velocità e coerenza operativa.

---

# Parte 10 - Dashboard Amministratore • Configurazioni Globali • Moderazione • Asset Grafici • Statistiche

# Obiettivo

La Dashboard Amministratore rappresenta il centro di controllo operativo di CollectorVerse.

Tutte le configurazioni dinamiche della piattaforma devono essere gestite attraverso la Dashboard senza richiedere modifiche al codice applicativo.

La Dashboard deve consentire il monitoraggio, la gestione e la configurazione completa dell'ecosistema CollectorVerse.

---

# Principi Fondamentali

La Dashboard deve essere:

- Sicura
- Scalabile
- Configurabile
- Tracciabile
- Modularizzabile
- Estendibile

---

# Regola Fondamentale

Qualsiasi valore operativo dovrebbe essere modificabile tramite Dashboard Admin senza richiedere una nuova pubblicazione dell'app quando tecnicamente possibile.

---

# Ruoli Amministrativi

L'accesso alla Dashboard è consentito esclusivamente ai ruoli autorizzati.

```text
Moderatore

Amministratore
```

---

# Moderatore

Può gestire:

- Segnalazioni Utenti
- Segnalazioni Immagini
- Segnalazioni Recensioni
- Segnalazioni Annunci
- Chat Segnalate
- Contenuti Segnalati

---

## Limitazioni

Non può:

```text
❌ modificare monetizzazione

❌ modificare configurazioni globali

❌ gestire infrastruttura

❌ nominare amministratori

❌ modificare piani

❌ modificare prezzi
```

---

# Amministratore

Possiede accesso completo alla Dashboard.

---

## Può Gestire

- Utenti
- Catalogo
- Marketplace
- Matching
- Monetizzazione
- Notifiche
- Sicurezza
- Configurazioni Globali
- Feature Flags
- Statistiche
- Asset Grafici

---

# Dashboard Home

La Dashboard deve fornire una panoramica immediata dello stato della piattaforma.

---

# Indicatori Principali

Visualizzare almeno:

- Utenti Registrati
- Utenti Attivi
- Nuovi Utenti
- Nuovi Premium
- Nuovi Premium Plus
- Nuovi Commercianti
- Commercianti Verificati
- Annunci Attivi
- Scansioni Giornaliere
- Revisioni Catalogo Aperte
- Segnalazioni Aperte
- Notifiche Inviate

---

# Gestione Utenti

Gli Amministratori devono poter ricercare qualsiasi account.

---

# Ricerca Utenti

Supportare almeno:

```text
Username

Email

ID Utente
```

---

# Scheda Utente

La scheda deve visualizzare:

- Profilo
- Piano
- Ruolo
- Stato Account
- CollectorScore
- Livello
- Affidabilità
- Storico Attività
- Segnalazioni Ricevute
- Storico Abbonamenti

---

# Operazioni Disponibili

```text
Sospendi

Riattiva

Blocca

Sblocca

Elimina

Modifica Piano

Modifica Ruolo
```

---

# Gestione Piani

La Dashboard deve consentire la gestione completa dei Piani.

---

# Piani Supportati

```text
Free

Premium

Premium Plus

Commerciante
```

---

# Operazioni Disponibili

```text
Crea

Modifica

Attiva

Disattiva

Archivia
```

---

# Gestione Prezzi

Gli Amministratori devono poter configurare:

- prezzi
- promozioni
- sconti
- offerte temporanee

senza modificare il codice applicativo.

---

# Gestione Durate

Durate iniziali:

```text
Mensile

Trimestrale

Annuale
```

---

# Durate Personalizzate

La Dashboard deve consentire la creazione di nuove durate.

---

## Esempi

```text
30 giorni

90 giorni

180 giorni

24 mesi
```

---

# Gestione Periodo di Prova

CollectorVerse supporta un periodo di prova gratuito.

---

## Configurazioni Disponibili

- Attivazione
- Disattivazione
- Durata
- Piano Associato
- Regole di Utilizzo

---

## Valore Iniziale Consigliato

```text
7 giorni
```

---

# Gestione Commercianti

La Dashboard deve supportare la gestione completa dei Commercianti.

---

# Operazioni Disponibili

```text
Verifica

Revoca Verifica

Sospendi

Riattiva

Elimina
```

---

# Commerciante Verificato

Gli Amministratori possono assegnare:

```text
✅ Commerciante Verificato
```

---

# Verifica

Può richiedere:

- Documentazione Aziendale
- Partita IVA
- Sito Web
- Attività Verificabile

---

# Gestione Catalogo

Gli Amministratori devono poter gestire l'intera struttura del Catalogo Universale.

---

# Entità Gestibili

```text
Categorie

Collezioni

Serie

Oggetti

Rarità

Versioni

Varianti
```

---

# Gestione Categorie

---

## Stati Disponibili

```text
In Sviluppo

Attiva

Nascosta

Archiviata
```

---

## Operazioni

```text
Crea

Modifica

Attiva

Nascondi

Archivia
```

---

# Gestione Collezioni

Operazioni consentite:

```text
Crea

Modifica

Attiva

Disattiva

Archivia
```

---

# Gestione Serie

Operazioni consentite:

```text
Crea

Modifica

Aggiorna release_date

Attiva

Disattiva

Archivia
```

---

# Gestione Rarità

Le Rarità appartengono alle Collezioni.

---

## Operazioni Disponibili

```text
Crea

Modifica

Unifica

Disattiva

Archivia
```

---

# Gestione Oggetti

Operazioni consentite:

```text
Crea

Modifica

Correggi

Disattiva

Archivia

Unifica Duplicati
```

---

# Gestione Versioni

Operazioni consentite:

```text
Crea

Modifica

Correggi

Disattiva

Archivia

Unifica
```

---

# Gestione Varianti

Operazioni consentite:

```text
Crea

Modifica

Correggi

Disattiva

Archivia

Unifica
```

---

# Centro Revisioni Catalogo

La Dashboard deve includere un Centro Revisioni dedicato.

---

# Elementi Revisionabili

- Oggetti
- Versioni
- Varianti
- Rarità
- Immagini
- Correzioni Catalogo

---

# Informazioni Visualizzate

- Categoria
- Collezione
- Serie
- Oggetto
- Versione
- Variante
- Stato Revisione
- Data Creazione
- Utente Proponente

---

# Azioni Disponibili

```text
Approva

Correggi

Rifiuta

Unifica
```

---

# Immagini Catalogo

Le immagini NON appartengono direttamente agli Oggetti.

---

# Regola Fondamentale

Le immagini possono appartenere esclusivamente a:

```text
ItemVersion

oppure

ItemVariant
```

---

# Gestione Immagini

Gli Amministratori devono poter gestire tutte le immagini catalogo.

---

# Operazioni Disponibili

```text
Approva

Rifiuta

Archivia

Imposta Ufficiale

Sostituisci Immagine Ufficiale

Blocca
```

---

# Priorità Visualizzazione Immagini

La piattaforma utilizza il seguente ordine:

```text
Immagine Variante
↓
Immagine Versione
↓
Placeholder
```

---

# Asset Grafici

La Dashboard deve consentire la gestione degli asset grafici.

---

# Asset Gestibili

- Loghi Categoria
- Banner Categoria
- Loghi Collezione
- Banner Collezione
- Badge
- Cornici Profilo
- Placeholder

---

# Placeholder

Placeholder iniziali:

```text
Categoria

Collezione

Oggetto

Profilo

Immagine Mancante
```

---

# Configurazioni Monetizzazione

La Dashboard deve consentire la gestione completa della monetizzazione.

---

# Configurazioni Disponibili

- Piani
- Prezzi
- Durate
- Periodo di Prova
- Bundle
- Pacchetti
- Reward Video
- Scansioni Bonus

---

# Provider Pagamenti

La piattaforma deve supportare provider configurabili.

---

## Provider Iniziale

```text
Google Play Billing
```

---

# Provider Pubblicitari

La piattaforma deve supportare provider pubblicitari configurabili.

---

## Provider Iniziale

```text
Google AdMob
```

---

# Gestione Pubblicità

Configurazioni disponibili:

- Banner
- Rewarded Video
- Frequenza
- Limiti Giornalieri
- Cooldown

---

# Gestione Marketplace

Configurazioni disponibili:

- Limiti Annunci
- Durata Annunci
- Visibilità Annunci
- Stati Annuncio

---

## Limiti Iniziali Consigliati

### Premium

```text
10 annunci
```

---

### Premium Plus

```text
30 annunci
```

---

### Commerciante

```text
100 annunci
```

---

# Gestione Scansioni

Configurazioni disponibili:

- Scansioni Giornaliere
- Scansioni Reward
- Cooldown
- Limiti Giornalieri
- Provider OCR
- Provider AI
- Soglia Affidabilità

---

## Limiti Iniziali Consigliati

### Free

```text
3 scansioni
```

### Premium

```text
20 scansioni
```

### Premium Plus

```text
40 scansioni
```

### Commerciante

```text
100 scansioni
```

---

# Gestione Matching

Configurazioni disponibili:

- Pesi Matching
- Formule Matching
- Distanza Geografica
- Filtri Geografici
- Soglie Compatibilità

---

# Gestione Gamification

Configurazioni disponibili:

- CollectorScore
- Livelli
- Badge
- Cornici
- Obiettivi
- Streak
- Esperto Serie

---

# Gestione Notifiche

Configurazioni disponibili:

- Categorie
- Template
- Priorità
- Canali
- Digest

---

# Gestione Valute

La Dashboard deve consentire la gestione delle valute supportate.

---

# Operazioni Disponibili

```text
Crea

Modifica

Nascondi

Archivia
```

---

# Feature Flags

La piattaforma deve supportare attivazione e disattivazione dinamica delle funzionalità.

---

# Funzionalità Gestibili

```text
Marketplace

Matching

Chat

Recensioni

Scanner

Notifiche

Catalogo Collaborativo

Importazione

Esportazione
```

---

# Audit Log

Ogni operazione amministrativa deve essere registrata.

---

# Informazioni Minime

- Amministratore
- Data
- Ora
- Azione
- Risorsa Coinvolta

---

# Caratteristiche

```text
Immodificabile

Persistente

Consultabile

Ricercabile
```

---

# Cestino Amministrativo

Gli elementi eliminati devono essere conservati temporaneamente.

---

## Durata Iniziale Consigliata

```text
30 giorni
```

---

# Operazioni Disponibili

```text
Ripristina

Elimina Definitivamente
```

---

# Statistiche

La Dashboard deve fornire statistiche avanzate sull'intera piattaforma.

---

# Statistiche Disponibili

- Crescita Utenti
- Crescita Catalogo
- Crescita Commercianti
- Conversioni Prova Gratuita
- Conversioni Abbonamenti
- Utilizzo Marketplace
- Utilizzo Matching
- Utilizzo Scanner
- Utilizzo Pubblicità
- Entrate Pubblicitarie
- Entrate Abbonamenti

---

# Esportazioni Amministrative

Gli Amministratori devono poter esportare:

- Catalogo
- Configurazioni
- Revisioni
- Statistiche
- Marketplace

---

# Modalità Manutenzione

La piattaforma deve supportare una modalità manutenzione.

---

# Operazioni Disponibili

```text
Attiva

Disattiva

Programma

Messaggio Personalizzato
```

---

# Effetti

Durante la manutenzione:

- l'accesso utenti può essere limitato
- alcune funzionalità possono essere disattivate
- Moderatori e Amministratori mantengono l'accesso

---

# Sicurezza Operativa

Le operazioni amministrative più critiche devono poter richiedere conferma aggiuntiva.

---

## Esempi

- Eliminazione definitiva
- Revoca Verifica Commerciante
- Cambio Ruolo
- Modifica Piano
- Ripristino Dati
- Disattivazione Categoria

---

# Obiettivo della Dashboard Admin

La Dashboard Admin rappresenta il punto centrale di gestione di CollectorVerse e deve consentire ad Amministratori e Moderatori di configurare, controllare, monitorare e mantenere l'intera piattaforma senza richiedere modifiche al codice applicativo, garantendo contemporaneamente sicurezza, tracciabilità, controllo operativo e scalabilità futura.

---

# Parte 11 - Strategia di Lancio • Crescita Progressiva • Evoluzione del Catalogo

# Obiettivo

CollectorVerse deve poter essere lanciata sul mercato senza richiedere il completamento dell'intero Catalogo Universale.

La crescita del catalogo deve avvenire progressivamente attraverso:

- amministratori
- commercianti
- community
- contributori catalogo

---

# Principio Fondamentale

```text
Una categoria completa

>

Molte categorie incomplete
```

---

# Strategia di Lancio

CollectorVerse deve essere progettata per consentire il rilascio pubblico anche con una sola categoria attiva.

---

# Categoria Attiva al Lancio

```text
Carte Collezionabili
```

---

# Motivazioni

- grande base utenti
- forte presenza di commercianti
- elevata attività marketplace
- ottima compatibilità con la scansione
- cataloghi facilmente reperibili
- forte propensione allo scambio

---

# Categorie in Sviluppo

Le categorie in sviluppo possono essere preparate dagli amministratori senza essere visibili agli utenti.

---

## Prima Fase

```text
Numismatica

Fumetti e Libri

LEGO e Costruzioni
```

---

## Seconda Fase

```text
Filatelia

Action Figure e Toys

Videogiochi
```

---

## Terza Fase

```text
Musica e Media

Orologi e Gioielli

Militaria e Storico
```

---

## Quarta Fase

```text
Modellismo

Antiquariato e Arte

Enologia e Spirits
```

---

# Crescita Progressiva

Le nuove categorie possono essere attivate direttamente dalla Dashboard Admin.

---

# Vantaggi

- riduzione dei tempi di lancio
- maggiore qualità del catalogo
- minore complessità iniziale
- validazione del mercato
- crescita controllata

---

# Processo Attivazione Categoria

```text
Creazione Categoria

↓

Popolamento Catalogo

↓

Verifica Qualità

↓

Attivazione Categoria

↓

Disponibile agli utenti
```

---

# Coinvolgimento Community

La crescita del catalogo deve essere supportata da:

- scansioni
- nuovi oggetti
- nuove versioni
- nuove varianti
- immagini collaborative
- contributori catalogo

---

# Priorità di Sviluppo

L'ordine di sviluppo futuro deve essere guidato da:

- numero utenti interessati
- numero follower categoria
- attività marketplace
- disponibilità cataloghi
- disponibilità commercianti

---

# Metriche Categoria

Per ogni categoria monitorare:

- Numero Collezioni
- Numero Serie
- Numero Oggetti
- Numero Versioni
- Numero Varianti
- Numero Utenti
- Numero Follower
- Numero Annunci
- Numero Commercianti

---

# Internazionalizzazione

CollectorVerse deve essere progettata per supportare utenti internazionali fin dalla Versione 1.0.

---

# Elementi Internazionali

- valute multiple
- lingue multiple
- geolocalizzazione globale
- marketplace internazionale
- catalogo condiviso globale

---

# Evoluzione del Prodotto

Le future versioni di CollectorVerse potranno introdurre:

- collezioni condivise
- strumenti avanzati per commercianti
- analytics avanzate
- integrazioni esterne
- nuove categorie
- nuove modalità di matching

---

# Compatibilità Futura

Ogni nuova funzionalità dovrà rispettare:

- compatibilità con il Catalogo Universale
- compatibilità con il Marketplace
- compatibilità con il Matching
- compatibilità con la Dashboard Admin

---

# Obiettivo Finale

Costruire una piattaforma universale in grado di gestire qualsiasi tipologia di collezione mantenendo:

- semplicità d'utilizzo
- elevata qualità del catalogo
- scalabilità
- sostenibilità economica
- crescita progressiva
