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

---

# Parte 2 - Utenti • Privacy • Sicurezza • Recensioni • Gestione Account • Ruoli • Profili

# Sistema Identità

CollectorVerse utilizza un sistema di identità progettato per supportare:

- collezionisti privati
- collezionisti avanzati
- commercianti professionali
- moderatori
- amministratori

Ogni account è identificato in modo permanente e univoco all'interno della piattaforma.

---

# Modello Account

CollectorVerse distingue chiaramente tra:

```text
Piano

e

Ruolo
```

Ogni account possiede sempre:

```text
1 Piano

+

1 Ruolo
```

Il Piano determina le funzionalità disponibili.

Il Ruolo determina i privilegi operativi e amministrativi.

---

# Identità Utente

Ogni account possiede:

- ID Interno Permanente
- Email
- Username
- Display Name
- Data Registrazione

---

# Username

Lo Username identifica tecnicamente l'account.

Caratteristiche:

```text
Univoco
Modificabile
Pubblico
```

---

# Display Name

Il Display Name rappresenta il nome visualizzato pubblicamente nella piattaforma.

Caratteristiche:

```text
Univoco
Modificabile
Pubblico
```

---

# Regole Identità

Devono essere univoci:

```text
Email
Username
Display Name
```

La modifica di Username o Display Name non altera:

- ID interno
- QR Code
- Cronologia attività
- Collezioni
- Wishlist
- Marketplace
- Recensioni
- Contributi Catalogo

---

# Registrazione

CollectorVerse supporta inizialmente:

```text
Email
Google
```

Al termine della registrazione vengono automaticamente creati:

- Profilo Utente
- Impostazioni Privacy
- Preferenze Notifiche
- Abbonamento Iniziale
- Configurazione Base Account

---

# Verifica Email

Gli account registrati tramite email devono completare la verifica dell'indirizzo email.

Fino alla verifica:

```text
Account limitato
```

Gli effetti sono configurabili tramite Dashboard Admin.

---

# Piani Disponibili

CollectorVerse supporta i seguenti piani.

```text
Free
Premium
Premium Plus
Commerciante
```

Un account può possedere un solo Piano attivo alla volta.

---

# Ruoli Disponibili

CollectorVerse supporta:

```text
Utente
Moderatore
Amministratore
```

I privilegi derivanti dal Ruolo prevalgono sempre su quelli derivanti dal Piano.

---

# Esempi Validi

```text
Free + Utente

Premium + Utente

Premium Plus + Utente

Commerciante + Utente

Free + Moderatore

Premium + Amministratore
```

---

# Profilo Utente

Ogni account dispone di un Profilo Utente.

---

# Informazioni Principali

Il Profilo può mostrare:

- Avatar
- Cover
- Username
- Display Name
- Piano Attivo
- Livello
- CollectorScore
- Badge
- Affidabilità
- Data Iscrizione
- Recensioni
- Collezioni Pubbliche
- Wishlist Pubbliche

---

# Affidabilità

L'affidabilità rappresenta un indicatore interno utilizzato da:

- Marketplace
- Matching
- Sistema Antispam
- Moderazione

L'affidabilità non viene mostrata numericamente.

Visualizzazione:

```text
🟢 Alta

🟡 Media

🔴 Bassa
```

---

# Privacy

Ogni utente può configurare separatamente la privacy.

---

# Visibilità Profilo

Valori supportati:

```text
Pubblico

Privato
```

---

# Visibilità Collezioni

Valori supportati:

```text
Pubblico

Privato
```

---

# Visibilità Wishlist

Valori supportati:

```text
Pubblico

Privato
```

---

# Permessi Contatto

Ogni utente può definire chi può inviare Richieste di Contatto.

Valori disponibili:

```text
Tutti

Solo Premium

Solo Commercianti

Nessuno
```

---

# Preferenze Notifiche

Ogni account possiede preferenze notifiche indipendenti.

Le notifiche possono essere abilitate o disabilitate separatamente per:

- Push
- Email
- In-App

---

# Valuta Preferita

Ogni utente può impostare una Valuta Preferita.

Esempi:

```text
EUR €
USD $
GBP £
JPY ¥
CHF
```

La modifica della valuta preferita non modifica i dati storici esistenti.

---

# Richiesta di Contatto

Una Conversazione non può essere creata direttamente.

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

# Informazioni Visualizzate

La Richiesta di Contatto può mostrare:

- Username
- Display Name
- Piano
- Affidabilità
- Media Recensioni
- Numero Recensioni
- CollectorScore
- Badge Principali

---

# Stati Richiesta di Contatto

```text
In Attesa
Accettata
Rifiutata
Bloccata
Scaduta
```

---

# Regole Fondamentali

Una Conversazione viene creata esclusivamente quando una Richiesta viene accettata.

Non possono esistere Richieste pendenti duplicate tra gli stessi utenti.

Può esistere una sola Conversazione attiva tra una coppia di utenti.

---

# Anti-Spam

Dopo un rifiuto non è possibile inviare immediatamente una nuova richiesta.

Valore iniziale consigliato:

```text
24 ore
```

Configurabile tramite Dashboard Admin.

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

Valori:

```text
Inviato
Letto
```

---

# Blocchi Utente

Ogni utente può bloccare un altro utente.

---

# Effetti del Blocco

Il blocco impedisce:

- Follow
- Richieste di Contatto
- Conversazioni
- Matching
- Marketplace reciproco
- Visibilità reciproca nei risultati

---

# Durata

Il blocco resta attivo fino a rimozione manuale.

---

# Merchant Profile

Gli account con Piano Commerciante possono possedere un Profilo Negozio.

Ogni account può possedere al massimo:

```text
1 Merchant Profile
```

---

# Informazioni Merchant

Visualizzare:

- Logo
- Banner
- Nome Attività
- Descrizione
- Sito Web
- Indirizzo
- Orari
- Recapiti Pubblici
- Categorie Trattate

---

# Merchant Verification

Ogni Merchant Profile può possedere una sola verifica.

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

Gli account approvati mostrano il badge:

```text
✅ Commerciante Verificato
```

---

# Regole Verifica

La verifica:

- non scade automaticamente
- rimane valida fino a modifica amministrativa
- può essere sospesa
- può essere revocata

---

# Google Business Profile

I Merchant possono collegare un profilo Google Business.

---

# Informazioni Disponibili

- Rating Medio
- Numero Recensioni
- Profilo Business
- Recensioni Pubbliche

---

# Recensioni

Gli utenti possono recensire altri utenti.

---

# Regola Fondamentale

Un utente può lasciare una sola recensione per un altro utente.

Vincolo logico:

```text
1 recensione per coppia utenti
```

---

# Modifica Recensione

La recensione può essere modificata in qualsiasi momento.

La modifica aggiorna la recensione esistente.

Non viene creata una nuova recensione.

---

# Utilizzo Recensioni

Le recensioni contribuiscono a:

- Affidabilità
- Matching
- Profilo Utente
- Profilo Commerciante

---

# Moderatori

I Moderatori possono gestire:

- Segnalazioni Utenti
- Segnalazioni Annunci
- Segnalazioni Immagini
- Segnalazioni Recensioni
- Chat Segnalate
- Contenuti Segnalati

---

# Limitazioni Moderatore

Non possono:

```text
❌ modificare monetizzazione
❌ modificare configurazioni globali
❌ nominare amministratori
❌ accedere all'infrastruttura
```

---

# Amministratori

Gli Amministratori possiedono accesso completo alla Dashboard Admin.

Possono gestire:

- Utenti
- Merchant
- Catalogo
- Marketplace
- Matching
- Sicurezza
- Notifiche
- Monetizzazione
- Configurazioni Globali

---

# Stati Account

Ogni account può trovarsi in uno dei seguenti stati.

```text
Attivo
Sospeso
Bloccato
Eliminato
```

---

# Attivo

Accesso completo secondo Piano e Ruolo.

---

# Sospeso

Accesso limitato secondo le regole amministrative.

---

# Bloccato

Accesso negato.

---

# Eliminato

Account trattato secondo GDPR e normative Privacy applicabili.

---

# Eliminazione Account

L'utente può richiedere l'eliminazione dell'account.

---

# Conservazione Contributi

I contributi approvati al Catalogo Universale:

- vengono conservati
- vengono anonimizzati
- rimangono patrimonio permanente della piattaforma

Esempi:

- Oggetti
- Versioni
- Varianti
- Immagini
- Correzioni Approvate

---

# Obiettivo del Sistema Utenti

Il sistema Utenti di CollectorVerse deve consentire la gestione di collezionisti privati, utenti avanzati, commercianti professionali e personale amministrativo attraverso una chiara separazione tra:

- Identità
- Piani
- Ruoli
- Privacy
- Comunicazioni
- Verifiche
- Recensioni
- Permessi Operativi

garantendo scalabilità, sicurezza e coerenza con l'intero ecosistema CollectorVerse.

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

---

# Parte 6 - Catalogo Collaborativo • Contributori Catalogo • Votazioni • Reputazione • Immagini

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

---

# Parte 10 - Dashboard Amministratore • Configurazioni Globali • Moderazione • Asset Grafici • Statistiche

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
