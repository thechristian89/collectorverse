
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

---

# Parte 1 - Vision e Fondamenta

# Stato Documento

Questo documento rappresenta la specifica ufficiale e definitiva di CollectorVerse.

Tutte le future attività di:

- UX
- Business Rules
- Database Architecture
- Data Model
- Supabase
- Frontend
- Mobile App

devono essere coerenti con quanto definito in questo Blueprint.

---

# Vision

CollectorVerse vuole diventare la piattaforma universale di riferimento per il collezionismo.

L'obiettivo è consentire ai collezionisti di tutto il mondo di:

- catalogare
- organizzare
- completare
- condividere
- acquistare
- vendere
- scambiare

qualsiasi tipologia di oggetto collezionabile attraverso un unico ecosistema digitale.

---

# Mission

Creare il più grande ecosistema digitale dedicato al collezionismo.

CollectorVerse deve permettere agli utenti di:

- gestire le proprie collezioni
- creare wishlist
- scansionare oggetti
- riconoscere oggetti
- trovare altri collezionisti
- trovare commercianti specializzati
- contribuire al catalogo globale
- condividere la propria esperienza

---

# Obiettivi Principali

CollectorVerse deve offrire:

- Catalogo Universale
- Catalogazione Personale
- Wishlist
- Marketplace
- Chat
- Matching
- Geolocalizzazione
- Scansione Oggetti
- Catalogo Collaborativo
- Versioni
- Varianti
- Community
- Gamification
- Dashboard Amministratore
- Monetizzazione sostenibile

---

# Filosofia del Progetto

CollectorVerse NON è:

- un sito di aste
- un intermediario finanziario
- un sistema di pagamento
- un gestore di spedizioni

CollectorVerse È:

- un catalogo universale
- una piattaforma di incontro
- una community di collezionisti
- uno strumento di gestione collezioni
- un sistema di scoperta e condivisione

---

# Principi Fondamentali

Ogni nuova funzionalità deve rispettare i seguenti principi.

---

## Semplicità

Le funzionalità devono essere utilizzabili anche da utenti senza competenze tecniche.

---

## Scalabilità

La piattaforma deve supportare:

- milioni di utenti
- milioni di oggetti
- milioni di immagini
- milioni di annunci

senza modifiche strutturali.

---

## Collaborazione

La community contribuisce alla crescita e al miglioramento del catalogo.

---

## Qualità

Tutte le informazioni devono poter essere:

- controllate
- corrette
- revisionate
- migliorate

---

## Configurabilità

Qualsiasi:

- numero
- limite
- soglia
- durata
- percentuale
- punteggio
- moltiplicatore
- valore economico

deve essere modificabile dalla Dashboard Admin senza modificare il codice applicativo.

---

## Estensibilità

CollectorVerse deve poter ampliare nel tempo:

- categorie
- collezioni
- serie
- oggetti
- versioni
- varianti

senza modificare la struttura del database.

---

# Strategia di Lancio

CollectorVerse non richiede che tutte le categorie siano disponibili al lancio.

Le categorie possono essere sviluppate e pubblicate progressivamente.

---

# Principio di Lancio

Una categoria completa è preferibile a molte categorie incomplete.

---

# Categoria Attiva al Lancio

Carte Collezionabili

---

# Categorie in Sviluppo

- Numismatica
- Fumetti e Libri
- LEGO e Costruzioni

---

# Categorie Future

- Filatelia
- Action Figure e Toys
- Videogiochi
- Musica e Media
- Orologi e Gioielli
- Militaria e Storico
- Modellismo
- Antiquariato e Arte
- Enologia e Spirits

---

# Architettura Generale

Utente

↓

Applicazione CollectorVerse

↓

Cloudflare

↓

Supabase

↓

PostgreSQL

↓

Cloudflare R2

↓

Cloudflare Images

---

# Stack Tecnologico Ufficiale

## Frontend

- React
- TypeScript
- Vite

---

## Backend

- Supabase

---

## Database

- PostgreSQL

---

## Storage

- Cloudflare R2

---

## Gestione Immagini

- Cloudflare Images

---

## Notifiche Push

- Firebase Cloud Messaging (FCM)

---

## Email

- Brevo

---

## Analytics

- PostHog

---

## Error Monitoring

- Sentry

---

## Business Intelligence

- Metabase

---

## Intelligenza Artificiale

- OpenAI API

Utilizzata esclusivamente come supporto avanzato nei processi di:

- scansione
- riconoscimento
- classificazione

e solo quando i sistemi tradizionali non sono sufficienti.

---

## Versionamento

- GitHub

---

# Governance del Progetto

Tutte le configurazioni operative devono essere gestite dalla Dashboard Admin senza pubblicare nuove versioni dell'applicazione quando tecnicamente possibile.

Questo principio si applica a:

- Marketplace
- Matching
- Scansioni
- Badge
- Livelli
- CollectorScore
- Versioni
- Varianti
- Notifiche
- Geolocalizzazione
- Pubblicità
- Monetizzazione

---

# Obiettivo Versione 1.0

L'obiettivo della Versione 1.0 è il rilascio pubblico della prima versione stabile di CollectorVerse.

La Versione 1.0 deve consentire:

- gestione collezioni
- catalogazione personale
- utilizzo del catalogo globale
- scansione degli oggetti
- marketplace
- matching
- catalogo collaborativo
- gamification
- amministrazione completa della piattaforma

senza necessità di modifiche strutturali all'architettura del sistema.

# Parte 2 - Utenti • Privacy • Sicurezza • Recensioni • Gestione Account

# Tipologie Utente

CollectorVerse prevede diverse tipologie di account.

---

## Collezionista

Rappresenta l'utente standard della piattaforma.

Può:

- creare collezioni
- utilizzare il catalogo
- creare wishlist
- effettuare scansioni
- seguire categorie
- seguire collezioni
- seguire serie
- seguire oggetti
- seguire utenti
- partecipare alla community

---

## Collezionista Premium

Include tutte le funzionalità del Collezionista.

Inoltre può:

- avviare nuove conversazioni
- utilizzare il marketplace
- creare annunci
- utilizzare il matching

---

## Collezionista Premium Plus

Include tutte le funzionalità Premium.

Inoltre può:

- utilizzare la geolocalizzazione utenti
- visualizzare la mappa utenti
- accedere ai matching avanzati

---

## Commerciante

Rappresenta un'attività commerciale.

Può:

- gestire un profilo attività
- comparire nella mappa
- creare annunci
- utilizzare la chat
- utilizzare il matching
- partecipare al programma Contributori Catalogo

---

## Commerciante Verificato

Badge assegnato manualmente dagli amministratori.

Visualizzazione:

✅ Commerciante Verificato

---

## Moderatore

Ruolo intermedio tra utente e amministratore.

Può gestire:

- segnalazioni
- immagini segnalate
- recensioni segnalate
- annunci segnalati
- contenuti segnalati

Non può gestire:

- configurazioni globali
- monetizzazione
- amministratori
- infrastruttura

---

## Amministratore

Accesso completo alla Dashboard Admin.

---

# Identificazione Account

Ogni profilo deve mostrare chiaramente il tipo di account.

Visualizzazioni disponibili:

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

# Indicatori Funzionalità

Ogni profilo deve visualizzare le funzionalità disponibili.

---

## Chat

Possibili stati:

```text
💬 Chat Disponibile
```

oppure

```text
🚫 Non può avviare nuove conversazioni
```

---

## Marketplace

Possibili stati:

```text
🟢 Marketplace Attivo
```

oppure

```text
⚪ Marketplace Non Attivo
```

---

# Registrazione

Modalità disponibili:

- Email
- Google

---

# Informazioni Richieste

## Utente

Campi obbligatori:

- Nome Utente
- Email
- Password (solo registrazione tramite Email)

---

## Commerciante

Campi aggiuntivi:

- Nome attività
- Categorie trattate
- Indirizzo attività
- Telefono (facoltativo)
- Sito Web (facoltativo)
- Collegamento Google Maps (facoltativo)

---

# Login

Supportato tramite:

- Email e Password
- Google

---

# Recupero Password

Disponibile per gli account registrati tramite Email.

---

# Profilo Utente

Ogni utente possiede un profilo personale.

---

## Informazioni Mostrate

- Avatar
- Cornice Profilo
- Nome Utente
- CollectorScore
- Livello
- Affidabilità
- Data Iscrizione
- Badge
- Recensioni

---

# Valuta Preferita

Ogni utente può configurare una valuta preferita.

Esempi:

```text
EUR €

USD $

GBP £

JPY ¥

CHF
```

La valuta verrà utilizzata automaticamente per tutti i prezzi inseriti dall'utente.

---

# Profilo Pubblico

Ogni utente possiede un profilo condivisibile.

Esempio:

```text
collectorverse.com/u/nomeutente
```

---

# Condivisione Profilo

Disponibile tramite:

- Link pubblico
- QR Code profilo

---

# QR Code

Il QR Code deve essere collegato all'identificativo interno dell'utente.

L'eventuale modifica dello username non deve invalidare il QR Code.

---

# Privacy Profilo

Configurabile dall'utente.

---

## Stati

```text
Pubblico

Privato
```

---

# Collezioni

Ogni collezione può essere:

```text
Pubblica

Privata
```

indipendentemente dalla visibilità del profilo.

---

# Wishlist

Ogni wishlist può essere:

```text
Pubblica

Privata
```

indipendentemente dalla visibilità del profilo.

---

# Ricerca Utenti

Tutti gli utenti possono:

- cercare utenti
- visualizzare profili pubblici
- seguire utenti

nel rispetto delle impostazioni privacy.

---

# Recensioni

Le recensioni rappresentano uno strumento di fiducia tra utenti.

Non costituiscono l'unico indicatore di affidabilità.

---

# Generazione Recensione

Le recensioni vengono generate tramite un link dedicato.

---

## Regole

Il link:

- dura 24 ore
- può essere utilizzato una sola volta
- può essere inviato solamente tramite chat CollectorVerse
- può essere utilizzato solo da utenti registrati

---

# Limiti

Una coppia di utenti può recensirsi una sola volta.

Valori configurabili tramite Dashboard Admin.

---

# Valutazione

Sistema a stelle.

Esempio:

```text
★★★★★
```

---

# Visualizzazione

Mostrare:

- Media recensioni
- Numero recensioni

Esempio:

```text
4,8 ★

132 recensioni
```

---

# Segnalazione Recensioni

Ogni recensione può essere segnalata.

Le segnalazioni vengono valutate da Moderatori e Amministratori.

---

# Affidabilità

CollectorVerse utilizza un indice di affidabilità interno.

---

## Possibili Parametri

- recensioni
- numero recensioni
- attività
- anzianità account
- CollectorScore
- badge
- storico comportamentale

---

# Visualizzazione Affidabilità

Non viene mostrato il valore numerico.

Visualizzare solamente:

```text
🟢 Alta

🟡 Media

🔴 Bassa
```

---

# Richieste di Contatto

Le richieste di contatto precedono l'apertura di una nuova chat.

---

## Informazioni Mostrate

Quando arriva una richiesta visualizzare:

- Nome Utente
- Tipologia Account
- Affidabilità
- Valutazione recensioni
- Numero recensioni
- CollectorScore
- Badge principali

---

## Azioni Disponibili

```text
✅ Accetta

❌ Rifiuta

🚫 Blocca Utente
```

---

# Anti-Spam

Dopo un rifiuto l'utente non può reinviare immediatamente una nuova richiesta.

Il tempo minimo è configurabile dalla Dashboard Admin.

Valore iniziale consigliato:

```text
1 giorno
```

---

# Impostazioni Richieste Chat

Ogni utente può decidere chi può contattarlo.

---

## Opzioni

```text
✅ Tutti

✅ Solo utenti Premium

✅ Solo commercianti

❌ Nessuno
```

---

# Chat Utenti Free

Gli utenti Free:

```text
✅ possono ricevere richieste di contatto

✅ possono ricevere messaggi

✅ possono rispondere alle conversazioni ricevute

❌ non possono avviare nuove conversazioni
```

---

# Chat Utenti Premium

Possono:

```text
✅ avviare conversazioni

✅ ricevere conversazioni

✅ rispondere
```

---

# Chat Utenti Premium Plus

Possono:

```text
✅ avviare conversazioni

✅ ricevere conversazioni

✅ rispondere
```

---

# Chat Commercianti

Possono:

```text
✅ avviare conversazioni

✅ ricevere conversazioni

✅ rispondere
```

---

# Blocco Utente

Il blocco utente è totale.

---

## Effetti

Se l'Utente A blocca l'Utente B:

l'Utente B non può:

```text
❌ visualizzare il profilo di A

❌ visualizzare collezioni pubbliche di A

❌ visualizzare wishlist pubbliche di A

❌ visualizzare oggetti in vendita di A

❌ visualizzare oggetti in scambio di A

❌ inviare richieste di contatto

❌ aprire chat

❌ seguire A

❌ comparire nei risultati di ricerca relativi ad A
```

---

# Sicurezza

CollectorVerse deve implementare un sistema di sicurezza multilivello.

---

# Verifica Email

Configurabile tramite Dashboard Admin.

---

# Autenticazione a Due Fattori (2FA)

Configurabile tramite Dashboard Admin.

---

## Stati Possibili

```text
Disattivata

Facoltativa

Obbligatoria
```

---

# Ruoli Consigliati

2FA obbligatoria per:

- Moderatori
- Amministratori

---

# Eliminazione Account

L'utente può richiedere:

```text
Eliminazione account

Cancellazione dati personali
```

nel rispetto della normativa GDPR.

---

# Contributi Catalogo

L'eliminazione dell'account NON elimina i contenuti catalogo già approvati.

---

## Esempi

- Oggetti
- Versioni
- Varianti
- Immagini

---

I contenuti approvati diventano patrimonio permanente di CollectorVerse.

L'autore viene anonimizzato.

---

# Commercianti

Ogni commerciante possiede un profilo dedicato.

---

## Informazioni Visualizzate

- Nome attività
- Logo
- Descrizione
- Email
- Telefono
- Sito Web
- Google Maps
- Orari di apertura
- Categorie trattate

---

# Recensioni Commercianti

CollectorVerse non gestisce recensioni interne dedicate ai commercianti.

---

## Soluzione Adottata

Visualizzazione delle recensioni provenienti da:

```text
Google Reviews
```

tramite collegamento al profilo Google Business del commerciante.

# Parte 3 - Abbonamenti • Monetizzazione • Pubblicità • Scansioni • Bundle • Pacchetti

# Modello Economico

CollectorVerse utilizza un modello Freemium.

La piattaforma è accessibile gratuitamente con funzionalità avanzate disponibili tramite abbonamenti e pacchetti opzionali.

---

# Tipologie Piano

CollectorVerse prevede tre livelli di accesso.

```text
Free

Premium

Premium Plus
```

---

# Piano Free

Il piano Free consente l'utilizzo delle funzionalità base della piattaforma.

---

## Funzionalità Incluse

- Catalogo Universale
- Collezioni personali
- Wishlist
- Ricerca utenti
- Visualizzazione profili pubblici
- Visualizzazione collezioni pubbliche
- Visualizzazione wishlist pubbliche
- Follow categorie
- Follow collezioni
- Follow serie
- Follow oggetti
- Follow utenti
- Follow commercianti
- Mappa commercianti
- Scansione oggetti
- Catalogo collaborativo
- Ricezione richieste di contatto
- Ricezione e risposta ai messaggi ricevuti

---

## Limitazioni

Non può:

```text
❌ avviare nuove conversazioni

❌ pubblicare annunci Marketplace

❌ utilizzare il Matching

❌ visualizzare utenti sulla mappa
```

---

# Piano Premium

Include tutte le funzionalità del piano Free.

---

## Funzionalità Aggiuntive

```text
✅ avviare conversazioni

✅ utilizzare la chat

✅ creare annunci Marketplace

✅ utilizzare il Matching
```

---

# Piano Premium Plus

Include tutte le funzionalità Premium.

---

## Funzionalità Aggiuntive

```text
✅ geolocalizzazione utenti

✅ mappa utenti

✅ Matching avanzato

✅ ricerca geografica avanzata
```

---

# Scansioni

CollectorVerse utilizza un sistema di scansioni giornaliere.

---

## Quantità Scansioni

Tutti i valori sono configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

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

---

# Consumo Scansione

La scansione viene consumata immediatamente dopo l'acquisizione della foto.

Flusso:

```text
Foto

↓

Consumo di 1 scansione

↓

Analisi
```

---

# Pubblicità

Gli utenti Free visualizzano contenuti pubblicitari.

---

## Tipologie

```text
Banner

Video Reward
```

---

# Banner

I banner devono essere mostrati in modo non invasivo.

La frequenza è configurabile dalla Dashboard Admin.

---

# Video Reward

Gli utenti possono ottenere scansioni aggiuntive guardando video pubblicitari.

---

## Ricompensa

Valore iniziale consigliato:

```text
+3 scansioni
```

---

## Limite Giornaliero

Valore iniziale consigliato:

```text
5 video al giorno
```

---

## Cooldown

Valore iniziale consigliato:

```text
15 minuti
```

---

Tutti i valori devono essere configurabili dalla Dashboard Admin.

---

# Area Scansioni

L'utente deve poter visualizzare:

```text
Scansioni disponibili

Scansioni utilizzate

Scansioni ottenute tramite reward

Video disponibili

Reset giornaliero
```

---

# Marketplace

L'accesso al Marketplace dipende dal piano attivo.

---

# Disponibilità Oggetti

Ogni oggetto presente nella collezione personale può essere marcato come:

```text
In Vendita

In Scambio
```

Le due opzioni possono essere utilizzate contemporaneamente.

---

# Utente Free

Può:

```text
✅ contrassegnare oggetti In Vendita

✅ contrassegnare oggetti In Scambio
```

---

Può inoltre mostrare tali disponibilità nel proprio profilo pubblico.

---

Non può:

```text
❌ creare annunci Marketplace
```

---

# Utente Premium

Può:

```text
✅ creare annunci Marketplace

✅ creare annunci di vendita

✅ creare annunci di scambio
```

---

# Utente Premium Plus

Può utilizzare tutte le funzionalità Marketplace disponibili per Premium.

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

La condizione appartiene esclusivamente alla copia posseduta dall'utente.

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

Tutti i prezzi inseriti dall'utente vengono registrati nella valuta scelta dall'utente stesso.

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

---

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

Venduto, scambiato o rimosso dall'utente.

---

# Scadenza Abbonamento

Se il piano Premium o Premium Plus termina:

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

---

# Superamento Limite

Se un utente supera il numero massimo di annunci consentiti:

mostrare un Wizard di selezione.

---

## Esempio

```text
Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona gli annunci da mantenere attivi.
```

---

# Pacchetti

CollectorVerse supporta pacchetti opzionali.

---

## Esempi

```text
Scansioni aggiuntive

Annunci aggiuntivi
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

# Abbonamenti

CollectorVerse supporta:

```text
Mensile

Trimestrale

Annuale
```

---

# Prezzi

Tutti i prezzi sono configurabili dalla Dashboard Admin.

Valori iniziali consigliati.

---

## Premium

Mensile

```text
€ 2,99
```

Trimestrale

```text
€ 7,99
```

Annuale

```text
€ 27,99
```

---

## Premium Plus

Mensile

```text
€ 4,99
```

Trimestrale

```text
€ 13,99
```

Annuale

```text
€ 49,99
```

---

# Bundle

CollectorVerse supporta bundle combinati.

---

## Premium Collector

```text
Premium Annuale

+

250 Scansioni

+

50 Annunci
```

Prezzo iniziale consigliato:

```text
€ 34,99
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

Prezzo iniziale consigliato:

```text
€ 69,99
```

---

# Fonti di Monetizzazione

CollectorVerse prevede:

```text
Abbonamenti

Bundle

Pacchetti

Banner pubblicitari

Video Reward
```

---

# Gestione Admin

Tutti i valori devono essere configurabili senza modificare il codice.

---

## Configurazioni Abbonamenti

- prezzi
- durate
- vantaggi

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
- video reward
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

# Parte 4 - Catalogo Universale • Categorie • Collezioni • Serie • Oggetti • Versioni • Varianti

# Catalogo Universale

Il Catalogo Universale rappresenta il cuore di CollectorVerse.

Tutte le funzionalità della piattaforma si basano sulla struttura del catalogo.

---

# Obiettivo

Consentire la catalogazione di qualsiasi tipologia di oggetto collezionabile.

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

# Struttura Ufficiale

Ogni elemento del catalogo deve rispettare la seguente gerarchia.

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

# Categoria

Rappresenta il livello più alto della classificazione.

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

Ogni categoria deve possedere uno stato.

---

## In Sviluppo

Categoria in preparazione.

Visibile esclusivamente agli amministratori.

---

## Attiva

Categoria disponibile per gli utenti.

Utilizzabile in:

- Catalogo
- Collezioni
- Wishlist
- Marketplace
- Matching
- Scansione
- Importazione
- Creazione Oggetti

---

## Nascosta

Categoria esistente ma temporaneamente non visibile agli utenti.

---

## Archiviata

Categoria non più supportata.

---

# Regola Visibilità Categoria

Le categorie che non si trovano nello stato:

```text
Attiva
```

non devono comparire in:

- Catalogo
- Collezioni
- Wishlist
- Marketplace
- Matching
- Ricerca
- Scansione
- Importazione
- Creazione Oggetti
- Creazione Versioni
- Creazione Varianti

---

# Informazioni Categoria

Per ogni categoria visualizzare:

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

Ogni categoria può contenere più collezioni.

---

## Esempi

Categoria:

Carte Collezionabili

↓

Collezioni:

- Pokémon
- Yu-Gi-Oh!
- Magic
- One Piece
- Lorcana

---

# Informazioni Collezione

Per ogni collezione visualizzare:

- Nome
- Logo
- Banner
- Numero Serie
- Numero Oggetti
- Percentuale Completamento Utente

---

# Serie

Ogni collezione può contenere più serie.

---

## Esempio

Pokémon

↓

Serie:

- Set Base
- Jungle
- Fossil
- Neo Genesis

---

# Informazioni Serie

Per ogni serie visualizzare:

- Nome
- Numero Oggetti
- Percentuale Completamento Utente

---

# Oggetto

L'oggetto rappresenta l'unità collezionabile principale.

---

## Esempio

Serie:

Set Base

↓

Oggetto:

Charizard 4/102

---

# Versione

Le versioni rappresentano differenti edizioni dello stesso oggetto.

Le versioni NON sono nuovi oggetti.

---

## Esempi

Charizard 4/102

↓

Versioni:

- Italiano
- Inglese
- Giapponese
- Tedesco

---

# Regola Fondamentale

Le versioni:

- non aumentano il numero degli oggetti
- non aumentano il completamento della serie
- non aumentano il completamento della collezione
- non aumentano il completamento della categoria

---

# Versione Generica

Ogni oggetto possiede almeno una versione.

Quando una collezione non utilizza versioni:

viene creata automaticamente:

```text
Versione Generica
```

---

# Collezioni che Utilizzano Versioni

Configurabile tramite Dashboard Admin.

---

## Esempi

Pokémon

✅ Utilizza Versioni

---

Monete

✅ Utilizza Versioni

---

Orologi

❌ Non Utilizza Versioni

↓

Versione Generica

---

# Oggetto Posseduto

Un oggetto viene considerato posseduto quando l'utente possiede almeno una versione.

---

## Esempio

Charizard

Versioni:

✅ Italiano

❌ Inglese

❌ Giapponese

---

Risultato:

```text
Oggetto posseduto
```

---

# Completamento Categoria

La percentuale di completamento rappresenta il progresso dell'utente nella categoria.

Formula:

```text
Oggetti posseduti dall'utente

/

Oggetti catalogati nella categoria
```

---

## Esempio

Categoria:

Carte Collezionabili

Oggetti catalogati:

10.000

Oggetti posseduti:

2.500

Completamento:

25%

---

# Completamento Collezione

Formula:

```text
Oggetti posseduti dall'utente

/

Oggetti catalogati nella collezione
```

---

## Esempio

Collezione:

Pokémon

Oggetti catalogati:

5.000

Oggetti posseduti:

750

Completamento:

15%

---

# Completamento Serie

Formula:

```text
Oggetti posseduti dall'utente

/

Oggetti catalogati nella serie
```

---

## Esempio

Serie:

Set Base

Oggetti catalogati:

102

Oggetti posseduti:

95

Completamento:

93%

---

# Completamento Versioni

Le versioni possiedono una progressione separata.

---

## Esempio

Charizard

Versioni:

✅ Italiano

✅ Inglese

❌ Giapponese

❌ Tedesco

---

Progressione:

```text
2 / 4 Versioni
```

---

# Varianti

Le varianti rappresentano differenze produttive o errori di produzione.

Le varianti NON sono nuovi oggetti.

Le varianti NON sono nuove versioni.

---

## Esempi

- errore di stampa
- errore di centratura
- errore di colore
- errore di conio

---

# Regola Fondamentale

Le varianti:

- non aumentano il numero degli oggetti
- non aumentano il completamento della serie
- non aumentano il completamento della collezione
- non aumentano il completamento della categoria

---

# Visualizzazione Varianti

Visualizzare:

```text
🔀 Varianti presenti
```

---

## Esempio

Charizard

🔀 3 Varianti

---

# Condizione dell'Oggetto

La condizione appartiene esclusivamente alla copia posseduta dall'utente.

---

## Regole

La condizione:

```text
❌ NON appartiene all'Oggetto

❌ NON appartiene alla Versione

❌ NON appartiene alla Variante

❌ NON appartiene al Catalogo Universale
```

---

# Valori Condizione

Valori iniziali consigliati:

```text
Sigillato

Come Nuovo

Ottimo

Buono

Discreto

Danneggiato
```

---

# Utilizzo Condizione

La condizione può essere associata a:

- Oggetto in Collezione
- Oggetto in Vendita
- Oggetto in Scambio

---

# Scheda Oggetto

Ogni oggetto possiede una scheda dedicata.

---

## Sezioni

- Dettagli
- Versioni
- Varianti
- Immagini
- Marketplace
- Statistiche

---

# Versioni nella Scheda Oggetto

Visualizzare:

- elenco versioni
- stato posseduto
- progressione versioni

---

# Varianti nella Scheda Oggetto

Visualizzare:

- elenco varianti
- immagini varianti
- descrizioni varianti

---

# Statistiche Oggetto

Visualizzare:

- utenti che lo possiedono
- utenti che lo desiderano
- scansioni effettuate
- annunci attivi
- annunci di scambio

---

# Creazione Nuovi Elementi

CollectorVerse supporta:

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante

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

Verificato

Rifiutato

Unificato
```

---

# Provvisorio

Elemento immediatamente utilizzabile.

Può essere:

- cercato
- catalogato
- aggiunto alle collezioni
- aggiunto alle wishlist
- utilizzato nel marketplace

---

# Controllo Duplicati

Prima della creazione di:

- Oggetti
- Versioni
- Varianti

CollectorVerse deve eseguire verifiche automatiche.

---

# Verifiche Disponibili

- nome
- codice identificativo
- OCR
- immagini
- hash immagini

---

# Follow Categoria

Gli utenti possono seguire una categoria.

---

## Utilizzo

Ricevere notifiche relative alla categoria.

---

# Eventi Notificabili

- Nuove Collezioni
- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

# Collezioni Preferite

Gli utenti possono salvare collezioni pubbliche.

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

Ogni collezione pubblica possiede:

- Link Pubblico
- QR Code dedicato

---

## Esempio

```text
collectorverse.com/u/mario/pokemon
```

---

# Regola Privacy

Se una collezione pubblica viene:

- eliminata
- resa privata

deve essere automaticamente rimossa dai preferiti degli altri utenti.

# Parte 5 - Sistema Scansione • OCR • Hash • AI • Wizard Catalogo • Cronologia Scansioni

# Sistema Scansione

Il sistema di scansione rappresenta una delle funzionalità principali di CollectorVerse.

L'obiettivo è permettere il riconoscimento rapido degli oggetti catalogati e semplificare la catalogazione delle collezioni personali.

---

# Obiettivi

- riconoscere oggetti esistenti
- ridurre l'inserimento manuale
- velocizzare la catalogazione
- migliorare la qualità del catalogo
- assistere l'utente nella creazione di nuovi contenuti

---

# Flusso Scansione

Il flusso ufficiale è il seguente.

```text
Categoria

↓

Collezione

↓

Versione

↓

Foto

↓

Consumo Scansione

↓

Analisi

↓

Risultato
```

---

# Selezione Categoria

Prima della scansione l'utente deve selezionare una categoria.

---

## Regola

Possono essere selezionate esclusivamente:

```text
Categorie Attive
```

---

# Selezione Collezione

Dopo la categoria.

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

Dopo la collezione.

---

# Obiettivo

Ridurre gli errori di riconoscimento.

---

# Versioni Disponibili

Visualizzare sempre le versioni già esistenti per la collezione selezionata.

---

## Esempio

```text
Italiano

Inglese

Giapponese

Tedesco
```

---

# Nuove Versioni

Se la versione desiderata non esiste:

```text
Nuova Versione
```

↓

Workflow di revisione catalogo.

---

# Collezioni senza Versioni

Se la collezione utilizza:

```text
Versione Generica
```

il campo Versione non deve essere mostrato.

---

# Acquisizione Foto

L'utente può:

- scattare una foto
- caricare una foto esistente

---

# Consumo Scansione

La scansione viene consumata immediatamente dopo l'acquisizione della foto.

---

# Flusso

```text
Foto

↓

1 scansione consumata

↓

Analisi
```

---

# Sistema di Analisi

CollectorVerse utilizza più livelli di riconoscimento.

---

## Livello 1

Hash immagini.

---

## Livello 2

OCR.

---

## Livello 3

Confronto Catalogo.

---

## Livello 4

AI come fallback.

---

# Hash Immagini

Confronto con immagini già presenti nel catalogo.

Utilizzato per velocizzare il riconoscimento.

---

# OCR

L'OCR estrae informazioni testuali.

---

## Esempi

- codici
- numerazioni
- nomi
- testi
- identificativi

---

# Confronto Catalogo

I risultati derivanti da:

- OCR
- Hash immagini

vengono confrontati con il Catalogo Universale.

---

# AI

L'intelligenza artificiale viene utilizzata esclusivamente quando i sistemi precedenti non producono un risultato sufficientemente affidabile.

---

# Risultati Scansione

Visualizzare:

- risultato suggerito
- livello di affidabilità
- possibili alternative

---

## Esempio

```text
Charizard 4/102

98%
```

---

```text
Pikachu 58/102

81%
```

---

```text
Charmander 46/102

72%
```

---

# Nessun Risultato

Se non esistono risultati sufficientemente affidabili:

mostrare il Wizard Catalogo.

---

# Wizard Catalogo

Permette la creazione guidata di nuovi elementi.

---

## Operazioni Disponibili

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante

---

# Nuovo Oggetto

Richiedere:

- Categoria
- Collezione
- Serie
- Nome
- Codice o Numero
- Versione
- Immagine
- Descrizione (facoltativa)

---

# Nuova Versione

Utilizzata quando:

```text
Oggetto esistente

+

Versione non esistente
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

+

Versione esistente

+

Nuova Variante
```

---

# Controlli Automatici

Prima della creazione il sistema deve verificare:

- duplicati
- nomi
- codici
- OCR
- immagini
- hash immagini

---

# Stato Iniziale

Oggetti, Versioni e Varianti create dagli utenti assumono lo stato:

```text
Provvisorio
```

---

# Utilizzo Immediato

Anche se Provvisorio, l'elemento può essere:

- cercato
- utilizzato
- aggiunto alle collezioni
- aggiunto alle wishlist
- utilizzato nel marketplace

---

# Cronologia Scansioni

Ogni utente possiede una cronologia personale delle scansioni effettuate.

---

# Posizione

```text
Profilo

↓

Cronologia Scansioni
```

---

# Informazioni Visualizzate

- Data
- Immagine
- Categoria
- Collezione
- Versione
- Risultato ottenuto

---

# Conservazione

Valore iniziale consigliato:

```text
Ultime 50 scansioni
```

Configurabile dalla Dashboard Admin.

---

# Errori di Scansione

Quando una scansione fallisce il sistema deve mostrare messaggi comprensibili.

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
Versione non selezionata
```

---

# Statistiche Scansione

CollectorVerse deve memorizzare:

- scansioni effettuate
- scansioni riuscite
- scansioni fallite
- scansioni AI

---

# Importazione Collezioni

CollectorVerse supporta l'importazione tramite:

```text
Excel

CSV
```

---

# Obiettivo

L'importazione serve esclusivamente a popolare la collezione personale dell'utente.

---

# Regola Fondamentale

L'importazione:

```text
❌ NON può creare Oggetti

❌ NON può creare Versioni

❌ NON può creare Varianti

❌ NON può modificare il Catalogo Universale
```

---

# Flusso Importazione

```text
Selezione Categoria

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

# Categoria

L'utente deve selezionare una categoria prima dell'importazione.

Possono essere selezionate esclusivamente:

```text
Categorie Attive
```

---

# Mapping Colonne

L'utente deve associare le colonne del file ai campi CollectorVerse.

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
Expansion
↓
Serie
```

---

# Simulazione

Prima dell'importazione definitiva il sistema deve mostrare:

- elementi riconosciuti
- elementi non riconosciuti
- possibili duplicati
- incongruenze

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
```

e

```text
NON generano automaticamente

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
```

---

# Azioni Disponibili

```text
Importa elementi riconosciuti

Esporta elenco elementi non riconosciuti
```

---

# Inserimento Manuale

Gli elementi non riconosciuti devono essere aggiunti tramite:

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante

seguendo il normale workflow del Catalogo Collaborativo.

---

# Dashboard Admin

Configurazioni modificabili senza aggiornare il codice.

---

## Scansioni

- scansioni giornaliere
- scansioni reward
- cooldown video
- limiti AI

---

## Cronologia

- numero scansioni conservate

---

## AI

- attivazione AI
- soglia affidabilità
- limiti utilizzo

---

## Importazione

- formati consentiti
- limiti file
- limiti righe
- soglie di simulazione

---

## Messaggi Errore

Tutti i messaggi devono poter essere personalizzati dalla Dashboard Admin.

# Parte 6 - Catalogo Collaborativo • Contributori Catalogo • Votazioni • Reputazione • Immagini

# Catalogo Collaborativo

CollectorVerse utilizza un sistema di crescita collaborativa del catalogo.

La community può contribuire alla creazione e al miglioramento del Catalogo Universale.

---

# Obiettivo

Consentire una crescita rapida del catalogo mantenendo elevata la qualità dei dati.

---

# Contributori Catalogo

I Contributori Catalogo sono utenti autorizzati a partecipare alle revisioni della community.

---

# Accesso Commercianti

I commercianti diventano automaticamente Contributori Catalogo.

---

## Limitazioni

Possono revisionare esclusivamente le categorie dichiarate nel proprio profilo.

---

# Accesso Utenti

Gli utenti possono essere invitati a diventare Contributori Catalogo.

---

## Requisito Minimo

Valore iniziale consigliato:

```text
30 giorni di iscrizione
```

Configurabile tramite Dashboard Admin.

---

# Invito

Quando un utente raggiunge i requisiti necessari riceve una notifica.

---

## Messaggio

```text
Vuoi aiutare CollectorVerse
a migliorare il Catalogo Universale?
```

---

# Accettazione

Se l'utente accetta:

entra nel programma Contributori Catalogo.

---

# Ambito di Revisione

Gli utenti possono revisionare esclusivamente le collezioni che possiedono.

---

## Esempio

Possiede:

- Pokémon
- LEGO
- Euro Italia

---

Può revisionare:

- Pokémon
- LEGO
- Euro Italia

---

Non può revisionare:

- Lorcana
- Magic
- Francobolli

se non presenti nelle proprie collezioni.

---

# Area Contributori Catalogo

Nuova sezione dedicata.

Percorso:

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
- Immagine
- Data proposta
- Utente proponente

---

# Sistema di Votazione

Ogni revisore può votare una sola volta per elemento.

---

# Voti Disponibili

```text
✅ Corretta

❌ Non Corretta

❓ Non So
```

---

# Motivazione

Se viene selezionato:

```text
❌ Non Corretta
```

mostrare:

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

Valore minimo:

```text
0
```

---

# Peso del Voto

Non tutti i voti possiedono lo stesso peso.

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

Applicato a:

- utenti
- commercianti

---

# Statistiche Contributore

Ogni Contributore Catalogo deve visualizzare:

- Correzioni Approvate
- Correzioni Respinte
- Reputazione
- Peso Voto Attuale

---

# Revisione Community

La community non approva direttamente gli elementi.

La community fornisce indicazioni agli amministratori.

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

Lo stato della revisione viene utilizzato esclusivamente per dare priorità al lavoro amministrativo.

---

# Decisione Finale

La decisione finale appartiene sempre ad un amministratore.

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

Quando una nuova collezione non possiede ancora una base utenti sufficiente:

le revisioni vengono affidate principalmente a:

- Commercianti
- Moderatori
- Amministratori

---

# Immagini Collaborative

CollectorVerse supporta un sistema di miglioramento continuo delle immagini.

---

# Obiettivo

Permettere alla community di migliorare progressivamente la qualità visiva del catalogo.

---

# Immagini Candidate

Ogni oggetto può possedere più immagini candidate.

---

# Valutazione Immagini

Formula completamente configurabile.

Valori iniziali consigliati:

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

Configurabile dalla Dashboard Admin.

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

Gli amministratori possono:

- eliminare immagini errate
- eliminare immagini inappropriate
- bloccare immagini
- sostituire immagini
- forzare immagine ufficiale

---

# Proprietà dei Contributi

I contributi approvati diventano parte permanente del Catalogo Universale.

---

# Contenuti Coinvolti

- Oggetti
- Versioni
- Varianti
- Immagini

---

# Eliminazione Account

Se l'autore elimina il proprio account:

```text
I contributi approvati rimangono nel catalogo.
```

---

## Effetti

```text
✅ contenuti conservati

✅ catalogo preservato

✅ autore anonimizzato
```

---

# Dashboard Admin

Configurazioni modificabili senza aggiornare il codice.

---

## Contributori Catalogo

- giorni minimi iscrizione
- soglie reputazione
- peso voto
- attivazione programma

---

## Revisioni

- voti minimi
- soglie revisione positiva
- soglie revisione negativa

---

## Immagini

- peso qualità tecnica
- peso voti community
- peso utilizzo
- soglia immagine ufficiale

---

## Programma Contributori

Può essere:

```text
Attivo

Disattivato
```

tramite Dashboard Admin.

# Parte 7 - Marketplace • Chat • Matching • Geolocalizzazione

# Marketplace

Il Marketplace permette agli utenti di vendere e scambiare oggetti presenti nelle proprie collezioni.

CollectorVerse non gestisce:

- pagamenti
- spedizioni
- transazioni economiche

Le trattative vengono gestite direttamente tra gli utenti.

---

# Obiettivi

Consentire ai collezionisti di:

- trovare oggetti mancanti
- vendere oggetti disponibili
- proporre scambi
- trovare altri collezionisti
- entrare in contatto con commercianti

---

# Disponibilità Oggetti

Ogni oggetto presente nella collezione personale può essere contrassegnato come:

```text
In Vendita

In Scambio
```

Le due opzioni possono essere utilizzate contemporaneamente.

---

# Disponibilità Utente

CollectorVerse distingue:

```text
Disponibilità Utente

↓

Annuncio Marketplace
```

---

# Utente Free

Può:

```text
✅ contrassegnare oggetti In Vendita

✅ contrassegnare oggetti In Scambio

✅ mostrare tali informazioni nel proprio profilo
```

---

Non può:

```text
❌ creare annunci Marketplace

❌ utilizzare il Matching
```

---

# Utente Premium

Può:

```text
✅ creare annunci Marketplace

✅ utilizzare il Matching

✅ utilizzare la Chat

✅ avviare conversazioni
```

---

# Utente Premium Plus

Include tutte le funzionalità Premium.

Inoltre può:

```text
✅ utilizzare la geolocalizzazione utenti

✅ visualizzare la mappa utenti

✅ utilizzare il Matching avanzato
```

---

# Commerciante

Può:

```text
✅ creare annunci Marketplace

✅ utilizzare la Chat

✅ utilizzare il Matching

✅ visualizzare la mappa utenti
```

---

# Profilo Utente

Gli utenti possono visualizzare:

```text
Disponibili per Vendita

Disponibili per Scambio

Wishlist Pubblica
```

nel rispetto delle impostazioni privacy.

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

# Annunci Marketplace

Ogni annuncio può contenere:

- Oggetto
- Versione
- Variante
- Condizione
- Prezzo
- Valuta
- Descrizione
- Posizione geografica

---

# Stati Annuncio

---

## Attivo

Visibile nel Marketplace.

---

## Sospeso

Esistente ma non visibile.

---

## Chiuso

Concluso o rimosso.

---

# Downgrade Piano

Quando un utente perde i requisiti necessari per utilizzare il Marketplace:

gli annunci vengono automaticamente sospesi.

---

## Esempio

```text
Premium

↓

Scadenza

↓

Free

↓

Annunci Sospesi
```

---

# Riattivazione

Quando l'utente torna ad avere un piano compatibile:

```text
Annunci riattivati automaticamente
```

---

# Limiti Piano

Configurabili tramite Dashboard Admin.

Valori iniziali consigliati.

---

## Premium

```text
10 annunci
```

---

## Premium Plus

```text
30 annunci
```

---

# Superamento Limite

Quando gli oggetti disponibili superano il numero massimo di annunci consentiti:

mostrare un Wizard di selezione.

---

## Esempio

```text
Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona quali mantenere attivi.
```

---

# Ricerca Marketplace

Consentire ricerche attraverso:

- testo
- categoria
- collezione
- serie
- oggetto
- versione
- variante
- distanza
- prezzo
- condizione

---

# Ordinamento

L'utente può scegliere il proprio ordinamento preferito.

---

## Esempi

- Prezzo
- Distanza
- Data pubblicazione
- Recensioni
- CollectorScore

---

# Preferenze Utente

L'ordinamento scelto viene salvato nel profilo.

---

# Wishlist

Gli utenti possono creare wishlist.

---

# Prezzo Massimo

Ogni elemento della wishlist può contenere:

```text
Prezzo Massimo Desiderato
```

---

## Esempio

```text
Charizard

Prezzo massimo:

150 €
```

---

# Condizione Minima

Ogni elemento della wishlist può contenere:

```text
Condizione Minima Accettata
```

---

## Esempio

```text
Charizard

Condizione minima:

Ottimo
```

---

# Utilizzo

Prezzo massimo e condizione minima possono essere utilizzati dal Matching.

---

# Chat

CollectorVerse include una chat interna.

---

# Accesso

Disponibile per:

- Premium
- Premium Plus
- Commercianti

---

# Funzionalità

- messaggi testuali
- invio immagini
- condivisione link recensione
- comunicazione tra utenti

---

# Allegati

Formati supportati:

```text
JPG

PNG

WEBP
```

---

Dimensione massima iniziale consigliata:

```text
10 MB
```

Configurabile tramite Dashboard Admin.

---

# Richieste di Contatto

L'apertura di una nuova conversazione avviene tramite richiesta di contatto.

---

# Informazioni Mostrate

Visualizzare:

- Nome Utente
- Tipologia Account
- Affidabilità
- Recensioni
- Numero recensioni
- CollectorScore
- Badge principali

---

# Azioni Disponibili

```text
✅ Accetta

❌ Rifiuta

🚫 Blocca Utente
```

---

# Anti-Spam

Se una richiesta viene rifiutata:

lo stesso utente non può inviare immediatamente una nuova richiesta.

---

## Configurazione

Il tempo minimo è configurabile dalla Dashboard Admin.

Valore iniziale consigliato:

```text
1 giorno
```

---

# Recensioni dalla Chat

Il link recensione può essere inviato esclusivamente tramite chat interna.

---

# Matching

Il Matching serve ad individuare opportunità rilevanti.

---

# Tipologie

- Matching acquisti
- Matching vendite
- Matching scambi

---

# Parametri Disponibili

- Oggetti posseduti
- Wishlist
- Prezzo massimo
- Condizione minima
- Distanza
- Recensioni
- Affidabilità
- CollectorScore

---

# Ordinamento Matching

L'utente può personalizzare l'ordine delle priorità.

---

## Esempio

```text
1. Prezzo

2. Distanza

3. Recensioni

4. CollectorScore
```

---

# Salvataggio Preferenze

Le preferenze vengono salvate nel profilo utente.

---

# Indice Affidabilità

L'affidabilità interna può essere utilizzata dal Matching per migliorare i risultati.

---

# Geolocalizzazione

CollectorVerse supporta funzionalità geografiche.

---

# Distanza Iniziale

Valore iniziale consigliato:

```text
25 km
```

---

# Espansione Ricerca

L'utente può aumentare il raggio di ricerca.

---

## Esempi

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

# Ricerca Avanzata

Consentire ricerca per:

- Regione
- Nazione
- Continente

---

# Continenti

- Europa
- Africa
- Asia
- America del Nord
- America del Sud
- Oceania

---

# Visualizzazione Distanze

Mostrare sempre:

- distanza utente
- distanza commerciante
- distanza annuncio

---

# Mappa

CollectorVerse include una mappa integrata.

---

# Utente Free

Può visualizzare:

```text
Commercianti
```

---

Non può visualizzare:

```text
Utenti
```

---

# Premium Plus

Può visualizzare:

```text
Utenti

Commercianti
```

---

# Commerciante

Può visualizzare:

```text
Utenti

Commercianti
```

---

# Filtri Mappa

Consentire filtri per:

- Categoria
- Collezione
- Distanza

---

# Follow

Gli utenti possono seguire:

- Categorie
- Collezioni
- Serie
- Oggetti
- Utenti
- Commercianti

---

# Notifiche Follow Categoria

- Nuove Collezioni
- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

---

# Notifiche Follow Collezione

- Nuove Serie
- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuovi commercianti che trattano la collezione

---

# Notifiche Follow Serie

- Nuovi Oggetti
- Nuove Varianti

---

# Notifiche Follow Oggetto

- Nuove Immagini
- Nuove Varianti
- Nuovi Annunci

---

# Notifiche Follow Utente

- Nuovi annunci
- Nuove collezioni pubbliche

---

# Notifiche Follow Commerciante

- Nuovi annunci
- Aggiornamenti profilo
- Nuove recensioni Google

---

# Segnalazione Annunci

Gli utenti possono segnalare annunci.

---

## Motivazioni

- Spam
- Truffa sospetta
- Prezzo non realistico
- Immagini inappropriate
- Contenuti non pertinenti

---

# Dashboard Admin

Configurazioni modificabili senza aggiornare il codice.

---

## Marketplace

- limiti annunci
- stati annunci
- durata annunci

---

## Chat

- attivazione chat
- limiti allegati
- tempo anti-spam

---

## Matching

- parametri disponibili
- attivazione matching
- peso dei parametri

---

## Geolocalizzazione

- raggi disponibili
- nazioni abilitate
- continenti disponibili

---

## Follow

- eventi notificabili
- categorie disponibili

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

Ogni utente deve poter adattare la propria esperienza alle proprie esigenze.

---

# Primo Accesso

Alla prima apertura dell'applicazione l'utente deve completare una configurazione guidata iniziale.

---

# Interessi Iniziali

L'utente può selezionare le categorie che lo interessano.

Esempio:

- Carte Collezionabili
- Numismatica
- Fumetti e Libri
- LEGO e Costruzioni

---

# Utilizzo Interessi

Le categorie selezionate vengono utilizzate per:

- Home Personalizzata
- Suggerimenti
- Matching
- Notifiche
- Contenuti in evidenza

---

# Home

La Home rappresenta il punto di accesso principale dell'app.

---

# Obiettivi

Fornire una panoramica immediata di:

- collezioni
- wishlist
- scansioni
- badge
- attività recenti
- marketplace
- matching

---

# Widget Home

La Home è composta da widget configurabili.

---

## Widget Base

- Le Mie Collezioni
- Wishlist
- Scansioni Disponibili
- Badge
- Attività Recenti

---

## Widget Premium

- Scambi Consigliati
- Utenti Consigliati

---

## Widget Premium Plus

- Match Vicini
- Utenti Vicini
- Opportunità Locali

---

# Personalizzazione Home

L'utente può:

- mostrare widget
- nascondere widget
- riordinare widget

---

# Obiettivi Giornalieri

Visualizzare:

- obiettivi disponibili
- avanzamento
- premi ottenibili

---

# Profilo Utente

Ogni utente possiede una schermata profilo dedicata.

---

# Informazioni Principali

Visualizzare:

- Avatar
- Cornice Profilo
- Nome Utente
- Tipologia Account
- CollectorScore
- Livello
- Affidabilità
- Data Iscrizione

---

# Tipologia Account

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

# Indicatori Funzionalità

Visualizzare:

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

---

# Wishlist

Ogni wishlist può essere:

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

# Le Mie Attività

Storico delle attività dell'utente.

---

## Eventi Visualizzati

- Oggetti creati
- Versioni create
- Varianti create
- Correzioni proposte
- Correzioni approvate
- Badge ottenuti
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
- Versione
- Risultato ottenuto

---

# Abbonamenti e Pacchetti

Sezione dedicata alla situazione commerciale dell'account.

---

## Visualizzare

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

La valuta selezionata verrà utilizzata automaticamente per gli oggetti messi in vendita.

---

# Profilo Pubblico

Ogni utente può condividere il proprio profilo.

---

## Informazioni Visibili

- Avatar
- Cornice
- CollectorScore
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

# QR Code

I QR Code devono essere collegati all'identificativo interno dell'utente.

La modifica dello username non deve invalidare il QR Code.

---

# Notifiche

CollectorVerse utilizza un sistema notifiche centralizzato.

---

# Tipologie di Notifica

## Push

Inviate tramite:

```text
Firebase Cloud Messaging
```

---

## Email

Inviate tramite:

```text
Brevo
```

---

## In-App

Disponibili all'interno del centro notifiche.

---

# Preferenze Notifiche

Ogni categoria di notifica può essere configurata separatamente.

Esempio:

```text
Push ✅

Email ❌

In-App ✅
```

---

# Sezioni Notifiche

- Tutte
- Non Lette
- Sistema

---

# Tipologie

## Marketplace

- Nuovi annunci
- Nuovi scambi
- Opportunità rilevanti

---

## Chat

- Nuove richieste di contatto
- Nuovi messaggi

---

## Matching

- Nuovi Match

---

## Catalogo

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti

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
- Nuovi commercianti che trattano la collezione

---

## Follow Serie

- Nuovi Oggetti
- Nuove Varianti

---

## Follow Oggetto

- Nuove Immagini
- Nuove Varianti
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

- Scadenza imminente
- Pacchetti congelati
- Bundle in scadenza

---

# Promemoria Scadenze

Configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

- 7 giorni prima
- 3 giorni prima
- giorno di scadenza

---

# Tutorial

CollectorVerse include un sistema tutorial integrato.

---

# Tutorial Iniziale

Visualizzato durante la prima configurazione.

---

# Contenuti

- Collezioni
- Catalogo
- Scansione
- Marketplace
- Matching
- Community

---

# Tutorial Successivi

Disponibili in qualsiasi momento dal profilo.

---

# Centro Assistenza

Area dedicata al supporto utenti.

---

## Contenuti

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

CollectorVerse supporta l'importazione delle collezioni.

---

## Formati

- Excel
- CSV

---

# Simulazione Importazione

Prima dell'importazione definitiva.

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

L'utente può:

- importare gli elementi riconosciuti
- esportare l'elenco degli elementi non riconosciuti

---

# Esportazione

Gli utenti possono esportare i propri dati.

---

## Formati

- PDF
- Excel

---

# Ricerca Globale

CollectorVerse dispone di una ricerca globale.

---

# Ricerca

Consentire ricerca di:

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

Configurazioni modificabili senza aggiornare il codice.

---

## Home

- widget disponibili
- widget Premium
- widget Premium Plus

---

## Profilo

- sezioni abilitate
- informazioni visibili

---

## Notifiche

- template
- categorie
- attivazione

---

## Tutorial

- step
- ordine
- obbligatorietà

---

## Importazione ed Esportazione

- formati consentiti
- dimensione massima file
- limiti importazione

# Parte 10 - Dashboard Amministratore • Configurazioni Globali • Moderazione • Asset Grafici • Statistiche

# Dashboard Amministratore

CollectorVerse dispone di una Dashboard Amministratore avanzata.

L'obiettivo è consentire la gestione completa della piattaforma senza modificare il codice applicativo.

---

# Principio Fondamentale

Qualsiasi:

- numero
- soglia
- limite
- durata
- percentuale
- punteggio
- moltiplicatore
- configurazione

deve essere modificabile tramite Dashboard Admin quando tecnicamente possibile.

---

# Accesso

Accessibile esclusivamente agli utenti autorizzati.

---

# Ruoli Amministrativi

## Moderatore

Può gestire:

- segnalazioni
- annunci segnalati
- recensioni segnalate
- immagini segnalate
- contenuti segnalati
- chat segnalate

Non può gestire:

- monetizzazione
- configurazioni globali
- amministratori
- infrastruttura

---

## Amministratore

Accesso completo alla Dashboard Admin.

---

# Sicurezza

L'accesso amministrativo deve supportare:

- verifica email
- autenticazione a due fattori
- controllo accessi
- audit log

---

## 2FA

Obbligatoria per:

- Moderatori
- Amministratori

Configurabile dalla Dashboard.

---

# Homepage Amministratore

Visualizzare:

- Nuovi utenti
- Nuovi commercianti
- Nuovi Premium
- Nuovi Premium Plus
- Oggetti da verificare
- Versioni da verificare
- Varianti da verificare
- Immagini da verificare
- Segnalazioni aperte

---

# Dashboard Statistiche

Visualizzare:

- Utenti attivi
- Premium attivi
- Premium Plus attivi
- Commercianti
- Oggetti catalogati
- Versioni catalogate
- Varianti catalogate
- Immagini caricate
- Scansioni effettuate
- Annunci attivi

---

# Trend

Visualizzare grafici relativi a:

- Iscrizioni
- Disiscrizioni
- Conversioni Premium
- Conversioni Premium Plus
- Utilizzo Marketplace
- Utilizzo Scansioni
- Crescita Catalogo

---

# Gestione Utenti

Permette la ricerca e gestione completa degli utenti.

---

## Informazioni Visualizzate

- Profilo
- Piano attivo
- CollectorScore
- Badge
- Affidabilità
- Storico attività
- Segnalazioni ricevute

---

## Azioni Disponibili

- sospendi
- riattiva
- blocca
- elimina
- resetta dati selezionati

---

# Gestione Commercianti

Visualizzare:

- profilo attività
- categorie trattate
- stato verifica
- statistiche

---

## Azioni Disponibili

- verifica commerciante
- rimuovi verifica
- sospendi
- riattiva
- elimina

---

# Gestione Catalogo

Permette la gestione di:

- categorie
- collezioni
- serie
- oggetti
- versioni
- varianti

---

# Gestione Categorie

Per ogni categoria visualizzare:

- Nome
- Logo
- Banner
- Stato
- Numero Collezioni
- Numero Serie
- Numero Oggetti
- Numero Follower

---

## Stati Categoria

```text
In Sviluppo

Attiva

Nascosta

Archiviata
```

---

## Azioni Disponibili

- Crea Categoria
- Modifica Categoria
- Attiva Categoria
- Nascondi Categoria
- Archivia Categoria

---

# Gestione Revisioni

Visualizzare:

- Revisione Positiva
- Revisione Negativa
- Revisione Incerta

---

## Azioni Disponibili

- verifica
- correggi
- rifiuta
- unifica

---

# Gestione Immagini

Visualizzare:

- immagini ufficiali
- immagini candidate
- immagini segnalate

---

## Azioni Disponibili

- approva
- elimina
- blocca
- sostituisci
- imposta immagine ufficiale

---

# Asset Grafici

Sezione dedicata agli asset di sistema.

---

# Gestione Asset

## Categorie

- logo
- banner
- copertina

---

## Collezioni

- logo
- banner
- copertina

---

## Badge

- immagine
- descrizione
- requisiti

---

## Cornici Profilo

- upload
- modifica
- eliminazione
- disattivazione

---

## Avatar

- upload
- sostituzione
- eliminazione

---

## Tutorial

- immagini
- schermate
- banner

---

## Banner Applicazione

- caricamento
- modifica
- attivazione
- disattivazione

---

# Placeholder di Sistema

Gestione centralizzata dei placeholder.

---

## Tipologie

- Placeholder Categoria
- Placeholder Collezione
- Placeholder Oggetto
- Placeholder Profilo
- Placeholder Immagine Mancante

---

# Configurazioni Globali

Area principale di configurazione della piattaforma.

---

# Scansioni

Configurare:

- scansioni Free
- scansioni Premium
- scansioni Premium Plus
- reward video
- video giornalieri
- cooldown

---

# Marketplace

Configurare:

- numero annunci Premium
- numero annunci Premium Plus
- durata annunci
- stati annunci

---

# Matching

Configurare:

- attivazione matching
- peso prezzo massimo
- peso condizione minima
- peso distanza
- peso recensioni
- peso affidabilità
- peso CollectorScore

---

# Geolocalizzazione

Configurare:

- raggi disponibili
- nazioni abilitate
- continenti disponibili

---

# Recensioni

Configurare:

- durata link recensione
- limiti recensioni
- attivazione sistema recensioni

---

# Richieste di Contatto

Configurare:

- attivazione richieste
- tempo anti-spam dopo rifiuto
- limiti richieste

---

# Contributori Catalogo

Configurare:

- giorni minimi iscrizione
- soglie reputazione
- peso voto
- soglie revisione

---

# CollectorScore

Configurare:

- punti attività
- bonus
- moltiplicatori

---

# Livelli

Configurare:

- soglie livelli
- nomi livelli

---

# Badge

Configurare:

- requisiti
- punti assegnati
- attivazione
- disattivazione

---

# Esperto Serie

Configurare:

- soglia 90%
- soglia 95%
- soglia 100%
- categorie abilitate

---

# Versioni

Configurare:

- utilizzo versioni
- utilizzo versione generica

---

# Varianti

Configurare:

- regole di approvazione
- soglie revisione

---

# Condizioni Oggetto

Configurare:

- elenco condizioni
- ordine visualizzazione
- attivazione condizione

---

## Valori Iniziali Consigliati

```text
Sigillato

Come Nuovo

Ottimo

Buono

Discreto

Danneggiato
```

---

# Valute

Gestione centralizzata delle valute disponibili.

---

## Azioni Disponibili

- crea valuta
- modifica valuta
- nascondi valuta
- archivia valuta

---

## Esempi

```text
EUR €

USD $

GBP £

JPY ¥

CHF
```

---

# Notifiche

Configurare:

- template Push
- template Email
- template In-App
- categorie notificabili

---

# Importazione

Configurare:

- formati consentiti
- dimensione file
- limiti righe
- regole simulazione

---

# Feature Flags

Possibilità di attivare o disattivare intere funzionalità.

---

## Funzionalità Gestibili

- Marketplace
- Matching
- Recensioni
- Chat
- Geolocalizzazione
- Catalogo Collaborativo
- Versioni
- Varianti
- Importazione
- Pubblicità

---

# Monetizzazione

Area dedicata alla gestione economica.

---

# Abbonamenti

Configurare:

- nome
- durata
- prezzo
- vantaggi

---

# Bundle

Configurare:

- contenuto
- durata
- prezzo

---

# Pacchetti

Configurare:

- contenuto
- quantità
- durata
- prezzo

---

# Pubblicità

Configurare:

- banner
- video reward
- frequenza

---

# Anteprima Configurazione

Prima di applicare modifiche rilevanti il sistema deve mostrare una stima dell'impatto.

---

## Esempio

```text
Annunci Premium

10

↓

20
```

---

Visualizzare:

```text
Utenti coinvolti

Annunci aggiuntivi disponibili

Impatto stimato
```

---

# Audit Log

Tutte le azioni amministrative devono essere registrate.

---

## Informazioni Salvate

- amministratore
- data
- ora
- azione
- elemento modificato

---

# Cestino

Elementi eliminati recuperabili.

---

## Durata Conservazione

Valore iniziale consigliato:

```text
30 giorni
```

Configurabile tramite Dashboard Admin.

---

# Backup

Consentire esportazioni amministrative.

---

## Dati Esportabili

- catalogo
- utenti
- marketplace
- revisioni
- configurazioni

---

# Modalità Manutenzione

Funzionalità attivabile dalla Dashboard.

---

## Utilizzo

Permette di bloccare temporaneamente l'utilizzo dell'applicazione.

---

# Statistiche Avanzate

Visualizzare:

- categorie più seguite
- collezioni più seguite
- serie più seguite
- oggetti più visualizzati
- categorie con maggiore crescita

---

# Statistiche Contributori

Visualizzare:

- migliori revisori
- revisioni effettuate
- reputazione
- affidabilità revisori

---

# Obiettivo Finale

Consentire agli amministratori di gestire completamente CollectorVerse senza modificare il codice applicativo e senza pubblicare aggiornamenti non necessari.

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
