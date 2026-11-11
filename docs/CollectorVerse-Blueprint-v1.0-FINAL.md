
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

# Parte 2 - Utenti • Privacy • Sicurezza • Recensioni • Gestione Account • Ruoli • Profili

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

Il Piano determina le funzionalità disponibili all'interno della piattaforma.

Il Ruolo determina i privilegi operativi e amministrativi.

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

# Ruoli Disponibili

CollectorVerse supporta i seguenti ruoli:

```text
Utente

Moderatore

Amministratore
```

I privilegi derivanti dal Ruolo prevalgono sempre su quelli derivanti dal Piano.

---

# Esempi di Account

Esempi validi:

```text
Free + Utente

Premium + Utente

Premium Plus + Utente

Commerciante + Utente

Free + Moderatore

Premium + Amministratore
```

---

# Registrazione

CollectorVerse supporta la registrazione tramite:

```text
Email

Google
```

Ogni account possiede:

- Identificativo interno permanente
- Username univoco
- Data di registrazione
- Profilo personale

L'identificativo interno non è modificabile.

La modifica dello username non altera:

- identità account
- collegamenti interni
- QR Code
- storico attività
- dati catalogati

---

# Profilo Utente

Ogni account dispone di un Profilo Utente.

Il profilo può mostrare:

- Avatar
- Username
- Piano attivo
- Livello
- CollectorScore
- Badge
- Affidabilità
- Data di iscrizione

La visibilità delle informazioni dipende dalle impostazioni Privacy dell'utente.

---

# Piano Free

Il Piano Free consente:

- utilizzo del Catalogo Universale
- gestione Collezioni Personali
- gestione Wishlist
- utilizzo del sistema Follow
- utilizzo delle Scansioni giornaliere disponibili
- partecipazione al Catalogo Collaborativo
- visualizzazione Marketplace
- ricezione Richieste di Contatto
- ricezione Messaggi
- risposta alle Conversazioni esistenti
- accesso alla Mappa Commercianti

---

## Limitazioni Piano Free

Non può:

```text
❌ avviare nuove Conversazioni

❌ creare Annunci Marketplace

❌ utilizzare il Matching

❌ comparire nella Mappa Utenti
```

---

# Piano Premium

Include tutte le funzionalità del Piano Free.

---

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

---

## Funzionalità Aggiuntive

```text
✅ Mappa Utenti

✅ Geolocalizzazione avanzata

✅ Matching avanzato

✅ Filtri geografici avanzati

✅ Visibilità geografica configurabile
```

---

# Piano Commerciante

Il Piano Commerciante è destinato a:

- negozi
- fumetterie
- card shop
- rivenditori professionali
- attività commerciali specializzate nel collezionismo

Il Piano Commerciante include tutte le funzionalità del Piano Premium Plus.

---

## Profilo Negozio

Ogni account Commerciante dispone di una pagina negozio dedicata.

Il Profilo Negozio può mostrare:

- Logo
- Banner
- Descrizione attività
- Sito web
- Indirizzo
- Orari di apertura
- Recapiti pubblici
- Categorie trattate

---

## Mappa Commercianti

I Commercianti possono comparire nella Mappa Commercianti.

La presenza sulla mappa è controllata dal titolare dell'attività ed è soggetta alle impostazioni privacy.

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

## Funzionalità Professionali

I Commercianti possono:

- pubblicare un numero maggiore di annunci
- usufruire di limiti scansione dedicati
- comparire nella Mappa Commercianti
- gestire un Profilo Negozio completo

Tutti i limiti sono configurabili dalla Dashboard Admin.

---

# Commerciante Verificato

Gli Amministratori possono assegnare lo stato:

```text
Commerciante Verificato
```

agli account Commerciante.

---

## Requisiti Possibili

La verifica può richiedere:

- documentazione aziendale
- partita IVA
- sito web
- presenza commerciale verificabile
- ulteriori verifiche definite dagli amministratori

---

## Badge Verifica

Gli account verificati mostrano il badge:

```text
✅ Commerciante Verificato
```

La perdita della verifica non modifica il Piano Commerciante.

---

# Moderatori

I Moderatori possono gestire:

- segnalazioni utenti
- segnalazioni annunci
- segnalazioni immagini
- segnalazioni recensioni
- contenuti segnalati
- chat segnalate

---

## Limitazioni Moderatore

Non possono:

```text
❌ modificare monetizzazione

❌ modificare configurazioni globali

❌ nominare Amministratori

❌ accedere all'infrastruttura
```

---

# Amministratori

Gli Amministratori possiedono accesso completo alla Dashboard Admin.

Possono gestire:

- utenti
- catalogo
- marketplace
- matching
- monetizzazione
- notifiche
- sicurezza
- configurazioni globali

---

# Richieste di Contatto

L'apertura di una nuova Conversazione richiede una Richiesta di Contatto preventiva.

La richiesta mostra:

- Username
- Piano attivo
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

Solo una richiesta Accettata genera una Conversazione.

---

# Anti-Spam

Dopo un rifiuto non è possibile inviare immediatamente una nuova richiesta.

Valore iniziale consigliato:

```text
1 giorno
```

Il valore è configurabile tramite Dashboard Admin.

---

# Permessi di Contatto

Ogni utente può definire chi può inviargli Richieste di Contatto.

---

## Opzioni Disponibili

```text
Tutti

Solo Premium

Solo Commercianti

Nessuno
```

---

# Blocchi Utente

Ogni utente può bloccare un altro utente.

Il blocco impedisce:

- visualizzazione del profilo
- visualizzazione annunci
- invio richieste di contatto
- apertura conversazioni
- follow
- comparsa reciproca nei risultati

Il blocco resta attivo fino alla sua rimozione manuale.

---

# Privacy

Ogni profilo può essere configurato come:

```text
Pubblico

Privato
```

Le Collezioni e le Wishlist possono avere impostazioni privacy indipendenti dal profilo.

---

# Valuta Preferita

Ogni utente può configurare una Valuta Preferita.

Esempi:

```text
EUR €

USD $

GBP £

JPY ¥

CHF
```

La modifica della valuta preferita non modifica i prezzi già inseriti.

---

# Stato Account

Ogni account può trovarsi in uno dei seguenti stati:

```text
Attivo

Sospeso

Bloccato

Eliminato
```

---

## Attivo

L'utente può utilizzare normalmente la piattaforma.

---

## Sospeso

L'utente dispone di accesso limitato secondo le regole amministrative.

---

## Bloccato

L'utente non può accedere alla piattaforma.

---

## Eliminato

L'account segue le procedure GDPR e Privacy previste dalla piattaforma.

---

# Eliminazione Account

L'utente può richiedere l'eliminazione del proprio account.

L'eliminazione deve rispettare le normative Privacy e GDPR applicabili.

I contributi approvati al Catalogo Universale:

- vengono conservati
- vengono anonimizzati
- diventano patrimonio permanente della piattaforma

Esempi:

- Oggetti
- Versioni
- Varianti
- Immagini
- Correzioni approvate

---

# Obiettivo del Sistema Utenti

Il sistema Utenti di CollectorVerse deve consentire la gestione di collezionisti privati, utenti avanzati, attività commerciali e personale amministrativo attraverso una separazione chiara tra Piani, Ruoli, Privacy e Permessi operativi.

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

# Disponibilità Oggetti

Ogni oggetto presente nella Collezione Personale può essere contrassegnato come:

```text
In Vendita

In Scambio
```

Le due opzioni possono coesistere.

La disponibilità non genera automaticamente un Annuncio Marketplace.

---

# Tipologie di Disponibilità

## In Vendita

L'utente è disposto a vendere l'oggetto.

---

## In Scambio

L'utente è disposto a scambiare l'oggetto con altri collezionisti.

---

# Accesso al Marketplace

L'accesso dipende dal Piano attivo dell'utente.

---

## Piano Free

Può:

```text
✅ contrassegnare oggetti In Vendita

✅ contrassegnare oggetti In Scambio

✅ mostrare tali disponibilità nel proprio profilo
```

Non può:

```text
❌ creare Annunci Marketplace
```

---

## Piano Premium

Può:

```text
✅ creare Annunci Marketplace

✅ creare annunci di vendita

✅ creare annunci di scambio
```

---

## Piano Premium Plus

Può utilizzare tutte le funzionalità Marketplace del Piano Premium.

---

## Piano Commerciante

Può utilizzare tutte le funzionalità Marketplace del Piano Premium Plus.

Dispone inoltre di:

- limiti annunci dedicati
- Profilo Negozio
- statistiche professionali
- Mappa Commercianti
- stato Commerciante Verificato

---

# Annunci Marketplace

Gli annunci sono pubblicazioni visibili all'interno del Marketplace.

Un annuncio può essere creato esclusivamente per un oggetto presente nella Collezione Personale dell'utente.

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
```

---

# Prezzo

Gli annunci di vendita devono possedere un prezzo.

Gli annunci di scambio possono non avere alcun prezzo.

Il prezzo viene sempre salvato nella valuta originale inserita dall'utente.

---

# Valute

Ogni utente possiede una Valuta Preferita configurabile.

Esempi:

```text
EUR €

USD $

GBP £

JPY ¥

CHF
```

CollectorVerse non effettua conversioni automatiche tra valute.

Gli utenti visualizzano sempre:

```text
Prezzo originale

+

Valuta originale
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

Venduto, scambiato o rimosso dal proprietario.

---

# Limiti Annunci

I limiti sono configurabili tramite Dashboard Admin.

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

Se il numero di annunci supera il limite consentito dal Piano:

mostrare un Wizard di selezione.

Esempio:

```text
Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona gli annunci da mantenere attivi.
```

---

# Scadenza Piano

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

# Ricerca Marketplace

Il Marketplace deve supportare:

- ricerca testuale
- ricerca catalografica
- filtri avanzati
- ordinamenti personalizzati

---

# Filtri Disponibili

Filtri minimi:

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
- Tipologia annuncio
- Tipologia account

---

# Ordinamenti

Ordinamenti iniziali consigliati:

- Compatibilità
- Data pubblicazione
- Prezzo
- Distanza
- Affidabilità
- CollectorScore
- Recensioni

---

# Matching

Il Matching rappresenta il sistema automatico che individua opportunità rilevanti tra utenti.

---

# Accesso al Matching

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
- Disponibili per Vendita
- Disponibili per Scambio
- Annunci Marketplace
- Affidabilità
- Recensioni
- CollectorScore

---

# Matching Acquisto

Individua:

```text
Oggetti desiderati

↓

presenti presso altri utenti
```

Può utilizzare:

- Wishlist
- prezzo massimo desiderato
- condizione minima accettata
- distanza geografica

---

# Matching Vendita

Individua:

```text
Utenti interessati

↓

agli oggetti disponibili
```

Può utilizzare:

- Wishlist compatibili
- distanza
- Affidabilità
- Recensioni

---

# Matching Scambio

Identifica situazioni in cui:

```text
Utente A possiede qualcosa
desiderato da Utente B

e

Utente B possiede qualcosa
desiderato da Utente A
```

---

# Geolocalizzazione

Il Matching può utilizzare la distanza geografica.

---

## Distanza Iniziale Consigliata

```text
25 km
```

---

## Estensioni Disponibili

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

Il Matching può filtrare per:

- Regione
- Nazione
- Continente

---

# Affidabilità

L'Affidabilità può influenzare il ranking dei risultati.

Gli utenti con Affidabilità superiore possono ottenere una priorità maggiore.

---

# Recensioni

Le recensioni possono influenzare:

- ranking
- ordinamento
- priorità dei risultati

---

# CollectorScore

Il CollectorScore può contribuire al ranking dei risultati.

---

# Versioni e Varianti

Il Matching deve supportare:

- Versioni specifiche
- Varianti specifiche

Una Wishlist che richiede una Variante specifica deve privilegiare risultati compatibili.

---

# Matching Professionale

Il Piano Commerciante dispone di funzionalità professionali dedicate.

---

## Opportunità Commerciali

Il sistema può individuare:

- utenti interessati agli oggetti del commerciante
- Wishlist compatibili
- aree geografiche con elevata domanda
- nuove opportunità commerciali

---

# Visualizzazione Risultati

Ogni risultato può mostrare:

- Oggetto
- Versione
- Variante
- Condizione
- Prezzo
- Valuta
- Distanza
- Affidabilità
- CollectorScore
- Recensioni

---

# Utenti Bloccati

Gli utenti bloccati non devono comparire nei risultati reciproci.

Non deve essere generato Matching tra utenti che hanno attivato un blocco reciproco.

---

# Contatto

Quando un Matching viene considerato interessante:

l'utente può avviare una Richiesta di Contatto.

L'apertura della Conversazione segue le regole previste dal sistema Chat.

---

# Notifiche Matching

CollectorVerse può inviare notifiche relative a:

- nuovi Match Acquisto
- nuovi Match Vendita
- nuovi Match Scambio
- nuovi annunci compatibili
- nuove opportunità professionali

Le notifiche rispettano le preferenze dell'utente.

---

# Statistiche

CollectorVerse può mantenere statistiche relative a:

- Matching generati
- Matching visualizzati
- Matching convertiti in contatto
- Matching convertiti in recensione
- Matching convertiti in transazione

---

# Obiettivo del Marketplace e del Matching

L'obiettivo del Marketplace e del Matching è facilitare l'incontro tra collezionisti e commercianti, aumentare la probabilità di completamento delle collezioni e favorire scambi e vendite rilevanti senza che CollectorVerse intervenga direttamente nelle transazioni economiche.

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

# Obiettivo

La Dashboard Amministratore rappresenta il centro di controllo operativo di CollectorVerse.

Tutte le configurazioni dinamiche della piattaforma devono essere gestite attraverso la Dashboard senza richiedere modifiche al codice applicativo.

La Dashboard deve consentire il monitoraggio, la gestione e la configurazione completa dell'ecosistema CollectorVerse.

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

- segnalazioni utenti
- segnalazioni immagini
- segnalazioni recensioni
- segnalazioni annunci
- contenuti segnalati
- chat segnalate

Non può:

```text
❌ modificare monetizzazione

❌ modificare configurazioni globali

❌ gestire infrastruttura

❌ nominare amministratori
```

---

# Amministratore

Possiede accesso completo alla Dashboard.

Può gestire:

- utenti
- catalogo
- marketplace
- matching
- monetizzazione
- notifiche
- sicurezza
- configurazioni globali
- feature flags
- statistiche

---

# Dashboard Home

La Dashboard deve fornire una vista riassuntiva dello stato della piattaforma.

---

## Indicatori Principali

Visualizzare almeno:

- utenti registrati
- utenti attivi
- nuovi utenti
- nuovi Premium
- nuovi Premium Plus
- nuovi Commercianti
- Commercianti Verificati
- annunci attivi
- scansioni giornaliere
- revisioni catalogo in attesa
- segnalazioni aperte
- notifiche inviate

---

# Gestione Utenti

Gli Amministratori devono poter ricercare qualsiasi account.

---

## Ricerca

Supportare almeno:

```text
Username

Email

ID Utente
```

---

## Scheda Utente

La scheda deve mostrare:

- Profilo
- Piano
- Ruolo
- Stato Account
- CollectorScore
- Livello
- Affidabilità
- Storico attività
- Segnalazioni ricevute
- Storico abbonamenti

---

## Operazioni Disponibili

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

## Piani Supportati

```text
Free

Premium

Premium Plus

Commerciante
```

---

## Operazioni Disponibili

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

senza modificare il codice.

---

# Gestione Durate

Durate iniziali:

```text
Mensile

Trimestrale

Annuale
```

---

## Durate Personalizzate

La Dashboard deve consentire la creazione di durate aggiuntive.

Esempi:

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

- attivazione/disattivazione
- durata
- piano associato
- regole di utilizzo

---

## Valore Iniziale Consigliato

```text
7 giorni
```

---

# Gestione Commercianti

La Dashboard deve supportare la gestione completa dei Commercianti.

---

## Operazioni Disponibili

```text
Verifica

Revoca Verifica

Sospendi

Riattiva

Elimina
```

---

# Commerciante Verificato

Gli Amministratori possono assegnare il badge:

```text
✅ Commerciante Verificato
```

---

## Verifica

La verifica può richiedere:

- documentazione aziendale
- partita IVA
- sito web
- attività verificabile

---

# Gestione Catalogo

Gli Amministratori devono poter gestire:

```text
Categorie

Collezioni

Serie

Oggetti

Versioni

Varianti
```

---

# Categorie

Stati supportati:

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

# Revisioni Catalogo

La Dashboard deve includere un Centro Revisioni.

---

## Revisione Elementi

Revisionabili:

- Oggetti
- Versioni
- Varianti
- Immagini
- Correzioni

---

## Azioni Disponibili

```text
Approva

Correggi

Rifiuta

Unifica
```

---

# Gestione Immagini

Gli Amministratori devono poter gestire tutte le immagini catalogo.

---

## Operazioni

```text
Approva

Rifiuta

Archivia

Imposta Ufficiale

Sostituisci Immagine Ufficiale
```

---

# Asset Grafici

La Dashboard deve gestire:

- loghi categoria
- banner categoria
- loghi collezione
- banner collezione
- badge
- cornici profilo
- immagini placeholder

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

## Configurazioni Disponibili

- piani
- prezzi
- durate
- periodo di prova
- bundle
- pacchetti
- reward video
- scansioni bonus

---

# Provider Pagamenti

La piattaforma deve supportare provider di pagamento configurabili.

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

- banner
- rewarded video
- frequenza
- limiti giornalieri
- cooldown

---

# Gestione Marketplace

Configurazioni disponibili:

- limiti annunci
- durata annunci
- visibilità annunci
- stati annunci

---

## Limiti Annunci Consigliati

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

# Gestione Scansioni

Configurazioni disponibili:

- scansioni giornaliere
- scansioni reward
- cooldown
- limiti giornalieri
- provider OCR
- provider AI

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

- pesi matching
- formule matching
- distanza geografica
- filtri geografici
- soglie compatibilità

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

- categorie
- template
- canali
- digest
- priorità

---

# Gestione Valute

La Dashboard deve consentire la gestione delle valute utilizzabili.

---

## Operazioni

```text
Crea

Modifica

Nascondi

Archivia
```

---

# Feature Flags

La piattaforma deve supportare l'attivazione e la disattivazione dinamica delle funzionalità.

---

## Funzionalità Gestibili

```text
Marketplace

Matching

Chat

Recensioni

Scansioni

Notifiche

Catalogo Collaborativo

Importazione

Esportazione
```

---

# Audit Log

Ogni operazione amministrativa deve essere registrata.

---

## Informazioni Minime

- amministratore
- data
- ora
- azione
- risorsa coinvolta

---

## Caratteristiche

```text
Immodificabile

Persistente

Consultabile

Ricercabile
```

---

# Cestino Amministrativo

Gli elementi eliminati devono essere conservati.

---

## Durata Iniziale Consigliata

```text
30 giorni
```

---

## Operazioni

```text
Ripristina

Elimina Definitivamente
```

---

# Statistiche

La Dashboard deve fornire statistiche avanzate.

---

## Statistiche Disponibili

- crescita utenti
- crescita catalogo
- crescita commercianti
- conversioni prova gratuita
- conversioni abbonamenti
- utilizzo marketplace
- utilizzo matching
- utilizzo scansioni
- utilizzo pubblicità
- entrate pubblicitarie
- entrate abbonamenti

---

# Esportazioni Amministrative

Gli Amministratori devono poter esportare:

- catalogo
- configurazioni
- revisioni
- statistiche
- marketplace

---

# Modalità Manutenzione

La piattaforma deve supportare una Modalità Manutenzione.

---

## Operazioni Disponibili

```text
Attiva

Disattiva

Programma

Messaggio Personalizzato
```

---

## Effetti

Durante la manutenzione:

- l'accesso utenti può essere limitato
- alcune funzionalità possono essere disattivate
- il personale amministrativo mantiene l'accesso

---

# Obiettivo della Dashboard Admin

La Dashboard Admin rappresenta il punto centrale di gestione di CollectorVerse e deve consentire ad Amministratori e Moderatori di configurare, controllare, monitorare e mantenere l'intera piattaforma senza richiedere modifiche al codice applicativo.

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
