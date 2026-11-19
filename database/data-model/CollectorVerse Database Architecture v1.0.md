# Vista Generale

```text
users
│
├── privacy_settings
├── user_collections
│   └── user_items
│
├── wishlists
│   └── wishlist_items
│
├── marketplace_listings
│   └── marketplace_offers
│       └── marketplace_offer_trade_items
│
├── matching_preferences
├── matching_opportunities
├── notifications
│
├── conversation_threads
│   ├── conversation_participants
│   │
│   └── messages
│       └── message_attachments
│
├── user_reviews
│
├── user_scores
│   ├── user_achievements
│   ├── user_badges
│   └── leaderboard_entries
│
├── merchant_verifications
│
├── scan_sessions
│   └── scan_results
│
└── catalog_contributions
    ├── catalog_contribution_attachments
    └── catalog_contribution_votes
```

---

## Motivazione

Questa vista rappresenta il punto di ingresso principale dell'ecosistema CollectorVerse.

La maggior parte delle funzionalità operative della piattaforma ruota attorno agli utenti e alle loro attività.

---

## Nota

Nel Catalogo Collaborativo il flusso operativo tipico è:

```text
Creazione Contributo

↓

Aggiunta Allegati

↓

Votazione Community
```

Per questo motivo gli allegati vengono mostrati prima dei voti.

---

# Catalogo Universale

```text
categories
│
└── collections
    │
    └── series
        │
        └── items
            │
            └── item_versions
                │
                ├── item_variants
                │   └── catalog_images
                │
                └── catalog_images
```

---

## Motivazione

Le immagini non appartengono direttamente agli Item.

Le immagini possono appartenere a:

```text
Item Version
```

oppure:

```text
Item Variant
```

tramite la tabella:

```text
catalog_images
```

---

## Priorità Visualizzazione

```text
Item Variant

↓

Item Version

↓

Placeholder
```

---

## Compatibilità Scanner

Lo Scanner può utilizzare immagini provenienti sia dalle Versioni sia dalle Varianti.

---

# Mappa Completa delle Foreign Key

## Obiettivo

Questa sezione descrive tutte le dipendenze tra le tabelle.

Serve per:

- generare correttamente PostgreSQL
- creare le tabelle nell'ordine corretto
- evitare errori di Foreign Key
- preparare Supabase
- preparare le migrazioni future

---

## Legenda

```text
A → B

significa:

A contiene una Foreign Key verso B
```

Esempio:

```text
user_items
→ items
```

significa:

user_items contiene una colonna che punta ad items.

# Nota Architetturale
catalog_images può appartenere ad una Item Version oppure ad una Item Variant.

Le immagini non sono ereditate automaticamente.

Una Variante può possedere immagini dedicate differenti dalla Versione di appartenenza.
---

# Livello 1 - Tabelle Fondamentali

Queste tabelle devono essere create per prime.

```text
users

currencies

languages

categories

rarities

feature_flags

system_settings

achievements

badges

leaderboards
```

---

## Motivazione

Non richiedono altre tabelle operative per essere create.

Costituiscono il livello base dell'intero database.

---

# Livello 2 - Infrastruttura Base e Dipendenze Dirette

```text
media_files
→ users

collections
→ categories

privacy_settings
→ users

saved_searches
→ users
→ categories
→ collections
→ series
→ items
→ item_versions
→ item_variants
→ currencies
```

---

## Motivazione

Queste tabelle dipendono direttamente dalle entità fondamentali e costituiscono il primo livello operativo della piattaforma.

---

## Nota

La tabella:

```text
media_files
```

viene creata nei livelli iniziali perché molte altre tabelle dipendono direttamente da essa.

---

## Esempi

```text
catalog_images

message_attachments

media_usages
```

---

## Nota su saved_searches

Molte Foreign Key di:

```text
saved_searches
```

sono opzionali.

Una ricerca salvata può utilizzare:

```text
nessun filtro

alcuni filtri

tutti i filtri
```

a seconda delle esigenze dell'utente.

---

# Livello 3 - Catalogo Universale (Livello Collezioni)

```text
series
→ collections
```

---

## Motivazione

Le Serie dipendono dalle Collezioni.

---

## Flusso Logico

```text
categories

↓

collections

↓

series
```

---

# Livello 4 - Catalogo Universale (Livello Item)

```text
items
→ series
```

---

## Motivazione

Gli Item appartengono sempre ad una Serie.

---

## Flusso Logico

```text
series

↓

items
```

---

# Livello 5 - Catalogo Universale (Versioni)

```text
item_versions
→ items
```

---

## Motivazione

Le Versioni appartengono ad un Item.

---

## Flusso Logico

```text
items

↓

item_versions
```

---

# Livello 6 - Catalogo Universale (Varianti e Immagini)

```text
item_variants
→ item_versions

catalog_images
→ media_files

→ item_versions
oppure
→ item_variants
```

---

## Motivazione

Le Varianti dipendono dalle Versioni.

Le immagini vengono archiviate tramite:

```text
media_files
```

e possono appartenere ad una:

```text
Item Version
```

oppure ad una:

```text
Item Variant
```

ma non ad entrambe contemporaneamente.

---

## Flusso Logico

```text
item_versions

↓

item_variants

↓

catalog_images
```

---

## Nota Importante

La tabella:

```text
catalog_images
```

utilizza una relazione esclusiva:

```text
item_version_id

oppure

item_variant_id
```

---

## Regola Architetturale

```text
item_version_id IS NOT NULL

XOR

item_variant_id IS NOT NULL
```

---

## Compatibilità Media Storage

Le immagini non sono memorizzate direttamente nella tabella.

La sorgente ufficiale del file è:

```text
media_files
```

tramite:

```text
media_file_id
```

---

## Esempio

```text
catalog_images

↓

media_file_id = 123

↓

Item Version
```

---

oppure

```text
catalog_images

↓

media_file_id = 456

↓

Item Variant
```

---

## Motivazione Architetturale

Questa struttura elimina duplicazioni e consente una gestione centralizzata delle immagini senza compromettere la flessibilità del Catalogo Universale.

--- 

# Livello 7 - Profili Utente e Collezioni

```text
user_collections
→ users

user_items
→ user_collections
→ items
→ item_versions
→ item_variants
→ currencies

wishlists
→ users

wishlist_items
→ wishlists
→ items
→ item_versions
→ item_variants
```

---

## Motivazione

Queste tabelle rappresentano la Catalogazione Personale.

---

## Flusso Logico

```text
users

↓

user_collections

↓

user_items
```

---

```text
users

↓

wishlists

↓

wishlist_items
```

---

# Livello 8 - Marketplace

```text
marketplace_listings
→ users
→ user_items
→ currencies

marketplace_offers
→ marketplace_listings
→ users
→ currencies

marketplace_offer_trade_items
→ marketplace_offers
→ user_items

marketplace_favorites
→ users
→ marketplace_listings

marketplace_reports
→ marketplace_listings
→ users

marketplace_listing_status_history
→ marketplace_listings
→ users
```

---

## Motivazione

Queste tabelle costituiscono il Marketplace della piattaforma.

---

## Flusso Logico

```text
marketplace_listings

↓

marketplace_offers

↓

marketplace_offer_trade_items
```

---

## Tabelle di Supporto

```text
marketplace_favorites

marketplace_reports

marketplace_listing_status_history
```

dipendono dagli Annunci Marketplace.

---

# Livello 9 - Matching

```text
matching_preferences
→ users

matching_opportunities
→ users
→ marketplace_listings
→ wishlist_items
→ user_items

matching_interactions
→ matching_opportunities
→ users
```

---

## Motivazione

Il Matching utilizza:

```text
Wishlist

Marketplace

Collezioni Personali
```

per generare opportunità.

---

## Flusso Logico

```text
matching_preferences

↓

matching_opportunities

↓

matching_interactions
```

---

# Livello 10 - Gamification

```text
user_scores
→ users

user_achievements
→ users
→ achievements

user_badges
→ users
→ badges

leaderboard_entries
→ leaderboards
→ users
```

---

## Motivazione

Il sistema Gamification ruota attorno agli utenti e ai cataloghi centrali:

```text
achievements

badges

leaderboards
```

---

## Flusso Logico

```text
users

↓

user_scores

↓

user_achievements

↓

user_badges

↓

leaderboard_entries
```

---

# Livello 11 - Notifiche

```text
notifications
→ users
```

---

## Motivazione

Le notifiche sono intenzionalmente indipendenti dalle altre tabelle operative.

---

## Nota

Le notifiche utilizzano:

```text
reference_type

reference_id
```

come collegamento logico alle altre entità della piattaforma.

---

## Vantaggio

Permette al sistema notifiche di restare flessibile e facilmente estendibile.


---

# Livello 12 - Messaggistica

```text
conversation_threads
→ users
→ marketplace_listings
→ matching_opportunities

conversation_participants
→ conversation_threads
→ users

messages
→ conversation_threads
→ users
→ messages

message_attachments
→ messages
→ media_files
```

---

## Motivazione

La Messaggistica si basa su una Conversazione che contiene Partecipanti e Messaggi.

---

## Flusso Logico

```text
conversation_threads

↓

conversation_participants

↓

messages

↓

message_attachments
```

---

## Nota Importante

La colonna:

```text
last_read_message_id
```

presente in:

```text
conversation_participants
```

deve essere trattata come Foreign Key aggiunta successivamente tramite:

```sql
ALTER TABLE
```

per evitare dipendenze circolari durante la creazione dello schema PostgreSQL.

---

# Livello 13 - Reputazione e Recensioni

```text
user_reviews
→ users
→ conversation_threads

merchant_verifications
→ users
```

---

## Motivazione

Le recensioni richiedono una effettiva interazione tra utenti.

La prova dell'interazione è:

```text
conversation_threads
```

---

## Regola Fondamentale

Non è possibile recensire un utente senza una Conversazione condivisa.

---

## Flusso Logico

```text
conversation_threads

↓

user_reviews
```

---

```text
users

↓

merchant_verifications
```

---

# Livello 14 - Media e Storage

```text
media_usages
→ media_files
```

---

## Motivazione

Tutti i file della piattaforma vengono centralizzati nella tabella:

```text
media_files
```

---

## File Gestiti

```text
Avatar

Catalog Images

Scanner Images

Merchant Documents

Contribution Attachments

Message Attachments

Badge Icons

Achievement Icons
```

---

## Flusso Logico

```text
media_files

↓

media_usages
```

---

## Nota Importante

La tabella:

```text
media_usages
```

utilizza relazioni polimorfiche.

Pertanto:

```text
entity_type

entity_id
```

non sono Foreign Key PostgreSQL.

Il collegamento viene gestito a livello applicativo.

---

## Esempio

```text
media_file

↓

avatar.jpg

↓

entity_type = user

↓

entity_id = UUID utente
```

---

```text
media_file

↓

charizard_front.jpg

↓

entity_type = item_variant

↓

entity_id = UUID variante
```

---

## Motivazione Architetturale

La separazione tra:

```text
media_files
```

e

```text
media_usages
```

consente:

- riutilizzo dei file
- eliminazione dei file orfani
- moderazione centralizzata
- storage scalabile
- supporto a qualsiasi futura entità della piattaforma

senza duplicare dati.

---

# Livello 15 - Analytics e Telemetria

```text
analytics_events
→ users

analytics_daily_metrics
```

---

## Motivazione

analytics_daily_metrics è una tabella aggregata.

Non necessita di Foreign Key operative.

---

## Flusso Logico

```text
analytics_events

↓

analytics_daily_metrics
```

---

## Nota

analytics_events utilizza:

```text
entity_type

entity_id
```

come riferimento facoltativo.

---

# Livello 16 - Internazionalizzazione

```text
translations
→ languages
```

---

## Motivazione

Le traduzioni dipendono dalla lingua.

---

## Nota

translations utilizza:

```text
entity_type

entity_id
```

per identificare il record tradotto.

---

## Flusso Logico

```text
languages

↓

translations
```

---

# Livello 17 - Storico e Versionamento

```text
entity_versions
→ users

data_restore_requests
→ users

system_snapshots
→ users
```

---

## Motivazione

Queste tabelle sono pensate per:

- storico
- audit
- recupero dati
- backup

---

## Flusso Logico

```text
users

├── entity_versions

├── data_restore_requests

└── system_snapshots
```

---

## Nota

Le tre tabelle sono indipendenti tra loro.

Condividono esclusivamente il riferimento agli utenti.

Non esistono Foreign Key dirette tra:

```text
entity_versions

data_restore_requests

system_snapshots
```

---

## Versionamento

La tabella:

```text
entity_versions
```

viene utilizzata per conservare le versioni storiche delle entità supportate.

Identificazione tramite:

```text
entity_type

entity_id
```

---

## Ripristino

La tabella:

```text
data_restore_requests
```

gestisce le richieste amministrative di recupero dati.

---

## Backup

La tabella:

```text
system_snapshots
```

contiene esclusivamente i metadati degli snapshot e dei backup disponibili.

---

## Motivazione Architetturale

La separazione tra:

```text
entity_versions

data_restore_requests

system_snapshots
```

consente di mantenere indipendenti:

- storico modifiche
- richieste di recupero
- gestione backup

senza introdurre dipendenze inutili nel database.

---

# Ordine Definitivo di Creazione Tabelle PostgreSQL

## Obiettivo

Questa sezione definisce l'ordine ufficiale di creazione delle tabelle del database CollectorVerse.

L'ordine è determinato dalle dipendenze delle Foreign Key.

Seguire questo ordine consente di:

- evitare errori PostgreSQL
- generare il DDL corretto
- preparare Supabase
- preparare Prisma
- preparare future migrazioni

---

# Gruppo 1 - Tabelle Fondamentali

```text
01 users

02 currencies

03 languages

04 categories

05 rarities

06 feature_flags

07 system_settings

08 achievements

09 badges

10 leaderboards
```

---

## Motivazione

Queste tabelle non dipendono da altre tabelle del sistema.

Costituiscono le fondamenta del database.

---

# Gruppo 2 - Infrastruttura Base

```text
11 media_files

12 collections

13 privacy_settings
```

---

## Motivazione

Queste tabelle dipendono solamente dalle fondamenta create nel Gruppo 1.

---

## Nota

La tabella:

```text
media_files
```

viene creata nei livelli iniziali perché molte altre tabelle dipendono direttamente da essa.

---

## Esempi

```text
catalog_images

message_attachments

media_usages
```

---

# Gruppo 3 - Catalogo Universale

```text
14 series

15 items

16 item_versions

17 item_variants

18 catalog_images
```

---

## Motivazione

Questo gruppo costruisce l'intera gerarchia del Catalogo Universale.

---

## Ordine

```text
categories

↓

collections

↓

series

↓

items

↓

item_versions

↓

item_variants

↓

catalog_images
```

---

## Nota Architetturale

La tabella:

```text
catalog_images
```

può appartenere ad una:

```text
Item Version
```

oppure ad una:

```text
Item Variant
```

ma mai ad entrambe contemporaneamente.

Le immagini non vengono ereditate automaticamente.

Una Variante può possedere immagini dedicate differenti rispetto alla propria Versione.

---

# Gruppo 4 - Ricerche Salvate

```text
19 saved_searches
```

---

## Motivazione

Le ricerche salvate dipendono dal Catalogo Universale completo.

Per questo motivo vengono create dopo:

```text
series

items

item_versions

item_variants
```

---

## Dipendenze

```text
saved_searches
→ users
→ categories
→ collections
→ series
→ items
→ item_versions
→ item_variants
→ currencies
```

---

## Nota

Tutte le Foreign Key di filtro sono opzionali.

Una ricerca salvata può utilizzare:

```text
nessun filtro

alcuni filtri

tutti i filtri
```

a seconda delle preferenze dell'utente.

---

# Gruppo 5 - Catalogazione Personale

```text
20 user_collections

21 user_items

22 wishlists

23 wishlist_items
```

---

## Motivazione

Queste tabelle consentono agli utenti di gestire la propria collezione e le wishlist.

---

## Motivazione

Questo gruppo implementa l'intero Marketplace.

Le dipendenze sono:

```text
marketplace_listings
```

↓

```text
marketplace_offers
```

↓

```text
marketplace_offer_trade_items
```

---

## Ordine Logico

```text
Annuncio

↓

Offerta

↓

Oggetti proposti nello scambio
```

---

## Tabelle di Supporto

```text
marketplace_favorites

marketplace_reports

marketplace_listing_status_history
```

dipendono dagli annunci marketplace e possono essere create successivamente.

---

# Gruppo 6 - Matching

```text
30 matching_preferences

31 matching_opportunities

32 matching_interactions
```

---

## Motivazione

Il sistema di Matching utilizza:

```text
Wishlist

Marketplace

Oggetti posseduti
```

per generare opportunità.

---

## Ordine Logico

```text
matching_preferences

↓

matching_opportunities

↓

matching_interactions
```

---

## Descrizione

### matching_preferences

Preferenze dell'utente.

---

### matching_opportunities

Match generati dal sistema.

---

### matching_interactions

Risposte e interazioni degli utenti sui match.

---

# Gruppo 7 - Catalogo Collaborativo

```text
33 catalog_contributions

34 catalog_contribution_attachments

35 catalog_contribution_votes
```

---

## Motivazione

Questo gruppo implementa il sistema di miglioramento collaborativo del Catalogo Universale.

---

## Ordine Logico

```text
catalog_contributions

↓

catalog_contribution_attachments

↓

catalog_contribution_votes
```

---

## Descrizione

### catalog_contributions

Proposta di modifica.

---

### catalog_contribution_attachments

Documentazione allegata.

---

### catalog_contribution_votes

Votazioni della community.

---

# Gruppo 8 - Scanner

```text
36 scan_sessions

37 scan_results
```

---

## Motivazione

Questo gruppo gestisce il riconoscimento automatico degli oggetti.

---

## Ordine Logico

```text
scan_sessions

↓

scan_results
```

---

## Descrizione

### scan_sessions

Tentativo di scansione.

---

### scan_results

Possibili risultati individuati.

---

# Gruppo 9 - Gamification

```text
38 user_scores

39 user_achievements

40 user_badges

41 leaderboard_entries
```

---

## Motivazione

Questo gruppo gestisce:

- punteggi
- livelli
- achievement
- badge
- classifiche

della piattaforma.

---

## Ordine Logico

```text
user_scores

↓

user_achievements

↓

user_badges

↓

leaderboard_entries
```

---

## Descrizione

### user_scores

Contiene il profilo di progressione dell'utente.

---

### user_achievements

Collega gli utenti agli Achievement ottenuti.

---

### user_badges

Collega gli utenti ai Badge ottenuti.

---

### leaderboard_entries

Contiene le posizioni degli utenti nelle classifiche.

---

## Dipendenze

```text
user_scores
→ users

user_achievements
→ users
→ achievements

user_badges
→ users
→ badges

leaderboard_entries
→ users
→ leaderboards
```

---

# Gruppo 10 - Notifiche

```text
42 notifications
```

---

## Motivazione

Questa tabella gestisce tutte le notifiche della piattaforma.

---

## Descrizione

La tabella può contenere notifiche generate da:

```text
Marketplace

Matching

Scanner

Messaggistica

Gamification

Catalogo Collaborativo

Sistema
```

---

## Dipendenze

```text
notifications
→ users
```

---

## Nota

Le notifiche utilizzano:

```text
reference_type

reference_id
```

per collegarsi logicamente ad altre entità.

Non esistono Foreign Key dirette verso le altre tabelle.

---

# Gruppo 11 - Messaggistica

```text
43 conversation_threads

44 conversation_participants

45 messages

46 message_attachments
```

---

## Motivazione

Questo gruppo implementa il sistema di comunicazione tra utenti.

---

## Ordine Logico

```text
conversation_threads

↓

conversation_participants

↓

messages

↓

message_attachments
```

---

## Descrizione

### conversation_threads

Contenitore della conversazione.

---

### conversation_participants

Partecipanti autorizzati.

---

### messages

Messaggi inviati nella conversazione.

---

### message_attachments

Allegati associati ai messaggi.

---

## Dipendenze

```text
conversation_threads
→ users
→ marketplace_listings
→ matching_opportunities

conversation_participants
→ conversation_threads
→ users

messages
→ conversation_threads
→ users

message_attachments
→ messages
→ media_files
```

---

## Nota Importante

La Foreign Key:

```text
last_read_message_id
```

presente in:

```text
conversation_participants
```

deve essere creata successivamente tramite:

```sql
ALTER TABLE
```

per evitare dipendenze circolari.

---

# Gruppo 12 - Reputazione e Recensioni

```text
47 user_reviews

48 merchant_verifications
```

---

## Motivazione

Questo gruppo gestisce:

- reputazione utenti
- recensioni
- verifiche commercianti

---

## Ordine Logico

```text
user_reviews

↓

merchant_verifications
```

---

## Descrizione

### user_reviews

Recensioni tra utenti.

---

### merchant_verifications

Verifica ufficiale delle attività commerciali.

---

## Dipendenze

```text
user_reviews
→ users
→ conversation_threads

merchant_verifications
→ users
```

---

## Regola Fondamentale

Una recensione può essere creata soltanto se esiste almeno una Conversazione condivisa tra i due utenti.

---

## Regola Anti-Duplicato

Per ogni coppia:

```text
reviewer_user_id

+

reviewed_user_id
```

può esistere una sola recensione.

Eventuali nuove recensioni aggiornano il record esistente.

---

# Gruppo 13 - Moderazione e Sicurezza

```text
49 user_blocks

50 moderation_cases

51 moderation_case_entities

52 audit_logs
```

---

## Motivazione

Questo gruppo gestisce:

- sicurezza utenti
- blocchi utenti
- moderazione contenuti
- audit amministrativo
- tracciabilità operazioni

---

## Ordine Logico

```text
user_blocks

↓

moderation_cases

↓

moderation_case_entities

↓

audit_logs
```

---

## Descrizione

### user_blocks

Blocco di un utente da parte di un altro utente.

---

### moderation_cases

Caso di moderazione aperto.

---

### moderation_case_entities

Entità coinvolte nel caso.

---

### audit_logs

Storico delle azioni eseguite.

---

## Dipendenze

```text
user_blocks
→ users

moderation_cases
→ users

moderation_case_entities
→ moderation_cases

audit_logs
→ users
```

---

# Gruppo 14 - Media e Storage

```text
53 media_usages
```

---

## Motivazione

Questo gruppo collega i file archiviati alle entità della piattaforma.

I file sono già gestiti da:

```text
media_files
```

creata nel Gruppo 2.

---

## Ordine Logico

```text
media_files

↓

media_usages
```

---

## Dipendenze

```text
media_usages
→ media_files
```

---

## Nota Importante

La tabella:

```text
media_usages
```

utilizza:

```text
entity_type

entity_id
```

come relazione polimorfica.

Tali campi non sono Foreign Key PostgreSQL.

Il collegamento è gestito dall'applicazione.

---

# Gruppo 15 - Analytics e Telemetria

```text
54 analytics_events

55 analytics_daily_metrics
```

---

## Motivazione

Questo gruppo consente di raccogliere:

- utilizzo piattaforma
- statistiche
- metriche
- business intelligence

---

## Ordine Logico

```text
analytics_events

↓

analytics_daily_metrics
```

---

## Descrizione

### analytics_events

Evento generato dal sistema.

---

### analytics_daily_metrics

Aggregazione giornaliera degli eventi.

---

## Dipendenze

```text
analytics_events
→ users

analytics_daily_metrics
```

---

## Nota

analytics_daily_metrics non richiede Foreign Key operative.

È una tabella aggregata.

---

# Gruppo 16 - Internazionalizzazione

```text
56 translations
```

---

## Motivazione

Questo gruppo consente il supporto multi-lingua dell'intera piattaforma.

---

## Ordine Logico

```text
languages

↓

translations
```

---

## Dipendenze

```text
translations
→ languages
```

---

## Nota Importante

La tabella:

```text
translations
```

utilizza:

```text
entity_type

entity_id
```

per individuare il record tradotto.

Questi campi non sono Foreign Key PostgreSQL.

---

# Gruppo 17 - Storico e Versionamento

```text
57 entity_versions

58 data_restore_requests

59 system_snapshots
```

---

## Motivazione

Questo gruppo gestisce:

- versionamento dati
- richieste di recupero
- storico modifiche
- backup logici

---

## Struttura Logica

```text
users

├── entity_versions

├── data_restore_requests

└── system_snapshots
```

---

## Descrizione

### entity_versions

Versioni storiche delle entità.

---

### data_restore_requests

Richieste di recupero dati.

---

### system_snapshots

Metadati dei backup e snapshot.

---

## Dipendenze

```text
entity_versions
→ users

data_restore_requests
→ users

system_snapshots
→ users
```

---

## Nota Importante

La tabella:

```text
entity_versions
```

utilizza:

```text
entity_type

entity_id
```

per identificare l'entità versionata.

Tali campi non sono Foreign Key PostgreSQL.

---

# Registro delle Relazioni Polimorfiche

## Obiettivo

Questa sezione documenta tutte le relazioni polimorfiche presenti nel database CollectorVerse.

Le relazioni polimorfiche utilizzano:

```text
entity_type
entity_id

oppure

reference_type
reference_id
```

al posto di una Foreign Key tradizionale.

---

## Attenzione

Le relazioni polimorfiche:

- non sono verificate da PostgreSQL
- non possiedono Foreign Key reali
- devono essere validate a livello applicativo

---

# Relazione polimorfica 1

# notifications

## Campi

```text
reference_type

reference_id
```

---

## Scopo

Permette ad una notifica di riferirsi a qualsiasi entità della piattaforma.

---

## Entità Supportate

```text
marketplace_listing

marketplace_offer

matching_opportunity

message

achievement

badge

scan_session

catalog_contribution

merchant_verification
```

---

## Esempio

```text
reference_type = achievement

reference_id = UUID Achievement
```

---

## Motivazione

Evita la necessità di decine di Foreign Key diverse nella tabella notifications.

---

# relazione polimorfica 2

# media_usages

## Campi

```text
entity_type

entity_id
```

---

## Scopo

Permette di collegare un file a qualsiasi entità della piattaforma.

---

## Entità Supportate

```text
user

catalog_image

catalog_contribution

merchant_verification

achievement

badge

scan_session

message
```

---

## Esempio

```text
entity_type = user

entity_id = UUID Utente
```

---

## Motivazione

Consente di riutilizzare lo stesso sistema storage per tutta la piattaforma.

---

# Relazione polimorfica 3

# translations

## Campi

```text
entity_type

entity_id
```

---

## Scopo

Permette di tradurre qualsiasi entità della piattaforma.

---

## Entità Supportate

```text
category

collection

series

item

item_version

item_variant

achievement

badge

system_setting
```

---

## Esempio

```text
entity_type = item

entity_id = UUID Item
```

---

## Motivazione

Permette un catalogo globale senza duplicare dati.

---

# Relazione polimorfica 4

# moderation_case_entities

## Campi

```text
entity_type

entity_id
```

---

## Scopo

Permette di collegare qualsiasi entità ad un caso di moderazione.

---

## Entità Supportate

```text
user

marketplace_listing

message

catalog_contribution

review

merchant_verification
```

---

## Esempio

```text
entity_type = message

entity_id = UUID Messaggio
```

---

## Motivazione

Consente alla Moderazione di funzionare su tutta la piattaforma senza modifiche strutturali.

---

#Relazione polimorfica 5

# analytics_events

## Campi

```text
entity_type

entity_id
```

---

## Scopo

Permette di associare un evento analitico ad una specifica entità.

---

## Entità Supportate

```text
item

marketplace_listing

match

message

scan_session

achievement
```

---

## Esempio

```text
entity_type = marketplace_listing

entity_id = UUID Listing
```

---

## Motivazione

Garantisce flessibilità nel sistema di Analytics.

---

# Relazione polimorfica 6

# entity_versions

## Campi

```text
entity_type

entity_id
```

---

## Scopo

Permette il versionamento di differenti entità utilizzando una sola tabella.

---

## Entità Supportate

```text
collection

series

item

item_version

item_variant

system_setting
```

---

## Esempio

```text
entity_type = item

entity_id = UUID Item
```

---

## Motivazione

Evita di creare una tabella di versionamento per ogni singola entità.

---

# Riepilogo Relazioni Polimorfiche

## Tabelle Coinvolte

```text
notifications

media_usages

translations

moderation_case_entities

analytics_events

entity_versions
```

---

## Regola Architetturale

Tutte le relazioni polimorfiche devono essere validate a livello applicativo.

PostgreSQL non garantisce l'integrità referenziale delle relazioni polimorfiche.

---

## Validazione Consigliata

Prima di salvare un record:

```text
Verificare entity_type

↓

Verificare esistenza entity_id

↓

Consentire salvataggio
```

---

# Registro delle Foreign Key Differite

## Obiettivo

Questa sezione documenta tutte le Foreign Key che non possono essere create durante la creazione iniziale delle tabelle.

Tali vincoli devono essere aggiunti successivamente tramite:

```sql
ALTER TABLE
```

---

## Motivazione

Le Foreign Key differite vengono utilizzate per evitare:

- dipendenze circolari
- errori di creazione tabelle
- problemi di bootstrap del database

---

# Foreign Key Differita 1

# conversation_participants.last_read_message_id

## Tabella

```text
conversation_participants
```

---

## Colonna

```text
last_read_message_id
```

---

## Tabella Destinazione

```text
messages.id
```

---

## Relazione

```text
conversation_participants

↓

last_read_message_id

↓

messages.id
```

---

## Perché è Differita

Durante la creazione iniziale:

```text
messages
```

dipende da:

```text
conversation_threads
```

---

e:

```text
conversation_participants
```

dipende da:

```text
conversation_threads
```

---

La presenza di:

```text
last_read_message_id
```

introduce una dipendenza aggiuntiva verso:

```text
messages
```

che è opportuno creare successivamente.

---

## Strategia

1. Creare conversation_participants senza la Foreign Key.

2. Creare messages.

3. Aggiungere la Foreign Key tramite:

```sql
ALTER TABLE
```

---

# verifica finale

# Riepilogo Foreign Key Differite

## Elenco

```text
conversation_participants.last_read_message_id
→ messages.id
```

---

## Numero Totale

```text
1 Foreign Key Differita
```

---

## Valutazione

L'architettura CollectorVerse presenta una sola Foreign Key differita.

Questo è un ottimo indicatore di qualità architetturale perché:

- riduce la complessità
- semplifica la creazione del database
- facilita le migrazioni
- migliora la manutenzione futura

---

# Convenzioni Globali PostgreSQL CollectorVerse

## Obiettivo

Questa sezione definisce gli standard architetturali e tecnici utilizzati da tutte le tabelle del database CollectorVerse.

Le convenzioni garantiscono:

- coerenza
- scalabilità
- manutenibilità
- compatibilità PostgreSQL
- compatibilità Supabase
- compatibilità ORM futuri

---

# Standard Identificativi

## Primary Key

Tutte le tabelle devono utilizzare:

```sql
UUID
```

come chiave primaria.

---

## Convenzione

Nome colonna:

```text
id
```

Tipo:

```sql
UUID PRIMARY KEY
```

---

## Motivazione

UUID offre:

- unicità globale
- migliore integrazione con Supabase
- sicurezza superiore agli ID incrementali
- supporto distribuito

---

## Esempio

```sql
id UUID PRIMARY KEY
```

---

# Standard Foreign Key

## Convenzione

Tutte le Foreign Key devono utilizzare il suffisso:

```text
_id
```

---

## Esempi

```text
user_id

item_id

collection_id

message_id

marketplace_listing_id
```

---

## Motivazione

Permette di identificare immediatamente una relazione.

---

# Standard Date e Orari

## Tipo Ufficiale

Tutte le date devono utilizzare:

```sql
TIMESTAMPTZ
```

---

## Motivazione

TIMESTAMPTZ:

- gestisce i fusi orari
- evita problemi internazionali
- è compatibile con Supabase
- è raccomandato da PostgreSQL

---

## Campi Standard

Ogni tabella principale deve possedere:

```text
created_at

updated_at
```

---

## Esempio

```sql
created_at TIMESTAMPTZ NOT NULL

updated_at TIMESTAMPTZ NOT NULL
```

---

# Standard Soft Delete

## Principio

I dati non devono essere eliminati fisicamente quando possibile.

---

## Campo Standard

```sql
deleted_at TIMESTAMPTZ NULL
```

---

## Regola

```text
NULL
=
Record attivo

Valorizzato
=
Record eliminato logicamente
```

---

## Tabelle Consigliate

```text
users

user_items

marketplace_listings

messages

catalog_contributions

user_reviews

media_files
```

---

## Tabelle Escluse

```text
achievements

badges

leaderboards

languages

feature_flags

system_settings
```

---

## Motivazione

Permette:

- recupero dati
- audit
- storico
- ripristini

---

# Standard Naming Convention

## Tabelle

Tutte le tabelle devono utilizzare:

```text
snake_case

plurale
```

---

## Colonne

Tutte le colonne devono utilizzare:

```text
snake_case
```

---

## Motivazione

Massima leggibilità e compatibilità PostgreSQL.

---

# Standard Indici

## Primary Key

Ogni tabella deve possedere:

```sql
PRIMARY KEY
```

---

## Foreign Key

Ogni Foreign Key deve possedere un indice dedicato.

---

## Campi Ricercati Frequentemente

Indicizzare quando presenti:

```text
status

created_at

updated_at

slug

code

email
```

---

## Motivazione

Riduzione dei tempi di esecuzione delle query.

---

# Standard UNIQUE

## Principio

I dati duplicati devono essere impediti a livello database.

---

## Esempi

```text
users.email

categories.slug

achievements.code

badges.code

leaderboards.code
```

---

## Relazioni Molti-a-Molti

Utilizzare UNIQUE composto.

---

## Esempio

```sql
UNIQUE (
user_id,
achievement_id
)
```

---

# Standard CHECK Constraint

## Principio

I valori invalidi non devono poter essere salvati.

---

## Esempi

### Rating

```sql
CHECK (rating BETWEEN 1 AND 5)
```

### Percentuali

```sql
CHECK (
completion_percentage >= 0
AND
completion_percentage <= 100
)
```

### Quantità

```sql
CHECK (
quantity >= 0
)
```

---

# Standard JSONB

## Consentito

```text
analytics_events

audit_logs

entity_versions

event metadata
```

---

## Vietato

Non utilizzare JSONB per dati relazionali che meritano colonne dedicate.

---

# Standard Relazioni Polimorfiche

## Campi Standard

```text
entity_type

entity_id
```

oppure:

```text
reference_type

reference_id
```

---

## Tabelle Autorizzate

```text
notifications

media_usages

translations

moderation_case_entities

analytics_events

entity_versions
```

---

## Regola

Le relazioni polimorfiche non utilizzano Foreign Key PostgreSQL.

La validazione viene effettuata a livello applicativo.

---

# Standard Audit

## Tabelle Interessate

```text
audit_logs

entity_versions
```

---

## Regola

I record di audit:

```text
non devono essere modificati

non devono essere eliminati
```

---

# Standard Row Level Security (RLS)

## Tabelle Soggette

```text
user_collections

user_items

wishlists

wishlist_items

notifications

conversation_threads

conversation_participants

messages

message_attachments

user_reviews

merchant_verifications

user_scores
```

---

## Regola Generale

Un utente può visualizzare esclusivamente i dati autorizzati secondo le policy applicative.

---

## Marketplace

I dati pubblici restano consultabili.

---

## Amministratori

Gli amministratori possono bypassare le policy RLS secondo i permessi assegnati.

---

# Standard UUID PostgreSQL

## Estensione Consigliata

```sql
pgcrypto
```

---

## Generazione UUID

```sql
gen_random_uuid()
```

---

## Esempio

```sql
id UUID PRIMARY KEY
DEFAULT gen_random_uuid()
```

---

## Motivazione

Compatibilità completa con PostgreSQL e Supabase.

---

# Conclusione

Queste convenzioni costituiscono lo standard ufficiale del database CollectorVerse.

Ogni nuova tabella dovrà rispettare integralmente queste regole salvo motivazione documentata e approvata.

Le convenzioni rappresentano il riferimento ufficiale per:

- progettazione
- sviluppo
- migrazioni
- manutenzione
- auditing
- integrazioni future

---

