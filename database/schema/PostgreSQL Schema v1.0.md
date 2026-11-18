# PostgreSQL Schema v1.0

# Stato Documento

Documento di progettazione dello schema PostgreSQL di CollectorVerse.

Questo documento traduce il CollectorVerse ERD v1.0 in una struttura dati implementabile mediante PostgreSQL e Supabase.

---

# Obiettivo

Definire:

- Tabelle
- Colonne
- Primary Key
- Foreign Key
- Vincoli
- Indici
- Relazioni

necessari per l'implementazione della piattaforma.

---

# Convenzioni

## Naming

Tutte le tabelle utilizzano:

- minuscolo
- snake_case
- nomi plurali

Esempi:

users
user_profiles
marketplace_listings
wishlist_items

---

## Chiavi Primarie

Tutte le tabelle utilizzano:

uuid

come Primary Key.

Formato:

id UUID PRIMARY KEY

---

## Timestamp Standard

Quando applicabile, tutte le tabelle utilizzano:

created_at
updated_at

---

## Soft Delete

Quando applicabile, le eliminazioni utilizzano:

deleted_at

invece della cancellazione fisica.

---

# Struttura dello Schema

1. Core Identity
2. Catalogo Universale
3. Catalogazione Personale
4. Marketplace
5. Matching
6. Catalogo Collaborativo
7. Scansioni
8. Gamification
9. Notifiche
10. Amministrazione
11. Importazione ed Esportazione

---

# Parte 1 - Core Identity

Questa sezione definisce le tabelle fondamentali della piattaforma.

Le tabelle di questa area rappresentano:

- utenti
- ruoli
- abbonamenti
- profili
- comunicazioni
- recensioni
- commercianti

---

# Tabella: user_roles

## Scopo

Definisce i ruoli disponibili all'interno della piattaforma.

La tabella permette l'estensione futura dei ruoli senza modifiche strutturali al database.

---

## Nome Tabella

user_roles

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco |
| code | VARCHAR(50) | SI | Codice interno ruolo |
| name | VARCHAR(100) | SI | Nome visualizzato |
| description | TEXT | NO | Descrizione del ruolo |
| is_active | BOOLEAN | SI | Ruolo attivo |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_active = TRUE

---

## Valori Iniziali

| Code | Name |
|--------|--------|
| user | Utente |
| moderator | Moderatore |
| admin | Amministratore |

---

## Relazioni

user_roles (1)
↓
(N)
users

---

## Vincoli

code deve essere univoco.

name deve essere univoco.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (is_active) 

---

# Tabella: users

## Scopo

Rappresenta tutti gli account registrati nella piattaforma CollectorVerse.

Ogni utente autenticato possiede una sola registrazione nella tabella users.

La tabella contiene esclusivamente le informazioni necessarie per:

- autenticazione
- autorizzazione
- gestione stato account
- collegamento alle altre aree della piattaforma

---

## Tipo Tabella

Principale

---

## Nome Tabella

users

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco dell'utente |
| email | VARCHAR(320) | SI | Email utilizzata per l'accesso |
| username | VARCHAR(50) | SI | Nome utente univoco |
| role_id | UUID | SI | Ruolo associato all'utente |
| account_status | VARCHAR(30) | SI | Stato account |
| is_email_verified | BOOLEAN | SI | Stato verifica email |
| created_at | TIMESTAMPTZ | SI | Data creazione account |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

account_status = active

is_email_verified = FALSE

---

## Valori Consentiti

### account_status

- active
- suspended
- blocked
- deleted

---

## Foreign Keys

role_id

→ user_roles.id

---

## Relazioni

user_roles (1)

↓

(N)

users

---

users (1)

↓

(1)

user_profiles

---

users (1)

↓

(1)

user_subscriptions

---

users (1)

↓

(1)

privacy_settings

---

users (1)

↓

(1)

notification_preferences

---

users (1)

↓

(1)

user_preferences

---

users (1)

↓

(0..1)

merchant_profiles

---

users (1)

↓

(N)

contact_requests

(mittente)

---

users (1)

↓

(N)

contact_requests

(destinatario)

---

users (1)

↓

(N)

user_reviews

(recensore)

---

users (1)

↓

(N)

user_reviews

(recensito)

---

users (1)

↓

(N)

user_blocks

(utente che blocca)

---

users (1)

↓

(N)

user_blocks

(utente bloccato)

---

users (1)

↓

(N)

messages

(mittente)

---

## Vincoli

email deve essere univoca.

username deve essere univoco.

role_id deve esistere nella tabella user_roles.

account_status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (email)

UNIQUE (username)

INDEX (role_id)

INDEX (account_status)

---

## Stati Account

### active

Account pienamente operativo.

Può utilizzare tutte le funzionalità consentite da:

- piano
- ruolo
- impostazioni privacy

---

### suspended

Account temporaneamente limitato.

L'accesso e le funzionalità disponibili dipendono dalle regole amministrative.

---

### blocked

Accesso negato.

L'utente non può utilizzare la piattaforma.

---

### deleted

Account eliminato logicamente.

I dati vengono gestiti secondo le policy GDPR e le regole di conservazione del Catalogo Universale.

---

## Note Architetturali

La tabella users rappresenta esclusivamente l'account dell'utente.

Le informazioni pubbliche vengono memorizzate nella tabella:

```text
user_profiles
```

Le informazioni relative alla gamification non vengono salvate nella tabella users.

I dati relativi a:

- CollectorScore
- Livelli
- Badge
- Cornici Profilo
- Streak

saranno gestiti dalle tabelle della sezione:

```text
Gamification
```

---

## Compatibilità Supabase

La tabella è progettata per integrarsi con:

```text
Supabase Auth
```

mediante sincronizzazione dell'identificativo utente.

L'ID dell'utente autenticato deve corrispondere all'ID registrato nella tabella users.

---

## Motivazione Architetturale

La tabella users rappresenta il nucleo identitario della piattaforma.

La separazione tra:

```text
users
```

e

```text
user_profiles
```

consente di isolare:

- dati di autenticazione
- dati pubblici
- sicurezza
- privacy

riducendo la complessità delle policy RLS e migliorando la sicurezza complessiva della piattaforma.

---

# Tabella: user_profiles

## Scopo

Rappresenta il profilo pubblico dell'utente.

La tabella contiene esclusivamente le informazioni pubbliche o semi-pubbliche visualizzabili dagli altri utenti in base alle impostazioni definite nella tabella:

```text
privacy_settings
```

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_profiles

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco del profilo |
| user_id | UUID | SI | Proprietario del profilo |
| display_name | VARCHAR(100) | SI | Nome pubblico visualizzato |
| avatar_url | TEXT | NO | Avatar del profilo |
| cover_image_url | TEXT | NO | Immagine di copertina |
| bio | TEXT | NO | Biografia utente |
| country_code | VARCHAR(10) | NO | Codice paese |
| region | VARCHAR(100) | NO | Regione |
| city | VARCHAR(100) | NO | Città |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultimo aggiornamento |

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(1)

user_profiles

---

users (1)

↓

(0..1)

merchant_profiles

---

## Vincoli

Ogni utente può possedere un solo profilo.

display_name deve essere univoco.

display_name non può essere vuoto.

user_id deve essere univoco.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

UNIQUE (display_name)

INDEX (country_code)

INDEX (region)

INDEX (city)

---

## Regole Business

Il profilo rappresenta l'identità pubblica dell'utente.

Le informazioni mostrate agli altri utenti dipendono dalle impostazioni registrate in:

```text
privacy_settings
```

---

## Informazioni Visualizzabili

Il profilo può mostrare:

- Avatar
- Cover
- Display Name
- Biografia
- Localizzazione
- Livello
- Badge
- CollectorScore
- Collezioni Pubbliche
- Wishlist Pubbliche
- Recensioni
- Statistiche Pubbliche

---

## Regola Privacy

La tabella:

```text
user_profiles
```

non gestisce direttamente la visibilità.

Tutta la logica di visibilità viene gestita esclusivamente tramite:

```text
privacy_settings
```

per evitare duplicazione dei dati e conflitti applicativi.

---

## Note Architetturali

display_name rappresenta l'identità pubblica dell'utente.

Per evitare omonimie all'interno della piattaforma:

```text
display_name deve essere univoco
```

---

La tabella contiene esclusivamente dati pubblici o semi-pubblici.

Non devono essere memorizzati:

- password
- email
- ruoli
- permessi
- stato account
- informazioni di autenticazione
- dati di abbonamento

---

Questi dati appartengono a:

```text
users
user_roles
user_subscriptions
```

---

## Compatibilità Marketplace

Il profilo pubblico può essere utilizzato per visualizzare:

- recensioni
- reputazione
- collezioni pubbliche
- attività pubblica marketplace

secondo le regole configurate nella privacy.

---

## Compatibilità Matching

Le informazioni pubbliche del profilo possono essere utilizzate per:

- suggerimenti utenti
- ricerca collezionisti
- scoperta commercianti
- ranking risultati

sempre nel rispetto delle impostazioni privacy.

---

## Compatibilità Gamification

Il profilo costituisce il punto di aggregazione visuale di:

- Livelli
- Badge
- Achievement
- CollectorScore
- Statistiche

che verranno memorizzati nelle tabelle dedicate della sezione Gamification.

---

## Motivazione Architetturale

La separazione tra:

```text
users
```

e

```text
user_profiles
```

consente:

- maggiore sicurezza
- migliore gestione privacy
- query più efficienti
- compatibilità con Supabase Auth
- compatibilità con RLS

ed evita l'esposizione accidentale di dati sensibili.

--- 

# Tabella: subscription_plans

## Scopo

Definisce i piani di abbonamento disponibili nella piattaforma CollectorVerse.

La tabella consente di gestire funzionalità, limiti e privilegi associati ai diversi livelli di abbonamento.

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

subscription_plans

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco del piano |
| code | VARCHAR(50) | SI | Codice interno piano |
| name | VARCHAR(100) | SI | Nome visualizzato |
| description | TEXT | NO | Descrizione del piano |
| is_active | BOOLEAN | SI | Piano disponibile |
| sort_order | INTEGER | SI | Ordine di visualizzazione |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_active = TRUE

sort_order = 0

---

## Valori Iniziali

| Code | Name |
|--------|--------|
| free | Free |
| premium | Premium |
| premium_plus | Premium Plus |
| merchant | Commerciante |

---

## Relazioni

subscription_plans (1)
↓
(N)
user_subscriptions

---

## Vincoli

code deve essere univoco.

name deve essere univoco.

sort_order deve essere maggiore o uguale a zero.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (is_active)

INDEX (sort_order)

---

## Note Architetturali

La tabella contiene esclusivamente la definizione dei piani.

Non contiene:

- utenti iscritti
- pagamenti
- date di rinnovo
- scadenze

Tali informazioni appartengono alla tabella user_subscriptions.

---

## Esempio Logico

subscription_plans

↓

Free
Premium
Premium Plus
Commerciante

↓

user_subscriptions

↓

users

---

# Tabella: user_subscriptions

## Scopo

Rappresenta l'abbonamento associato ad un utente.

La tabella collega gli account ai piani disponibili e consente di gestire attivazioni, rinnovi, cambi piano e scadenze.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_subscriptions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco della sottoscrizione |
| user_id | UUID | SI | Utente proprietario |
| subscription_plan_id | UUID | SI | Piano associato |
| status | VARCHAR(30) | SI | Stato della sottoscrizione |
| starts_at | TIMESTAMP | SI | Data inizio validità |
| expires_at | TIMESTAMP | NO | Data fine validità |
| auto_renew | BOOLEAN | SI | Rinnovo automatico |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |
| deleted_at | TIMESTAMP | NO | Soft Delete |

---

## Valori Predefiniti

auto_renew = FALSE

status = active

---

## Valori Consentiti

### status

- active
- expired
- cancelled
- suspended
- pending

---

## Foreign Keys

user_id
→ users.id

subscription_plan_id
→ subscription_plans.id

---

## Relazioni

users (1)
↓
(1)
user_subscriptions

---

subscription_plans (1)
↓
(N)
user_subscriptions

---

## Vincoli

Ogni utente può possedere una sola sottoscrizione corrente.

subscription_plan_id deve esistere nella tabella subscription_plans.

user_id deve esistere nella tabella users.

status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (subscription_plan_id)

INDEX (status)

INDEX (expires_at)

---

## Note Architetturali

La tabella rappresenta lo stato corrente dell'abbonamento.

Eventuali funzionalità future di storico abbonamenti potranno essere implementate tramite una tabella dedicata:

subscription_history

senza modificare la struttura principale.

---

# Tabella: privacy_settings

## Scopo

Definisce le impostazioni di privacy associate ad un utente.

La tabella controlla la visibilità di profilo, collezioni, wishlist e attività pubbliche all'interno della piattaforma.

---

## Tipo Tabella

Principale

---

## Nome Tabella

privacy_settings

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco delle impostazioni |
| user_id | UUID | SI | Proprietario delle impostazioni |
| profile_visibility | VARCHAR(20) | SI | Visibilità del profilo |
| collections_visibility | VARCHAR(20) | SI | Visibilità delle collezioni |
| wishlist_visibility | VARCHAR(20) | SI | Visibilità delle wishlist |
| inventory_visibility | VARCHAR(20) | SI | Visibilità degli oggetti posseduti |
| marketplace_visibility | VARCHAR(20) | SI | Visibilità attività marketplace |
| allow_contact_requests | BOOLEAN | SI | Consente richieste di contatto |
| allow_followers | BOOLEAN | SI | Consente follow utenti |
| show_location | BOOLEAN | SI | Mostra localizzazione pubblica |
| show_statistics | BOOLEAN | SI | Mostra statistiche pubbliche |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

profile_visibility = public

collections_visibility = public

wishlist_visibility = private

inventory_visibility = public

marketplace_visibility = public

allow_contact_requests = TRUE

allow_followers = TRUE

show_location = FALSE

show_statistics = TRUE

---

## Valori Consentiti

### profile_visibility

- public
- collectors_only
- private

---

### collections_visibility

- public
- collectors_only
- private

---

### wishlist_visibility

- public
- collectors_only
- private

---

### inventory_visibility

- public
- collectors_only
- private

---

### marketplace_visibility

- public
- collectors_only
- private

---

## Foreign Keys

user_id
→ users.id

---

## Relazioni

users (1)
↓
(1)
privacy_settings

---

privacy_settings
↓
Influenza

↓

user_profiles

user_collections

wishlists

user_items

marketplace_listings

---

## Vincoli

Ogni utente può possedere una sola configurazione privacy.

user_id deve essere univoco.

Tutti i campi di visibilità devono contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (profile_visibility)

INDEX (collections_visibility)

INDEX (wishlist_visibility)

---

## Note Architetturali

La tabella privacy_settings sarà utilizzata direttamente dalle Row Level Security (RLS) Policy di Supabase.

Le impostazioni registrate in questa tabella influenzeranno:

- accesso ai profili
- accesso alle collezioni
- accesso alle wishlist
- accesso agli oggetti posseduti
- accesso alle informazioni di marketplace

La progettazione è stata pensata per essere compatibile con Supabase RLS senza necessità di duplicare logiche nel frontend.

---

## Esempio Logico

Utente

↓

privacy_settings

↓

Profilo = Pubblico

Collezioni = Pubbliche

Wishlist = Private

↓

Controllo automatico accessi

---

# Tabella: notification_preferences

## Scopo

Definisce le preferenze di notifica associate ad un utente.

La tabella controlla quali notifiche possono essere ricevute e attraverso quali canali.

---

## Tipo Tabella

Principale

---

## Nome Tabella

notification_preferences

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco delle preferenze |
| user_id | UUID | SI | Proprietario delle preferenze |
| marketplace_enabled | BOOLEAN | SI | Notifiche Marketplace |
| matching_enabled | BOOLEAN | SI | Notifiche Matching |
| chat_enabled | BOOLEAN | SI | Notifiche Chat |
| reviews_enabled | BOOLEAN | SI | Notifiche Recensioni |
| gamification_enabled | BOOLEAN | SI | Notifiche Gamification |
| catalog_enabled | BOOLEAN | SI | Notifiche Catalogo |
| security_enabled | BOOLEAN | SI | Notifiche Sicurezza |
| push_enabled | BOOLEAN | SI | Canale Push attivo |
| email_enabled | BOOLEAN | SI | Canale Email attivo |
| in_app_enabled | BOOLEAN | SI | Canale In-App attivo |
| digest_enabled | BOOLEAN | SI | Ricezione Digest |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

marketplace_enabled = TRUE

matching_enabled = TRUE

chat_enabled = TRUE

reviews_enabled = TRUE

gamification_enabled = TRUE

catalog_enabled = TRUE

security_enabled = TRUE

push_enabled = TRUE

email_enabled = TRUE

in_app_enabled = TRUE

digest_enabled = FALSE

---

## Foreign Keys

user_id
→ users.id

---

## Relazioni

users (1)
↓
(1)
notification_preferences

---

notification_preferences
↓
Influenza

↓

notifications

notification_deliveries

notification_digests

---

## Vincoli

Ogni utente può possedere una sola configurazione notifiche.

user_id deve essere univoco.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (marketplace_enabled)

INDEX (matching_enabled)

INDEX (security_enabled)

---

## Note Architetturali

Le preferenze sono separate dal sistema di consegna notifiche.

La tabella definisce esclusivamente ciò che l'utente desidera ricevere.

Le notifiche effettivamente generate verranno memorizzate nelle tabelle:

- notifications
- notification_deliveries
- notification_digests

---

## Compatibilità Supabase

Questa tabella verrà utilizzata dalle funzioni applicative per:

- filtrare notifiche
- generare digest
- decidere il canale di consegna
- applicare preferenze utente

senza duplicare logica nel frontend.

---

## Esempio Logico

Utente

↓

notification_preferences

↓

Marketplace = Attivo

Matching = Attivo

Email = Disattivata

Push = Attiva

↓

Sistema Notifiche

---

# Tabella: merchant_profiles

## Scopo

Rappresenta il profilo commerciale di un utente.

La tabella contiene le informazioni pubbliche relative ad attività professionali, negozi fisici e negozi online associati agli utenti della piattaforma.

---

## Tipo Tabella

Principale

---

## Nome Tabella

merchant_profiles

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco del profilo commerciante |
| user_id | UUID | SI | Proprietario del profilo |
| business_name | VARCHAR(150) | SI | Nome attività |
| business_description | TEXT | NO | Descrizione attività |
| website_url | TEXT | NO | Sito web |
| email_public | VARCHAR(320) | NO | Email pubblica |
| phone_public | VARCHAR(50) | NO | Telefono pubblico |
| country_code | VARCHAR(10) | NO | Paese |
| region | VARCHAR(100) | NO | Regione |
| city | VARCHAR(100) | NO | Città |
| address_public | TEXT | NO | Indirizzo pubblico |
| is_active | BOOLEAN | SI | Profilo commerciante attivo |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_active = TRUE

---

## Foreign Keys

user_id
→ users.id

---

## Relazioni

users (1)
↓
(0..1)
merchant_profiles

---

merchant_profiles (1)
↓
(0..1)
merchant_verifications

---

merchant_profiles (1)
↓
(0..1)
google_business_profiles

---

merchant_profiles (1)
↓
(N)
marketplace_listings

---

merchant_profiles (1)
↓
(N)
follow_merchants

---

## Vincoli

Ogni utente può possedere al massimo un profilo commerciante.

user_id deve essere univoco.

business_name non può essere vuoto.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (business_name)

INDEX (is_active)

INDEX (country_code)

INDEX (region)

INDEX (city)

---

## Note Architetturali

Lo stato di verifica NON viene salvato in questa tabella.

La verifica ufficiale viene determinata esclusivamente tramite:

merchant_verifications

Questo evita duplicazioni e problemi di sincronizzazione.

---

# Tabella: merchant_verifications

## Scopo

Rappresenta la verifica ufficiale di un commerciante da parte di CollectorVerse.

La tabella memorizza lo stato di verifica e le informazioni amministrative associate al processo di validazione.

---

## Tipo Tabella

Principale

---

## Nome Tabella

merchant_verifications

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco verifica |
| merchant_profile_id | UUID | SI | Profilo commerciante verificato |
| verification_status | VARCHAR(30) | SI | Stato verifica |
| verified_at | TIMESTAMP | NO | Data verifica |
| verified_by_user_id | UUID | NO | Utente che ha eseguito la verifica |
| verification_notes | TEXT | NO | Note amministrative |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Consentiti

### verification_status

- pending
- approved
- rejected
- suspended

---

## Valori Predefiniti

verification_status = pending

---

## Foreign Keys

merchant_profile_id
→ merchant_profiles.id

verified_by_user_id
→ users.id

---

## Relazioni

merchant_profiles (1)
↓
(0..1)
merchant_verifications

---

users (1)
↓
(N)
merchant_verifications

(utente che ha eseguito la verifica)

---

## Vincoli

Ogni merchant_profile può avere una sola registrazione di verifica.

merchant_profile_id deve essere univoco.

verification_status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (merchant_profile_id)

INDEX (verification_status)

INDEX (verified_at)

INDEX (verified_by_user_id)

---

## Note Architetturali

La presenza di una registrazione approvata in questa tabella determina il badge:

Commerciante Verificato

visibile pubblicamente nella piattaforma.

La tabella consente future estensioni come:

- verifica documentale
- verifica partita IVA
- verifica identità

Eventuali modifiche dello stato di verifica verranno effettuate dagli amministratori tramite aggiornamento della registrazione esistente.

Non è previsto un sistema di rinnovo periodico della verifica.

Le autorizzazioni relative alla possibilità di eseguire verifiche verranno gestite tramite:

- ruoli applicativi
- policy RLS
- servizi backend

e non tramite vincoli del database relazionale.

---

## Compatibilità Marketplace

La verifica può influenzare:

- visibilità annunci
- ranking risultati
- Matching
- affidabilità percepita
- badge commerciante verificato

---

## Esempio Logico

users

↓

merchant_profiles

↓

merchant_verifications

↓

approved

↓

Commerciante Verificato

---

# Tabella: google_business_profiles

## Scopo

Rappresenta il profilo Google Business Profile associato ad un commerciante.

La tabella consente l'integrazione tra CollectorVerse e Google Business Profile per mostrare informazioni pubbliche e recensioni provenienti da Google.

---

## Tipo Tabella

Principale

---

## Nome Tabella

google_business_profiles

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco |
| merchant_profile_id | UUID | SI | Profilo commerciante associato |
| google_place_id | VARCHAR(255) | SI | Identificativo Google Place |
| business_name | VARCHAR(150) | SI | Nome attività su Google |
| business_url | TEXT | NO | URL Google Business |
| average_rating | NUMERIC(3,2) | NO | Valutazione media |
| review_count | INTEGER | NO | Numero recensioni |
| last_sync_at | TIMESTAMP | NO | Ultima sincronizzazione |
| is_active | BOOLEAN | SI | Collegamento attivo |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_active = TRUE

review_count = 0

---

## Foreign Keys

merchant_profile_id
→ merchant_profiles.id

---

## Relazioni

merchant_profiles (1)
↓
(0..1)
google_business_profiles

---

google_business_profiles (1)
↓
(N)
google_business_reviews

---

## Vincoli

Ogni merchant_profile può essere associato ad un solo Google Business Profile.

merchant_profile_id deve essere univoco.

google_place_id deve essere univoco.

business_name non può essere vuoto.

average_rating deve essere compreso tra 0 e 5.

review_count deve essere maggiore o uguale a zero.

---

## Indici

PRIMARY KEY (id)

UNIQUE (merchant_profile_id)

UNIQUE (google_place_id)

INDEX (average_rating)

INDEX (review_count)

INDEX (is_active)

---

## Note Architetturali

La tabella memorizza solamente i dati principali del profilo Google Business.

Le recensioni vengono gestite separatamente nella tabella:

google_business_reviews

Questo approccio evita duplicazioni e consente sincronizzazioni indipendenti.

---

## Compatibilità Marketplace

Le informazioni raccolte possono essere utilizzate per:

- mostrare reputazione commerciale
- aumentare la fiducia degli utenti
- migliorare il ranking dei commercianti verificati
- supportare il sistema Matching

---

## Esempio Logico

users

↓

merchant_profiles

↓

google_business_profiles

↓

Valutazione Media

Numero Recensioni

Link Google Business

---

# Tabella: google_business_reviews

## Scopo

Rappresenta una recensione proveniente da Google Business Profile.

La tabella consente di memorizzare e visualizzare informazioni pubbliche relative alle recensioni associate ad un commerciante.

---

## Tipo Tabella

Principale

---

## Nome Tabella

google_business_reviews

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco recensione |
| google_business_profile_id | UUID | SI | Profilo Google Business associato |
| google_review_id | VARCHAR(255) | SI | Identificativo recensione Google |
| author_name | VARCHAR(255) | NO | Nome autore recensione |
| rating | INTEGER | SI | Valutazione numerica |
| review_text | TEXT | NO | Contenuto recensione |
| review_date | TIMESTAMP | NO | Data recensione originale |
| is_visible | BOOLEAN | SI | Visibilità su CollectorVerse |
| last_sync_at | TIMESTAMP | NO | Ultima sincronizzazione |
| created_at | TIMESTAMP | SI | Data creazione record |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_visible = TRUE

---

## Valori Consentiti

### rating

- 1
- 2
- 3
- 4
- 5

---

## Foreign Keys

google_business_profile_id
→ google_business_profiles.id

---

## Relazioni

google_business_profiles (1)
↓
(N)
google_business_reviews

---

## Vincoli

google_review_id deve essere univoco.

rating deve essere compreso tra 1 e 5.

google_business_profile_id deve esistere nella tabella google_business_profiles.

---

## Indici

PRIMARY KEY (id)

UNIQUE (google_review_id)

INDEX (google_business_profile_id)

INDEX (rating)

INDEX (review_date)

INDEX (is_visible)

---

## Note Architetturali

La tabella contiene esclusivamente dati provenienti da Google Business Profile.

CollectorVerse non modifica il contenuto delle recensioni.

Le recensioni possono essere:

- sincronizzate
- aggiornate
- nascoste localmente

senza modificare il dato originale presente su Google.

---

## Compatibilità Marketplace

Le recensioni possono contribuire a:

- reputazione commerciante
- ranking marketplace
- risultati matching
- fiducia degli utenti

---

## Esempio Logico

merchant_profiles

↓

google_business_profiles

↓

google_business_reviews

↓

★★★★★

"Servizio eccellente"

↓

Profilo Pubblico Negozio

---

# Tabella: contact_requests

## Scopo

Rappresenta una richiesta di contatto tra due utenti.

La tabella viene utilizzata come passaggio preliminare all'apertura di una conversazione privata.

---

## Tipo Tabella

Principale

---

## Nome Tabella

contact_requests

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco richiesta |
| sender_user_id | UUID | SI | Utente mittente |
| receiver_user_id | UUID | SI | Utente destinatario |
| status | VARCHAR(30) | SI | Stato richiesta |
| message | TEXT | NO | Messaggio iniziale |
| responded_at | TIMESTAMP | NO | Data risposta |
| created_at | TIMESTAMP | SI | Data invio |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Consentiti

### status

- pending
- accepted
- rejected
- cancelled

---

## Valori Predefiniti

status = pending

---

## Foreign Keys

sender_user_id
→ users.id

receiver_user_id
→ users.id

---

## Relazioni

users (1)
↓
(N)
contact_requests

(mittente)

---

users (1)
↓
(N)
contact_requests

(destinatario)

---

contact_requests (1)
↓
(0..1)
conversations

---

## Vincoli

sender_user_id deve essere diverso da receiver_user_id.

Lo stato deve contenere un valore valido.

Entrambi gli utenti devono esistere nella tabella users.

Non possono esistere più richieste di contatto pendenti tra la stessa coppia di utenti.

Può esistere una sola conversazione attiva tra la stessa coppia di utenti.

Le modalità di riapertura o creazione di una nuova conversazione verranno definite nella logica applicativa.

---

## Indici

PRIMARY KEY (id)

INDEX (sender_user_id)

INDEX (receiver_user_id)

INDEX (status)

INDEX (created_at)

---

## Note Architetturali

La richiesta di contatto rappresenta il punto di ingresso delle comunicazioni private.

Una conversazione può essere aperta solo dopo l'accettazione della richiesta.

Le richieste rifiutate o annullate non generano conversazioni.

---

## Compatibilità Privacy

La creazione di una richiesta deve rispettare:

- privacy_settings
- user_blocks
- eventuali limitazioni amministrative

Le policy verranno implementate tramite Supabase RLS e logica applicativa.

---

## Esempio Logico

Utente A

↓

contact_requests

↓

pending

↓

accepted

↓

conversation

↓

messages

---

# Tabella: conversations

## Scopo

Rappresenta una conversazione privata tra utenti della piattaforma.

La tabella funge da contenitore per i messaggi scambiati tra utenti.

---

## Tipo Tabella

Principale

---

## Nome Tabella

conversations

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco conversazione |
| contact_request_id | UUID | SI | Richiesta contatto che ha generato la conversazione |
| created_at | TIMESTAMP | SI | Data creazione conversazione |
| updated_at | TIMESTAMP | SI | Data ultimo aggiornamento |
| closed_at | TIMESTAMP | NO | Data chiusura conversazione |

---

## Foreign Keys

contact_request_id
→ contact_requests.id

---

## Relazioni

contact_requests (1)
↓
(0..1)
conversations

---

conversations (1)
↓
(N)
messages

---

## Vincoli

contact_request_id deve esistere nella tabella contact_requests.

Ogni richiesta accettata può generare una sola conversazione.

contact_request_id deve essere univoco.

---

## Indici

PRIMARY KEY (id)

UNIQUE (contact_request_id)

INDEX (created_at)

INDEX (updated_at)

INDEX (closed_at)

---

## Note Architetturali

La conversazione non memorizza direttamente i partecipanti.

I partecipanti vengono determinati attraverso:

contact_requests

↓

sender_user_id

receiver_user_id

Questo approccio evita la duplicazione dei dati.

---

## Compatibilità Marketplace

La stessa conversazione può essere utilizzata per:

- compravendita
- scambio
- contatti tra collezionisti
- contatti con commercianti

senza richiedere strutture diverse.

---

## Esempio Logico

Utente A

↓

contact_request

↓

accepted

↓

conversation

↓

messages

---

# Tabella: messages

## Scopo

Rappresenta un singolo messaggio inviato all'interno di una conversazione.

La tabella costituisce l'unità minima del sistema di comunicazione tra utenti.

---

## Tipo Tabella

Principale

---

## Nome Tabella

messages

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco messaggio |
| conversation_id | UUID | SI | Conversazione associata |
| sender_user_id | UUID | SI | Utente mittente |
| message_type | VARCHAR(20) | SI | Tipo messaggio |
| content | TEXT | SI | Contenuto messaggio |
| is_read | BOOLEAN | SI | Stato lettura |
| read_at | TIMESTAMP | NO | Data lettura |
| created_at | TIMESTAMP | SI | Data invio |
| updated_at | TIMESTAMP | SI | Data modifica |
| deleted_at | TIMESTAMP | NO | Soft Delete |

---

## Valori Consentiti

### message_type

- text
- system
- marketplace
- trade

---

## Valori Predefiniti

message_type = text

is_read = FALSE

---

## Foreign Keys

conversation_id
→ conversations.id

sender_user_id
→ users.id

---

## Relazioni

conversations (1)
↓
(N)
messages

---

users (1)
↓
(N)
messages

---

## Vincoli

conversation_id deve esistere nella tabella conversations.

sender_user_id deve esistere nella tabella users.

content non può essere vuoto.

message_type deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (conversation_id)

INDEX (sender_user_id)

INDEX (created_at)

INDEX (is_read)

---

## Note Architetturali

La tabella memorizza esclusivamente i messaggi.

Le informazioni sui partecipanti alla conversazione vengono recuperate tramite:

conversations

↓

contact_requests

↓

users

Lo stato di lettura è riferito al destinatario del messaggio identificato attraverso i partecipanti della conversazione.

Essendo supportata una sola conversazione privata tra due utenti, non è necessario gestire uno stato di lettura per più destinatari.

I messaggi rimangono disponibili anche dopo la lettura.

La cancellazione utilizza il meccanismo di Soft Delete tramite:

deleted_at

per preservare la cronologia delle conversazioni.

---

## Estensioni Future

Versioni successive potranno introdurre:

- allegati
- immagini
- documenti
- messaggi di sistema avanzati
- notifiche contestuali

senza modificare la struttura principale delle conversazioni.

---

## Compatibilità Marketplace

I messaggi possono essere utilizzati per:

- compravendita
- scambio
- richieste informazioni
- contatti tra collezionisti
- contatti con commercianti

---

## Esempio Logico

contact_request

↓

accepted

↓

conversation

↓

message

↓

message

↓

message

---

# Tabella: user_blocks

## Scopo

Rappresenta il blocco di un utente da parte di un altro utente.

La tabella consente di limitare o impedire interazioni tra utenti secondo le regole di privacy e sicurezza della piattaforma.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_blocks

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco blocco |
| blocker_user_id | UUID | SI | Utente che esegue il blocco |
| blocked_user_id | UUID | SI | Utente bloccato |
| reason | VARCHAR(100) | NO | Motivazione facoltativa |
| created_at | TIMESTAMP | SI | Data blocco |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Foreign Keys

blocker_user_id
→ users.id

blocked_user_id
→ users.id

---

## Relazioni

users (1)
↓
(N)
user_blocks

(utente che blocca)

---

users (1)
↓
(N)
user_blocks

(utente bloccato)

---

## Vincoli

blocker_user_id deve essere diverso da blocked_user_id.

Entrambi gli utenti devono esistere nella tabella users.

Una coppia utente-bloccato può esistere una sola volta.

---

## Indici

PRIMARY KEY (id)

UNIQUE (blocker_user_id, blocked_user_id)

INDEX (blocker_user_id)

INDEX (blocked_user_id)

INDEX (created_at)

---

## Note Architetturali

Il blocco è unidirezionale.

Esempio:

Utente A blocca Utente B

↓

Utente B non può interagire con Utente A.

Il blocco non implica automaticamente che anche Utente B abbia bloccato Utente A.

---

## Impatti Funzionali

La presenza di un record nella tabella user_blocks può impedire:

- invio richieste di contatto
- apertura conversazioni
- invio messaggi
- follow utenti
- visualizzazione profili
- matching automatico
- notifiche tra utenti coinvolti

Le regole definitive verranno implementate tramite:

- logica applicativa
- Supabase RLS
- servizi backend

---

## Esempio Logico

Utente A

↓

user_blocks

↓

Utente B

↓

Interazioni Bloccate

---

# Tabella: user_reviews

## Scopo

Rappresenta una recensione lasciata da un utente nei confronti di un altro utente.

La tabella viene utilizzata per costruire il sistema reputazionale della piattaforma.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_reviews

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco recensione |
| reviewer_user_id | UUID | SI | Utente autore recensione |
| reviewed_user_id | UUID | SI | Utente recensito |
| rating | INTEGER | SI | Valutazione numerica |
| title | VARCHAR(150) | NO | Titolo recensione |
| review_text | TEXT | NO | Testo recensione |
| is_visible | BOOLEAN | SI | Visibilità recensione |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |
| deleted_at | TIMESTAMP | NO | Soft Delete |

---

## Valori Consentiti

### rating

- 1
- 2
- 3
- 4
- 5

---

## Valori Predefiniti

is_visible = TRUE

---

## Foreign Keys

reviewer_user_id
→ users.id

reviewed_user_id
→ users.id

---

## Relazioni

users (1)
↓
(N)
user_reviews

(recensore)

---

users (1)
↓
(N)
user_reviews

(recensito)

---

## Vincoli

reviewer_user_id deve essere diverso da reviewed_user_id.

rating deve essere compreso tra 1 e 5.

reviewer_user_id deve esistere nella tabella users.

reviewed_user_id deve esistere nella tabella users.

Può esistere una sola recensione tra la stessa coppia recensore-recensito.

---

## Indici

PRIMARY KEY (id)

UNIQUE (reviewer_user_id, reviewed_user_id)

INDEX (rating)

INDEX (created_at)

INDEX (is_visible)

---

## Note Architetturali

Ogni utente può lasciare una sola recensione per un altro utente.

Quando una recensione viene modificata:

- viene aggiornata la riga esistente
- viene aggiornato updated_at

Non viene creata una nuova recensione.

La recensione rappresenta una valutazione puntuale.

I valori aggregati come:

- media recensioni
- numero recensioni
- indice affidabilità

non vengono salvati in questa tabella.

Tali valori verranno calcolati da:

- query aggregate
- viste PostgreSQL
- statistiche dedicate

---

## Compatibilità Marketplace

Le recensioni possono essere lasciate dopo:

- compravendita completata
- scambio completato
- interazione verificata tra utenti

Le regole definitive verranno implementate tramite logica applicativa.

---

## Compatibilità Matching

I risultati del Matching potranno utilizzare:

- media recensioni
- numero recensioni
- reputazione utente

per migliorare il ranking delle opportunità.

---

# Tabella: currencies

## Scopo

Definisce le valute supportate dalla piattaforma CollectorVerse.

La tabella viene utilizzata per:

- Marketplace
- Annunci
- Profili Utente
- Preferenze Utente
- Esportazioni
- Future funzionalità commerciali

CollectorVerse non effettua conversioni automatiche tra valute.

La valuta viene utilizzata esclusivamente come riferimento di visualizzazione e registrazione dei prezzi.

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

currencies

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco |
| code | VARCHAR(10) | SI | Codice ISO valuta |
| symbol | VARCHAR(10) | SI | Simbolo valuta |
| name | VARCHAR(100) | SI | Nome valuta |
| is_active | BOOLEAN | SI | Valuta disponibile |
| sort_order | INTEGER | SI | Ordine visualizzazione |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Valori Predefiniti

is_active = TRUE

sort_order = 0

---

## Valori Iniziali

| Code | Symbol | Name |
|--------|--------|--------|
| EUR | € | Euro |
| USD | $ | US Dollar |
| GBP | £ | British Pound |
| JPY | ¥ | Japanese Yen |
| CHF | CHF | Swiss Franc |

---

## Relazioni

currencies (1)
↓
(N)
user_preferences

---

currencies (1)
↓
(N)
marketplace_listings

---

## Vincoli

code deve essere univoco.

symbol non può essere vuoto.

name deve essere univoco.

sort_order deve essere maggiore o uguale a zero.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (is_active)

INDEX (sort_order)

---

## Note Architetturali

La tabella currencies rappresenta il catalogo ufficiale delle valute supportate.

La disattivazione di una valuta:

- impedisce nuove selezioni
- non modifica dati storici
- non altera gli annunci già pubblicati

---

## Compatibilità Marketplace

I prezzi devono sempre essere registrati:

Prezzo Originale

+

Valuta Originale

Esempi:

120 EUR

45 USD

10.000 JPY

---

## Esempio Logico

currencies

↓

EUR
USD
GBP
JPY
CHF

↓

Marketplace

↓

Annunci

# Tabella: user_preferences

## Scopo

Memorizza le preferenze personali dell'utente.

Attualmente viene utilizzata principalmente per la gestione della valuta preferita.

La struttura è progettata per supportare future estensioni senza modifiche invasive.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_preferences

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco |
| user_id | UUID | SI | Proprietario preferenze |
| preferred_currency_id | UUID | SI | Valuta preferita |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |

---

## Foreign Keys

user_id
→ users.id

preferred_currency_id
→ currencies.id

---

## Relazioni

users (1)
↓
(1)
user_preferences

---

currencies (1)
↓
(N)
user_preferences

---

## Vincoli

Ogni utente può avere una sola configurazione preferenze.

user_id deve essere univoco.

preferred_currency_id deve esistere nella tabella currencies.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (preferred_currency_id)

---

## Note Architetturali

La valuta preferita viene utilizzata come valore predefinito durante:

- creazione annunci
- pubblicazione vendite
- pubblicazione scambi con prezzo
- funzionalità marketplace

La modifica della valuta preferita:

- non altera gli annunci esistenti
- non modifica prezzi storici
- non converte importi esistenti

---

## Compatibilità Blueprint

Coerente con:

- Parte 2 (Valuta Preferita)
- Parte 3 (Marketplace)
- Parte 9 (Profilo Utente)

---

## Esempio Logico

users

↓

user_preferences

↓

EUR

↓

Nuovo Annuncio

↓

Valuta Preselezionata = EUR

# Parte 2 - Catalogo Universale

# Tabella: categories

## Scopo

Rappresenta il livello più alto della classificazione del Catalogo Universale.

Ogni Collezione appartiene obbligatoriamente ad una Categoria.

La Categoria costituisce il punto di ingresso del sistema di navigazione del catalogo.

---

## Tipo Tabella

Principale

---

## Nome Tabella

categories

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco categoria |
| name | VARCHAR(150) | SI | Nome categoria |
| slug | VARCHAR(200) | SI | URL friendly identifier |
| description | TEXT | NO | Descrizione categoria |
| logo_url | TEXT | NO | URL logo categoria |
| banner_url | TEXT | NO | URL banner categoria |
| status | VARCHAR(30) | SI | Stato categoria |
| sort_order | INTEGER | SI | Ordine visualizzazione |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data ultima modifica |
| deleted_at | TIMESTAMP | NO | Soft Delete |

---

## Valori Predefiniti

sort_order = 0

status = development

---

## Valori Consentiti

### status

```text
development
active
hidden
archived
```

---

## Significato Stati

### development

Categoria in preparazione.

Visibile esclusivamente agli amministratori.

---

### active

Categoria disponibile pubblicamente.

Utilizzabile in:

- Catalogo
- Scanner
- Marketplace
- Matching
- Wishlist
- Collezioni Personali
- Importazione

---

### hidden

Categoria temporaneamente nascosta.

Non disponibile agli utenti.

I dati restano conservati.

---

### archived

Categoria archiviata.

Non più utilizzabile.

Conservata esclusivamente per finalità storiche.

---

## Relazioni

categories (1)

↓

(N)

collections

---

## Vincoli

name deve essere univoco.

slug deve essere univoco.

sort_order deve essere maggiore o uguale a zero.

status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (name)

UNIQUE (slug)

INDEX (status)

INDEX (sort_order)

---

## Valori Iniziali Previsti

| Nome |
|--------|
| Carte Collezionabili |
| Numismatica |
| Filatelia |
| Fumetti e Libri |
| LEGO e Costruzioni |
| Action Figure e Toys |
| Videogiochi |
| Musica e Media |
| Orologi e Gioielli |
| Militaria e Storico |
| Modellismo |
| Antiquariato e Arte |
| Enologia e Spirits |

---

## Regole Business

Una Collezione deve appartenere ad una sola Categoria.

Una Categoria può possedere molte Collezioni.

L'eliminazione fisica di una Categoria non è consentita.

La gestione deve avvenire tramite:

```text
hidden

oppure

archived
```

---

## Compatibilità Scanner

Lo Scanner deve mostrare esclusivamente le categorie:

```text
active
```

---

## Compatibilità Marketplace

Gli annunci appartenenti ad una categoria:

```text
hidden
```

oppure

```text
archived
```

devono essere esclusi dai risultati pubblici.

---

## Compatibilità Matching

Il Matching deve ignorare categorie:

```text
hidden

archived
```

---

## Compatibilità Dashboard Admin

Gli Amministratori devono poter:

```text
Creare

Modificare

Attivare

Nascondere

Archiviare

Riordinare
```

una Categoria senza modificare il codice applicativo.

---

## Esempio Logico

Categorie

↓

Carte Collezionabili

↓

Pokémon

↓

Set Base

↓

Charizard

---

Categorie

↓

Numismatica

↓

Euro Italia

↓

2 Euro Commemorativi

↓

Moneta Specifica

---

## Motivazione Architetturale

Le Categorie sono state separate dalle Collezioni per consentire:

- navigazione semplificata
- crescita progressiva del catalogo
- attivazione graduale delle categorie
- statistiche separate
- gestione indipendente tramite Dashboard Admin

senza modifiche strutturali future del database.

---

# Tabella: collections

## Scopo

Rappresenta una Collezione appartenente ad una specifica Categoria.

Una Collezione raggruppa Serie appartenenti allo stesso ecosistema collezionistico.

Esempi:

- Pokémon
- Magic The Gathering
- Yu-Gi-Oh!
- Disney Lorcana
- One Piece Card Game

oppure

- Euro Italia
- Dollari USA

oppure

- LEGO Star Wars
- LEGO Technic

---

## Tipo Tabella

Principale

---

## Nome Tabella

collections

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco collezione |
| category_id | UUID | SI | Categoria proprietaria |
| name | VARCHAR(150) | SI | Nome collezione |
| slug | VARCHAR(200) | SI | Identificativo URL friendly |
| description | TEXT | NO | Descrizione collezione |
| logo_url | TEXT | NO | Logo collezione |
| banner_url | TEXT | NO | Banner collezione |
| status | VARCHAR(30) | SI | Stato collezione |
| sort_order | INTEGER | SI | Ordine visualizzazione |
| created_at | TIMESTAMP | SI | Data creazione |
| updated_at | TIMESTAMP | SI | Data modifica |
| deleted_at | TIMESTAMP | NO | Soft Delete |

---

## Valori Predefiniti

status = active

sort_order = 0

---

## Valori Consentiti

### status

```text
active
hidden
archived
```

---

## Significato Stati

### active

Collezione utilizzabile.

Disponibile in:

- Catalogo
- Scanner
- Marketplace
- Matching
- Wishlist
- Collezioni Personali

---

### hidden

Collezione temporaneamente nascosta.

Non visibile agli utenti.

I dati restano conservati.

---

### archived

Collezione archiviata.

Non più utilizzabile.

Conservata esclusivamente per finalità storiche.

---

## Foreign Keys

category_id

→ categories.id

---

## Relazioni

categories (1)

↓

(N)

collections

---

collections (1)

↓

(N)

rarities

---

collections (1)

↓

(N)

series

---

collections (1)

↓

(N)

collection_followers

(Futuro)

---

collections (1)

↓

(N)

collection_favorites

(Futuro)

---

## Vincoli

category_id deve esistere nella tabella categories.

name non può essere vuoto.

slug deve essere univoco.

sort_order deve essere maggiore o uguale a zero.

status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (slug)

INDEX (category_id)

INDEX (name)

INDEX (status)

INDEX (sort_order)

---

## Regole Business

Una Collezione appartiene ad una sola Categoria.

Una Categoria può possedere molte Collezioni.

Una Collezione può possedere molte Serie.

Una Collezione possiede il proprio insieme di Rarità.

---

## Compatibilità Rarità

Le Rarità non sono globali.

Le Rarità appartengono esclusivamente alla Collezione.

Esempio:

```text
Pokémon
↓
Common
Uncommon
Rare
Ultra Rare
```

---

```text
Magic
↓
Common
Uncommon
Rare
Mythic Rare
```

---

Le stesse rarità possono avere significati differenti in collezioni differenti.

---

## Compatibilità Scanner

Durante la scansione:

```text
Categoria
↓
Collezione
↓
Versione
↓
Scansione
```

Lo Scanner utilizza la Collezione selezionata per limitare il campo di ricerca.

---

## Compatibilità Marketplace

Ogni annuncio Marketplace deve poter essere ricondotto a:

```text
Categoria
↓
Collezione
↓
Serie
↓
Oggetto
```

---

## Compatibilità Matching

Il Matching utilizza la Collezione come filtro principale.

Esempio:

```text
Utente interessato a Pokémon
```

↓

```text
Mostrare opportunità Pokémon
```

↓

```text
Ignorare Magic
```

---

## Compatibilità Notifiche

Gli utenti possono seguire una Collezione.

Eventi notificabili:

```text
Nuove Serie

Nuovi Oggetti

Nuove Versioni

Nuove Varianti

Nuovi Commercianti
```

---

## Compatibilità Catalogo Collaborativo

Le proposte possono riguardare:

```text
Nuove Serie

Nuovi Oggetti

Nuove Versioni

Nuove Varianti

Nuove Rarità
```

sempre all'interno di una Collezione specifica.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Attivare

Nascondere

Archiviare

Riordinare
```

una Collezione senza modificare il codice applicativo.

---

## Esempio Logico

Carte Collezionabili

↓

Pokémon

↓

Serie

↓

Set Base

↓

Oggetti

↓

Charizard

↓

Versioni

↓

Varianti

---

Numismatica

↓

Euro Italia

↓

Serie

↓

2 Euro Commemorativi

↓

Monete

---

## Motivazione Architetturale

La separazione tra Categoria e Collezione consente:

- crescita progressiva del catalogo
- gestione indipendente delle rarità
- notifiche dedicate
- statistiche separate
- attivazione graduale delle aree della piattaforma
- supporto a qualsiasi categoria futura

senza richiedere modifiche strutturali al database.

---

# Tabella: rarities

## Scopo

Rappresenta le rarità disponibili all'interno di una specifica Collezione.

Le rarità NON sono globali.

Ogni Collezione possiede il proprio insieme di rarità.

Questo approccio consente di supportare qualsiasi tipologia di collezione senza imporre uno standard universale.

---

## Tipo Tabella

Principale

---

## Nome Tabella

rarities

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco rarità |
| collection_id | UUID | SI | Collezione proprietaria |
| name | VARCHAR(150) | SI | Nome rarità |
| description | TEXT | NO | Descrizione rarità |
| color_hex | VARCHAR(20) | NO | Colore rappresentativo |
| sort_order | INTEGER | SI | Ordine visualizzazione |
| is_active | BOOLEAN | SI | Rarità utilizzabile |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

sort_order = 0

is_active = TRUE

---

## Foreign Keys

collection_id

→ collections.id

---

## Relazioni

collections (1)

↓

(N)

rarities

---

rarities (1)

↓

(N)

items

---

## Vincoli

collection_id deve esistere nella tabella collections.

name non può essere vuoto.

sort_order deve essere maggiore o uguale a zero.

All'interno della stessa Collezione non possono esistere due Rarità con lo stesso nome.

---

## Indici

PRIMARY KEY (id)

INDEX (collection_id)

INDEX (sort_order)

INDEX (is_active)

UNIQUE (collection_id, name)

---

## Regole Business

Una Rarità appartiene ad una sola Collezione.

Una Collezione può possedere molte Rarità.

La stessa rarità può esistere in Collezioni differenti.

---

## Esempio Pokémon

```text
Common

Uncommon

Rare

Ultra Rare

Illustration Rare

Special Illustration Rare

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

## Compatibilità Catalogo Collaborativo

Gli utenti possono proporre nuove Rarità.

Workflow:

```text
Nuova Rarità
↓
Catalogo Collaborativo
↓
Revisione Community
↓
Decisione Amministratore
↓
Pubblicazione
```

---

## Compatibilità Marketplace

La rarità viene ereditata automaticamente dagli Item.

Non viene duplicata sugli annunci.

---

## Compatibilità Matching

La rarità può essere utilizzata come filtro:

```text
Ultra Rare

Mythic Rare

Legendary
```

oppure come criterio di ranking.

---

## Motivazione Architetturale

Le rarità sono entità indipendenti perché:

- appartengono alla Collezione
- sono riutilizzate da molti Item
- possono essere corrette centralmente
- evitano duplicazioni

supportando qualsiasi categoria futura.

---

# Tabella: series

## Scopo

Rappresenta una Serie appartenente ad una specifica Collezione.

La Serie costituisce il contenitore principale degli Item.

---

## Tipo Tabella

Principale

---

## Nome Tabella

series

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco serie |
| collection_id | UUID | SI | Collezione proprietaria |
| name | VARCHAR(200) | SI | Nome serie |
| code | VARCHAR(100) | NO | Codice serie |
| release_date | DATE | SI | Data ufficiale uscita |
| description | TEXT | NO | Descrizione |
| status | VARCHAR(30) | SI | Stato serie |
| sort_order | INTEGER | SI | Ordinamento manuale |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = active

sort_order = 0

---

## Valori Consentiti

### status

```text
active
hidden
archived
```

---

## Foreign Keys

collection_id

→ collections.id

---

## Relazioni

collections (1)

↓

(N)

series

---

series (1)

↓

(N)

items

---

## Vincoli

collection_id deve esistere nella tabella collections.

name non può essere vuoto.

release_date è obbligatoria.

sort_order deve essere maggiore o uguale a zero.

status deve contenere un valore valido.

All'interno della stessa Collezione non possono esistere due Serie con lo stesso nome.

---

## Indici

PRIMARY KEY (id)

INDEX (collection_id)

INDEX (release_date)

INDEX (status)

INDEX (sort_order)

UNIQUE (collection_id, name)

---

## Regole Business

Una Serie appartiene ad una sola Collezione.

Una Collezione può possedere molte Serie.

Una Serie può possedere molti Item.

---

## Ordinamento Ufficiale

La Serie deve essere ordinata principalmente tramite:

```text
release_date
```

---

## Esempio Pokémon

```text
Set Base

Jungle

Fossil

Team Rocket
```

---

## Esempio Magic

```text
Alpha

Beta

Unlimited

Revised
```

---

## Compatibilità Collezioni Personali

Le percentuali di completamento vengono calcolate a livello Serie.

---

## Compatibilità Marketplace

Ogni annuncio deve essere riconducibile ad una specifica Serie.

---

## Compatibilità Matching

Il Matching può utilizzare la Serie come filtro di precisione.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Nascondere

Archiviare

Riordinare
```

le Serie senza modifiche al codice applicativo.

---

## Motivazione Architetturale

La Serie rappresenta il vero contenitore logico degli Item.

La sua esistenza consente:

- completamento collezioni
- statistiche avanzate
- matching più preciso
- ordinamento cronologico

senza duplicare informazioni sugli Item.

---

# Tabella: items

## Scopo

Rappresenta l'entità collezionabile principale del Catalogo Universale.

L'Item costituisce il riferimento centrale per:

- Catalogo
- Scanner
- Marketplace
- Matching
- Wishlist
- Collezioni Personali

Versioni e Varianti rappresentano specializzazioni dello stesso Item.

---

## Tipo Tabella

Principale

---

## Nome Tabella

items

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco item |
| series_id | UUID | SI | Serie di appartenenza |
| rarity_id | UUID | SI | Rarità associata |
| name | VARCHAR(255) | SI | Nome item |
| code | VARCHAR(100) | NO | Codice interno |
| catalog_number | VARCHAR(100) | NO | Numero catalogo |
| description | TEXT | NO | Descrizione |
| status | VARCHAR(30) | SI | Stato item |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = active

---

## Valori Consentiti

### status

```text
active
hidden
archived
```

---

## Foreign Keys

series_id

→ series.id

---

rarity_id

→ rarities.id

---

## Relazioni

series (1)

↓

(N)

items

---

rarities (1)

↓

(N)

items

---

items (1)

↓

(N)

item_versions

---

items (1)

↓

(N)

user_items

(Futuro)

---

items (1)

↓

(N)

wishlist_items

(Futuro)

---

items (1)

↓

(N)

marketplace_listings

(Futuro)

---

## Vincoli

series_id deve esistere nella tabella series.

rarity_id deve esistere nella tabella rarities.

name non può essere vuoto.

status deve contenere un valore valido.

All'interno della stessa Serie non possono esistere due Item con lo stesso nome.

---

## Indici

PRIMARY KEY (id)

INDEX (series_id)

INDEX (rarity_id)

INDEX (catalog_number)

INDEX (status)

UNIQUE (series_id, name)

---

## Regole Business

Ogni Item appartiene ad una sola Serie.

Ogni Item appartiene ad una sola Rarità.

Ogni Item deve possedere almeno una Versione.

---

## Rarità

La rarità appartiene sempre all'Item.

Non appartiene a:

```text
ItemVersion

ItemVariant
```

---

## Esempio Pokémon

```text
Serie:
Set Base

↓

Item:
Charizard

↓

Rarità:
Ultra Rare
```

---

## Esempio Magic

```text
Serie:
Alpha

↓

Item:
Black Lotus

↓

Rarità:
Rare
```

---

## Compatibilità Collezioni Personali

Il completamento principale viene calcolato a livello Item.

---

## Compatibilità Wishlist

Le Wishlist si basano principalmente sugli Item.

Possono essere successivamente specializzate tramite:

```text
Versione

Variante
```

---

## Compatibilità Scanner

Lo Scanner segue la gerarchia:

```text
Item
↓
Versione
↓
Variante
```

---

## Compatibilità Marketplace

Ogni annuncio deve essere riconducibile almeno ad un Item.

---

## Compatibilità Matching

Il Matching utilizza l'Item come riferimento principale.

---

## Compatibilità Catalogo Collaborativo

Gli utenti possono proporre:

```text
Nuovi Item
```

all'interno di una Serie esistente.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Correggere

Nascondere

Archiviare

Unificare Duplicati
```

---

## Unificazione Duplicati

Gli Item duplicati devono poter essere unificati.

Esempio:

```text
Charizard

Charizard Base Set
```

↓

```text
Charizard
```

---

Tutte le relazioni devono essere migrate automaticamente verso il record sopravvissuto.

---

## Motivazione Architetturale

L'Item rappresenta l'entità collezionabile principale del sistema.

La sua separazione da Versioni e Varianti:

- riduce duplicazioni
- migliora Marketplace
- migliora Matching
- migliora Scanner
- migliora Wishlist
- mantiene il Catalogo stabile

e consente la crescita futura del Catalogo Universale senza modifiche strutturali.

---

# Tabella: item_versions

## Scopo

Rappresenta una Versione appartenente ad un Item.

Le Versioni consentono di distinguere differenti edizioni, lingue, distribuzioni o pubblicazioni dello stesso Item.

Le Versioni NON rappresentano nuovi Item.

Le Versioni NON rappresentano Varianti.

---

## Tipo Tabella

Principale

---

## Nome Tabella

item_versions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco versione |
| item_id | UUID | SI | Item proprietario |
| name | VARCHAR(200) | SI | Nome versione |
| version_type | VARCHAR(50) | SI | Tipologia versione |
| description | TEXT | NO | Descrizione |
| is_default | BOOLEAN | SI | Versione predefinita |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_default = FALSE

version_type = generic

---

## Valori Consentiti

### version_type

```text
language
edition
distribution
generic
other
```

---

## Foreign Keys

item_id

→ items.id

---

## Relazioni

items (1)

↓

(N)

item_versions

---

item_versions (1)

↓

(N)

item_variants

---

item_versions (1)

↓

(N)

catalog_images

---

item_versions (1)

↓

(N)

user_items

(Futuro)

---

item_versions (1)

↓

(N)

wishlist_items

(Futuro)

---

item_versions (1)

↓

(N)

marketplace_listings

(Futuro)

---

## Vincoli

item_id deve esistere nella tabella items.

name non può essere vuoto.

version_type deve contenere un valore valido.

All'interno dello stesso Item non possono esistere due Versioni con lo stesso nome.

Può esistere una sola Versione con:

```text
is_default = TRUE
```

per ogni Item.

---

## Indici

PRIMARY KEY (id)

INDEX (item_id)

INDEX (version_type)

INDEX (is_default)

UNIQUE (item_id, name)

---

## Vincolo Logico Aggiuntivo

```text
Per ogni Item:

item_id + is_default = TRUE

può esistere una sola volta.
```

---

## Regole Business

Ogni Versione appartiene ad un solo Item.

Un Item può possedere molte Versioni.

Ogni Item deve possedere almeno una Versione.

---

## Versione Generica

Quando una Collezione non utilizza il concetto di Versione:

```text
Il sistema crea automaticamente

Versione Generica
```

---

## Esempio Linguistico

```text
Charizard

↓

Italiano

Inglese

Francese

Tedesco

Giapponese
```

---

## Esempio Editoriale

```text
Black Lotus

↓

Alpha

Beta

Unlimited
```

---

## Compatibilità Scanner

Lo Scanner identifica:

```text
Item
↓
Versione
↓
Variante
```

---

## Compatibilità Marketplace

Gli annunci devono poter distinguere:

```text
Charizard Inglese
```

da:

```text
Charizard Giapponese
```

---

## Compatibilità Matching

Le Versioni influenzano direttamente il Matching.

---

## Compatibilità Wishlist

Le Wishlist possono specificare:

```text
Item

oppure

Item + Versione
```

---

## Compatibilità Catalogo Collaborativo

Gli utenti possono proporre nuove Versioni quando:

```text
Item esistente
+
Versione assente
```

---

## Compatibilità Immagini

Le immagini possono appartenere a:

```text
ItemVersion
```

oppure:

```text
ItemVariant
```

---

## Motivazione Architetturale

La separazione delle Versioni dagli Item consente di rappresentare differenze reali senza duplicare l'intero Oggetto.

Questo approccio:

- migliora Scanner
- migliora Matching
- migliora Marketplace
- migliora Wishlist
- riduce duplicazioni

e garantisce scalabilità futura.

---

# Tabella: item_variants

## Scopo

Rappresenta una Variante appartenente ad una specifica Versione.

Le Varianti rappresentano differenze fisiche o produttive della stessa Versione.

Le Varianti NON rappresentano nuovi Item.

Le Varianti NON rappresentano nuove Versioni.

---

## Tipo Tabella

Principale

---

## Nome Tabella

item_variants

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco variante |
| item_version_id | UUID | SI | Versione proprietaria |
| name | VARCHAR(200) | SI | Nome variante |
| description | TEXT | NO | Descrizione |
| is_default | BOOLEAN | SI | Variante predefinita |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_default = FALSE

---

## Foreign Keys

item_version_id

→ item_versions.id

---

## Relazioni

item_versions (1)

↓

(N)

item_variants

---

item_variants (1)

↓

(N)

catalog_images

---

item_variants (1)

↓

(N)

user_items

(Futuro)

---

item_variants (1)

↓

(N)

wishlist_items

(Futuro)

---

item_variants (1)

↓

(N)

marketplace_listings

(Futuro)

---

## Vincoli

item_version_id deve esistere nella tabella item_versions.

name non può essere vuoto.

All'interno della stessa Versione non possono esistere due Varianti con lo stesso nome.

Può esistere una sola Variante con:

```text
is_default = TRUE
```

per ogni Versione.

---

## Indici

PRIMARY KEY (id)

INDEX (item_version_id)

INDEX (is_default)

UNIQUE (item_version_id, name)

---

## Vincolo Logico Aggiuntivo

```text
Per ogni Versione:

item_version_id + is_default = TRUE

può esistere una sola volta.
```

---

## Regole Business

Una Variante appartiene ad una sola Versione.

Una Versione può possedere molte Varianti.

Le Varianti sono opzionali.

Una Versione può non possedere alcuna Variante.

---

## Esempio Pokémon

```text
Charizard
↓
Versione Inglese
↓
Holo

Reverse Holo

Gold

Promo Stamp

Error Print
```

---

## Esempio Funko

```text
Batman
↓
Versione Generica
↓
Glow In The Dark

Metallic

Chase
```

---

## Compatibilità Scanner

Lo Scanner identifica:

```text
Item
↓
Versione
↓
Variante
```

La Variante rappresenta il massimo livello di precisione.

---

## Compatibilità Marketplace

Gli annunci devono poter distinguere:

```text
Charizard Inglese Holo
```

da:

```text
Charizard Inglese Reverse Holo
```

---

## Compatibilità Matching

Le Varianti partecipano direttamente al Matching.

---

## Compatibilità Wishlist

Le Wishlist possono specificare:

```text
Item

Item + Versione

Item + Versione + Variante
```

---

## Compatibilità Catalogo Collaborativo

Gli utenti possono proporre nuove Varianti.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Correggere

Archiviare

Unificare
```

Varianti duplicate.

---

## Motivazione Architetturale

Le Varianti consentono di rappresentare differenze reali all'interno della stessa Versione.

Questo approccio:

- migliora la precisione dello Scanner
- migliora il Marketplace
- migliora il Matching
- evita duplicazioni

e mantiene il Catalogo coerente.

---

# Tabella: catalog_images

## Scopo

Rappresenta le immagini del Catalogo Universale.

Le immagini vengono utilizzate da:

- Catalogo Universale
- Scanner
- Marketplace
- Wishlist
- Collezioni Personali
- Catalogo Collaborativo
- Dashboard Admin

---

# Regola Fondamentale

Le immagini NON appartengono direttamente agli Item.

Le immagini possono appartenere esclusivamente a:

```text
ItemVersion
```

oppure:

```text
ItemVariant
```

---

## Tipo Tabella

Principale

---

## Nome Tabella

catalog_images

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco immagine |
| item_version_id | UUID | NO | Versione associata |
| item_variant_id | UUID | NO | Variante associata |
| image_url | TEXT | SI | URL immagine |
| image_type | VARCHAR(50) | SI | Tipologia immagine |
| is_official | BOOLEAN | SI | Immagine ufficiale |
| is_active | BOOLEAN | SI | Immagine utilizzabile |
| width | INTEGER | NO | Larghezza immagine |
| height | INTEGER | NO | Altezza immagine |
| file_size_bytes | BIGINT | NO | Dimensione file |
| image_hash | VARCHAR(255) | NO | Hash immagine |
| ai_score | NUMERIC(5,2) | NO | Valutazione AI |
| community_score | NUMERIC(5,2) | NO | Valutazione Community |
| usage_score | NUMERIC(5,2) | NO | Frequenza utilizzo |
| total_score | NUMERIC(5,2) | NO | Punteggio totale |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_official = FALSE

is_active = TRUE

community_score = 0

usage_score = 0

total_score = 0

---

## Valori Consentiti

### image_type

```text
front
back
package
detail
version
variant
other
```

---

## Foreign Keys

item_version_id

→ item_versions.id

---

item_variant_id

→ item_variants.id

---

## Relazioni

item_versions (1)

↓

(N)

catalog_images

---

item_variants (1)

↓

(N)

catalog_images

---

## Vincolo Fondamentale

Deve essere valorizzato uno ed uno soltanto tra:

```text
item_version_id
```

oppure:

```text
item_variant_id
```

Non è consentito valorizzare entrambi contemporaneamente.

---

## Regola XOR

```text
item_version_id IS NOT NULL

XOR

item_variant_id IS NOT NULL
```

---

## Vincoli

image_url non può essere vuoto.

is_official deve avere un valore.

is_active deve avere un valore.

width deve essere maggiore di zero se valorizzato.

height deve essere maggiore di zero se valorizzato.

file_size_bytes deve essere maggiore di zero se valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (item_version_id)

INDEX (item_variant_id)

INDEX (is_official)

INDEX (is_active)

INDEX (total_score)

UNIQUE (image_hash)

---

## Regole Business

Una Versione può possedere molte immagini.

Una Variante può possedere molte immagini.

Una immagine appartiene ad una sola Versione oppure ad una sola Variante.

---

## Immagine Ufficiale

Per ogni Versione o Variante può esistere una sola immagine ufficiale.

```text
is_official = TRUE
```

---

## Priorità Visualizzazione

```text
Immagine Variante
↓
Immagine Versione
↓
Placeholder
```

---

## Compatibilità Scanner

Lo Scanner utilizza prioritariamente:

```text
Immagine Ufficiale Variante
```

oppure:

```text
Immagine Ufficiale Versione
```

per:

- Hash Matching
- OCR Support
- AI Recognition

---

## Compatibilità Marketplace

Gli annunci mostrano:

```text
Immagine Variante
```

quando disponibile.

Altrimenti:

```text
Immagine Versione
```

---

## Compatibilità Wishlist

La Wishlist segue la stessa priorità:

```text
Variante
↓
Versione
↓
Placeholder
```

---

## Compatibilità Catalogo Collaborativo

Gli utenti possono proporre nuove immagini.

Workflow:

```text
Nuova Immagine
↓
Revisione
↓
Valutazione
↓
Approvazione
```

---

## Compatibilità Moderazione

Le immagini devono poter essere:

```text
Segnalate

Revisionate

Disattivate
```

---

## Motivazione Architetturale

La separazione delle immagini dagli Item:

- supporta Versioni
- supporta Varianti
- migliora Scanner
- migliora Marketplace
- riduce duplicazioni
- migliora la qualità del Catalogo

ed implementa integralmente il Blueprint CollectorVerse.

---

# REVISIONE ARCHITETTURALE v1.0

## Stato Revisione

Le seguenti modifiche sostituiscono e integrano lo schema PostgreSQL v1.0 di CollectorVerse.

Queste correzioni sono considerate obbligatorie per garantire:

- coerenza con il Blueprint
- compatibilità PostgreSQL
- compatibilità Supabase
- compatibilità RLS
- integrità dei dati
- prevenzione dei duplicati

---

# Correzione 1 - Tabella users

## Problema

La colonna:

```text
is_active
```

non consente di distinguere:

```text
active
suspended
blocked
deleted
```

come previsto dal Blueprint.

---

## Sostituzione

### Rimuovere

```markdown
| is_active | BOOLEAN | SI | Stato attivo dell'account |
```

---

### Inserire

```markdown
| account_status | VARCHAR(30) | SI | Stato account |
```

---

## Valore Predefinito

### Rimuovere

```text
is_active = TRUE
```

---

### Inserire

```text
account_status = active
```

---

## Valori Consentiti

```markdown
## Valori Consentiti

### account_status

- active
- suspended
- blocked
- deleted
```

---

## Indici

### Rimuovere

```text
INDEX (is_active)
```

---

### Inserire

```text
INDEX (account_status)
```

---

# Correzione 2 - Tabella user_profiles

## Problema

La visibilità del profilo è definita due volte:

```text
user_profiles.profile_visibility
```

e

```text
privacy_settings.profile_visibility
```

Questo genera ambiguità.

---

## Rimozione

Eliminare completamente:

```markdown
| profile_visibility | VARCHAR(20) | SI | Livello di visibilità |
```

---

Eliminare completamente:

```markdown
## Valori Predefiniti

profile_visibility = public
```

---

Eliminare completamente:

```markdown
## Valori Consentiti

### profile_visibility

- public
- collectors_only
- private
```

---

Eliminare dai vincoli:

```text
profile_visibility deve contenere un valore valido.
```

---

Eliminare dagli indici:

```text
INDEX (profile_visibility)
```

---

## Regola Ufficiale

La visibilità del profilo viene gestita esclusivamente dalla tabella:

```text
privacy_settings
```

---

# Correzione 3 - Tabella rarities

## Problema

Possono essere create rarità duplicate nella stessa Collezione.

---

## Vincolo da aggiungere

```markdown
All'interno della stessa Collezione non possono esistere due Rarità con lo stesso nome.
```

---

## Indice da aggiungere

```text
UNIQUE (collection_id, name)
```

---

# Correzione 4 - Tabella series

## Problema

Possono esistere Serie duplicate nella stessa Collezione.

---

## Vincolo da aggiungere

```markdown
All'interno della stessa Collezione non possono esistere due Serie con lo stesso nome.
```

---

## Indice da aggiungere

```text
UNIQUE (collection_id, name)
```

---

# Correzione 5 - Tabella items

## Problema

Possono esistere Item duplicati nella stessa Serie.

---

## Vincolo da aggiungere

```markdown
All'interno della stessa Serie non possono esistere due Item con lo stesso nome.
```

---

## Indice da aggiungere

```text
UNIQUE (series_id, name)
```

---

# Correzione 6 - Tabella item_versions

## Problema

Possono esistere:

```text
Italiano
Italiano
Italiano
```

per lo stesso Item.

---

## Vincolo da aggiungere

```markdown
All'interno dello stesso Item non possono esistere due Versioni con lo stesso nome.
```

---

## Indice da aggiungere

```text
UNIQUE (item_id, name)
```

---

## Vincolo Versione Default

```markdown
Può esistere una sola Versione con:

is_default = TRUE

per ogni Item.
```

---

## Regola Tecnica

```text
item_id + is_default = TRUE

può esistere una sola volta.
```

---

# Correzione 7 - Tabella item_variants

## Problema

Possono esistere:

```text
Holo
Holo
Holo
```

per la stessa Versione.

---

## Vincolo da aggiungere

```markdown
All'interno della stessa Versione non possono esistere due Varianti con lo stesso nome.
```

---

## Indice da aggiungere

```text
UNIQUE (item_version_id, name)
```

---

## Vincolo Variante Default

```markdown
Può esistere una sola Variante con:

is_default = TRUE

per ogni Versione.
```

---

## Regola Tecnica

```text
item_version_id + is_default = TRUE

può esistere una sola volta.
```

---

# Correzione 8 - Tabella catalog_images

## Problema

La regola attuale consente:

```text
item_version_id valorizzato

e

item_variant_id valorizzato
```

contemporaneamente.

Questo viola il Blueprint.

---

## Sostituzione Completa

### Rimuovere

```markdown
Deve essere valorizzato almeno uno tra:

item_version_id

oppure

item_variant_id
```

---

### Inserire

```markdown
## Vincolo Fondamentale

Deve essere valorizzato uno ed uno soltanto tra:

item_version_id

oppure

item_variant_id

Non è consentito valorizzare entrambi contemporaneamente.
```

---

## Regola XOR

```text
item_version_id IS NOT NULL

XOR

item_variant_id IS NOT NULL
```

---

# Correzione 9 - Tabella catalog_images

## Prevenzione Duplicati

Aggiungere:

```text
UNIQUE (image_hash)
```

---

## Obiettivo

Impedire il caricamento multiplo della stessa immagine.

---

# Correzione 10 - Uso di TIMESTAMPTZ

## Problema

Lo schema utilizza:

```text
TIMESTAMP
```

---

## Standard PostgreSQL + Supabase

Utilizzare sempre:

```text
TIMESTAMPTZ
```

---

## Sostituzione Globale

Sostituire ovunque nel documento:

```text
TIMESTAMP
```

con:

```text
TIMESTAMPTZ
```

---

## Motivazione

Permette la corretta gestione di:

- timezone
- notifiche
- marketplace internazionale
- date scansioni
- scadenze
- attività utenti
- sincronizzazioni cloud

---

# Stato Finale

Dopo l'applicazione di queste correzioni:

```text
✅ Core Identity Completa
✅ Catalogo Universale Completo
✅ Compatibile PostgreSQL
✅ Compatibile Supabase
✅ Compatibile RLS
✅ Gestione Duplicati Corretta
✅ Marketplace Ready
✅ Matching Ready
✅ Scanner Ready
✅ Catalogo Collaborativo Ready
✅ Scalabile a milioni di record
```

Lo schema aggiornato può essere considerato:

```text
CollectorVerse PostgreSQL Schema v1.0

STATO: CONGELATO

PRONTO PER:

- Parte 3 Catalogazione Personale
- Marketplace
- Matching
- Scanner
- Gamification
```

---

# Parte 3 - Catalogazione Personale

# Tabella: user_collections

## Scopo

Rappresenta una Collezione Personale creata da un utente.

Le Collezioni Personali consentono di organizzare gli oggetti posseduti in gruppi logici definiti dall'utente.

Questa tabella NON rappresenta le Collezioni del Catalogo Universale.

Rappresenta esclusivamente contenitori personali.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_collections

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco collezione personale |
| user_id | UUID | SI | Proprietario della collezione |
| name | VARCHAR(150) | SI | Nome collezione |
| description | TEXT | NO | Descrizione collezione |
| is_default | BOOLEAN | SI | Collezione predefinita |
| is_public | BOOLEAN | SI | Visibilità pubblica |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_default = FALSE

is_public = TRUE

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

user_collections

---

user_collections (1)

↓

(N)

user_items

---

## Vincoli

user_id deve esistere nella tabella users.

name non può essere vuoto.

All'interno dello stesso utente non possono esistere due Collezioni Personali con lo stesso nome.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (is_public)

INDEX (is_default)

UNIQUE (user_id, name)

---

## Regole Business

Ogni Collezione Personale appartiene ad un solo utente.

Un utente può possedere molte Collezioni Personali.

---

## Collezione Predefinita

Ogni utente deve possedere almeno una Collezione Personale.

Alla registrazione viene creata automaticamente:

```text
La Mia Collezione
```

---

## Vincolo Collezione Predefinita

Per ogni utente:

```text
Può esistere una sola Collezione Personale con:

is_default = TRUE
```

---

## Esempi

```text
La Mia Collezione
```

---

```text
Carte Pokémon
```

---

```text
Carte Gradate
```

---

```text
Doppioni da Scambiare
```

---

```text
Investimenti
```

---

## Compatibilità Privacy

La visibilità della Collezione Personale viene influenzata da:

```text
privacy_settings
```

e

```text
is_public
```

---

## Compatibilità Collezioni Pubbliche

Le Collezioni Personali pubbliche possono essere mostrate nel profilo utente.

---

## Compatibilità Marketplace

Una Collezione Personale può contenere oggetti:

```text
Posseduti

In Vendita

Disponibili per Scambio
```

tramite le tabelle successive.

---

## Compatibilità Matching

Le Collezioni Personali vengono utilizzate per:

- suggerimenti
- matching
- statistiche
- completamento raccolte

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Archiviare
```

le Collezioni Personali in caso di abuso.

---

## Compatibilità Statistiche

Statistiche possibili:

```text
Numero Oggetti

Numero Versioni

Numero Varianti

Valore Stimato

Percentuale Completamento
```

---

## Esempio Logico

Utente

↓

user_collections

↓

Carte Pokémon

↓

Oggetti Posseduti

---

Utente

↓

user_collections

↓

Doppioni

↓

Oggetti Disponibili per Scambio

---

## Motivazione Architetturale

Le Collezioni Personali sono state separate dagli Oggetti Posseduti perché consentono:

- organizzazione libera
- categorie personalizzate
- gestione doppioni
- gestione investimenti
- gestione scambi

senza modificare il Catalogo Universale.

La separazione garantisce massima flessibilità e supporta qualsiasi stile collezionistico.

---

# Tabella: user_items

## Scopo

Rappresenta il possesso di uno specifico oggetto da parte di uno specifico utente.

Questa è una delle tabelle più importanti dell'intera piattaforma.

Il Catalogo Universale definisce:

```text
Cosa esiste
```

La tabella user_items definisce:

```text
Cosa possiede realmente un utente
```

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_items

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco possesso |
| user_collection_id | UUID | SI | Collezione personale proprietaria |
| item_id | UUID | SI | Item associato |
| item_version_id | UUID | NO | Versione associata |
| item_variant_id | UUID | NO | Variante associata |
| quantity | INTEGER | SI | Quantità posseduta |
| condition_code | VARCHAR(30) | NO | Stato conservazione |
| purchase_price | NUMERIC(12,2) | NO | Prezzo acquisto |
| purchase_currency_id | UUID | NO | Valuta acquisto |
| estimated_value | NUMERIC(12,2) | NO | Valore stimato |
| estimated_currency_id | UUID | NO | Valuta valore stimato |
| acquisition_date | DATE | NO | Data acquisizione |
| notes | TEXT | NO | Note personali |
| is_for_sale | BOOLEAN | SI | Disponibile per vendita |
| is_for_trade | BOOLEAN | SI | Disponibile per scambio |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

quantity = 1

is_for_sale = FALSE

is_for_trade = FALSE

---

## Valori Consentiti

### condition_code

```text
new
mint
near_mint
excellent
good
fair
poor
damaged
```

---

## Significato Condizioni

### new

Oggetto nuovo.

---

### mint

Condizioni perfette.

---

### near_mint

Quasi perfette.

---

### excellent

Lievi segni di utilizzo.

---

### good

Normale usura.

---

### fair

Usura evidente.

---

### poor

Condizioni molto compromesse.

---

### damaged

Oggetto danneggiato.

---

## Foreign Keys

user_collection_id

→ user_collections.id

---

item_id

→ items.id

---

item_version_id

→ item_versions.id

---

item_variant_id

→ item_variants.id

---

purchase_currency_id

→ currencies.id

---

estimated_currency_id

→ currencies.id

---

## Relazioni

user_collections (1)

↓

(N)

user_items

---

items (1)

↓

(N)

user_items

---

item_versions (1)

↓

(N)

user_items

---

item_variants (1)

↓

(N)

user_items

---

currencies (1)

↓

(N)

user_items

---

## Vincoli

user_collection_id deve esistere.

item_id deve esistere.

quantity deve essere maggiore di zero.

purchase_price non può essere negativa.

estimated_value non può essere negativa.

condition_code deve contenere un valore valido se valorizzato.

---

## Vincolo Gerarchico

Se viene specificata una Variante:

```text
item_variant_id
```

deve appartenere alla Versione indicata.

---

Se viene specificata una Versione:

```text
item_version_id
```

deve appartenere all'Item indicato.

---

## Regole Business

Ogni record rappresenta un possesso reale dell'utente.

---

## Esempio 1

```text
Utente

↓

Charizard

↓

Versione Inglese

↓

Holo

↓

Quantità = 1
```

---

## Esempio 2

```text
Utente

↓

Pikachu

↓

Versione Italiana

↓

Quantità = 3
```

---

## Quantità

La tabella supporta la gestione di:

```text
Copie singole

Duplicati

Lotti
```

---

### Esempio

```text
Charizard

Quantità = 4
```

significa:

```text
L'utente possiede 4 copie
```

---

## Compatibilità Collezioni Personali

Ogni Oggetto Posseduto appartiene ad una Collezione Personale.

Esempio:

```text
Carte Pokémon
```

oppure

```text
Doppioni
```

oppure

```text
Investimenti
```

---

## Compatibilità Marketplace

Gli oggetti possono essere marcati come:

```text
is_for_sale = TRUE
```

oppure

```text
is_for_trade = TRUE
```

---

Questo NON crea automaticamente un annuncio.

L'annuncio verrà gestito dalle tabelle Marketplace.

---

## Compatibilità Matching

Il Matching utilizza:

```text
Oggetti posseduti

Oggetti in vendita

Oggetti scambiabili
```

per individuare opportunità.

---

## Compatibilità Wishlist

Il sistema può confrontare:

```text
Wishlist Utente A
```

con

```text
user_items Utente B
```

per proporre Match.

---

## Compatibilità Scanner

Dopo una scansione riuscita:

```text
Scanner
↓
Identificazione
↓
Aggiunta a user_items
```

---

## Compatibilità Statistiche

La tabella alimenta:

```text
Numero Oggetti Posseduti

Numero Versioni

Numero Varianti

Valore Stimato

Collezione Totale

Completamento Serie

Completamento Collezione
```

---

## Compatibilità Gamification

La tabella viene utilizzata per calcolare:

```text
CollectorScore

Livelli

Badge

Achievement
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Ripristinare

Archiviare
```

record problematici.

---

## Esempio Logico

Utente

↓

Carte Pokémon

↓

Charizard

↓

Versione Inglese

↓

Holo

↓

Quantità = 2

↓

Disponibile per Scambio

---

Utente

↓

Monete Rare

↓

2 Euro Dante

↓

Versione Generica

↓

Quantità = 1

↓

Collezione Personale

---

## Motivazione Architetturale

La tabella user_items rappresenta il collegamento tra:

```text
Catalogo Universale
```

e

```text
Possesso Reale dell'Utente
```

La separazione tra:

```text
Catalogo

e

Possesso
```

consente:

- catalogo condiviso
- collezioni personali illimitate
- gestione duplicati
- marketplace
- matching
- statistiche avanzate
- gamification

senza alterare il Catalogo Universale.

---

# Tabella: wishlists

## Scopo

Rappresenta una Wishlist appartenente ad uno specifico utente.

Una Wishlist permette di organizzare gli oggetti desiderati dall'utente.

La Wishlist NON contiene direttamente gli oggetti desiderati.

Gli elementi desiderati verranno memorizzati nella tabella:

```text
wishlist_items
```

---

## Tipo Tabella

Principale

---

## Nome Tabella

wishlists

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco wishlist |
| user_id | UUID | SI | Proprietario wishlist |
| name | VARCHAR(150) | SI | Nome wishlist |
| description | TEXT | NO | Descrizione wishlist |
| is_default | BOOLEAN | SI | Wishlist predefinita |
| is_public | BOOLEAN | SI | Wishlist pubblica |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_default = FALSE

is_public = TRUE

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

wishlists

---

wishlists (1)

↓

(N)

wishlist_items

---

## Vincoli

user_id deve esistere nella tabella users.

name non può essere vuoto.

All'interno dello stesso utente non possono esistere due Wishlist con lo stesso nome.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (is_default)

INDEX (is_public)

UNIQUE (user_id, name)

---

## Regole Business

Ogni Wishlist appartiene ad un solo utente.

Un utente può possedere più Wishlist.

---

## Wishlist Predefinita

Alla registrazione viene creata automaticamente una Wishlist:

```text
La Mia Wishlist
```

---

## Vincolo Wishlist Predefinita

Per ogni utente:

```text
Può esistere una sola Wishlist con:

is_default = TRUE
```

---

## Esempi

```text
La Mia Wishlist
```

---

```text
Pokémon da Completare
```

---

```text
Carte da Investimento
```

---

```text
Ricerca Prioritaria
```

---

```text
Scambi Desiderati
```

---

## Compatibilità Privacy

La visibilità della Wishlist dipende da:

```text
privacy_settings
```

e

```text
is_public
```

---

## Visibilità Effettiva

Una Wishlist viene mostrata pubblicamente soltanto se:

```text
privacy_settings permette la visibilità
```

e

```text
is_public = TRUE
```

---

## Compatibilità Matching

Le Wishlist rappresentano il principale input del Matching.

Il sistema confronta:

```text
wishlist_items
```

con:

```text
user_items
```

per individuare opportunità.

---

## Compatibilità Marketplace

Le Wishlist permettono di individuare annunci potenzialmente interessanti.

Esempio:

```text
Wishlist

↓

Charizard

↓

Nuovo Annuncio Marketplace

↓

Notifica Utente
```

---

## Compatibilità Scanner

Dopo una scansione:

```text
Oggetto non posseduto
```

↓

```text
Aggiunta alla Wishlist
```

---

## Compatibilità Notifiche

La Wishlist può generare notifiche per:

```text
Nuovi Annunci

Nuovi Scambi

Nuovi Possessori

Nuove Opportunità Matching
```

---

## Compatibilità Gamification

Le Wishlist possono essere utilizzate per calcolare:

```text
Obiettivi Completati

Oggetti Ricercati

Progressione Collezione

Achievement
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Ripristinare

Archiviare
```

Wishlist problematiche.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Wishlist

Numero Elementi Desiderati

Wishlist Completate

Wishlist Attive

Tasso Completamento
```

---

## Esempio Logico

Utente

↓

wishlists

↓

Pokémon da Completare

↓

wishlist_items

↓

Charizard

Blastoise

Venusaur

---

Utente

↓

wishlists

↓

Carte da Investimento

↓

wishlist_items

↓

Lugia

Umbreon

Gengar

---

## Motivazione Architetturale

Le Wishlist sono state separate dagli elementi desiderati perché consentono:

- più wishlist per utente
- organizzazione personalizzata
- priorità differenti
- statistiche dedicate
- matching più preciso
- notifiche mirate

senza modificare la struttura del Catalogo Universale.

Questa separazione garantisce massima flessibilità e supporta qualsiasi tipologia di collezionista.

---

# Tabella: wishlist_items

## Scopo

Rappresenta un elemento desiderato all'interno di una Wishlist.

Questa tabella contiene i collegamenti tra:

```text
Wishlist
```

e

```text
Item

Versione

Variante
```

La tabella costituisce il cuore del sistema di:

- Matching
- Ricerca Oggetti
- Notifiche Marketplace
- Completamento Collezioni
- Suggerimenti Acquisto
- Suggerimenti Scambio

---

## Tipo Tabella

Principale

---

## Nome Tabella

wishlist_items

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco elemento wishlist |
| wishlist_id | UUID | SI | Wishlist proprietaria |
| item_id | UUID | SI | Item desiderato |
| item_version_id | UUID | NO | Versione desiderata |
| item_variant_id | UUID | NO | Variante desiderata |
| quantity_desired | INTEGER | SI | Quantità desiderata |
| priority_level | VARCHAR(20) | SI | Priorità |
| notes | TEXT | NO | Note personali |
| is_active | BOOLEAN | SI | Elemento attivo |
| created_at | TIMESTAMPTZ | SI | Data inserimento |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

quantity_desired = 1

priority_level = medium

is_active = TRUE

---

## Valori Consentiti

### priority_level

```text
low

medium

high

critical
```

---

## Significato Priorità

### low

Interesse basso.

---

### medium

Interesse normale.

---

### high

Ricerca attiva.

---

### critical

Massima priorità.

Oggetto ricercato con urgenza.

---

## Foreign Keys

wishlist_id

→ wishlists.id

---

item_id

→ items.id

---

item_version_id

→ item_versions.id

---

item_variant_id

→ item_variants.id

---

## Relazioni

wishlists (1)

↓

(N)

wishlist_items

---

items (1)

↓

(N)

wishlist_items

---

item_versions (1)

↓

(N)

wishlist_items

---

item_variants (1)

↓

(N)

wishlist_items

---

## Vincoli

wishlist_id deve esistere.

item_id deve esistere.

quantity_desired deve essere maggiore di zero.

priority_level deve contenere un valore valido.

is_active deve contenere un valore valido.

---

## Vincolo Gerarchico

Se viene specificata una Variante:

```text
item_variant_id
```

deve appartenere alla Versione indicata.

---

Se viene specificata una Versione:

```text
item_version_id
```

deve appartenere all'Item indicato.

---

## Vincolo Anti-Duplicato

La stessa Wishlist non può contenere due volte:

```text
Lo stesso Item

+
Stessa Versione

+
Stessa Variante
```

---

## Indici

PRIMARY KEY (id)

INDEX (wishlist_id)

INDEX (item_id)

INDEX (item_version_id)

INDEX (item_variant_id)

INDEX (priority_level)

INDEX (is_active)

---

## Regole Business

Un elemento Wishlist può riferirsi a:

```text
Solo Item
```

oppure:

```text
Item + Versione
```

oppure:

```text
Item + Versione + Variante
```

---

## Esempio 1

```text
Charizard
```

Significa:

```text
Qualsiasi Charizard
```

---

## Esempio 2

```text
Charizard

+

Versione Inglese
```

Significa:

```text
Solo Charizard Inglese
```

---

## Esempio 3

```text
Charizard

+

Versione Inglese

+

Gold
```

Significa:

```text
Solo Charizard Inglese Gold
```

---

## Compatibilità Matching

Il Matching confronta:

```text
wishlist_items
```

con:

```text
user_items
```

---

### Esempio

Utente A desidera:

```text
Charizard Inglese Gold
```

↓

Utente B possiede:

```text
Charizard Inglese Gold
```

↓

```text
Match Potenziale
```

---

## Compatibilità Marketplace

Gli annunci vengono confrontati automaticamente con gli elementi Wishlist.

---

### Esempio

Marketplace:

```text
Nuovo Annuncio

↓

Charizard Inglese Gold
```

↓

wishlist_items

↓

Charizard Inglese Gold
```

↓

```text
Notifica Utente
```

---

## Compatibilità Scanner

Dopo una scansione:

```text
Oggetto Mancante
```

↓

```text
Aggiunta alla Wishlist
```

---

## Compatibilità Collezioni Personali

Quando un oggetto viene acquisito:

```text
wishlist_item
```

↓

```text
user_item
```

↓

Possibile rimozione automatica dalla Wishlist.

---

## Compatibilità Notifiche

La Wishlist può generare notifiche per:

```text
Nuovi Annunci

Nuovi Possessori

Nuove Opportunità di Scambio

Match Perfetti

Match Parziali
```

---

## Compatibilità Gamification

Gli elementi Wishlist vengono utilizzati per calcolare:

```text
Obiettivi Completati

Progressione Collezione

Achievement

CollectorScore
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Oggetti Ricercati

Numero Match Trovati

Numero Acquisti Derivati

Numero Wishlist Completate

Percentuale Completamento Wishlist
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Ripristinare

Archiviare
```

elementi problematici.

---

## Esempio Logico

Wishlist

↓

Pokémon da Completare

↓

wishlist_items

↓

Charizard

Blastoise

Venusaur

---

Wishlist

↓

Investimenti

↓

wishlist_items

↓

Umbreon Gold Star

Lugia First Edition

Pikachu Illustrator

---

## Motivazione Architetturale

La separazione tra:

```text
wishlists
```

e

```text
wishlist_items
```

consente:

- più wishlist per utente
- priorità differenti
- matching avanzato
- notifiche mirate
- statistiche dettagliate
- gestione indipendente degli elementi desiderati

senza modificare il Catalogo Universale.

Questa struttura è coerente con il Blueprint CollectorVerse e costituisce la base per Marketplace, Matching e Notifiche intelligenti.

---

# Parte 4 - Marketplace

# Tabella: marketplace_listings

## Scopo

Rappresenta un annuncio Marketplace pubblicato da un utente.

Un annuncio è sempre associato ad un oggetto realmente posseduto dall'utente.

L'annuncio può riguardare:

- vendita
- scambio
- vendita e scambio

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_listings

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco annuncio |
| seller_user_id | UUID | SI | Proprietario annuncio |
| user_item_id | UUID | SI | Oggetto posseduto collegato |
| listing_type | VARCHAR(30) | SI | Tipologia annuncio |
| status | VARCHAR(30) | SI | Stato annuncio |
| title | VARCHAR(255) | SI | Titolo annuncio |
| description | TEXT | NO | Descrizione annuncio |
| price_amount | NUMERIC(12,2) | NO | Prezzo richiesto |
| currency_id | UUID | NO | Valuta |
| quantity_available | INTEGER | SI | Quantità disponibile |
| published_at | TIMESTAMPTZ | NO | Data pubblicazione |
| expires_at | TIMESTAMPTZ | NO | Data scadenza |
| view_count | INTEGER | SI | Numero visualizzazioni |
| favorite_count | INTEGER | SI | Numero preferiti |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = draft

view_count = 0

favorite_count = 0

quantity_available = 1

---

## Valori Consentiti

### listing_type

```text
sale
trade
sale_trade
```

---

### status

```text
draft

active

reserved

completed

expired

cancelled

suspended
```

---

## Significato Listing Type

### sale

Annuncio di sola vendita.

---

### trade

Annuncio di solo scambio.

---

### sale_trade

Vendita oppure scambio.

---

## Significato Status

### draft

Bozza non pubblicata.

---

### active

Annuncio visibile.

---

### reserved

Oggetto temporaneamente impegnato.

---

### completed

Operazione conclusa.

---

### expired

Annuncio scaduto.

---

### cancelled

Annuncio ritirato.

---

### suspended

Annuncio sospeso dalla moderazione.

---

## Foreign Keys

seller_user_id

→ users.id

---

user_item_id

→ user_items.id

---

currency_id

→ currencies.id

---

## Relazioni

users (1)

↓

(N)

marketplace_listings

---

user_items (1)

↓

(N)

marketplace_listings

---

currencies (1)

↓

(N)

marketplace_listings

---

marketplace_listings (1)

↓

(N)

marketplace_favorites

(Futuro)

---

marketplace_listings (1)

↓

(N)

marketplace_reports

(Futuro)

---

marketplace_listings (1)

↓

(N)

marketplace_offers

(Futuro)

---

## Vincoli

seller_user_id deve esistere.

user_item_id deve esistere.

listing_type deve contenere un valore valido.

status deve contenere un valore valido.

quantity_available deve essere maggiore di zero.

price_amount deve essere maggiore o uguale a zero se valorizzato.

---

## Vincolo Proprietà

L'oggetto collegato:

```text
user_item_id
```

deve appartenere allo stesso utente indicato in:

```text
seller_user_id
```

---

## Regole Business

Un annuncio può essere creato esclusivamente per un oggetto realmente posseduto.

---

## Vendita

Per annunci:

```text
sale

oppure

sale_trade
```

può essere valorizzato:

```text
price_amount
```

---

## Scambio

Per annunci:

```text
trade
```

il prezzo può essere assente.

---

## Quantità

La quantità disponibile non può superare la quantità posseduta.

---

### Esempio

```text
User Item

Quantità Posseduta = 5
```

↓

```text
Marketplace Listing

Quantità Disponibile = 3
```

Valido.

---

```text
Marketplace Listing

Quantità Disponibile = 7
```

Non valido.

---

## Compatibilità Matching

Il Matching utilizza:

```text
listing_type

Item

Versione

Variante
```

per individuare opportunità.

---

## Compatibilità Wishlist

Gli annunci vengono confrontati con:

```text
wishlist_items
```

---

### Esempio

Wishlist:

```text
Charizard Inglese Gold
```

↓

Marketplace:

```text
Charizard Inglese Gold
```

↓

```text
Potenziale Match
```

---

## Compatibilità Notifiche

Un annuncio può generare notifiche quando:

```text
Nuovo Annuncio

Cambio Prezzo

Scadenza

Nuovo Match
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Nascondere

Sospendere

Archiviare
```

gli annunci.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Visualizzazioni

Preferiti

Contatti Ricevuti

Offerte Ricevute

Conversioni

Vendite
```

---

## Esempio Logico

Utente

↓

user_items

↓

Charizard Inglese Gold

↓

marketplace_listing

↓

Vendita

↓

250,00 EUR

↓

Active

---

Utente

↓

user_items

↓

Blastoise Italiano

↓

marketplace_listing

↓

Trade

↓

Active

---

## Motivazione Architetturale

La separazione tra:

```text
user_items
```

e

```text
marketplace_listings
```

consente:

- possesso senza pubblicazione
- pubblicazione selettiva
- gestione quantità
- vendite multiple
- scambi
- cronologia annunci

senza alterare la struttura delle collezioni personali.

Questa architettura costituisce il nucleo del Marketplace CollectorVerse e supporta milioni di annunci senza modifiche strutturali future.

---

# Tabella: marketplace_offers

## Scopo

Rappresenta una proposta effettuata su un annuncio Marketplace.

La proposta può essere:

- economica
- di scambio
- mista

La tabella gestisce l'intero ciclo di negoziazione tra utenti.

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_offers

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco offerta |
| marketplace_listing_id | UUID | SI | Annuncio destinatario |
| buyer_user_id | UUID | SI | Utente offerente |
| offer_type | VARCHAR(30) | SI | Tipologia offerta |
| status | VARCHAR(30) | SI | Stato offerta |
| offered_amount | NUMERIC(12,2) | NO | Importo offerto |
| currency_id | UUID | NO | Valuta offerta |
| message | TEXT | NO | Messaggio accompagnatorio |
| expires_at | TIMESTAMPTZ | NO | Scadenza proposta |
| responded_at | TIMESTAMPTZ | NO | Data risposta |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = pending

---

## Valori Consentiti

### offer_type

```text
purchase
trade
purchase_trade
```

---

### status

```text
pending

accepted

rejected

cancelled

expired

countered
```

---

## Significato Offer Type

### purchase

Proposta economica.

---

### trade

Proposta di scambio.

---

### purchase_trade

Proposta mista:

```text
Scambio

+

Importo aggiuntivo
```

---

## Significato Status

### pending

Offerta in attesa.

---

### accepted

Offerta accettata.

---

### rejected

Offerta rifiutata.

---

### cancelled

Offerta annullata dall'offerente.

---

### expired

Offerta scaduta.

---

### countered

Controproposta generata.

---

## Foreign Keys

marketplace_listing_id

→ marketplace_listings.id

---

buyer_user_id

→ users.id

---

currency_id

→ currencies.id

---

## Relazioni

marketplace_listings (1)

↓

(N)

marketplace_offers

---

users (1)

↓

(N)

marketplace_offers

---

currencies (1)

↓

(N)

marketplace_offers

---

marketplace_offers (1)

↓

(N)

marketplace_offer_trade_items

(Futuro)

---

marketplace_offers (1)

↓

(N)

marketplace_offer_history

(Futuro)

---

## Vincoli

marketplace_listing_id deve esistere.

buyer_user_id deve esistere.

offer_type deve contenere un valore valido.

status deve contenere un valore valido.

offered_amount deve essere maggiore di zero se valorizzato.

---

## Vincolo Proprietà

L'offerente non può essere il proprietario dell'annuncio.

---

### Non consentito

```text
seller_user_id

=

buyer_user_id
```

---

## Regole Business

Un annuncio può ricevere molte offerte.

Una offerta appartiene ad un solo annuncio.

Una offerta appartiene ad un solo offerente.

---

## Offerta Economica

Per:

```text
purchase
```

deve essere valorizzato:

```text
offered_amount
```

---

## Offerta di Scambio

Per:

```text
trade
```

l'importo può essere assente.

Gli oggetti proposti verranno gestiti tramite:

```text
marketplace_offer_trade_items
```

---

## Offerta Mista

Per:

```text
purchase_trade
```

sono consentiti:

```text
Importo

+

Oggetti in Scambio
```

---

## Indici

PRIMARY KEY (id)

INDEX (marketplace_listing_id)

INDEX (buyer_user_id)

INDEX (status)

INDEX (offer_type)

INDEX (expires_at)

INDEX (created_at)

---

## Compatibilità Marketplace

Le offerte costituiscono il sistema principale di trattativa.

---

### Esempio Vendita

Annuncio:

```text
Charizard Gold
```

↓

Prezzo:

```text
250 EUR
```

↓

Offerta:

```text
220 EUR
```

---

### Esempio Scambio

Annuncio:

```text
Umbreon Gold Star
```

↓

Offerta:

```text
Lugia First Edition
```

---

### Esempio Misto

Annuncio:

```text
Charizard Gold
```

↓

Offerta:

```text
Blastoise First Edition

+

100 EUR
```

---

## Compatibilità Matching

Le offerte vengono utilizzate per identificare:

```text
Interessi reali

Trattative attive

Tasso conversione
```

---

## Compatibilità Notifiche

Le offerte possono generare notifiche per:

```text
Nuova Offerta

Offerta Accettata

Offerta Rifiutata

Controproposta

Scadenza Offerta
```

---

## Compatibilità Messaggistica

Un'offerta può essere collegata ad una conversazione privata.

---

### Esempio

```text
Marketplace Offer

↓

Conversation

↓

Messages
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Offerte

Offerte Accettate

Offerte Rifiutate

Tasso Conversione

Tempo Medio Risposta
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Revisionare

Bloccare

Archiviare
```

offerte problematiche.

---

## Esempio Logico

Marketplace Listing

↓

Charizard Gold

↓

Marketplace Offer

↓

220 EUR

↓

Pending

↓

Accepted

---

Marketplace Listing

↓

Lugia First Edition

↓

Marketplace Offer

↓

Umbreon Gold Star

↓

Trade

↓

Pending

---

## Motivazione Architetturale

La separazione tra:

```text
marketplace_listings
```

e

```text
marketplace_offers
```

consente:

- più offerte sullo stesso annuncio
- gestione trattative
- controproposte
- storico negoziazioni
- supporto vendita
- supporto scambio
- supporto formule miste

senza modificare l'annuncio originale.

Questa struttura costituisce il motore delle trattative del Marketplace CollectorVerse.

---

# Tabella: marketplace_offer_trade_items

## Scopo

Rappresenta gli oggetti proposti in una Offerta di Scambio.

La tabella viene utilizzata quando una proposta Marketplace contiene:

```text
Scambio
```

oppure:

```text
Scambio + Importo Economico
```

Questa tabella permette di specificare con precisione quali oggetti vengono offerti dall'utente.

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_offer_trade_items

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco elemento di scambio |
| marketplace_offer_id | UUID | SI | Offerta associata |
| user_item_id | UUID | SI | Oggetto offerto nello scambio |
| quantity | INTEGER | SI | Quantità proposta |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

quantity = 1

---

## Foreign Keys

marketplace_offer_id

→ marketplace_offers.id

---

user_item_id

→ user_items.id

---

## Relazioni

marketplace_offers (1)

↓

(N)

marketplace_offer_trade_items

---

user_items (1)

↓

(N)

marketplace_offer_trade_items

---

## Vincoli

marketplace_offer_id deve esistere.

user_item_id deve esistere.

quantity deve essere maggiore di zero.

---

## Vincolo Proprietà

L'oggetto indicato in:

```text
user_item_id
```

deve appartenere all'utente che ha creato l'offerta.

---

### Non consentito

```text
Utente A

↓

Offerta

↓

Oggetto appartenente a Utente B
```

---

## Vincolo Disponibilità

La quantità proposta nello scambio non può superare la quantità realmente posseduta.

---

### Esempio

Utente possiede:

```text
5 Charizard
```

---

Può proporre:

```text
1 Charizard

oppure

3 Charizard

oppure

5 Charizard
```

---

Non può proporre:

```text
6 Charizard
```

---

## Vincolo Anti-Duplicato

All'interno della stessa offerta non può comparire due volte lo stesso:

```text
user_item
```

---

## Indici

PRIMARY KEY (id)

INDEX (marketplace_offer_id)

INDEX (user_item_id)

UNIQUE (marketplace_offer_id, user_item_id)

---

## Regole Business

Una Offerta può includere:

```text
Nessun Oggetto
```

per offerte economiche pure.

---

Oppure:

```text
Uno o più Oggetti
```

per gli scambi.

---

## Esempio Scambio Semplice

Annuncio:

```text
Charizard Gold
```

---

Offerta:

```text
Umbreon Gold Star
```

---

marketplace_offer_trade_items

```text
Umbreon Gold Star
```

---

## Esempio Scambio Multiplo

Annuncio:

```text
Lugia First Edition
```

---

Offerta:

```text
Charizard

+

Blastoise

+

Venusaur
```

---

marketplace_offer_trade_items

```text
Charizard

Blastoise

Venusaur
```

---

## Esempio Scambio Misto

Annuncio:

```text
Pikachu Illustrator
```

---

Offerta:

```text
Charizard Gold

+

500 EUR
```

---

marketplace_offers

```text
offered_amount = 500
```

---

marketplace_offer_trade_items

```text
Charizard Gold
```

---

## Compatibilità Marketplace

La tabella costituisce il cuore degli scambi.

Consente di supportare:

```text
1 contro 1

1 contro molti

Molti contro molti

Scambio + denaro
```

---

## Compatibilità Matching

Gli oggetti proposti vengono utilizzati per identificare:

```text
Interessi reciproci

Opportunità di scambio

Match avanzati
```

---

## Compatibilità Wishlist

Durante l'analisi delle offerte il sistema può verificare se:

```text
Oggetto Offerto
```

è presente nella:

```text
Wishlist del venditore
```

---

### Esempio

Venditore cerca:

```text
Umbreon Gold Star
```

---

Offerente propone:

```text
Umbreon Gold Star
```

---

```text
Match Migliorato
```

---

## Compatibilità Notifiche

Possono essere generate notifiche per:

```text
Nuova Offerta di Scambio

Oggetto Correlato alla Wishlist

Accettazione

Rifiuto

Controproposta
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Scambi Proposti

Oggetti Proposti

Oggetti Accettati

Valore Stimato Scambi

Tasso Accettazione
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Revisionare

Archiviare

Moderare
```

gli oggetti coinvolti nelle trattative.

---

## Esempio Logico

Marketplace Listing

↓

Charizard Gold

↓

Marketplace Offer

↓

Trade

↓

marketplace_offer_trade_items

↓

Umbreon Gold Star

↓

Pending

---

Marketplace Listing

↓

Lugia First Edition

↓

Marketplace Offer

↓

Trade + Cash

↓

marketplace_offer_trade_items

↓

Charizard

Blastoise

↓

500 EUR

↓

Pending

---

## Motivazione Architetturale

La separazione tra:

```text
marketplace_offers
```

e

```text
marketplace_offer_trade_items
```

consente di gestire qualsiasi tipologia di scambio senza limitazioni strutturali.

Questo approccio supporta:

- scambi complessi
- più oggetti
- offerte miste
- matching avanzato
- statistiche dettagliate

e rende il Marketplace CollectorVerse estendibile a qualsiasi categoria futura senza modifiche al database.

---

# Tabella: marketplace_favorites

## Scopo

Rappresenta il salvataggio di un annuncio Marketplace tra i preferiti di un utente.

Questa funzionalità permette agli utenti di:

- monitorare annunci interessanti
- confrontare più annunci
- seguire l'evoluzione dei prezzi
- ricevere notifiche sugli annunci salvati
- ritrovare facilmente annunci visualizzati in precedenza

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_favorites

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco preferito |
| user_id | UUID | SI | Utente che salva il preferito |
| marketplace_listing_id | UUID | SI | Annuncio salvato |
| created_at | TIMESTAMPTZ | SI | Data aggiunta ai preferiti |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Foreign Keys

user_id

→ users.id

---

marketplace_listing_id

→ marketplace_listings.id

---

## Relazioni

users (1)

↓

(N)

marketplace_favorites

---

marketplace_listings (1)

↓

(N)

marketplace_favorites

---

## Vincoli

user_id deve esistere.

marketplace_listing_id deve esistere.

---

## Vincolo Anti-Duplicato

Lo stesso utente non può salvare più volte lo stesso annuncio.

---

### Non consentito

```text
Utente A

↓

Annuncio 123

↓

Preferito
```

---

```text
Utente A

↓

Annuncio 123

↓

Preferito
```

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (marketplace_listing_id)

INDEX (created_at)

UNIQUE (user_id, marketplace_listing_id)

---

## Regole Business

Un utente può aggiungere ai preferiti qualsiasi annuncio visibile.

Un annuncio può essere aggiunto ai preferiti da molti utenti.

---

## Compatibilità Marketplace

I preferiti consentono di:

```text
Seguire Annunci

Monitorare Prezzi

Confrontare Opportunità

Creare Liste Personali
```

---

## Compatibilità Notifiche

Un annuncio preferito può generare notifiche quando:

```text
Cambio Prezzo

Cambio Stato

Scadenza Annuncio

Nuove Offerte

Annuncio Completato
```

---

## Esempio

Utente salva:

```text
Charizard Gold
```

---

Successivamente:

```text
Prezzo 250 EUR
↓
Prezzo 220 EUR
```

↓

```text
Notifica Utente
```

---

## Compatibilità Matching

Gli annunci salvati rappresentano un forte indicatore di interesse.

Possono essere utilizzati per:

```text
Migliorare Matching

Suggerimenti

Raccomandazioni
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Preferiti Totali

Annunci più Salvati

Utenti più Attivi

Conversioni da Preferito a Acquisto
```

---

## Compatibilità Profilo Utente

Statistiche disponibili:

```text
Numero Annunci Salvati

Cronologia Preferiti

Interessi Marketplace
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Analizzare

Moderare
```

i dati aggregati dei preferiti.

---

## Compatibilità Algoritmi Futuri

I preferiti possono essere utilizzati per:

```text
Suggerimenti Personalizzati

Consigli Acquisto

Ranking Marketplace

Ricerche Popolari
```

---

## Esempio Logico

Utente

↓

marketplace_favorites

↓

Charizard Gold

Lugia First Edition

Umbreon Gold Star

↓

Monitoraggio Automatico

---

Marketplace Listing

↓

100 Utenti Preferiti

↓

Alta Popolarità

↓

Maggiore Visibilità

---

## Motivazione Architetturale

La separazione tra:

```text
marketplace_listings
```

e

```text
marketplace_favorites
```

consente:

- monitoraggio indipendente degli annunci
- notifiche dedicate
- statistiche avanzate
- ranking Marketplace
- raccomandazioni personalizzate

senza modificare direttamente la struttura degli annunci.

Questa tabella costituisce uno degli elementi fondamentali del Marketplace CollectorVerse per misurare interesse e popolarità degli annunci.

---

# Tabella: marketplace_reports

## Scopo

Rappresenta una segnalazione effettuata da un utente nei confronti di un annuncio Marketplace.

La tabella viene utilizzata per:

- contrastare frodi
- contrastare truffe
- contrastare spam
- identificare oggetti falsi
- identificare contenuti inappropriati
- supportare il lavoro di moderazione

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_reports

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco segnalazione |
| marketplace_listing_id | UUID | SI | Annuncio segnalato |
| reporter_user_id | UUID | SI | Utente segnalante |
| report_reason | VARCHAR(50) | SI | Motivo segnalazione |
| status | VARCHAR(30) | SI | Stato gestione |
| description | TEXT | NO | Dettagli aggiuntivi |
| reviewed_by_user_id | UUID | NO | Moderatore o amministratore che ha gestito il caso |
| reviewed_at | TIMESTAMPTZ | NO | Data revisione |
| resolution_notes | TEXT | NO | Note risoluzione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = pending

---

## Valori Consentiti

### report_reason

```text
fraud

counterfeit

duplicate_listing

wrong_category

misleading_description

inappropriate_content

spam

stolen_item

other
```

---

### status

```text
pending

under_review

approved

rejected

closed
```

---

## Significato Report Reason

### fraud

Possibile tentativo di truffa.

---

### counterfeit

Possibile oggetto falso.

---

### duplicate_listing

Annuncio duplicato.

---

### wrong_category

Categoria errata.

---

### misleading_description

Descrizione ingannevole.

---

### inappropriate_content

Contenuti non consentiti.

---

### spam

Spam o pubblicità abusiva.

---

### stolen_item

Possibile bene rubato.

---

### other

Motivazione non classificabile.

---

## Significato Status

### pending

Segnalazione ricevuta.

In attesa di revisione.

---

### under_review

Caso in fase di analisi.

---

### approved

Segnalazione confermata.

---

### rejected

Segnalazione respinta.

---

### closed

Caso chiuso.

---

## Foreign Keys

marketplace_listing_id

→ marketplace_listings.id

---

reporter_user_id

→ users.id

---

reviewed_by_user_id

→ users.id

---

## Relazioni

marketplace_listings (1)

↓

(N)

marketplace_reports

---

users (1)

↓

(N)

marketplace_reports

(segnalante)

---

users (1)

↓

(N)

marketplace_reports

(revisore)

---

## Vincoli

marketplace_listing_id deve esistere.

reporter_user_id deve esistere.

report_reason deve contenere un valore valido.

status deve contenere un valore valido.

---

## Vincolo Anti-Duplicato

Lo stesso utente non può avere più segnalazioni aperte sullo stesso annuncio.

---

### Non consentito

```text
Utente A

↓

Annuncio 123

↓

Segnalazione Pending
```

---

```text
Utente A

↓

Annuncio 123

↓

Nuova Segnalazione Pending
```

---

## Indici

PRIMARY KEY (id)

INDEX (marketplace_listing_id)

INDEX (reporter_user_id)

INDEX (reviewed_by_user_id)

INDEX (report_reason)

INDEX (status)

INDEX (created_at)

---

## Regole Business

Una segnalazione riguarda un solo annuncio.

Un annuncio può ricevere molte segnalazioni.

Una segnalazione appartiene ad un solo segnalante.

---

## Workflow Moderazione

```text
Utente

↓

Segnala Annuncio

↓

Pending

↓

Under Review

↓

Approved / Rejected

↓

Closed
```

---

## Effetti Possibili

Una segnalazione approvata può causare:

```text
Nascondi Annuncio

Sospendi Annuncio

Limita Visibilità

Avvia Verifica

Blocca Utente

Aumenta Livello Rischio
```

---

## Compatibilità Marketplace

Le segnalazioni influenzano:

```text
Qualità Marketplace

Sicurezza

Affidabilità Venditori

Ranking Annunci
```

---

## Compatibilità Profilo Utente

Le segnalazioni approvate possono contribuire a:

```text
Riduzione Affidabilità

Limitazioni Marketplace

Azioni Moderative
```

---

## Compatibilità Notifiche

Le segnalazioni possono generare notifiche per:

```text
Nuova Segnalazione

Cambio Stato

Caso Chiuso

Richiesta Informazioni
```

---

## Compatibilità Dashboard Admin

I moderatori e amministratori devono poter:

```text
Visualizzare

Filtrare

Revisionare

Approvare

Respingere

Chiudere
```

segnalazioni.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Segnalazioni

Segnalazioni Approvate

Segnalazioni Respinte

Tempo Medio Revisione

Categorie Più Segnalate

Utenti Più Segnalati
```

---

## Esempio Logico

Marketplace Listing

↓

Charizard Gold

↓

Marketplace Report

↓

Counterfeit

↓

Pending

↓

Approved

↓

Annuncio Sospeso

---

Marketplace Listing

↓

Lugia First Edition

↓

Marketplace Report

↓

Duplicate Listing

↓

Under Review

↓

Rejected

↓

Annuncio Attivo

---

## Motivazione Architetturale

La separazione tra:

```text
marketplace_listings
```

e

```text
marketplace_reports
```

consente:

- moderazione indipendente
- cronologia segnalazioni
- statistiche dedicate
- prevenzione abusi
- miglioramento sicurezza

senza modificare direttamente gli annunci.

Questa tabella costituisce il nucleo del sistema di moderazione del Marketplace CollectorVerse e garantisce la qualità dell'ecosistema nel tempo.

---

# Tabella: marketplace_listing_status_history

## Scopo

Rappresenta la cronologia degli stati di un annuncio Marketplace.

La tabella consente di tracciare tutti i cambiamenti di stato subiti da un annuncio nel corso del tempo.

Questa tabella viene utilizzata per:

- audit amministrativo
- statistiche
- cronologia attività
- analisi performance annunci
- monitoraggio moderazione

---

## Tipo Tabella

Principale

---

## Nome Tabella

marketplace_listing_status_history

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco storico |
| marketplace_listing_id | UUID | SI | Annuncio associato |
| previous_status | VARCHAR(30) | NO | Stato precedente |
| new_status | VARCHAR(30) | SI | Nuovo stato |
| changed_by_user_id | UUID | NO | Utente che ha causato il cambio |
| change_reason | VARCHAR(100) | NO | Motivazione del cambio |
| notes | TEXT | NO | Note aggiuntive |
| created_at | TIMESTAMPTZ | SI | Data cambio stato |

---

## Valori Consentiti

### previous_status

Può contenere:

```text
draft

active

reserved

completed

expired

cancelled

suspended
```

oppure essere:

```text
NULL
```

quando viene registrato il primo stato dell'annuncio.

---

### new_status

```text
draft

active

reserved

completed

expired

cancelled

suspended
```

---

### change_reason

Valori consigliati:

```text
user_action

automatic_expiration

offer_accepted

manual_close

moderation_action

system_update

other
```

---

## Foreign Keys

marketplace_listing_id

→ marketplace_listings.id

---

changed_by_user_id

→ users.id

---

## Relazioni

marketplace_listings (1)

↓

(N)

marketplace_listing_status_history

---

users (1)

↓

(N)

marketplace_listing_status_history

---

## Vincoli

marketplace_listing_id deve esistere.

new_status deve contenere un valore valido.

Se valorizzato:

```text
previous_status
```

deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (marketplace_listing_id)

INDEX (changed_by_user_id)

INDEX (new_status)

INDEX (created_at)

---

## Regole Business

Ogni modifica dello stato dell'annuncio deve generare automaticamente un nuovo record.

I record storici non devono essere modificati.

I record storici non devono essere eliminati.

---

## Esempio Ciclo Normale

```text
Draft

↓

Active

↓

Reserved

↓

Completed
```

---

## Storico Registrato

```text
Record 1

NULL
↓

Draft
```

---

```text
Record 2

Draft
↓

Active
```

---

```text
Record 3

Active
↓

Reserved
```

---

```text
Record 4

Reserved
↓

Completed
```

---

## Esempio Moderazione

```text
Active

↓

Suspended
```

---

Motivazione:

```text
moderation_action
```

---

## Compatibilità Marketplace

Permette di conoscere:

```text
Quando è stato pubblicato

Quando è stato sospeso

Quando è stato riservato

Quando è stato chiuso
```

---

## Compatibilità Statistiche

Statistiche possibili:

```text
Tempo Medio Pubblicazione

Tempo Medio Vendita

Tempo Medio Riserva

Tempo Medio Chiusura

Tasso Scadenza Annunci
```

---

## Compatibilità Profilo Utente

Statistiche possibili:

```text
Annunci Pubblicati

Annunci Completati

Annunci Scaduti

Annunci Cancellati
```

---

## Compatibilità Moderazione

Consente agli amministratori di vedere:

```text
Chi ha modificato

Quando ha modificato

Stato precedente

Nuovo stato

Motivazione
```

---

## Compatibilità Audit

Nessuna modifica deve cancellare la cronologia.

La tabella costituisce il log ufficiale degli stati degli annunci Marketplace.

---

## Compatibilità Notifiche

I cambiamenti di stato possono generare notifiche:

```text
Annuncio Pubblicato

Annuncio Riservato

Annuncio Completato

Annuncio Sospeso

Annuncio Scaduto
```

---

## Esempio Logico

Marketplace Listing

↓

Charizard Gold

↓

Status History

↓

Draft

↓

Active

↓

Reserved

↓

Completed

---

Marketplace Listing

↓

Umbreon Gold Star

↓

Status History

↓

Draft

↓

Active

↓

Suspended

---

## Motivazione Architetturale

La separazione tra:

```text
marketplace_listings
```

e

```text
marketplace_listing_status_history
```

consente di mantenere una cronologia permanente delle modifiche senza alterare il record principale dell'annuncio.

Questo approccio supporta:

- audit
- statistiche
- moderazione
- notifiche
- storico attività

senza introdurre concetti finanziari o transazioni economiche non gestite da CollectorVerse.

---

# Tabella: saved_searches

## Scopo

Rappresenta una ricerca salvata da un utente.

Le ricerche salvate consentono agli utenti di monitorare automaticamente il Marketplace senza dover ripetere manualmente le stesse ricerche.

Questa funzionalità costituisce la base per:

- notifiche automatiche
- monitoraggio nuovi annunci
- monitoraggio variazioni prezzo
- monitoraggio disponibilità oggetti
- suggerimenti personalizzati

---

## Tipo Tabella

Principale

---

## Nome Tabella

saved_searches

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco ricerca |
| user_id | UUID | SI | Proprietario ricerca |
| name | VARCHAR(150) | SI | Nome ricerca salvata |
| search_query | TEXT | NO | Testo originale ricerca |
| category_id | UUID | NO | Categoria filtrata |
| collection_id | UUID | NO | Collezione filtrata |
| series_id | UUID | NO | Serie filtrata |
| item_id | UUID | NO | Item specifico |
| item_version_id | UUID | NO | Versione specifica |
| item_variant_id | UUID | NO | Variante specifica |
| min_price | NUMERIC(12,2) | NO | Prezzo minimo |
| max_price | NUMERIC(12,2) | NO | Prezzo massimo |
| currency_id | UUID | NO | Valuta riferimento |
| listing_type | VARCHAR(30) | NO | Tipologia annuncio |
| notify_new_listings | BOOLEAN | SI | Notifica nuovi annunci |
| notify_price_changes | BOOLEAN | SI | Notifica variazioni prezzo |
| is_active | BOOLEAN | SI | Ricerca attiva |
| last_match_at | TIMESTAMPTZ | NO | Ultimo risultato trovato |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

notify_new_listings = TRUE

notify_price_changes = TRUE

is_active = TRUE

---

## Valori Consentiti

### listing_type

```text
sale

trade

sale_trade
```

---

## Foreign Keys

user_id

→ users.id

---

category_id

→ categories.id

---

collection_id

→ collections.id

---

series_id

→ series.id

---

item_id

→ items.id

---

item_version_id

→ item_versions.id

---

item_variant_id

→ item_variants.id

---

currency_id

→ currencies.id

---

## Relazioni

users (1)

↓

(N)

saved_searches

---

categories (1)

↓

(N)

saved_searches

---

collections (1)

↓

(N)

saved_searches

---

series (1)

↓

(N)

saved_searches

---

items (1)

↓

(N)

saved_searches

---

item_versions (1)

↓

(N)

saved_searches

---

item_variants (1)

↓

(N)

saved_searches

---

## Vincoli

user_id deve esistere.

min_price deve essere maggiore o uguale a zero se valorizzato.

max_price deve essere maggiore o uguale a zero se valorizzato.

Se valorizzati:

```text
min_price ≤ max_price
```

---

listing_type deve contenere un valore valido se valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (category_id)

INDEX (collection_id)

INDEX (series_id)

INDEX (item_id)

INDEX (item_version_id)

INDEX (item_variant_id)

INDEX (is_active)

INDEX (last_match_at)

---

## Regole Business

Una ricerca può essere:

```text
Generica
```

oppure:

```text
Molto Specifica
```

---

## Esempio Ricerca Generica

```text
Pokémon
```

---

## Esempio Ricerca Categoria

```text
Carte Collezionabili
```

---

## Esempio Ricerca Collezione

```text
Pokémon
```

---

## Esempio Ricerca Serie

```text
Set Base
```

---

## Esempio Ricerca Item

```text
Charizard
```

---

## Esempio Ricerca Completa

```text
Charizard

↓

Versione Inglese

↓

Gold

↓

Prezzo Max = 500 EUR
```

---

## Compatibilità Marketplace

Le ricerche salvate vengono confrontate periodicamente con:

```text
marketplace_listings
```

per individuare nuovi risultati compatibili.

---

## Compatibilità Notifiche

Possono generare notifiche per:

```text
Nuovo Annuncio

Riduzione Prezzo

Nuovo Match

Nuova Variante Disponibile
```

---

## Esempio

Ricerca Salvata:

```text
Charizard Gold
```

---

Nuovo Annuncio:

```text
Charizard Gold

220 EUR
```

↓

```text
Notifica Utente
```

---

## Compatibilità Matching

Le ricerche salvate rappresentano un forte segnale di interesse.

Possono essere utilizzate per:

```text
Suggerimenti

Raccomandazioni

Ranking Opportunità
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Ricerche Salvate

Numero Match Trovati

Numero Notifiche Generate

Numero Acquisti Successivi
```

---

## Compatibilità Profilo Utente

Dati utilizzabili per:

```text
Oggetti Più Ricercati

Categorie Preferite

Interessi Principali
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Analizzare

Aggregare

Monitorare
```

trend e richieste degli utenti.

---

## Esempio Logico

Utente

↓

saved_searches

↓

Charizard Gold

↓

Marketplace

↓

Nuovo Annuncio

↓

Notifica

---

Utente

↓

saved_searches

↓

2 Euro Commemorativi Italia

↓

Marketplace

↓

Nuovo Annuncio

↓

Notifica

---

## Motivazione Architetturale

La separazione tra:

```text
saved_searches
```

e

```text
marketplace_listings
```

consente:

- monitoraggio continuo
- notifiche automatiche
- personalizzazione avanzata
- suggerimenti intelligenti
- statistiche di interesse

senza modificare la struttura del Marketplace.

Questa tabella costituisce una delle basi delle funzionalità proattive di CollectorVerse e migliora significativamente l'esperienza utente nel tempo.

---

# Parte 5 - Matching

# Tabella: matching_opportunities

## Scopo

Rappresenta una opportunità di Matching generata automaticamente dal sistema.

Una opportunità viene creata quando il motore di Matching individua una possibile relazione tra:

- oggetti posseduti
- wishlist
- annunci marketplace
- interessi utenti

---

## Tipo Tabella

Principale

---

## Nome Tabella

matching_opportunities

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco opportunità |
| target_user_id | UUID | SI | Utente destinatario opportunità |
| source_user_id | UUID | NO | Utente che genera l'opportunità |
| marketplace_listing_id | UUID | NO | Annuncio coinvolto |
| wishlist_item_id | UUID | NO | Elemento wishlist coinvolto |
| user_item_id | UUID | NO | Oggetto posseduto coinvolto |
| match_type | VARCHAR(30) | SI | Tipo di matching |
| match_score | NUMERIC(5,2) | SI | Punteggio matching |
| status | VARCHAR(30) | SI | Stato opportunità |
| generated_at | TIMESTAMPTZ | SI | Data generazione |
| viewed_at | TIMESTAMPTZ | NO | Data visualizzazione |
| dismissed_at | TIMESTAMPTZ | NO | Data ignorata |
| expires_at | TIMESTAMPTZ | NO | Data scadenza |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

status = active

match_score = 0

---

## Valori Consentiti

### match_type

```text
wishlist_match

marketplace_match

trade_match

collection_match

duplicate_match
```

---

### status

```text
active

viewed

dismissed

expired
```

---

## Significato Match Type

### wishlist_match

Un utente possiede un oggetto presente nella wishlist di un altro utente.

---

### marketplace_match

Un annuncio Marketplace corrisponde ad una wishlist.

---

### trade_match

Possibile opportunità di scambio reciproco.

---

### collection_match

Interessi collezionistici compatibili.

---

### duplicate_match

Oggetto duplicato potenzialmente interessante per altri utenti.

---

## Foreign Keys

target_user_id

→ users.id

---

source_user_id

→ users.id

---

marketplace_listing_id

→ marketplace_listings.id

---

wishlist_item_id

→ wishlist_items.id

---

user_item_id

→ user_items.id

---

## Relazioni

users (1)

↓

(N)

matching_opportunities

(destinatario)

---

users (1)

↓

(N)

matching_opportunities

(generatore opportunità)

---

marketplace_listings (1)

↓

(N)

matching_opportunities

---

wishlist_items (1)

↓

(N)

matching_opportunities

---

user_items (1)

↓

(N)

matching_opportunities

---

## Vincoli

target_user_id deve esistere.

match_type deve contenere un valore valido.

status deve contenere un valore valido.

match_score deve essere compreso tra:

```text
0

e

100
```

---

## Regole Business

Una opportunità deve sempre appartenere ad un utente destinatario.

Una opportunità può coinvolgere:

```text
Marketplace

oppure

Wishlist

oppure

User Item

oppure

più elementi contemporaneamente
```

---

## Match Score

Il punteggio rappresenta la qualità dell'opportunità.

---

### Esempio

```text
100

↓

Match Perfetto
```

---

```text
75

↓

Match Molto Forte
```

---

```text
50

↓

Match Interessante
```

---

```text
25

↓

Match Debole
```

---

## Esempio Wishlist Match

Utente A cerca:

```text
Charizard Gold
```

---

Utente B possiede:

```text
Charizard Gold
```

---

Sistema:

```text
matching_opportunity

↓

wishlist_match

↓

score 100
```

---

## Esempio Marketplace Match

Utente A cerca:

```text
Umbreon Gold Star
```

---

Marketplace:

```text
Nuovo Annuncio
```

---

Sistema:

```text
marketplace_match
```

---

## Esempio Trade Match

Utente A desidera:

```text
Lugia
```

---

Utente B possiede:

```text
Lugia
```

---

Utente B desidera:

```text
Charizard
```

---

Utente A possiede:

```text
Charizard
```

---

Sistema:

```text
trade_match

score 100
```

---

## Compatibilità Notifiche

Le opportunità possono generare notifiche:

```text
Nuovo Match

Nuovo Scambio

Nuovo Annuncio Compatibile

Nuova Opportunità Marketplace
```

---

## Compatibilità Dashboard Utente

La dashboard può mostrare:

```text
Match Attivi

Nuove Opportunità

Match Perfetti

Opportunità Scambio
```

---

## Compatibilità Gamification

Le opportunità possono contribuire a:

```text
Achievement

CollectorScore

Obiettivi Completamento
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Match Generati

Match Visualizzati

Match Completati

Match Ignorati

Tasso Conversione
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Monitorare

Analizzare

Ricalcolare

Eliminare
```

opportunità errate.

---

## Esempio Logico

Wishlist

↓

Charizard Gold

↓

Marketplace Listing

↓

Charizard Gold

↓

matching_opportunities

↓

score 100

↓

active

---

User A

↓

Charizard

↓

User B

↓

Lugia

↓

Interessi Reciproci

↓

trade_match

↓

score 100

---

## Motivazione Architetturale

La tabella matching_opportunities rappresenta il risultato del motore intelligente di CollectorVerse.

La separazione delle opportunità dai dati sorgente consente:

- ricalcolo indipendente
- prestazioni elevate
- notifiche efficienti
- statistiche dedicate
- storico opportunità

senza dover rieseguire continuamente algoritmi complessi sul database operativo.

Questa tabella costituisce il cuore del sistema di Matching della piattaforma.

---

# Tabella: matching_preferences

## Scopo

Rappresenta le preferenze personali utilizzate dal motore di Matching.

Questa tabella consente ad ogni utente di configurare il comportamento del sistema di suggerimenti automatici.

Le preferenze influenzano:

- Matching Marketplace
- Matching Scambi
- Matching Collezionisti
- Matching Wishlist
- Notifiche Opportunità

---

## Tipo Tabella

Principale

---

## Nome Tabella

matching_preferences

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco preferenze |
| user_id | UUID | SI | Proprietario preferenze |
| enable_marketplace_matches | BOOLEAN | SI | Abilita matching marketplace |
| enable_trade_matches | BOOLEAN | SI | Abilita matching scambi |
| enable_collection_matches | BOOLEAN | SI | Abilita matching collezionisti |
| enable_duplicate_matches | BOOLEAN | SI | Abilita matching duplicati |
| enable_wishlist_matches | BOOLEAN | SI | Abilita matching wishlist |
| minimum_match_score | NUMERIC(5,2) | SI | Soglia minima matching |
| notify_new_matches | BOOLEAN | SI | Notifica nuove opportunità |
| notify_trade_matches | BOOLEAN | SI | Notifica opportunità di scambio |
| notify_marketplace_matches | BOOLEAN | SI | Notifica opportunità marketplace |
| notify_collection_matches | BOOLEAN | SI | Notifica compatibilità collezionisti |
| include_merchants | BOOLEAN | SI | Considera commercianti |
| include_private_collectors | BOOLEAN | SI | Considera collezionisti privati |
| is_active | BOOLEAN | SI | Matching attivo |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

enable_marketplace_matches = TRUE

enable_trade_matches = TRUE

enable_collection_matches = TRUE

enable_duplicate_matches = TRUE

enable_wishlist_matches = TRUE

minimum_match_score = 50

notify_new_matches = TRUE

notify_trade_matches = TRUE

notify_marketplace_matches = TRUE

notify_collection_matches = TRUE

include_merchants = TRUE

include_private_collectors = TRUE

is_active = TRUE

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(1)

matching_preferences

---

matching_preferences

↓

Influenza

↓

matching_opportunities

---

## Vincoli

user_id deve esistere.

user_id deve essere univoco.

minimum_match_score deve essere compreso tra:

```text
0

e

100
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (is_active)

INDEX (minimum_match_score)

---

## Regole Business

Ogni utente possiede una sola configurazione Matching.

La configurazione viene creata automaticamente durante la registrazione.

---

## Matching Disattivato

Se:

```text
is_active = FALSE
```

il sistema non deve:

```text
Generare Matching

Inviare Notifiche Matching
```

---

Le opportunità storiche restano disponibili.

---

## Soglia Matching

La soglia minima controlla la qualità delle opportunità.

---

### Esempio

```text
minimum_match_score = 80
```

↓

Mostrare solo match di alta qualità.

---

### Esempio

```text
minimum_match_score = 30
```

↓

Mostrare anche opportunità deboli.

---

## Matching Marketplace

Se:

```text
enable_marketplace_matches = TRUE
```

il sistema confronta:

```text
Wishlist

↓

Marketplace Listings
```

---

## Matching Scambi

Se:

```text
enable_trade_matches = TRUE
```

il sistema confronta:

```text
Wishlist

↓

User Items

↓

Possibili Scambi
```

---

## Matching Duplicati

Se:

```text
enable_duplicate_matches = TRUE
```

il sistema considera:

```text
Oggetti Duplicati
```

come potenziali opportunità.

---

## Matching Collezionisti

Se:

```text
enable_collection_matches = TRUE
```

il sistema può suggerire:

```text
Utenti con interessi simili

Utenti compatibili

Commercianti specializzati
```

---

## Compatibilità Marketplace

Le preferenze influenzano:

```text
Notifiche Nuovi Annunci

Suggerimenti

Ranking Opportunità
```

---

## Compatibilità Wishlist

Le preferenze influenzano:

```text
Monitoraggio Oggetti Ricercati

Segnalazioni Nuove Disponibilità
```

---

## Compatibilità Notifiche

Le notifiche vengono inviate soltanto se:

```text
Matching Attivo

+

Preferenza Notifica Attiva
```

---

## Compatibilità Dashboard Utente

L'utente deve poter:

```text
Attivare

Disattivare

Configurare

Personalizzare
```

l'intero sistema Matching.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Match Ricevuti

Numero Match Ignorati

Numero Match Accettati

Tasso Conversione

Punteggio Medio Match
```

---

## Esempio Logico

Utente

↓

matching_preferences

↓

Marketplace ✅

Scambi ✅

Duplicati ✅

Commercianti ✅

Score Minimo = 70

↓

matching_opportunities

↓

Solo Match ≥ 70

---

Utente

↓

matching_preferences

↓

Marketplace ✅

Scambi ❌

Duplicati ❌

Commercianti ❌

Score Minimo = 90

↓

Solo Match Molto Forti

---

## Motivazione Architetturale

La separazione tra:

```text
matching_preferences
```

e

```text
matching_opportunities
```

consente di:

- personalizzare il Matching
- ridurre rumore informativo
- aumentare qualità suggerimenti
- controllare le notifiche
- migliorare l'esperienza utente

senza modificare il motore di Matching.

Questa tabella costituisce il livello di configurazione personale dell'intero sistema intelligente di CollectorVerse.

---

# Tabella: matching_interactions

## Scopo

Rappresenta le interazioni effettuate dagli utenti sulle opportunità generate dal sistema di Matching.

Questa tabella permette di registrare:

- visualizzazioni
- aperture
- interessi
- contatti
- ignorati
- conversioni

e costituisce il principale strumento di apprendimento del motore di Matching.

---

## Tipo Tabella

Principale

---

## Nome Tabella

matching_interactions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco interazione |
| matching_opportunity_id | UUID | SI | Opportunità coinvolta |
| user_id | UUID | SI | Utente che esegue l'azione |
| interaction_type | VARCHAR(30) | SI | Tipo interazione |
| interaction_score | INTEGER | SI | Punteggio rilevanza |
| notes | TEXT | NO | Note aggiuntive |
| created_at | TIMESTAMPTZ | SI | Data interazione |

---

## Valori Predefiniti

interaction_score = 0

---

## Valori Consentiti

### interaction_type

```text
viewed

opened

favorited

contacted

offer_created

accepted

dismissed

ignored
```

---

## Significato Interazioni

### viewed

L'opportunità è stata visualizzata.

---

### opened

L'utente ha aperto il dettaglio.

---

### favorited

L'utente ha aggiunto ai preferiti.

---

### contacted

L'utente ha contattato la controparte.

---

### offer_created

L'utente ha creato un'offerta.

---

### accepted

L'utente ha accettato l'opportunità.

---

### dismissed

L'opportunità è stata esplicitamente rifiutata.

---

### ignored

L'opportunità è stata ignorata.

---

## Foreign Keys

matching_opportunity_id

→ matching_opportunities.id

---

user_id

→ users.id

---

## Relazioni

matching_opportunities (1)

↓

(N)

matching_interactions

---

users (1)

↓

(N)

matching_interactions

---

## Vincoli

matching_opportunity_id deve esistere.

user_id deve esistere.

interaction_type deve contenere un valore valido.

interaction_score deve essere compreso tra:

```text
-100

e

100
```

---

## Indici

PRIMARY KEY (id)

INDEX (matching_opportunity_id)

INDEX (user_id)

INDEX (interaction_type)

INDEX (created_at)

---

## Regole Business

Una opportunità può generare molte interazioni.

Le interazioni non devono essere cancellate.

Le interazioni costituiscono dati storici e analitici.

---

## Punteggio Interazione

Il punteggio rappresenta il valore dell'azione per il sistema.

---

### Esempio Configurazione

```text
viewed = 5

opened = 10

favorited = 20

contacted = 40

offer_created = 70

accepted = 100

dismissed = -25

ignored = -10
```

---

## Compatibilità Matching

Le interazioni vengono utilizzate per migliorare:

```text
Match Score

Raccomandazioni

Prioritizzazione Risultati
```

---

## Esempio

Utente:

```text
Visualizza sempre Match Pokémon
```

---

Sistema:

```text
Aumenta priorità Pokémon
```

---

## Compatibilità Marketplace

Interazioni positive verso:

```text
Marketplace Match
```

possono migliorare:

```text
Suggerimenti Futuri
```

---

## Compatibilità Wishlist

Se l'utente interagisce spesso con:

```text
Carte Gradate
```

↓

Il Matching può privilegiare:

```text
Carte Gradate
```

nelle opportunità successive.

---

## Compatibilità Notifiche

Le interazioni consentono al sistema di capire:

```text
Quali notifiche funzionano

Quali notifiche vengono ignorate
```

---

## Compatibilità Gamification

Le interazioni possono contribuire a:

```text
Achievement

CollectorScore

Badges
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Match Visualizzati

Match Aperti

Match Ignorati

Match Convertiti

Tasso Conversione

Interesse per Categoria
```

---

## Compatibilità Dashboard Utente

L'utente può visualizzare:

```text
Storico Match

Storico Opportunità

Storico Interazioni
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Analizzare

Aggregare

Studiare

Ottimizzare
```

il comportamento del sistema Matching.

---

## Esempio Logico

matching_opportunity

↓

Charizard Gold

↓

matching_interaction

↓

viewed

↓

opened

↓

contacted

↓

offer_created

---

matching_opportunity

↓

Umbreon Gold Star

↓

matching_interaction

↓

viewed

↓

dismissed

---

## Motivazione Architetturale

La separazione tra:

```text
matching_opportunities
```

e

```text
matching_interactions
```

consente di misurare il comportamento reale degli utenti senza modificare le opportunità originali.

Questo approccio permette:

- apprendimento del sistema
- statistiche avanzate
- ottimizzazione algoritmi
- raccomandazioni personalizzate
- analisi conversioni

e costituisce la base per l'evoluzione futura del motore intelligente di CollectorVerse.

---

