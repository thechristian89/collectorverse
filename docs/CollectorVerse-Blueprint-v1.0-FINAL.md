# CollectorVerse Blueprint v1.0 FINAL

## Stato Documento

Versione ufficiale e definitiva del progetto CollectorVerse.

Questo documento rappresenta la fonte ufficiale delle specifiche funzionali dell'applicazione.

Tutte le future decisioni di progettazione, sviluppo, database e infrastruttura dovranno essere coerenti con quanto definito in questo Blueprint.

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

Ogni funzionalità deve rispettare i seguenti principi:

## Semplicità

Le funzionalità devono essere utilizzabili anche da utenti senza competenze tecniche.

---

## Scalabilità

La piattaforma deve supportare:

- milioni di utenti
- milioni di oggetti
- milioni di immagini

senza modifiche strutturali.

---

## Collaborazione

La community contribuisce alla crescita del catalogo.

---

## Qualità

Tutte le informazioni devono poter essere verificate, corrette e migliorate.

---

## Configurabilità

Qualsiasi numero, soglia, limite, percentuale o durata deve essere configurabile tramite Dashboard Admin senza modificare il codice.

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

## Invio Email

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

Utilizzata esclusivamente come supporto avanzato e fallback nei processi di scansione e riconoscimento.

---

## Versionamento

- GitHub

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

# Versione 1.0

L'obiettivo della Versione 1.0 è il rilascio pubblico della prima versione stabile dell'applicazione.

Le funzionalità previste saranno definite nelle sezioni successive del Blueprint.

---

---

# Tipologie Utente

CollectorVerse prevede diverse tipologie di utenti.

---

## Collezionista

Rappresenta l'utente standard della piattaforma.

Può:

- creare collezioni
- utilizzare il catalogo
- creare wishlist
- effettuare scansioni
- seguire utenti
- seguire collezioni
- seguire serie
- seguire oggetti
- partecipare alla community

---

## Commerciante

Utente che rappresenta un'attività commerciale.

Può:

- gestire un profilo attività
- indicare categorie trattate
- apparire nella mappa commercianti
- ricevere follower
- partecipare ai Contributori Catalogo nelle proprie categorie

---

## Commerciante Verificato

Badge assegnato manualmente da un amministratore.

Visualizzazione:

✅ Commerciante Verificato

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
- Password (solo registrazione Email)

---

## Commerciante

Campi aggiuntivi:

- Nome attività
- Categorie trattate
- Indirizzo
- Telefono (facoltativo)
- Sito Web (facoltativo)
- Google Maps (facoltativo)

---

# Login

Modalità disponibili:

- Email e Password
- Google

---

# Recupero Password

Disponibile per gli account registrati tramite Email.

---

# Profilo Utente

Ogni utente possiede un profilo.

---

## Informazioni Profilo

- Avatar
- Cornice Profilo
- Nome Utente
- CollectorScore
- Livello
- Badge
- Recensioni
- Data iscrizione
- Collezioni pubbliche
- Wishlist pubbliche

---

## Stato Profilo

Visualizzare:

Iscritto dal:

GG/MM/AAAA

---

# Profilo Pubblico

Ogni utente può possedere un profilo pubblico condivisibile.

Esempio:

collectorverse.com/u/nomeutente

---

## Condivisione

Disponibile tramite:

- Link pubblico
- QR Code profilo

---

# Privacy Profilo

Configurabile dall'utente.

---

## Opzioni

- Profilo pubblico
- Profilo privato

---

# Collezioni Pubbliche

Ogni collezione può essere impostata come:

- Pubblica
- Privata

indipendentemente dallo stato del profilo.

---

# Esempi

Profilo Privato

+

Collezione Pubblica

✅ Consentito

---

Profilo Pubblico

+

Collezione Privata

✅ Consentito

---

# Wishlist Pubbliche

Ogni wishlist può essere:

- Pubblica
- Privata

---

# Ricerca Utenti

## Free

Può:

- cercare utenti
- visualizzare profili pubblici
- seguire utenti

---

## Premium

Include tutte le funzioni Free.

Può inoltre:

- utilizzare la chat

---

## Premium Plus

Include tutte le funzioni Premium.

Può inoltre:

- utilizzare la geolocalizzazione utenti

---

# Recensioni Utente

Le recensioni rappresentano una funzionalità secondaria di supporto alla fiducia tra utenti.

Le recensioni NON rappresentano l'unico indicatore di affidabilità.

---

# Generazione Recensione

Un utente può generare:

Link Recensione

---

## Regole

Il link:

- dura 24 ore
- può essere utilizzato una sola volta
- può essere inviato solo tramite chat CollectorVerse
- può essere utilizzato solo da utenti registrati

---

# Limiti

Una coppia di utenti può generare una sola recensione.

Le soglie sono configurabili tramite Dashboard Admin.

---

# Valutazione

Sistema a stelle.

Esempio:

★★★★★

---

# Visualizzazione Profilo

Mostrare sempre:

- Media recensioni
- Numero recensioni

Esempio:

4,8 ★

(132 recensioni)

---

# Segnalazione Recensioni

Ogni recensione può essere segnalata.

L'amministratore decide eventuali interventi.

---

# Affidabilità Utente

CollectorVerse utilizza un Indice Affidabilità interno.

---

## Utilizzo

L'indice viene utilizzato per:

- Matching
- Ordinamento utenti
- Suggerimenti utenti

---

## Componenti possibili

- Recensioni
- Numero recensioni
- Data iscrizione
- CollectorScore
- Badge
- Storico attività

---

L'Indice Affidabilità NON viene mostrato numericamente agli utenti.

---

# Visualizzazione Affidabilità

Mostrare solamente:

🟢 Alta

🟡 Media

🔴 Bassa

---

# Commercianti

I commercianti possiedono un profilo dedicato.

---

## Informazioni Profilo Commerciante

- Nome attività
- Logo
- Descrizione
- Telefono
- Email
- Sito Web
- Google Maps
- Orari apertura
- Categorie trattate

---

# Recensioni Commercianti

CollectorVerse NON gestisce recensioni interne per i commercianti.

---

## Soluzione adottata

Visualizzazione recensioni esterne tramite:

Google Reviews

con collegamento al profilo Google Business.

---

# Sicurezza

CollectorVerse deve implementare un sistema di sicurezza multilivello.

---

## Verifica Email

Configurabile tramite Dashboard Admin.

---

## 2FA

Autenticazione a due fattori.

Configurabile tramite Dashboard Admin.

---

# Utilizzo 2FA

Può essere:

- Disattivata
- Facoltativa
- Obbligatoria

---

# Ruoli Consigliati

2FA obbligatoria per:

- Admin
- Super Admin

Configurabile in futuro anche per:

- Commercianti verificati

---

# Eliminazione Account

Disponibile dal profilo utente.

---

## Effetti

L'utente può richiedere:

- eliminazione account
- cancellazione dati personali

nel rispetto della normativa GDPR.

---

---

# Modello Economico

CollectorVerse utilizza un modello Freemium.

La piattaforma è accessibile gratuitamente con funzionalità avanzate disponibili tramite abbonamenti e pacchetti opzionali.

---

# Tipologie Piano

CollectorVerse prevede tre livelli di accesso.

- Free
- Premium
- Premium Plus

---

# Piano Free

Il piano Free consente di utilizzare le funzionalità base della piattaforma.

---

## Funzionalità Incluse

- Catalogo
- Collezioni
- Wishlist
- Segui utenti
- Segui collezioni
- Segui serie
- Segui oggetti
- Ricerca utenti
- Profili pubblici
- Collezioni pubbliche
- Wishlist pubbliche
- Mappa commercianti

---

## Limitazioni

Non può:

- utilizzare la chat
- utilizzare il matching
- pubblicare annunci nel marketplace
- visualizzare utenti sulla mappa

---

# Piano Premium

Il piano Premium sblocca le funzionalità social e marketplace.

---

## Funzionalità Incluse

Tutte le funzionalità Free.

Più:

- Chat
- Marketplace
- Annunci pubblici
- Scambi consigliati
- Utenti da seguire

---

# Piano Premium Plus

Il piano Premium Plus rappresenta il livello più completo.

---

## Funzionalità Incluse

Tutte le funzionalità Premium.

Più:

- Matching avanzato
- Geolocalizzazione utenti
- Mappa utenti
- Match vicini
- Utenti vicini

---

# Scansioni

CollectorVerse utilizza un sistema di scansioni giornaliere.

---

## Quantità Scansioni

Le quantità sono configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

Free

3 scansioni al giorno

---

Premium

20 scansioni al giorno

---

Premium Plus

40 scansioni al giorno

---

# Consumo Scansioni

La scansione viene consumata immediatamente dopo l'acquisizione della foto.

Ordine:

Foto

↓

1 scansione consumata

↓

Analisi

---

# Pubblicità

Gli utenti Free visualizzano pubblicità.

---

## Tipologie

- Banner
- Video Reward

---

# Banner

Posizionati in modo non invasivo all'interno dell'applicazione.

La presenza e la frequenza sono configurabili dalla Dashboard Admin.

---

# Video Reward

Gli utenti possono guardare video pubblicitari per ottenere scansioni aggiuntive.

---

## Ricompensa

Valore configurabile tramite Dashboard Admin.

Valore iniziale consigliato:

+3 scansioni

---

## Limite Giornaliero

Configurabile tramite Dashboard Admin.

Valore iniziale consigliato:

5 video al giorno

---

## Cooldown

Configurabile tramite Dashboard Admin.

Valore iniziale consigliato:

15 minuti

---

# Schermata Scansioni

Visualizzare:

- scansioni disponibili
- scansioni utilizzate
- scansioni ottenute tramite reward
- reset giornaliero
- video disponibili

---

# Marketplace

L'accesso al marketplace è determinato dal piano attivo.

---

# Oggetti in Vendita e Scambio

Ogni oggetto può essere contrassegnato come:

- In Vendita
- In Scambio

anche senza un piano Premium attivo.

---

# Utente Free

Può:

- contrassegnare gli oggetti
- preparare il catalogo personale

---

Non può:

- pubblicare annunci
- comparire nel marketplace
- partecipare al matching

---

# Passaggio Free → Premium

Quando un utente passa a Premium:

gli oggetti marcati come:

- In Vendita
- In Scambio

possono essere trasformati in annunci Marketplace.

---

# Limiti Annunci

Configurabili dalla Dashboard Admin.

Valori iniziali consigliati:

Premium

10 annunci

---

Premium Plus

30 annunci

---

# Superamento Limiti

Se gli oggetti disponibili sono superiori agli annunci consentiti:

mostrare un Wizard.

Esempio:

Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona quali rendere visibili.

---

# Stato Annunci

Ogni annuncio può assumere i seguenti stati.

---

## Attivo

Visibile nel Marketplace.

---

## Sospeso

Esistente ma non visibile.

---

## Chiuso

Concluso, venduto, scambiato o rimosso dall'utente.

---

# Scadenza Abbonamento

Se il piano Premium o Premium Plus termina:

gli annunci vengono automaticamente sospesi.

---

## Effetti

- non sono eliminati
- non sono visibili
- non partecipano al matching

---

# Riattivazione

Al rinnovo di un piano compatibile:

gli annunci vengono riattivati automaticamente.

---

# Pacchetti Aggiuntivi

CollectorVerse supporta pacchetti opzionali.

---

## Esempi

- scansioni aggiuntive
- annunci aggiuntivi

---

# Stato Pacchetti

---

## Attivo

Pacchetto utilizzabile.

---

## Congelato

Pacchetto temporaneamente sospeso.

---

## Scaduto

Pacchetto terminato.

---

# Congelamento Pacchetti

Se un utente perde il requisito necessario all'utilizzo del pacchetto:

il pacchetto viene congelato.

---

## Esempio

Premium

+

Pacchetto +100 annunci

↓

Scadenza Premium

↓

Pacchetto congelato

↓

Tempo residuo conservato

---

## Rinnovo

Quando l'utente torna ad avere un piano compatibile:

il pacchetto riprende dal tempo residuo rimasto.

---

# Abbonamenti

CollectorVerse supporta:

- Mensile
- Trimestrale
- Annuale

---

# Prezzi

I prezzi sono configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

---

Premium Mensile

€ 2,99

---

Premium Trimestrale

€ 7,99

---

Premium Annuale

€ 27,99

---

Premium Plus Mensile

€ 4,99

---

Premium Plus Trimestrale

€ 13,99

---

Premium Plus Annuale

€ 49,99

---

# Bundle

CollectorVerse supporta bundle combinati.

---

## Premium Collector

Premium Annuale

+

250 scansioni

+

50 annunci

---

Prezzo consigliato:

€ 34,99

---

## Premium Plus Collector

Premium Plus Annuale

+

1000 scansioni

+

100 annunci

---

Prezzo consigliato:

€ 69,99

---

# Monetizzazione

Le fonti di monetizzazione previste sono:

- Abbonamenti
- Bundle
- Pacchetti
- Banner pubblicitari
- Video Reward

---

# Gestione Admin

Tutti i seguenti parametri devono essere modificabili senza aggiornare il codice.

---

## Abbonamenti

- prezzi
- durata
- vantaggi

---

## Marketplace

- numero annunci
- durata annunci
- limiti piano

---

## Scansioni

- scansioni giornaliere
- reward video
- cooldown

---

## Pubblicità

- banner attivi
- video reward attivi

---

## Bundle

- composizione
- prezzo
- durata

---

## Pacchetti

- prezzo
- quantità
- durata

---

# Catalogo Universale

Il Catalogo Universale rappresenta il cuore di CollectorVerse.

Tutte le funzionalità della piattaforma si basano sulla struttura del catalogo.

---

# Obiettivo

Consentire la catalogazione di qualsiasi tipologia di oggetto collezionabile.

Esempi:

- Carte Collezionabili
- Figurine
- Monete
- Banconote
- Francobolli
- Fumetti
- Libri
- LEGO
- Action Figure
- Videogiochi
- Dischi
- Modellismo
- Vini
- Orologi
- Antiquariato

---

# Struttura Ufficiale

Ogni elemento del catalogo deve rispettare la seguente gerarchia.

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

---

# Categoria

Rappresenta il livello più alto della classificazione.

---

## Esempi

- Carte Collezionabili
- Numismatica
- Filatelia
- Fumetti e Libri
- LEGO
- Modellismo
- Videogiochi

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

# Serie

Ogni collezione può contenere più serie.

---

## Esempi

Pokémon

↓

Serie:

- Set Base
- Jungle
- Fossil
- Neo Genesis

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

Versione Generica

---

# Collezioni che utilizzano Versioni

Configurabile tramite Dashboard Admin.

---

## Esempi

Pokémon

✅ Versioni

---

Monete

✅ Versioni

---

Orologi

❌ Versioni

↓

Utilizzare Versione Generica

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

✅ Oggetto posseduto

---

# Completamento Versioni

CollectorVerse deve comunque mostrare l'avanzamento delle versioni.

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

2/4 versioni possedute

---

# Varianti

Le varianti rappresentano differenze produttive o errori di produzione.

Le varianti NON sono nuovi oggetti.

Le varianti NON sono nuove versioni.

---

## Esempi

- errore stampa
- errore centratura
- errore colore
- errore conio

---

# Regola Fondamentale

Le varianti:

- non aumentano il numero oggetti
- non aumentano il completamento serie
- non aumentano il completamento collezione
- non aumentano il completamento categoria

---

# Visualizzazione Varianti

Nel catalogo visualizzare:

🔀 Varianti presenti

---

## Esempio

Charizard

🔀 3 Varianti

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

# Statistiche Oggetto

Visualizzare:

- utenti che lo possiedono
- utenti che lo desiderano
- scansioni effettuate
- annunci attivi
- annunci scambio

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

# Creazione Nuovi Elementi

CollectorVerse supporta:

- Nuovo Oggetto
- Nuova Versione
- Nuova Variante

---

# Stato Iniziale

Ogni nuovo elemento creato dalla community assume lo stato:

Provvisorio

---

# Stati Disponibili

- Provvisorio
- Verificato
- Rifiutato
- Unificato

---

# Provvisorio

Elemento utilizzabile immediatamente.

Può essere:

- cercato
- catalogato
- aggiunto alle collezioni
- aggiunto alla wishlist
- utilizzato nel marketplace

---

# Verificato

Elemento approvato definitivamente.

---

# Rifiutato

Elemento non valido.

---

# Unificato

Elemento fuso con un altro elemento esistente.

---

# Controllo Duplicati

Prima della creazione di:

- Oggetti
- Versioni
- Varianti

CollectorVerse deve eseguire verifiche automatiche.

---

# Controlli Possibili

- nome
- codice
- OCR
- immagini
- hash immagini

---

# Nuove Versioni

Le nuove versioni seguono lo stesso processo di verifica delle varianti.

---

# Flusso Nuova Versione

Versione creata

↓

Provvisoria

↓

Revisione community

↓

Controllo amministratore

↓

Versione verificata

---

# Flusso Nuova Variante

Variante creata

↓

Provvisoria

↓

Revisione community

↓

Controllo amministratore

↓

Variante verificata

---

# Collezioni Preferite

Gli utenti possono salvare collezioni pubbliche.

---

## Funzionalità

⭐ Salva Collezione

---

# Sezione Profilo

Collezioni Preferite

---

# Collezioni Pubbliche

Ogni collezione pubblica possiede:

- link pubblico
- QR Code dedicato

---

## Esempio

collectorverse.com/u/mario/pokemon

---

# Regola Privacy

Se una collezione pubblica viene:

- eliminata
- resa privata

deve essere automaticamente rimossa dai preferiti degli altri utenti.

---

# Sistema Scansione

Il sistema di scansione rappresenta una delle funzionalità principali di CollectorVerse.

L'obiettivo è permettere il riconoscimento rapido degli oggetti catalogati.

---

# Obiettivi

- riconoscere oggetti esistenti
- ridurre inserimenti manuali
- velocizzare la catalogazione
- migliorare la qualità del catalogo
- assistere l'utente nella creazione di nuovi contenuti

---

# Flusso Scansione

Il flusso ufficiale è il seguente.

Categoria

↓

Collezione

↓

Versione

↓

Foto

↓

Consumo scansione

↓

Analisi

↓

Risultati

---

# Selezione Categoria

Prima della foto l'utente deve selezionare la categoria.

---

## Esempi

- Pokémon
- Monete
- Fumetti
- LEGO
- Francobolli

---

# Selezione Collezione

Dopo la categoria.

---

## Esempio

Categoria:

Pokémon

↓

Collezione:

Pokémon

---

# Selezione Versione

Dopo la collezione.

---

## Obiettivo

Ridurre gli errori di riconoscimento.

---

# Versioni Disponibili

Visualizzare tutte le versioni già esistenti.

---

## Esempi

- Italiano
- Inglese
- Giapponese
- Tedesco

---

# Collezioni senza Versioni

Se la collezione utilizza:

Versione Generica

il campo versione non deve essere mostrato.

---

# Acquisizione Foto

L'utente scatta o carica una foto.

---

# Consumo Scansione

La scansione viene consumata immediatamente dopo l'acquisizione della foto.

Ordine:

Foto

↓

1 scansione consumata

↓

Analisi

---

# Analisi

CollectorVerse utilizza più livelli di riconoscimento.

---

## Livello 1

Hash immagini.

---

## Livello 2

OCR.

---

## Livello 3

Confronto catalogo.

---

## Livello 4

AI come fallback.

---

# Hash Immagini

Confronto tra immagini già presenti nel catalogo.

Utilizzato per velocizzare il riconoscimento.

---

# OCR

L'OCR estrae informazioni testuali dalla foto.

---

## Esempi

- codici
- numerazioni
- nomi
- testi

---

# Confronto Catalogo

I risultati OCR e Hash vengono confrontati con il catalogo esistente.

---

# AI

L'intelligenza artificiale viene utilizzata esclusivamente quando le verifiche precedenti non producono un risultato sufficientemente affidabile.

---

# Risultati Scansione

Visualizzare:

- risultato suggerito
- livello affidabilità
- possibili alternative

---

## Esempio

Charizard 4/102

98%

---

Pikachu 58/102

81%

---

Charmander 46/102

72%

---

# Nessun Risultato

Se il sistema non trova risultati soddisfacenti:

mostrare il Wizard Catalogo.

---

# Wizard Catalogo

Permette la creazione guidata di nuovi elementi.

---

## Opzioni

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
- Numero/Codice
- Versione
- Immagine
- Descrizione facoltativa

---

# Nuova Versione

Utilizzata quando:

l'oggetto esiste

ma la versione non esiste.

---

## Esempio

Charizard esiste

↓

Versione Spagnola non presente

↓

Nuova Versione

---

# Nuova Variante

Utilizzata quando:

oggetto e versione esistono

ma esiste una nuova variante.

---

# Controlli Automatici

Prima della creazione il sistema deve verificare:

- duplicati
- nome
- codice
- OCR
- immagini
- hash

---

# Stato Iniziale

Oggetti, Versioni e Varianti create manualmente assumono lo stato:

Provvisorio

---

# Utilizzo Immediato

Anche se Provvisorio, l'elemento può essere:

- cercato
- utilizzato
- catalogato
- inserito in wishlist
- utilizzato nel marketplace

---

# Cronologia Scansioni

Ogni utente possiede una cronologia personale.

---

# Posizione

Profilo

↓

Cronologia Scansioni

---

# Informazioni Visualizzate

- Data
- Immagine
- Risultato ottenuto
- Categoria
- Collezione
- Versione

---

# Limiti

Visualizzare almeno:

Ultime 50 scansioni

Valore configurabile tramite Dashboard Admin.

---

# Errori di Scansione

Quando la scansione fallisce:

mostrare messaggi chiari e comprensibili.

---

## Esempi

Immagine troppo sfocata

---

Immagine troppo scura

---

Oggetto non riconosciuto

---

Nessuna versione selezionata

---

# Statistiche Scansione

CollectorVerse deve memorizzare:

- scansioni effettuate
- scansioni riuscite
- scansioni fallite
- scansioni tramite AI

---

# Dashboard Admin

Configurazioni modificabili senza aggiornare il codice.

---

## Scansioni

- scansioni giornaliere
- scansioni reward
- cooldown video
- scansioni AI

---

## Cronologia

- numero scansioni conservate

---

## AI

- attivazione AI
- soglia affidabilità
- limiti utilizzo AI

---

## Messaggi Errore

Tutti i messaggi devono poter essere personalizzati dalla Dashboard Admin.

---

# Catalogo Collaborativo

CollectorVerse utilizza un sistema di crescita collaborativa del catalogo.

La community può contribuire alla creazione e al miglioramento del catalogo globale.

---

# Obiettivo

Consentire una crescita rapida del catalogo mantenendo elevata la qualità dei dati.

---

# Contributori Catalogo

I Contributori Catalogo sono utenti autorizzati a partecipare alle revisioni.

---

# Accesso Commercianti

I commercianti diventano automaticamente Contributori Catalogo.

---

## Limitazione

Possono revisionare esclusivamente le categorie che hanno dichiarato nel proprio profilo.

---

# Accesso Utenti

Gli utenti possono essere invitati a diventare Contributori Catalogo.

---

## Requisito

Valore iniziale consigliato:

30 giorni di iscrizione

Configurabile tramite Dashboard Admin.

---

# Invito

Dopo aver raggiunto il requisito:

l'utente riceve una notifica.

---

## Messaggio

Vuoi aiutare CollectorVerse a migliorare il catalogo globale?

---

# Accettazione

Se accetta:

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

Profilo

↓

Contributori Catalogo

---

# Sezioni Disponibili

- Nuovi Oggetti
- Nuove Versioni
- Nuove Varianti
- Nuove Immagini
- Correzioni Catalogo

---

# Informazioni Visualizzate

Ogni revisione mostra:

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

# Possibili Voti

✅ Corretta

❌ Non Corretta

❓ Non So

---

# Motivazione

Se viene selezionato:

❌ Non Corretta

mostrare un campo:

Motivazione (facoltativa)

---

# Andamento Revisione

I revisori possono vedere l'andamento della votazione.

---

## Dati Visualizzati

Corretta: X

Non Corretta: X

Non So: X

Totale Voti: X

---

# Peso del Voto

Non tutti i voti hanno lo stesso peso.

---

# Reputazione Contributore

Formula:

Correzioni Approvate

-

Correzioni Respinte

---

# Valore Minimo

La reputazione non può mai assumere valori negativi.

Valore minimo:

0

---

# Peso Voto

Configurabile dalla Dashboard Admin.

Valori iniziali consigliati:

Reputazione 0-9

↓

Peso 1

---

Reputazione 10-29

↓

Peso 2

---

Reputazione 30-99

↓

Peso 3

---

Reputazione 100+

↓

Peso 5

---

# Applicazione

Valido sia per:

- utenti
- commercianti

---

# Statistiche Contributore

Ogni Contributore Catalogo deve visualizzare:

- Correzioni approvate
- Correzioni respinte
- Reputazione
- Peso voto attuale

---

# Revisione Community

La community NON approva direttamente gli elementi.

La community fornisce indicazioni agli amministratori.

---

# Stati Revisione

---

## Revisione Positiva

Valori configurabili.

Esempio:

- almeno 20 voti
- almeno 85% Corretta

---

## Revisione Negativa

Valori configurabili.

Esempio:

- almeno 20 voti
- almeno 85% Non Corretta

---

## Revisione Incerta

Tutti gli altri casi.

---

# Utilizzo Revisioni

Lo stato della revisione serve esclusivamente a dare priorità al lavoro amministrativo.

---

# Decisione Finale

La decisione finale spetta sempre all'amministratore.

---

# Azioni Amministratore

✅ Verifica

✏️ Correggi

❌ Rifiuta

🔀 Unifica

---

# Nuove Collezioni

Quando una nuova collezione non possiede ancora utenti:

le revisioni vengono affidate a:

- Commercianti della categoria
- Amministratori

---

# Immagini Collaborative

CollectorVerse utilizza un sistema di immagini collaborative.

---

# Obiettivo

Permettere alla community di migliorare continuamente la qualità delle immagini.

---

# Immagini Candidate

Ogni oggetto può avere più immagini candidate.

---

# Valutazione Immagini

Formula configurabile tramite Dashboard Admin.

Valori iniziali consigliati:

Qualità Tecnica

50%

---

Voti Community

40%

---

Utilizzo

10%

---

# Immagine Ufficiale

L'immagine con il punteggio più alto diventa immagine ufficiale.

---

# Soglia Minima

Configurabile tramite Dashboard Admin.

Valore iniziale consigliato:

80 / 100

---

# Nuova Immagine

Ogni nuova immagine entra come:

Immagine Candidata

---

# Prime Fasi

Quando un'immagine non possiede ancora voti o utilizzi:

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

# Dashboard Admin

Configurazioni modificabili.

---

## Contributori

- giorni minimi iscrizione
- soglie reputazione
- peso voto

---

## Revisioni

- voti minimi
- soglie revisione positiva
- soglie revisione negativa

---

## Immagini

- peso qualità
- peso voti
- peso utilizzo
- soglia immagine ufficiale

---

## Programma Contributori

Attivabile o disattivabile tramite Dashboard Admin.

---

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
- vendere oggetti duplicati
- scambiare oggetti
- trovare altri collezionisti

---

# Oggetti Disponibili

Ogni oggetto può essere contrassegnato come:

- In Vendita
- In Scambio

Le due opzioni possono essere utilizzate contemporaneamente.

---

## Esempio

Charizard

✅ In Vendita

✅ In Scambio

---

# Disponibilità e Annunci

CollectorVerse distingue:

Oggetto

↓

Disponibile per Vendita / Scambio

↓

Annuncio Marketplace

---

# Utente Free

Può:

- contrassegnare oggetti come In Vendita
- contrassegnare oggetti come In Scambio

---

Non può:

- pubblicare annunci
- comparire nel Marketplace
- utilizzare il Matching

---

# Utente Premium

Può:

- pubblicare annunci
- utilizzare la chat
- comparire nel Marketplace

---

# Utente Premium Plus

Include tutte le funzionalità Premium.

Più:

- Matching avanzato
- Geolocalizzazione utenti
- Mappa utenti

---

# Annunci Marketplace

Ogni annuncio può contenere:

- Oggetto
- Versione
- Variante
- Immagini
- Prezzo
- Descrizione
- Stato
- Posizione geografica

---

# Stati Annuncio

---

## Attivo

Visibile agli utenti.

---

## Sospeso

Presente ma non visibile.

---

## Chiuso

Concluso o rimosso.

---

# Downgrade Piano

Quando un utente perde il diritto di utilizzare il Marketplace:

gli annunci vengono automaticamente sospesi.

---

## Esempio

Premium

↓

Scadenza

↓

Free

↓

Annunci sospesi

---

# Riattivazione

Al rinnovo di un piano compatibile:

gli annunci vengono riattivati automaticamente.

---

# Limiti Piano

I limiti annunci sono configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

Premium

10 annunci

---

Premium Plus

30 annunci

---

# Superamento Limite

Quando un utente possiede più oggetti disponibili del consentito:

mostrare un Wizard.

---

## Esempio

Hai 57 oggetti disponibili.

Con il tuo piano puoi pubblicarne 10.

Seleziona gli annunci da mantenere attivi.

---

# Ricerca Marketplace

Consentire ricerche attraverso:

- testo
- categoria
- collezione
- serie
- oggetto
- versione
- distanza
- prezzo

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

Ogni elemento wishlist può contenere:

Prezzo Massimo Desiderato

---

## Esempio

Charizard

Prezzo massimo:

150 €

---

# Utilizzo

Il valore può essere utilizzato dal Matching.

---

# Chat

CollectorVerse include una chat interna.

---

# Accesso

Disponibile per:

- Premium
- Premium Plus

---

# Funzioni

- Messaggi testuali
- Invio immagini
- Link recensione
- Comunicazione utenti

---

# Recensioni dalla Chat

Il link recensione può essere inviato esclusivamente tramite chat interna.

---

# Matching

Il matching serve ad individuare opportunità rilevanti.

---

# Tipologie

- Matching acquisti
- Matching vendite
- Matching scambi

---

# Parametri Possibili

- Oggetti posseduti
- Wishlist
- Prezzo massimo
- Distanza
- Recensioni
- CollectorScore

---

# Ordinamento Matching

L'utente può personalizzare l'ordine delle priorità.

---

## Esempio

1. Prezzo
2. Distanza
3. Recensioni
4. CollectorScore

---

# Salvataggio

Le preferenze vengono salvate nel profilo utente.

---

# Indice Affidabilità

L'Indice Affidabilità può essere utilizzato internamente per migliorare i risultati.

---

# Geolocalizzazione

CollectorVerse supporta funzionalità geografiche.

---

# Ricerca Locale

Raggi configurabili tramite Dashboard Admin.

Valori iniziali consigliati:

- 10 km
- 25 km
- 50 km
- 100 km
- 250 km
- 500 km

---

# Ricerca Avanzata

Consentire ricerche per:

- Regione
- Nazione
- Continente

---

## Continenti

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

# Utenti Free

Possono visualizzare:

- Commercianti

---

Non possono visualizzare:

- Utenti

---

# Premium Plus

Può visualizzare:

- Utenti
- Commercianti

---

# Filtri Mappa

Consentire filtri per:

- Categoria
- Collezione
- Distanza

---

# Commercianti

Ogni commerciante può comparire nella mappa.

---

# Profilo Commerciante

Visualizzare:

- Nome attività
- Logo
- Descrizione
- Google Maps
- Orari apertura
- Categorie trattate

---

# Follow

Gli utenti possono seguire:

- Utenti
- Collezioni
- Serie
- Oggetti
- Commercianti

---

# Notifiche Follow

---

## Utente

- Nuovi annunci
- Nuove collezioni pubbliche

---

## Collezione

- Nuovi oggetti
- Nuove versioni
- Nuove varianti

---

## Serie

- Nuovi oggetti
- Nuove varianti

---

## Oggetto

- Nuove immagini
- Nuove varianti
- Nuovi annunci

---

## Commerciante

- Nuovi annunci
- Aggiornamenti profilo
- Nuove recensioni Google

---

# Dashboard Admin

Configurazioni modificabili.

---

## Marketplace

- limiti annunci
- durata annunci
- stati annunci

---

## Matching

- parametri disponibili
- attivazione matching

---

## Geolocalizzazione

- raggi disponibili
- visibilità mappa

---

## Chat

- attivazione chat
- limiti allegati

---

## Wishlist

- utilizzo prezzo massimo
- parametri matching

---

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

# Punteggi

Tutti i punteggi sono configurabili tramite Dashboard Admin.

---

## Esempi

- Profilo completato
- Oggetto aggiunto
- Collezione completata
- Badge ottenuto
- Correzione approvata
- Attività giornaliera

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

Le cornici devono essere visibili:

- Profilo utente
- Collezioni pubbliche
- Chat
- Marketplace
- Commenti e revisioni

---

# Badge

CollectorVerse utilizza un sistema badge.

---

# Obiettivi Badge

Premiare:

- esperienza
- partecipazione
- completamento collezioni
- contributo alla community
- fedeltà

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

---

## Fedeltà

Esempi:

- 30 giorni
- 180 giorni
- 365 giorni

---

## Marketplace

Esempi:

- Primo Annuncio
- Primo Scambio

---

## Community

Esempi:

- Primo Follow
- Collezione Pubblica

---

## Contributori Catalogo

Badge dedicati ai revisori.

---

# Livelli Contributori Catalogo

---

## Contributore Catalogo

Livello iniziale.

---

## Contributore Esperto

Revisore con esperienza.

---

## Curatore Catalogo

Contributore altamente affidabile.

---

# Esperto Serie

CollectorVerse riconosce gli utenti esperti di una determinata serie.

---

# Esempio

Pokémon

↓

Set Base

↓

Completamento elevato

↓

Badge Esperto Set Base

---

# Utilizzo

Mostrare il badge nel profilo pubblicamente.

---

# Progressione

Ogni badge deve mostrare:

- stato attuale
- progresso
- requisiti mancanti

---

## Esempio

500 Oggetti

Progressione:

322 / 500

---

# Obiettivi Giornalieri

CollectorVerse supporta obiettivi giornalieri.

---

# Esempi

- Effettua 3 scansioni
- Aggiungi un oggetto
- Aggiorna la wishlist
- Effettua una revisione

---

# Ricompense

Configurabili tramite Dashboard Admin.

---

## Esempi

- CollectorScore
- Badge speciali
- Bonus temporanei

---

# Sezione Badge

Ogni utente possiede una schermata dedicata.

---

# Filtri

- Tutti
- Ottenuti
- Non Ottenuti
- Progressione

---

# Affidabilità Visiva

L'indice affidabilità interno non viene mostrato numericamente.

---

# Rappresentazione

Mostrare solamente:

🟢 Alta

🟡 Media

🔴 Bassa

---

# Profilo Utente

Nel profilo visualizzare:

- CollectorScore
- Livello
- Cornice
- Badge
- Affidabilità
- Data iscrizione

---

# Dashboard Admin

Configurazioni modificabili.

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

- attivi/disattivi
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
- premi
- quantità

---

## Affidabilità

- parametri utilizzati
- peso dei parametri

---

# Esperienza Utente

L'interfaccia di CollectorVerse deve essere semplice, intuitiva e configurabile.

Ogni utente deve poter personalizzare la propria esperienza.

---

# Home

La Home rappresenta il punto di accesso principale dell'app.

---

# Obiettivi

Fornire una panoramica immediata di:

- collezioni
- scansioni
- wishlist
- badge
- attività recenti
- marketplace
- matching

---

# Widget Home

La Home è composta da widget.

---

## Widget Base

- Le mie collezioni
- Scansioni disponibili
- Wishlist
- Badge
- Attività recenti

---

## Widget Premium

- Scambi consigliati
- Utenti da seguire

---

## Widget Premium Plus

- Match vicini
- Utenti vicini

---

# Personalizzazione Home

L'utente può:

- mostrare widget
- nascondere widget
- riordinare widget

---

# Obiettivi Giornalieri

Visualizzare nella Home:

- obiettivi disponibili
- stato avanzamento
- premi ottenibili

---

# Profilo Utente

Ogni utente possiede una schermata profilo dedicata.

---

# Informazioni Principali

Visualizzare:

- Avatar
- Cornice profilo
- Nome utente
- CollectorScore
- Livello
- Affidabilità
- Data iscrizione

---

# Sezioni Profilo

- Collezioni
- Wishlist
- Annunci
- Recensioni
- Badge
- Contributori Catalogo
- Le mie attività
- Cronologia scansioni
- Import/Export
- Tutorial
- Centro assistenza
- Abbonamenti e pacchetti

---

# Le Mie Attività

Area dedicata allo storico delle attività dell'utente.

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

## Informazioni

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

- Piano attivo
- Scadenza
- Bundle attivi
- Pacchetti attivi
- Pacchetti congelati
- Pacchetti scaduti

---

## Esempio

Pacchetto +100 Annunci

Stato:

Congelato

Tempo residuo:

8 mesi e 12 giorni

---

# Collezioni Pubbliche

Ogni utente può condividere le proprie collezioni pubbliche.

---

# Condivisione

Permettere:

- Link pubblico
- QR Code dedicato

---

# Profilo Pubblico

Ogni utente può condividere il proprio profilo.

---

## Informazioni Visibili

- Avatar
- Cornice
- CollectorScore
- Badge
- Recensioni
- Collezioni pubbliche

---

# Condivisione Profilo

Permettere:

- Link pubblico
- QR Code profilo

---

# QR Code

I QR Code devono essere collegati all'identificativo interno dell'utente.

---

## Obiettivo

Evitare problemi in caso di modifica dello username.

---

# Notifiche

CollectorVerse utilizza un sistema notifiche centralizzato.

---

# Sezioni

- Tutte
- Non lette
- Sistema

---

# Tipologie

## Marketplace

- Nuovi annunci
- Nuovi scambi
- Nuove opportunità

---

## Chat

- Nuovi messaggi

---

## Matching

- Nuovi match

---

## Catalogo

- Nuovi oggetti
- Nuove versioni
- Nuove varianti

---

## Follow

- Aggiornamenti utenti seguiti
- Aggiornamenti collezioni seguite
- Aggiornamenti serie seguite
- Aggiornamenti oggetti seguiti

---

## Gamification

- Nuovi badge
- Passaggio livello
- Obiettivi completati

---

## Abbonamenti

- Scadenza imminente
- Pacchetti congelati
- Bundle in scadenza

---

# Promemoria Scadenza

Valori configurabili tramite Dashboard Admin.

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

- Problemi tecnici
- Errori catalogo
- Recensioni
- Immagini
- Utenti

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

Oggetti trovati:

1200

---

Oggetti riconosciuti:

1182

---

Oggetti da verificare:

18

---

Possibili duplicati:

4

---

# Correzione Guidata

I dati mancanti o errati devono essere corretti prima dell'importazione definitiva.

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

Permettere ricerca di:

- Categorie
- Collezioni
- Serie
- Oggetti
- Versioni
- Utenti
- Commercianti

---

# Dashboard Admin

Configurazioni modificabili.

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
- attivazione
- categorie

---

## Tutorial

- step tutorial
- ordine
- obbligatorietà

---

## Import/Export

- formati consentiti
- limiti file

---

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
- configurazione

deve essere modificabile dalla Dashboard Admin quando tecnicamente possibile.

---

# Accesso

Accessibile esclusivamente agli amministratori autorizzati.

---

# Sicurezza

2FA obbligatoria per:

- Admin
- Super Admin

Configurabile dalla Dashboard.

---

# Homepage Amministratore

Mostrare:

- Nuovi utenti oggi
- Nuovi commercianti oggi
- Utenti eliminati oggi
- Commercianti eliminati oggi
- Oggetti da verificare
- Versioni da verificare
- Varianti da verificare
- Immagini da verificare

---

# Dashboard Statistiche

Visualizzare:

- Utenti attivi
- Utenti Premium
- Utenti Premium Plus
- Commercianti
- Oggetti catalogati
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
- Utilizzo scansioni
- Utilizzo marketplace

---

# Gestione Utenti

Ricerca utenti.

Visualizzazione:

- dati profilo
- abbonamenti
- reputazione contributore
- storico attività
- segnalazioni

---

# Azioni Utente

Possibilità di:

- sospendere
- riattivare
- bloccare
- eliminare

---

# Gestione Commercianti

Visualizzare:

- profilo attività
- categorie dichiarate
- stato verifica
- statistiche

---

# Azioni Commerciante

- verifica account
- sospensione
- riattivazione
- eliminazione

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

# Azioni Catalogo

- creare
- modificare
- verificare
- rifiutare
- unificare
- eliminare

---

# Gestione Revisioni

Visualizzare:

- revisione positiva
- revisione negativa
- revisione incerta

---

# Azioni Revisioni

- verifica
- correzione
- rifiuto
- unificazione

---

# Gestione Immagini

Visualizzare:

- immagini ufficiali
- immagini candidate
- immagini segnalate

---

# Azioni Immagini

- approva
- elimina
- blocca
- sostituisci
- imposta immagine ufficiale

---

# Asset Grafici

Sezione dedicata alle immagini di sistema.

---

# Gestione Asset

Categorie

---

Permettere:

- logo
- banner
- immagine copertina

---

Collezioni

---

Permettere:

- logo
- banner
- immagine copertina

---

Badge

---

Permettere:

- immagine badge
- descrizione
- requisiti

---

Cornici Profilo

---

Permettere:

- upload immagini
- sostituzione immagini
- disattivazione cornici

---

Avatar

---

Permettere:

- upload
- modifica
- eliminazione

---

Tutorial

---

Permettere:

- immagini tutorial
- schermate tutorial
- banner tutorial

---

Banner Applicazione

---

Permettere:

- caricamento
- modifica
- attivazione
- disattivazione

---

# Configurazioni Globali

Area principale di configurazione.

---

# Scansioni

Configurare:

- scansioni Free
- scansioni Premium
- scansioni Premium Plus
- scansioni reward
- video massimi
- cooldown

---

# Marketplace

Configurare:

- annunci Premium
- annunci Premium Plus
- durata annunci
- scadenza annunci

---

# Matching

Configurare:

- parametri disponibili
- ponderazione parametri
- attivazione matching

---

# Geolocalizzazione

Configurare:

- raggi disponibili
- nazioni abilitate
- continenti disponibili

---

# Recensioni

Configurare:

- durata link
- recensioni per coppia utenti
- attivazione recensioni

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

- soglie livello
- nomi livello

---

# Badge

Configurare:

- requisiti
- punti assegnati
- stato attivo/disattivo

---

# Versioni

Configurare:

- utilizzo versioni
- utilizzo versione generica

---

# Varianti

Configurare:

- regole varianti
- soglie approvazione

---

# Importazione

Configurare:

- dimensione file
- formati consentiti

---

# Feature Flags

Possibilità di attivare o disattivare intere funzionalità.

---

# Funzionalità Gestibili

- Marketplace
- Matching
- Recensioni
- Geolocalizzazione
- Contributori Catalogo
- Versioni
- Varianti
- Pubblicità
- Chat
- Importazione

---

# Monetizzazione

Area dedicata alla gestione economica.

---

# Abbonamenti

Configurare:

- nome
- prezzo
- durata
- vantaggi

---

# Bundle

Configurare:

- contenuto
- prezzo
- durata

---

# Pacchetti

Configurare:

- quantità
- prezzo
- validità

---

# Pubblicità

Configurare:

- banner
- video reward
- frequenza

---

# Audit Log

Tutte le azioni amministrative devono essere registrate.

---

# Informazioni Registrate

- amministratore
- data
- ora
- azione
- elemento modificato

---

# Cestino

Elementi eliminati recuperabili.

---

# Recupero

Durata configurabile.

Valore iniziale consigliato:

30 giorni

---

# Backup

Consentire esportazioni amministrative.

---

# Esportazioni

- catalogo
- utenti
- marketplace
- revisioni
- configurazioni

---

# Modalità Manutenzione

Feature attivabile dalla Dashboard.

---

# Utilizzo

Permette di bloccare temporaneamente l'utilizzo dell'app.

---

# Sicurezza

Configurare:

- tentativi login
- obbligatorietà 2FA
- verifiche email

---

# Notifiche Sistema

Configurare:

- template
- categorie
- frequenza

---

# Statistiche Avanzate

Visualizzare:

- categorie più seguite
- collezioni più seguite
- serie più seguite
- oggetti più visualizzati

---

# Contributori Catalogo

Visualizzare:

- migliori revisori
- revisioni effettuate
- reputazione
- affidabilità revisori

---

# Obiettivo Finale

Consentire agli amministratori di gestire CollectorVerse senza modificare il codice applicativo e senza pubblicare aggiornamenti non necessari.
