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

Le recensioni consentono alla community di valutare:

- affidabilità
- correttezza
- qualità della comunicazione
- esperienza complessiva

Le recensioni possono essere lasciate esclusivamente tra utenti che hanno effettivamente interagito tramite una conversazione sulla piattaforma.

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
| id | UUID | SI | Identificativo recensione |
| reviewer_user_id | UUID | SI | Utente autore recensione |
| reviewed_user_id | UUID | SI | Utente recensito |
| conversation_thread_id | UUID | SI | Conversazione che abilita la recensione |
| rating | INTEGER | SI | Valutazione |
| review_text | TEXT | NO | Testo recensione |
| is_visible | BOOLEAN | SI | Visibilità recensione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_visible = TRUE

---

## Valori Consentiti

### rating

```text
1

2

3

4

5
```

---

## Significato Valutazioni

### 1

Esperienza molto negativa.

---

### 2

Esperienza negativa.

---

### 3

Esperienza neutra.

---

### 4

Esperienza positiva.

---

### 5

Esperienza eccellente.

---

## Foreign Keys

reviewer_user_id

→ users.id

---

reviewed_user_id

→ users.id

---

conversation_thread_id

→ conversation_threads.id

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

conversation_threads (1)

↓

(N)

user_reviews

---

## Vincoli

reviewer_user_id deve esistere.

reviewed_user_id deve esistere.

conversation_thread_id deve esistere.

rating deve essere compreso tra:

```text
1

e

5
```

---

## Vincolo Anti-Autorecensione

Non è consentito:

```text
reviewer_user_id

=

reviewed_user_id
```

---

## Vincolo Conversazione

L'utente recensore e l'utente recensito devono essere partecipanti della Conversazione indicata.

La conversazione deve esistere.

Non è consentito recensire utenti con cui non è mai esistita una conversazione.

---

## Vincolo Anti-Duplicato

Un utente può possedere una sola recensione verso uno specifico utente.

```text
UNIQUE
(
reviewer_user_id,
reviewed_user_id
)
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (reviewer_user_id, reviewed_user_id)

INDEX (reviewer_user_id)

INDEX (reviewed_user_id)

INDEX (conversation_thread_id)

INDEX (rating)

INDEX (is_visible)

INDEX (created_at)

---

## Regole Business

Le recensioni contribuiscono alla reputazione dell'utente.

Le recensioni archiviate devono rimanere nello storico.

Le recensioni possono essere moderate dagli amministratori.

---

## Aggiornamento Recensione

Se un utente tenta di recensire nuovamente lo stesso utente:

```text
NON viene creato un nuovo record.
```

---

Il sistema deve aggiornare il record esistente.

Devono essere aggiornati:

```text
rating

review_text

updated_at

conversation_thread_id
```

---

## Compatibilità Marketplace

Le recensioni possono nascere da conversazioni originate da annunci Marketplace.

---

## Compatibilità Matching

Le recensioni possono nascere da conversazioni originate da opportunità di Matching.

---

## Compatibilità Messaggistica

La Conversazione rappresenta la prova dell'effettiva interazione tra gli utenti.

---

## Compatibilità User Scores

Le recensioni contribuiscono al calcolo di:

```text
reputation_score
```

presente in:

```text
user_scores
```

---

## Compatibilità Profilo Utente

Il profilo può mostrare:

```text
Media Recensioni

Numero Recensioni

Ultime Recensioni
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Nascondere

Ripristinare
```

recensioni abusive.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Media Recensioni

Numero Recensioni

Distribuzione Voti

Migliori Utenti

Utenti Più Recensiti
```

---

## Esempio Logico

Conversation Thread

↓

Marketplace

↓

Utente A

↓

Utente B

↓

Recensione

↓

5 Stelle

↓

"Eccellente comunicazione"

---

## Motivazione Architetturale

La recensione è consentita soltanto dopo una reale interazione documentata tramite Conversazione.

Questo approccio:

- riduce recensioni false
- aumenta affidabilità
- migliora reputazione
- protegge gli utenti

e costituisce la base del sistema di fiducia di CollectorVerse.

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

Rappresenta le immagini ufficiali e comunitarie associate al Catalogo Universale.

Le immagini vengono utilizzate da:

- Catalogo Universale
- Scanner
- Marketplace
- Wishlist
- Collezioni Personali
- Catalogo Collaborativo
- Matching

Questa tabella definisce il ruolo catalografico dell'immagine.

Il file fisico viene gestito dalla tabella:

```text
media_files
```

---

## Regola Fondamentale

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
| id | UUID | SI | Identificativo immagine catalogo |
| media_file_id | UUID | SI | File immagine associato |
| item_version_id | UUID | NO | Versione associata |
| item_variant_id | UUID | NO | Variante associata |
| image_url | TEXT | NO | URL compatibilità legacy |
| image_type | VARCHAR(50) | SI | Tipologia immagine |
| is_official | BOOLEAN | SI | Immagine ufficiale |
| is_active | BOOLEAN | SI | Immagine utilizzabile |
| width | INTEGER | NO | Larghezza immagine |
| height | INTEGER | NO | Altezza immagine |
| file_size_bytes | BIGINT | NO | Dimensione file |
| image_hash | VARCHAR(255) | NO | Hash immagine |
| ai_score | NUMERIC(5,2) | NO | Valutazione AI |
| community_score | NUMERIC(5,2) | NO | Valutazione community |
| usage_score | NUMERIC(5,2) | NO | Frequenza utilizzo |
| total_score | NUMERIC(5,2) | NO | Punteggio totale |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
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

media_file_id

→ media_files.id

---

item_version_id

→ item_versions.id

---

item_variant_id

→ item_variants.id

---

## Relazioni

media_files (1)

↓

(N)

catalog_images

---

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

---

## Regola XOR

```text
item_version_id IS NOT NULL

XOR

item_variant_id IS NOT NULL
```

---

## Vincoli

media_file_id deve esistere.

image_type deve contenere un valore valido.

is_official deve avere un valore.

is_active deve avere un valore.

width deve essere maggiore di zero se valorizzato.

height deve essere maggiore di zero se valorizzato.

file_size_bytes deve essere maggiore di zero se valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (media_file_id)

INDEX (item_version_id)

INDEX (item_variant_id)

INDEX (is_official)

INDEX (is_active)

INDEX (total_score)

INDEX (image_hash)

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

```text
Hash Matching

OCR Support

AI Recognition
```

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

Le immagini possono essere:

```text
Revisionate

Segnalate

Disattivate

Archiviate
```

attraverso:

```text
media_files
```

e i sistemi di moderazione.

---

## Evoluzione Architetturale

Il campo:

```text
image_url
```

rimane disponibile per compatibilità applicativa.

La sorgente ufficiale del file è:

```text
media_file_id
```

tramite:

```text
media_files
```

---

## Esempio Logico

Item Variant

↓

Charizard Gold

↓

Catalog Image

↓

media_file

↓

charizard_gold_front.jpg

↓

front

↓

official

---

## Motivazione Architetturale

La separazione tra:

```text
catalog_images
```

e

```text
media_files
```

consente di mantenere distinto:

- il file fisico
- l'utilizzo catalografico

Questo approccio:

- elimina duplicazioni
- migliora la moderazione
- migliora lo storage
- migliora lo Scanner
- migliora il Catalogo

e supporta la crescita futura della piattaforma.

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

Offerta economica.

---

### trade

Proposta di scambio.

---

### purchase_trade

Proposta composta da:

```text
Scambio

+

Importo Economico
```

---

## Significato Status

### pending

Offerta in attesa di risposta.

---

### accepted

Offerta accettata.

---

### rejected

Offerta rifiutata.

---

### cancelled

Offerta annullata.

---

### expired

Offerta scaduta.

---

### countered

Controproposta effettuata.

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

### Non Consentito

```text
seller_user_id

=

buyer_user_id
```

---

## Vincolo Offerta Accettata

Per ogni Annuncio Marketplace:

```text
Può esistere una sola Offerta con:

status = accepted
```

---

## Vincolo Logico PostgreSQL

Per ogni:

```text
marketplace_listing_id
```

può esistere una sola Offerta Accettata.

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

gli oggetti proposti vengono gestiti tramite:

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

Oggetti Proposti
```

---

## Accettazione Offerta

Quando una Offerta viene impostata come:

```text
accepted
```

tutte le altre offerte attive dello stesso annuncio devono essere automaticamente aggiornate a:

```text
rejected
```

oppure:

```text
cancelled
```

secondo le regole applicative.

---

## Compatibilità Marketplace

Le offerte costituiscono il nucleo delle trattative.

---

## Compatibilità Matching

Le offerte vengono utilizzate per identificare:

```text
Interessi Reali

Possibili Scambi

Conversioni Marketplace
```

---

## Compatibilità Notifiche

Possono essere generate notifiche per:

```text
Nuova Offerta

Offerta Accettata

Offerta Rifiutata

Controproposta

Scadenza Offerta
```

---

## Compatibilità Messaggistica

La creazione di un'offerta può essere collegata ad una Conversazione.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Offerte

Tasso Accettazione

Tasso Rifiuto

Tempo Medio Risposta

Valore Medio Offerte
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

↓

Tutte le altre offerte

↓

Rejected

---

Marketplace Listing

↓

Umbreon Gold Star

↓

Marketplace Offer

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

consente di gestire trattative multiple mantenendo una sola conclusione valida per ogni annuncio.

Questo approccio:

- evita conflitti
- evita vendite multiple dello stesso oggetto
- migliora la coerenza dei dati
- semplifica la gestione Marketplace

e costituisce il motore delle negoziazioni di CollectorVerse.

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

# Parte 6 - Catalogo Collaborativo

# Tabella: catalog_contributions

## Scopo

Rappresenta una proposta di modifica o aggiunta al Catalogo Universale effettuata da un utente.

La tabella costituisce il punto centrale del Catalogo Collaborativo.

Attraverso questa tabella gli utenti possono proporre:

- Nuove Collezioni
- Nuove Serie
- Nuovi Item
- Nuove Versioni
- Nuove Varianti
- Nuove Rarità
- Nuove Immagini
- Correzioni Catalogo

---

## Tipo Tabella

Principale

---

## Nome Tabella

catalog_contributions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco contributo |
| contributor_user_id | UUID | SI | Utente autore proposta |
| contribution_type | VARCHAR(50) | SI | Tipologia contributo |
| status | VARCHAR(30) | SI | Stato contributo |
| title | VARCHAR(255) | SI | Titolo proposta |
| description | TEXT | SI | Descrizione dettagliata |
| target_table | VARCHAR(100) | NO | Tabella catalogo interessata |
| target_record_id | UUID | NO | Record coinvolto |
| reviewed_by_user_id | UUID | NO | Revisore amministratore |
| reviewed_at | TIMESTAMPTZ | NO | Data revisione |
| review_notes | TEXT | NO | Note revisione |
| approved_at | TIMESTAMPTZ | NO | Data approvazione |
| rejected_at | TIMESTAMPTZ | NO | Data rifiuto |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = pending

---

## Valori Consentiti

### contribution_type

```text
new_collection

new_series

new_item

new_version

new_variant

new_rarity

new_image

correction
```

---

### status

```text
pending

under_review

approved

rejected

implemented

archived
```

---

## Significato Stati

### pending

Proposta ricevuta.

In attesa di revisione.

---

### under_review

Proposta in fase di analisi.

---

### approved

Proposta approvata.

---

### rejected

Proposta rifiutata.

---

### implemented

Implementata nel Catalogo Universale.

---

### archived

Archiviata.

---

## Foreign Keys

contributor_user_id

→ users.id

---

reviewed_by_user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

catalog_contributions

(autore)

---

users (1)

↓

(N)

catalog_contributions

(revisore)

---

catalog_contributions (1)

↓

(N)

catalog_contribution_votes

(Futuro)

---

catalog_contributions (1)

↓

(N)

catalog_contribution_attachments

(Futuro)

---

## Vincoli

contributor_user_id deve esistere.

title non può essere vuoto.

description non può essere vuota.

contribution_type deve contenere un valore valido.

status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (contributor_user_id)

INDEX (reviewed_by_user_id)

INDEX (contribution_type)

INDEX (status)

INDEX (created_at)

---

## Regole Business

Ogni contributo appartiene ad un solo utente.

Un utente può creare molti contributi.

Ogni contributo deve essere revisionato prima di modificare il Catalogo Universale.

---

## Esempio Nuovo Item

Utente:

```text
Propone Charizard Crystal
```

↓

Tipo:

```text
new_item
```

↓

Status:

```text
pending
```

---

## Esempio Nuova Variante

Utente:

```text
Propone Variante Error Print
```

↓

Tipo:

```text
new_variant
```

---

## Esempio Correzione

Utente:

```text
Segnala Numero Catalogo Errato
```

↓

Tipo:

```text
correction
```

---

## Workflow Standard

```text
Utente

↓

Catalog Contribution

↓

Pending

↓

Under Review

↓

Approved

↓

Implemented

↓

Catalogo Universale
```

---

## Workflow Rifiuto

```text
Utente

↓

Catalog Contribution

↓

Pending

↓

Under Review

↓

Rejected
```

---

## Compatibilità Catalogo Universale

Le modifiche approvate possono generare:

```text
Nuove Serie

Nuovi Item

Nuove Versioni

Nuove Varianti

Nuove Rarità

Nuove Immagini
```

---

## Compatibilità Gamification

I contributi possono assegnare:

```text
CollectorScore

Badge

Achievement

Livelli Community
```

---

## Compatibilità Notifiche

L'utente può ricevere notifiche per:

```text
Contributo Approvato

Contributo Rifiutato

Richiesta Informazioni

Implementazione Avvenuta
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Revisionare

Approvare

Rifiutare

Implementare

Archiviare
```

i contributi.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Contributi

Contributi Approvati

Contributi Rifiutati

Tempo Medio Revisione

Utenti Più Attivi
```

---

## Esempio Logico

Catalog Contribution

↓

New Item

↓

Charizard Crystal

↓

Pending

↓

Approved

↓

Implemented

↓

Items

---

Catalog Contribution

↓

Correction

↓

Numero Catalogo Errato

↓

Pending

↓

Rejected

---

## Motivazione Architetturale

La separazione tra:

```text
Catalogo Universale
```

e

```text
Catalog Contributions
```

garantisce che nessun utente possa modificare direttamente i dati ufficiali.

Questo approccio consente:

- crescita collaborativa
- controllo qualità
- moderazione
- audit storico
- gamification della community

senza compromettere l'integrità del Catalogo Universale.

La tabella costituisce il punto centrale dell'intero sistema di Catalogo Collaborativo.

---

# Tabella: catalog_contribution_attachments

## Scopo

Rappresenta gli allegati associati ad un contributo del Catalogo Collaborativo.

Gli allegati consentono agli utenti di fornire prove, documentazione e materiale di supporto per facilitare la revisione delle proposte.

La tabella viene utilizzata per:

- immagini
- fotografie
- scansioni
- documentazione
- riferimenti catalografici
- prove di autenticità
- esempi visivi

---

## Tipo Tabella

Principale

---

## Nome Tabella

catalog_contribution_attachments

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco allegato |
| catalog_contribution_id | UUID | SI | Contributo associato |
| attachment_type | VARCHAR(30) | SI | Tipologia allegato |
| file_url | TEXT | SI | URL file |
| file_name | VARCHAR(255) | SI | Nome file originale |
| file_size_bytes | BIGINT | NO | Dimensione file |
| mime_type | VARCHAR(100) | NO | Tipo file |
| image_width | INTEGER | NO | Larghezza immagine |
| image_height | INTEGER | NO | Altezza immagine |
| description | TEXT | NO | Descrizione allegato |
| is_primary | BOOLEAN | SI | Allegato principale |
| created_at | TIMESTAMPTZ | SI | Data caricamento |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_primary = FALSE

---

## Valori Consentiti

### attachment_type

```text
image

scan

document

reference

proof

other
```

---

## Significato Tipologie

### image

Fotografia o immagine generica.

---

### scan

Scansione ad alta qualità.

---

### document

Documento allegato.

---

### reference

Materiale di riferimento esterno.

---

### proof

Prova di autenticità o esistenza.

---

### other

Tipologia non classificata.

---

## Foreign Keys

catalog_contribution_id

→ catalog_contributions.id

---

## Relazioni

catalog_contributions (1)

↓

(N)

catalog_contribution_attachments

---

## Vincoli

catalog_contribution_id deve esistere.

file_url non può essere vuoto.

file_name non può essere vuoto.

file_size_bytes deve essere maggiore di zero se valorizzato.

image_width deve essere maggiore di zero se valorizzato.

image_height deve essere maggiore di zero se valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (catalog_contribution_id)

INDEX (attachment_type)

INDEX (is_primary)

INDEX (created_at)

---

## Regole Business

Un contributo può avere:

```text
Nessun Allegato

Uno

Molti Allegati
```

---

Ogni allegato appartiene ad un solo contributo.

---

## Allegato Principale

Per ogni contributo può esistere un solo allegato con:

```text
is_primary = TRUE
```

---

## Vincolo Logico

```text
Per ogni catalog_contribution:

Può esistere un solo allegato principale.
```

---

## Esempio Nuovo Item

Contributo:

```text
Nuovo Item

↓

Charizard Crystal
```

---

Allegati:

```text
Foto Fronte

Foto Retro

Scansione Alta Risoluzione
```

---

## Esempio Nuova Variante

Contributo:

```text
Nuova Variante

↓

Error Print
```

---

Allegati:

```text
Foto Errore

Dettaglio Errore

Confronto Versione Standard
```

---

## Esempio Correzione Catalogo

Contributo:

```text
Numero Catalogo Errato
```

---

Allegato:

```text
Pagina Catalogo Ufficiale
```

---

## Compatibilità Revisione

I revisori devono poter visualizzare tutti gli allegati associati ad una proposta.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Scaricare

Moderare

Rifiutare

Archiviare
```

gli allegati.

---

## Compatibilità Catalogo Collaborativo

Gli allegati costituiscono il materiale di supporto per:

```text
Nuove Collezioni

Nuove Serie

Nuovi Item

Nuove Versioni

Nuove Varianti

Nuove Rarità

Nuove Immagini

Correzioni
```

---

## Compatibilità Moderazione

Gli allegati devono poter essere:

```text
Revisionati

Segnalati

Rimossi

Archiviati
```

in caso di contenuti non conformi.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Allegati

Numero Immagini

Numero Documenti

Dimensione Totale Archiviata

Contributi con Allegati
```

---

## Esempio Logico

Catalog Contribution

↓

New Item

↓

Charizard Crystal

↓

catalog_contribution_attachments

↓

front.jpg

back.jpg

scan.png

---

Catalog Contribution

↓

Correction

↓

Numero Catalogo

↓

catalog_contribution_attachments

↓

reference.pdf

---

## Motivazione Architetturale

La separazione tra:

```text
catalog_contributions
```

e

```text
catalog_contribution_attachments
```

consente:

- più allegati per proposta
- prove documentali
- audit completo
- moderazione indipendente
- gestione immagini e documenti

senza appesantire il record principale del contributo.

Questa tabella costituisce il sistema di supporto documentale del Catalogo Collaborativo e garantisce una revisione più accurata e trasparente delle proposte della community.

---

# Tabella: catalog_contribution_votes

## Scopo

Rappresenta il voto espresso da un utente nei confronti di una proposta del Catalogo Collaborativo.

La tabella viene utilizzata per raccogliere il parere della community prima della decisione finale degli amministratori.

I voti della community NON modificano automaticamente il Catalogo Universale.

Costituiscono un supporto al processo decisionale.

---

## Tipo Tabella

Principale

---

## Nome Tabella

catalog_contribution_votes

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco voto |
| catalog_contribution_id | UUID | SI | Contributo votato |
| user_id | UUID | SI | Utente votante |
| vote_type | VARCHAR(20) | SI | Tipo voto |
| rejection_reason | TEXT | NO | Motivazione del voto negativo |
| created_at | TIMESTAMPTZ | SI | Data voto |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Consentiti

### vote_type

```text
approve

reject

unknown
```

---

## Significato Voti

### approve

L'utente ritiene che la proposta sia corretta e debba essere approvata.

---

### reject

L'utente ritiene che la proposta presenti problemi o non debba essere approvata.

L'utente può inserire una motivazione.

---

### unknown

L'utente non possiede informazioni sufficienti per esprimere un giudizio.

Questo voto consente alla community di segnalare interesse verso la proposta senza influenzare positivamente o negativamente il risultato.

---

## Foreign Keys

catalog_contribution_id

→ catalog_contributions.id

---

user_id

→ users.id

---

## Relazioni

catalog_contributions (1)

↓

(N)

catalog_contribution_votes

---

users (1)

↓

(N)

catalog_contribution_votes

---

## Vincoli

catalog_contribution_id deve esistere.

user_id deve esistere.

vote_type deve contenere un valore valido.

---

## Vincolo Anti-Duplicato

Lo stesso utente può votare una sola volta per lo stesso contributo.

---

### Non consentito

```text
Utente A

↓

Contributo 123

↓

Approve
```

---

e successivamente:

```text
Utente A

↓

Contributo 123

↓

Approve
```

---

## Indici

PRIMARY KEY (id)

INDEX (catalog_contribution_id)

INDEX (user_id)

INDEX (vote_type)

INDEX (created_at)

UNIQUE (catalog_contribution_id, user_id)

---

## Regole Business

Un voto appartiene ad un singolo contributo.

Un utente può votare molti contributi.

Un contributo può ricevere molti voti.

---

## Motivazione Voto Negativo

Quando il voto è:

```text
reject
```

l'utente può inserire una motivazione facoltativa.

---

### Esempi

```text
Oggetto già presente nel catalogo.
```

---

```text
Numero catalogo errato.
```

---

```text
Le immagini caricate non sono sufficienti.
```

---

```text
Informazioni non verificabili.
```

---

## Modifica Voto

L'utente può modificare il proprio voto.

In questo caso:

```text
viene aggiornato il record esistente
```

e

```text
updated_at
```

viene aggiornato.

---

## Compatibilità Catalogo Collaborativo

I voti vengono mostrati all'interno della proposta.

---

### Esempio

```text
Approve = 37

Reject = 4

Unknown = 12
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter visualizzare:

```text
Numero Approve

Numero Reject

Numero Unknown

Motivazioni Reject
```

prima della decisione finale.

---

## Compatibilità Gamification

La partecipazione alle votazioni può contribuire a:

```text
CollectorScore

Badge Community

Achievement Collaborazione
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Voti Espressi

Numero Approve

Numero Reject

Numero Unknown

Tasso Partecipazione

Contributi Più Votati
```

---

## Esempio Logico

Catalog Contribution

↓

Nuovo Item

↓

Charizard Crystal

↓

Catalog Contribution Votes

↓

Approve

Approve

Approve

Reject
(Motivazione: Item già presente)

Unknown

↓

Supporto Decisione Admin

---

## Motivazione Architetturale

La separazione tra:

```text
catalog_contributions
```

e

```text
catalog_contribution_votes
```

consente di raccogliere il consenso della community senza modificare direttamente il Catalogo Universale.

L'introduzione del voto:

```text
unknown
```

riduce i voti casuali o forzati da parte degli utenti meno esperti.

La motivazione opzionale per:

```text
reject
```

fornisce contesto utile ai revisori e migliora la qualità del processo collaborativo.

Questa tabella costituisce il sistema di validazione sociale del Catalogo Collaborativo CollectorVerse.

---

# Parte 7 - Scanner

# Tabella: scan_sessions

## Scopo

Rappresenta una singola scansione effettuata da un utente.

Una Sessione di Scansione corrisponde ad una singola immagine inviata al sistema di riconoscimento.

L'immagine può provenire da:

- Fotocamera
- Upload Manuale

Il sistema analizzerà l'immagine e produrrà uno o più risultati possibili.

---

## Tipo Tabella

Principale

---

## Nome Tabella

scan_sessions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco sessione |
| user_id | UUID | SI | Proprietario sessione |
| source_image_url | TEXT | SI | Immagine analizzata |
| status | VARCHAR(30) | SI | Stato scansione |
| scan_source | VARCHAR(30) | SI | Origine immagine |
| total_matches | INTEGER | SI | Numero risultati trovati |
| ai_confidence | NUMERIC(5,2) | NO | Affidabilità generale |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| completed_at | TIMESTAMPTZ | NO | Data completamento |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

status = processing

total_matches = 0

---

## Valori Consentiti

### status

```text
processing

completed

partial_match

no_match

failed

cancelled
```

---

### scan_source

```text
camera

upload
```

---

## Significato Status

### processing

Scansione in elaborazione.

---

### completed

Riconoscimento completato.

Il sistema ha individuato almeno un risultato valido.

---

### partial_match

Il sistema ha trovato risultati plausibili ma richiede conferma utente.

---

### no_match

Nessuna corrispondenza trovata.

---

### failed

Errore tecnico.

---

### cancelled

Scansione annullata.

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

scan_sessions

---

scan_sessions (1)

↓

(N)

scan_results

---

## Vincoli

user_id deve esistere.

source_image_url non può essere vuoto.

status deve contenere un valore valido.

scan_source deve contenere un valore valido.

total_matches deve essere maggiore o uguale a zero.

ai_confidence deve essere compreso tra:

```text
0

e

100
```

se valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (status)

INDEX (scan_source)

INDEX (created_at)

INDEX (completed_at)

---

## Regole Business

Ogni Sessione di Scansione appartiene ad un solo utente.

Ogni Sessione utilizza una sola immagine.

Una Sessione può produrre:

```text
Nessun Risultato

Uno

Molti Risultati Possibili
```

---

## Esempio Match Perfetto

Utente

↓

Carica Immagine

↓

Charizard Gold

↓

Match 99%

↓

completed

---

## Esempio Match Parziale

Utente

↓

Carica Immagine

↓

Possibili Risultati

↓

Charizard Gold

95%

↓

Charizard Reverse

82%

↓

partial_match

---

## Esempio Nessun Match

Utente

↓

Carica Immagine

↓

Nessun Risultato

↓

no_match

---

## Compatibilità Catalogo Universale

Le scansioni possono identificare:

```text
Item

Versione

Variante
```

---

## Compatibilità Collezioni Personali

Dopo la conferma dell'utente:

```text
scan_session
```

↓

```text
scan_result
```

↓

```text
user_items
```

---

## Compatibilità Catalogo Collaborativo

Se il sistema restituisce:

```text
no_match
```

l'utente può proporre:

```text
Nuovo Item

Nuova Versione

Nuova Variante
```

tramite Catalogo Collaborativo.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Scansioni

Numero Match

Numero No Match

Precisione Scanner

Tempo Medio Elaborazione
```

---

## Compatibilità Gamification

Le scansioni possono contribuire a:

```text
CollectorScore

Achievement

Livelli Scanner
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Analizzare

Monitorare
```

l'utilizzo dello Scanner.

---

## Esempio Logico

Utente

↓

scan_session

↓

source_image_url

↓

Charizard.jpg

↓

completed

↓

scan_results

↓

Charizard Gold

98%

---

## Motivazione Architetturale

Una Sessione di Scansione rappresenta un singolo tentativo di riconoscimento.

La separazione tra:

```text
scan_sessions
```

e

```text
scan_results
```

consente:

- storico scansioni
- audit
- statistiche
- miglioramento AI
- supporto OCR

senza duplicare dati del Catalogo Universale.

La tabella costituisce il punto di ingresso dell'intero sistema Scanner CollectorVerse.

---

# Tabella: scan_results

## Scopo

Rappresenta un possibile risultato prodotto dal motore di riconoscimento durante una Sessione di Scansione.

Una singola scansione può generare:

```text
0 risultati

1 risultato

N risultati possibili
```

ordinati per affidabilità.

Questa tabella contiene le possibili corrispondenze individuate dal sistema.

---

## Tipo Tabella

Principale

---

## Nome Tabella

scan_results

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco risultato |
| scan_session_id | UUID | SI | Sessione di scansione associata |
| item_id | UUID | SI | Item identificato |
| item_version_id | UUID | NO | Versione identificata |
| item_variant_id | UUID | NO | Variante identificata |
| confidence_score | NUMERIC(5,2) | SI | Livello di affidabilità |
| rank_position | INTEGER | SI | Posizione nel ranking |
| is_selected | BOOLEAN | SI | Risultato scelto dall'utente |
| user_confirmed | BOOLEAN | SI | Conferma esplicita utente |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

is_selected = FALSE

user_confirmed = FALSE

rank_position = 1

---

## Foreign Keys

scan_session_id

→ scan_sessions.id

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

scan_sessions (1)

↓

(N)

scan_results

---

items (1)

↓

(N)

scan_results

---

item_versions (1)

↓

(N)

scan_results

---

item_variants (1)

↓

(N)

scan_results

---

## Vincoli

scan_session_id deve esistere.

item_id deve esistere.

confidence_score deve essere compreso tra:

```text
0

e

100
```

---

rank_position deve essere maggiore di zero.

---

## Vincolo Gerarchico

Se valorizzato:

```text
item_version_id
```

deve appartenere all'Item indicato.

---

Se valorizzato:

```text
item_variant_id
```

deve appartenere alla Versione indicata.

---

## Vincolo Selezione

Per ogni sessione può esistere un solo risultato con:

```text
is_selected = TRUE
```

---

## Indici

PRIMARY KEY (id)

INDEX (scan_session_id)

INDEX (item_id)

INDEX (item_version_id)

INDEX (item_variant_id)

INDEX (confidence_score)

INDEX (rank_position)

INDEX (is_selected)

INDEX (user_confirmed)

---

## Regole Business

Ogni risultato appartiene ad una sola Sessione di Scansione.

Una Sessione può produrre molti risultati.

I risultati devono essere ordinati dal più probabile al meno probabile.

---

## Ranking

Il sistema deve ordinare i risultati utilizzando:

```text
confidence_score
```

in ordine decrescente.

---

### Esempio

```text
Charizard Gold

98.50%
```

↓

Posizione 1

---

```text
Charizard Reverse Holo

85.20%
```

↓

Posizione 2

---

```text
Charizard Japanese

76.10%
```

↓

Posizione 3

---

## Risultato Selezionato

Quando l'utente conferma un risultato:

```text
is_selected = TRUE
```

---

ed eventualmente:

```text
user_confirmed = TRUE
```

---

## Esempio

Scanner:

```text
Charizard Gold

98%
```

---

Utente:

```text
Conferma
```

---

Risultato:

```text
is_selected = TRUE

user_confirmed = TRUE
```

---

## Compatibilità Collezioni Personali

Dopo la conferma:

```text
scan_result
```

↓

```text
user_items
```

↓

Aggiunta Collezione Personale

---

## Compatibilità Catalogo Collaborativo

Se tutti i risultati hanno affidabilità molto bassa:

```text
Possibile Nuovo Item
```

---

Il sistema può suggerire:

```text
Catalog Contribution
```

---

## Compatibilità AI

La tabella viene utilizzata per:

```text
Training Dataset

Miglioramento Algoritmi

Correzione Errori

Monitoraggio Precisione
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Match Corretti

Match Errati

Precisione AI

Risultati Confermati

Risultati Rifiutati
```

---

## Compatibilità Gamification

Le scansioni confermate possono contribuire a:

```text
CollectorScore

Achievement Scanner

Livelli Scanner
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Analizzare

Confrontare

Correggere
```

i risultati generati dal sistema.

---

## Esempio Logico

scan_session

↓

Charizard.jpg

↓

scan_results

↓

1. Charizard Gold
98%

↓

2. Charizard Reverse
85%

↓

3. Charizard Japanese
76%

↓

Utente Conferma

↓

Charizard Gold

---

## Motivazione Architetturale

La separazione tra:

```text
scan_sessions
```

e

```text
scan_results
```

consente di conservare tutte le possibili interpretazioni generate dal motore di riconoscimento.

Questo approccio permette:

- trasparenza del processo
- miglioramento continuo dell'AI
- conferma manuale dell'utente
- statistiche accurate
- audit storico

senza alterare il Catalogo Universale.

La tabella costituisce il nucleo operativo del sistema Scanner CollectorVerse.

---

# Parte 8 - Gamification

# Tabella: user_scores

## Scopo

Rappresenta il profilo di progressione dell'utente all'interno di CollectorVerse.

La tabella centralizza tutte le informazioni principali relative alla crescita dell'utente nella piattaforma.

Questa tabella viene utilizzata per:

- CollectorScore
- Livello Utente
- Esperienza
- Ranking
- Progressione
- Achievement
- Badge
- Classifiche

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_scores

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco punteggio |
| user_id | UUID | SI | Proprietario punteggio |
| collector_score | BIGINT | SI | Punteggio totale CollectorVerse |
| experience_points | BIGINT | SI | Esperienza accumulata |
| current_level | INTEGER | SI | Livello corrente |
| reputation_score | NUMERIC(5,2) | SI | Punteggio reputazione |
| contribution_score | BIGINT | SI | Punteggio contributi catalogo |
| marketplace_score | BIGINT | SI | Punteggio marketplace |
| scanner_score | BIGINT | SI | Punteggio scanner |
| achievement_points | BIGINT | SI | Punti achievement |
| last_level_up_at | TIMESTAMPTZ | NO | Ultimo avanzamento livello |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

collector_score = 0

experience_points = 0

current_level = 1

reputation_score = 0

contribution_score = 0

marketplace_score = 0

scanner_score = 0

achievement_points = 0

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(1)

user_scores

---

user_scores

↓

Influenza

↓

user_badges

(Futuro)

---

user_scores

↓

Influenza

↓

user_achievements

(Futuro)

---

user_scores

↓

Influenza

↓

leaderboards

(Futuro)

---

## Vincoli

user_id deve esistere.

user_id deve essere univoco.

collector_score deve essere maggiore o uguale a zero.

experience_points deve essere maggiore o uguale a zero.

current_level deve essere maggiore di zero.

reputation_score deve essere compreso tra:

```text
0

e

100
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (collector_score)

INDEX (current_level)

INDEX (reputation_score)

INDEX (updated_at)

---

## Regole Business

Ogni utente possiede un solo profilo punteggio.

Il profilo viene creato automaticamente durante la registrazione.

---

## CollectorScore

Il CollectorScore rappresenta il punteggio globale dell'utente.

Può essere influenzato da:

```text
Collezione Personale

Marketplace

Scanner

Catalogo Collaborativo

Achievement

Badge
```

---

## Experience Points

I punti esperienza rappresentano la progressione generale dell'utente.

---

### Esempio

```text
Acquisizione Oggetto

+

Scansione Confermata

+

Contributo Approvato

↓

Esperienza
```

---

## Livelli

I livelli vengono calcolati tramite:

```text
experience_points
```

---

### Esempio

```text
Livello 1

0 XP
```

---

```text
Livello 2

100 XP
```

---

```text
Livello 10

5000 XP
```

---

Le soglie definitive verranno definite nelle regole applicative.

---

## Reputation Score

Misura l'affidabilità dell'utente.

Può essere influenzato da:

```text
Recensioni Positive

Recensioni Negative

Marketplace

Comportamento Community
```

---

## Contribution Score

Punteggio ottenuto tramite:

```text
Catalogo Collaborativo

Proposte Approvate

Voti Community
```

---

## Marketplace Score

Punteggio ottenuto tramite:

```text
Annunci

Offerte

Attività Marketplace
```

---

## Scanner Score

Punteggio ottenuto tramite:

```text
Scansioni

Conferme Scanner

Correzioni AI
```

---

## Achievement Points

Punti assegnati dagli Achievement.

---

## Compatibilità Collezioni Personali

Le attività che possono contribuire al punteggio includono:

```text
Nuovi Oggetti

Nuove Serie Completate

Nuove Collezioni
```

---

## Compatibilità Marketplace

Attività considerate:

```text
Pubblicazione Annunci

Offerte

Interazioni

Partecipazione
```

---

## Compatibilità Matching

Le interazioni positive possono contribuire al punteggio.

---

## Compatibilità Catalogo Collaborativo

Attività considerate:

```text
Contributi

Approvazioni

Partecipazione Community
```

---

## Compatibilità Scanner

Attività considerate:

```text
Scansioni Corrette

Conferme Utente

Miglioramento Dataset
```

---

## Compatibilità Notifiche

I cambi di livello possono generare notifiche:

```text
Level Up

Nuovo Badge

Nuovo Achievement
```

---

## Compatibilità Dashboard Utente

L'utente può visualizzare:

```text
CollectorScore

Livello

Esperienza

Progressione

Ranking
```

---

## Compatibilità Classifiche

Le classifiche possono utilizzare:

```text
CollectorScore

Livello

Experience Points
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Ricalcolare

Correggere

Monitorare
```

i punteggi.

---

## Esempio Logico

Utente

↓

user_scores

↓

CollectorScore = 12500

↓

Level = 18

↓

Reputation = 96

↓

Marketplace Score = 2500

↓

Contribution Score = 1800

---

## Motivazione Architetturale

La separazione tra:

```text
users
```

e

```text
user_scores
```

consente di gestire la progressione senza modificare continuamente il profilo utente.

Questo approccio permette:

- scalabilità
- classifiche
- achievement
- badge
- reputazione
- statistiche avanzate

senza duplicare informazioni nel resto del sistema.

La tabella costituisce il nucleo centrale dell'intero sistema Gamification di CollectorVerse.

---

# Tabella: achievements

## Scopo

Rappresenta il catalogo ufficiale degli Achievement disponibili nella piattaforma CollectorVerse.

Gli Achievement costituiscono obiettivi permanenti che gli utenti possono sbloccare svolgendo attività specifiche.

Questa tabella definisce:

- obiettivo
- descrizione
- requisiti
- punteggio assegnato
- categoria
- livello di difficoltà

Gli Achievement NON appartengono direttamente agli utenti.

L'assegnazione agli utenti verrà gestita nella tabella:

```text
user_achievements
```

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

achievements

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco achievement |
| code | VARCHAR(100) | SI | Codice interno univoco |
| name | VARCHAR(150) | SI | Nome achievement |
| description | TEXT | SI | Descrizione achievement |
| category | VARCHAR(30) | SI | Categoria achievement |
| difficulty | VARCHAR(30) | SI | Livello difficoltà |
| points_reward | INTEGER | SI | Punti assegnati |
| icon_url | TEXT | NO | Icona visualizzata |
| is_hidden | BOOLEAN | SI | Achievement segreto |
| is_active | BOOLEAN | SI | Achievement disponibile |
| sort_order | INTEGER | SI | Ordinamento visualizzazione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

points_reward = 0

is_hidden = FALSE

is_active = TRUE

sort_order = 0

---

## Valori Consentiti

### category

```text
collection

marketplace

scanner

community

matching

milestone

special
```

---

### difficulty

```text
bronze

silver

gold

platinum

legendary
```

---

## Significato Categorie

### collection

Achievement legati alla collezione personale.

---

### marketplace

Achievement legati al Marketplace.

---

### scanner

Achievement legati allo Scanner.

---

### community

Achievement legati alla partecipazione nella Community.

---

### matching

Achievement legati al sistema di Matching.

---

### milestone

Achievement di avanzamento generale.

---

### special

Achievement speciali o eventi temporanei.

---

## Significato Difficoltà

### bronze

Obiettivo semplice.

---

### silver

Obiettivo intermedio.

---

### gold

Obiettivo avanzato.

---

### platinum

Obiettivo molto difficile.

---

### legendary

Achievement raro e prestigioso.

---

## Relazioni

achievements (1)

↓

(N)

user_achievements

(Futuro)

---

## Vincoli

code deve essere univoco.

name deve essere univoco.

points_reward deve essere maggiore o uguale a zero.

sort_order deve essere maggiore o uguale a zero.

category deve contenere un valore valido.

difficulty deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (category)

INDEX (difficulty)

INDEX (is_hidden)

INDEX (is_active)

INDEX (sort_order)

---

## Regole Business

Gli Achievement sono definiti esclusivamente dagli amministratori.

Gli utenti non possono creare Achievement.

---

## Achievement Segreti

Se:

```text
is_hidden = TRUE
```

l'Achievement non deve essere visibile fino allo sblocco.

---

### Esempio

```text
Collezionista Leggendario
```

↓

Visibile solo dopo il completamento.

---

## Esempi Collection

```text
Primo Oggetto

Possiedi il primo oggetto.
```

---

```text
Collezionista Pokémon

Possiedi 100 oggetti Pokémon.
```

---

```text
Completista

Completa una Serie.
```

---

## Esempi Marketplace

```text
Primo Annuncio

Pubblica il primo annuncio.
```

---

```text
Mercante Attivo

Pubblica 100 annunci.
```

---

## Esempi Scanner

```text
Prima Scansione

Completa la prima scansione.
```

---

```text
Scanner Esperto

Completa 1000 scansioni.
```

---

## Esempi Community

```text
Primo Contributo

Invia una proposta catalogo.
```

---

```text
Curatore Community

Ottieni 50 contributi approvati.
```

---

## Compatibilità User Scores

Gli Achievement assegnano punti utilizzati per:

```text
CollectorScore

Experience Points

Progressione Utente
```

---

## Compatibilità Gamification

Gli Achievement possono sbloccare:

```text
Badge

Titoli

Cornici Profilo

Ricompense Speciali
```

---

## Compatibilità Notifiche

Lo sblocco di un Achievement può generare:

```text
Notifica

Animazione

Messaggio di Congratulazioni
```

---

## Compatibilità Dashboard Utente

Gli utenti devono poter vedere:

```text
Achievement Ottenuti

Achievement Mancanti

Progressione Achievement
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Disattivare

Riordinare
```

gli Achievement senza modificare il codice applicativo.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Achievement Più Ottenuti

Achievement Più Rari

Percentuale Completamento

Distribuzione Difficoltà
```

---

## Esempio Logico

Achievement

↓

Primo Oggetto

↓

Category

Collection

↓

Difficulty

Bronze

↓

Reward

50 Punti

---

Achievement

↓

Scanner Master

↓

Category

Scanner

↓

Difficulty

Gold

↓

Reward

1000 Punti

---

## Motivazione Architetturale

La separazione tra:

```text
achievements
```

e

```text
user_achievements
```

consente di mantenere un catalogo centrale degli obiettivi senza duplicare informazioni sugli utenti.

Questo approccio permette:

- gestione centralizzata
- modifica regole
- statistiche globali
- crescita futura della gamification

senza alterare i dati degli utenti.

La tabella costituisce il catalogo ufficiale degli Achievement di CollectorVerse.

---

# Tabella: user_achievements

## Scopo

Rappresenta gli Achievement ottenuti dagli utenti.

La tabella collega:

```text
Utente
```

e

```text
Achievement
```

registrando:

- stato avanzamento
- data sblocco
- punti ottenuti
- progresso raggiunto

Questa tabella rappresenta lo storico reale della progressione dell'utente nel sistema Gamification.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_achievements

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco assegnazione |
| user_id | UUID | SI | Proprietario achievement |
| achievement_id | UUID | SI | Achievement associato |
| status | VARCHAR(30) | SI | Stato achievement |
| progress_value | INTEGER | SI | Avanzamento corrente |
| target_value | INTEGER | SI | Obiettivo richiesto |
| completion_percentage | NUMERIC(5,2) | SI | Percentuale completamento |
| points_awarded | INTEGER | SI | Punti assegnati |
| unlocked_at | TIMESTAMPTZ | NO | Data sblocco |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

status = in_progress

progress_value = 0

completion_percentage = 0

points_awarded = 0

---

## Valori Consentiti

### status

```text
in_progress

completed

claimed

expired
```

---

## Significato Stati

### in_progress

Achievement in corso.

---

### completed

Achievement completato.

---

### claimed

Ricompensa assegnata all'utente.

---

### expired

Achievement non più ottenibile.

Utilizzato principalmente per eventi speciali.

---

## Foreign Keys

user_id

→ users.id

---

achievement_id

→ achievements.id

---

## Relazioni

users (1)

↓

(N)

user_achievements

---

achievements (1)

↓

(N)

user_achievements

---

## Vincoli

user_id deve esistere.

achievement_id deve esistere.

progress_value deve essere maggiore o uguale a zero.

target_value deve essere maggiore di zero.

completion_percentage deve essere compresa tra:

```text
0

e

100
```

---

points_awarded deve essere maggiore o uguale a zero.

---

## Vincolo Anti-Duplicato

Lo stesso utente può possedere una sola registrazione per ciascun Achievement.

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id, achievement_id)

INDEX (user_id)

INDEX (achievement_id)

INDEX (status)

INDEX (completion_percentage)

INDEX (unlocked_at)

---

## Regole Business

Un Achievement può essere assegnato a molti utenti.

Un utente può ottenere molti Achievement.

---

## Progressione Achievement

Gli Achievement possono essere:

```text
Istantanei
```

oppure

```text
Progressivi
```

---

### Achievement Istantaneo

```text
Primo Oggetto

↓

Possiedi il primo oggetto
```

↓

```text
Completato immediatamente
```

---

### Achievement Progressivo

```text
Collezionista Pokémon

↓

Possiedi 100 oggetti Pokémon
```

---

Esempio:

```text
34 / 100

↓

34%
```

---

## Sblocco Achievement

Quando:

```text
progress_value

=

target_value
```

↓

```text
status = completed
```

↓

```text
unlocked_at valorizzato
```

---

## Assegnazione Punti

Al completamento:

```text
achievement.points_reward
```

↓

```text
points_awarded
```

↓

```text
user_scores
```

---

## Compatibilità User Scores

Gli Achievement contribuiscono a:

```text
CollectorScore

Experience Points

Achievement Points
```

---

## Compatibilità Badge

Gli Achievement possono sbloccare:

```text
Badge

Titoli

Cornici Profilo
```

nelle tabelle successive.

---

## Compatibilità Notifiche

Quando un Achievement viene completato:

```text
Notifica

Animazione

Messaggio Congratulazioni
```

---

## Compatibilità Dashboard Utente

L'utente deve visualizzare:

```text
Achievement Completati

Achievement In Corso

Progressione

Ricompense
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Achievement

Achievement Completati

Achievement Rari

Percentuale Completamento

Punteggio Totale Achievement
```

---

## Compatibilità Gamification

La tabella costituisce uno dei principali generatori di:

```text
CollectorScore

Livelli

Progressione Utente
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Correggere

Ricalcolare

Assegnare

Revocare
```

Achievement in casi eccezionali.

---

## Esempio Logico

Utente

↓

Achievement

↓

Primo Oggetto

↓

Target = 1

↓

Progress = 1

↓

Completed

↓

Unlocked

↓

50 Punti

---

Utente

↓

Achievement

↓

Collezionista Pokémon

↓

Target = 100

↓

Progress = 34

↓

34%

↓

In Progress

---

## Motivazione Architetturale

La separazione tra:

```text
achievements
```

e

```text
user_achievements
```

consente di mantenere un catalogo centrale degli obiettivi e registrare separatamente la progressione dei singoli utenti.

Questo approccio permette:

- tracking avanzato della progressione
- achievement progressivi
- statistiche dettagliate
- notifiche automatiche
- integrazione con livelli e punteggi

senza modificare la definizione originale degli Achievement.

La tabella costituisce il collegamento principale tra gli utenti e il sistema di Achievement di CollectorVerse.

---

# Tabella: badges

## Scopo

Rappresenta il catalogo ufficiale dei Badge disponibili nella piattaforma CollectorVerse.

I Badge sono elementi visivi che identificano risultati, specializzazioni, riconoscimenti e status ottenuti dagli utenti.

A differenza degli Achievement:

```text
Achievement
=
Obiettivo completato

Badge
=
Riconoscimento visuale ottenuto
```

Un Badge può essere ottenuto:

- tramite Achievement
- tramite attività Marketplace
- tramite Catalogo Collaborativo
- tramite eventi speciali
- tramite verifiche amministrative

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

badges

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco badge |
| code | VARCHAR(100) | SI | Codice interno badge |
| name | VARCHAR(150) | SI | Nome badge |
| description | TEXT | SI | Descrizione badge |
| badge_type | VARCHAR(30) | SI | Tipologia badge |
| rarity_level | VARCHAR(30) | SI | Rarità badge |
| icon_url | TEXT | NO | Icona badge |
| color_hex | VARCHAR(20) | NO | Colore rappresentativo |
| is_hidden | BOOLEAN | SI | Badge nascosto |
| is_active | BOOLEAN | SI | Badge attivo |
| sort_order | INTEGER | SI | Ordinamento visualizzazione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

is_hidden = FALSE

is_active = TRUE

sort_order = 0

---

## Valori Consentiti

### badge_type

```text
achievement

collection

marketplace

scanner

community

verification

special
```

---

### rarity_level

```text
common

rare

epic

legendary
```

---

## Significato Badge Type

### achievement

Badge ottenuto tramite Achievement.

---

### collection

Badge ottenuto tramite attività collezionistiche.

---

### marketplace

Badge ottenuto tramite attività Marketplace.

---

### scanner

Badge ottenuto tramite utilizzo Scanner.

---

### community

Badge ottenuto tramite partecipazione Community.

---

### verification

Badge assegnato tramite verifica ufficiale.

---

### special

Badge speciale o evento limitato.

---

## Significato Rarity Level

### common

Badge comune.

---

### rare

Badge raro.

---

### epic

Badge molto raro.

---

### legendary

Badge prestigioso e difficile da ottenere.

---

## Relazioni

badges (1)

↓

(N)

user_badges

(Futuro)

---

## Vincoli

code deve essere univoco.

name deve essere univoco.

badge_type deve contenere un valore valido.

rarity_level deve contenere un valore valido.

sort_order deve essere maggiore o uguale a zero.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (badge_type)

INDEX (rarity_level)

INDEX (is_hidden)

INDEX (is_active)

INDEX (sort_order)

---

## Regole Business

I Badge vengono definiti esclusivamente dagli amministratori.

Gli utenti non possono creare Badge.

---

## Badge Nascosti

Se:

```text
is_hidden = TRUE
```

il Badge non è visibile fino al suo ottenimento.

---

## Esempi Achievement

```text
Primo Oggetto
```

↓

```text
Badge Collezionista Esordiente
```

---

```text
100 Achievement Points
```

↓

```text
Badge Achievement Hunter
```

---

## Esempi Collection

```text
Completamento Serie
```

↓

```text
Badge Completista
```

---

```text
1000 Oggetti Posseduti
```

↓

```text
Badge Mega Collezionista
```

---

## Esempi Marketplace

```text
100 Annunci Pubblicati
```

↓

```text
Badge Mercante Attivo
```

---

## Esempi Scanner

```text
1000 Scansioni Corrette
```

↓

```text
Badge Scanner Master
```

---

## Esempi Community

```text
50 Contributi Approvati
```

↓

```text
Badge Curatore Community
```

---

## Esempi Verification

```text
Merchant Verificato
```

↓

```text
Badge Verified Merchant
```

---

## Compatibilità User Profiles

I Badge possono essere visualizzati nel profilo utente.

---

## Compatibilità Gamification

I Badge rappresentano uno dei principali elementi visuali della progressione.

---

## Compatibilità Notifiche

L'ottenimento di un Badge può generare:

```text
Notifica

Animazione

Messaggio Speciale
```

---

## Compatibilità Dashboard Utente

L'utente può visualizzare:

```text
Badge Ottenuti

Badge Rari

Badge Mancanti

Progressione Badge
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Disattivare

Nascondere

Riordinare
```

i Badge senza modifiche applicative.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Badge Più Ottenuti

Badge Più Rari

Distribuzione Badge

Badge Leggendari
```

---

## Esempio Logico

Badge

↓

Collezionista Esordiente

↓

Collection

↓

Common

---

Badge

↓

Scanner Master

↓

Scanner

↓

Epic

---

Badge

↓

Verified Merchant

↓

Verification

↓

Rare

---

Badge

↓

Legendary Collector

↓

Special

↓

Legendary

---

## Motivazione Architetturale

La separazione tra:

```text
badges
```

e

```text
user_badges
```

consente di mantenere un catalogo centrale dei riconoscimenti visuali senza duplicare dati sugli utenti.

Questo approccio permette:

- gestione centralizzata
- badge dinamici
- eventi speciali
- badge temporanei
- statistiche globali
- espansione futura

senza modificare i profili utente.

La tabella costituisce il catalogo ufficiale dei Badge di CollectorVerse.

---

# Tabella: user_badges

## Scopo

Rappresenta i Badge ottenuti dagli utenti.

La tabella collega:

```text
Utente
```

e

```text
Badge
```

registrando:

- data ottenimento
- origine assegnazione
- stato attivo
- visibilità
- badge in evidenza

Questa tabella costituisce il profilo pubblico dei riconoscimenti ottenuti dall'utente.

---

## Tipo Tabella

Principale

---

## Nome Tabella

user_badges

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco assegnazione badge |
| user_id | UUID | SI | Proprietario badge |
| badge_id | UUID | SI | Badge ottenuto |
| source_type | VARCHAR(30) | SI | Origine assegnazione |
| is_featured | BOOLEAN | SI | Badge in evidenza |
| is_visible | BOOLEAN | SI | Badge visibile nel profilo |
| earned_at | TIMESTAMPTZ | SI | Data ottenimento |
| expires_at | TIMESTAMPTZ | NO | Data scadenza |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

is_featured = FALSE

is_visible = TRUE

---

## Valori Consentiti

### source_type

```text
achievement

marketplace

scanner

community

verification

admin

event
```

---

## Significato Origini

### achievement

Badge ottenuto tramite completamento Achievement.

---

### marketplace

Badge ottenuto tramite attività Marketplace.

---

### scanner

Badge ottenuto tramite Scanner.

---

### community

Badge ottenuto tramite Catalogo Collaborativo o attività Community.

---

### verification

Badge assegnato tramite verifica ufficiale.

---

### admin

Badge assegnato manualmente da amministratori.

---

### event

Badge ottenuto tramite eventi speciali.

---

## Foreign Keys

user_id

→ users.id

---

badge_id

→ badges.id

---

## Relazioni

users (1)

↓

(N)

user_badges

---

badges (1)

↓

(N)

user_badges

---

## Vincoli

user_id deve esistere.

badge_id deve esistere.

source_type deve contenere un valore valido.

---

## Vincolo Anti-Duplicato

Lo stesso utente non può ottenere più volte lo stesso Badge.

---

### Non Consentito

```text
Utente

↓

Badge Scanner Master

↓

Ottenuto
```

---

e successivamente:

```text
Utente

↓

Badge Scanner Master

↓

Nuovo Inserimento
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id, badge_id)

INDEX (user_id)

INDEX (badge_id)

INDEX (source_type)

INDEX (is_featured)

INDEX (is_visible)

INDEX (earned_at)

---

## Regole Business

Un Badge può essere assegnato a molti utenti.

Un utente può ottenere molti Badge.

---

## Badge in Evidenza

Un Badge può essere evidenziato nel profilo utente.

---

### Esempio

Profilo Utente

↓

Badge Visibili

```text
Legendary Collector

Verified Merchant

Scanner Master
```

---

## Vincolo Badge Evidenza

Si consiglia di limitare il numero di Badge in evidenza.

---

### Esempio

```text
Massimo 3 Badge Evidenziati
```

per utente.

---

## Badge Temporanei

Alcuni Badge possono avere una scadenza.

---

### Esempio

```text
Evento Natale 2027
```

↓

```text
expires_at
```

---

## Badge Permanenti

La maggior parte dei Badge non possiede una scadenza.

---

### Esempio

```text
Scanner Master
```

↓

```text
expires_at = NULL
```

---

## Compatibilità User Profiles

I Badge visibili possono essere mostrati nel profilo dell'utente.

---

## Compatibilità User Scores

L'ottenimento di Badge può contribuire a:

```text
CollectorScore

Experience Points

Reputation Score
```

---

## Compatibilità Achievement

Molti Badge possono essere assegnati automaticamente dopo:

```text
Achievement Completato
```

---

### Esempio

Achievement:

```text
Scanner Expert
```

↓

Badge:

```text
Scanner Master
```

---

## Compatibilità Marketplace

Badge visualizzabili in annunci:

```text
Verified Merchant

Mercante Attivo

Top Trader
```

---

## Compatibilità Catalogo Collaborativo

Badge visualizzabili nei contributi:

```text
Curatore Community

Esperto Catalogo

Top Contributor
```

---

## Compatibilità Notifiche

Lo sblocco di un Badge può generare:

```text
Notifica

Animazione

Popup Celebrativo
```

---

## Compatibilità Dashboard Utente

L'utente può visualizzare:

```text
Badge Ottenuti

Badge Rari

Badge In Evidenza

Cronologia Badge
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Assegnare

Revocare

Nascondere

Ripristinare
```

Badge specifici.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Badge Totali

Badge Rari

Badge Leggendari

Distribuzione Badge

Badge Più Ottenuti
```

---

## Esempio Logico

Utente

↓

user_badges

↓

Scanner Master

↓

earned_at

↓

2027-06-15

↓

Visible

---

Utente

↓

user_badges

↓

Verified Merchant

↓

Featured

↓

Visible

---

Utente

↓

user_badges

↓

Evento Natale

↓

Expires At

↓

2028-01-15

---

## Motivazione Architetturale

La separazione tra:

```text
badges
```

e

```text
user_badges
```

consente di mantenere un catalogo centralizzato dei Badge e registrare separatamente quelli effettivamente ottenuti dagli utenti.

Questo approccio permette:

- gestione flessibile
- badge permanenti
- badge temporanei
- badge evento
- badge verificati
- profili personalizzati

senza modificare il catalogo ufficiale dei Badge.

La tabella costituisce il collegamento principale tra i Badge e gli utenti all'interno del sistema Gamification CollectorVerse.

---

# Tabella: leaderboards

## Scopo

Rappresenta il catalogo ufficiale delle Classifiche disponibili nella piattaforma CollectorVerse.

Le classifiche consentono di confrontare gli utenti sulla base di differenti criteri di ranking.

Questa tabella definisce:

- tipologia classifica
- criterio di ordinamento
- stato
- periodicità
- visibilità

Le posizioni effettive degli utenti verranno memorizzate nella tabella:

```text
leaderboard_entries
```

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

leaderboards

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco classifica |
| code | VARCHAR(100) | SI | Codice interno classifica |
| name | VARCHAR(150) | SI | Nome classifica |
| description | TEXT | NO | Descrizione classifica |
| leaderboard_type | VARCHAR(30) | SI | Tipologia classifica |
| scoring_source | VARCHAR(50) | SI | Origine punteggio |
| refresh_frequency | VARCHAR(30) | SI | Frequenza aggiornamento |
| is_global | BOOLEAN | SI | Classifica globale |
| is_public | BOOLEAN | SI | Visibile agli utenti |
| is_active | BOOLEAN | SI | Classifica attiva |
| sort_order | INTEGER | SI | Ordine visualizzazione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

is_global = TRUE

is_public = TRUE

is_active = TRUE

sort_order = 0

refresh_frequency = daily

---

## Valori Consentiti

### leaderboard_type

```text
global

collection

marketplace

scanner

community

achievement

special_event
```

---

### scoring_source

```text
collector_score

experience_points

marketplace_score

scanner_score

contribution_score

achievement_points

reputation_score
```

---

### refresh_frequency

```text
real_time

hourly

daily

weekly

monthly
```

---

## Significato Tipologie

### global

Classifica generale della piattaforma.

---

### collection

Classifica basata sull'attività collezionistica.

---

### marketplace

Classifica relativa al Marketplace.

---

### scanner

Classifica relativa all'utilizzo dello Scanner.

---

### community

Classifica relativa al Catalogo Collaborativo.

---

### achievement

Classifica relativa agli Achievement.

---

### special_event

Classifica creata per eventi limitati nel tempo.

---

## Foreign Keys

Nessuna.

---

## Relazioni

leaderboards (1)

↓

(N)

leaderboard_entries

---

## Vincoli

code deve essere univoco.

name deve essere univoco.

leaderboard_type deve contenere un valore valido.

scoring_source deve contenere un valore valido.

refresh_frequency deve contenere un valore valido.

sort_order deve essere maggiore o uguale a zero.

---

## Indici

PRIMARY KEY (id)

UNIQUE (code)

UNIQUE (name)

INDEX (leaderboard_type)

INDEX (scoring_source)

INDEX (is_active)

INDEX (is_public)

INDEX (sort_order)

---

## Regole Business

Le classifiche sono definite esclusivamente dagli amministratori.

Gli utenti non possono creare classifiche.

---

## Esempi Classifiche

### Collector Score Globale

```text
Code

global_collector_score
```

↓

```text
Scoring Source

collector_score
```

---

### Marketplace Ranking

```text
Code

marketplace_ranking
```

↓

```text
Scoring Source

marketplace_score
```

---

### Scanner Ranking

```text
Code

scanner_ranking
```

↓

```text
Scoring Source

scanner_score
```

---

### Community Ranking

```text
Code

community_ranking
```

↓

```text
Scoring Source

contribution_score
```

---

### Achievement Ranking

```text
Code

achievement_ranking
```

↓

```text
Scoring Source

achievement_points
```

---

## Compatibilità User Scores

Le classifiche ottengono i valori da:

```text
user_scores
```

---

## Compatibilità Gamification

Le classifiche possono assegnare:

```text
Achievement

Badge

Titoli

Cornici Profilo
```

---

## Compatibilità Eventi Speciali

È possibile creare classifiche temporanee.

---

### Esempio

```text
Evento Pokémon 2027
```

↓

```text
special_event
```

↓

```text
Classifica dedicata
```

---

## Compatibilità Notifiche

Le classifiche possono generare notifiche quando un utente:

```text
Entra in Top 100

Entra in Top 10

Raggiunge il Primo Posto

Perde una Posizione Importante
```

---

## Compatibilità Dashboard Utente

Gli utenti devono poter visualizzare:

```text
Classifiche Disponibili

Posizione Attuale

Storico Ranking

Top Utenti
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Attivare

Disattivare

Riordinare
```

le classifiche senza modifiche al codice applicativo.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Classifiche

Partecipanti

Distribuzione Punteggi

Attività Utenti

Trend Storici
```

---

## Esempio Logico

Leaderboards

↓

Global Collector Score

↓

Leaderboard Entries

↓

Utente A

Rank #1

---

Leaderboards

↓

Marketplace Ranking

↓

Leaderboard Entries

↓

Utente B

Rank #5

---

Leaderboards

↓

Scanner Ranking

↓

Leaderboard Entries

↓

Utente C

Rank #2

---

## Motivazione Architetturale

La separazione tra:

```text
leaderboards
```

e

```text
leaderboard_entries
```

consente di definire centralmente tutte le classifiche della piattaforma senza duplicare configurazioni.

Questo approccio permette:

- classifiche multiple
- classifiche temporanee
- classifiche stagionali
- classifiche speciali
- scalabilità futura

senza modificare la struttura della Gamification.

La tabella costituisce il catalogo ufficiale delle classifiche di CollectorVerse.

---

# Tabella: leaderboard_entries

## Scopo

Rappresenta la posizione di un utente all'interno di una Classifica.

La tabella contiene le classifiche effettive generate dal sistema e permette di visualizzare:

- posizione
- punteggio
- variazione classifica
- storico ranking

Questa tabella viene aggiornata dai processi di calcolo delle classifiche.

---

## Tipo Tabella

Principale

---

## Nome Tabella

leaderboard_entries

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco posizione |
| leaderboard_id | UUID | SI | Classifica associata |
| user_id | UUID | SI | Utente classificato |
| rank_position | INTEGER | SI | Posizione attuale |
| score_value | BIGINT | SI | Punteggio registrato |
| previous_rank_position | INTEGER | NO | Posizione precedente |
| rank_change | INTEGER | SI | Variazione posizione |
| percentile_rank | NUMERIC(5,2) | NO | Percentile utente |
| snapshot_date | TIMESTAMPTZ | SI | Data generazione classifica |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

rank_change = 0

---

## Foreign Keys

leaderboard_id

→ leaderboards.id

---

user_id

→ users.id

---

## Relazioni

leaderboards (1)

↓

(N)

leaderboard_entries

---

users (1)

↓

(N)

leaderboard_entries

---

## Vincoli

leaderboard_id deve esistere.

user_id deve esistere.

rank_position deve essere maggiore di zero.

score_value deve essere maggiore o uguale a zero.

---

## Vincolo Anti-Duplicato

Per ogni generazione della classifica:

```text
Lo stesso utente può comparire una sola volta.
```

---

### Regola

```text
leaderboard_id
+
user_id
+
snapshot_date
```

devono identificare un record univoco.

---

## Indici

PRIMARY KEY (id)

INDEX (leaderboard_id)

INDEX (user_id)

INDEX (rank_position)

INDEX (score_value)

INDEX (snapshot_date)

UNIQUE (leaderboard_id, user_id, snapshot_date)

---

## Regole Business

Ogni record rappresenta la situazione dell'utente in una specifica classifica in uno specifico momento.

I record storici non devono essere sovrascritti.

I record storici consentono l'analisi dell'evoluzione delle classifiche.

---

## Posizione

La posizione viene assegnata in base al punteggio della classifica.

---

### Esempio

```text
Rank 1

Score 15000
```

---

```text
Rank 2

Score 14920
```

---

```text
Rank 3

Score 14700
```

---

## Rank Change

Indica lo spostamento rispetto alla generazione precedente.

---

### Esempio

Posizione Precedente

```text
15
```

↓

Posizione Attuale

```text
8
```

↓

```text
rank_change = +7
```

---

### Esempio

Posizione Precedente

```text
3
```

↓

Posizione Attuale

```text
9
```

↓

```text
rank_change = -6
```

---

## Percentile

Permette di determinare la collocazione relativa dell'utente.

---

### Esempio

```text
Percentile 99
```

↓

Top 1%

---

### Esempio

```text
Percentile 90
```

↓

Top 10%

---

## Compatibilità User Scores

Le classifiche possono essere generate utilizzando:

```text
collector_score

experience_points

reputation_score

scanner_score

marketplace_score

contribution_score
```

---

## Compatibilità Dashboard Utente

L'utente può visualizzare:

```text
Posizione Attuale

Storico Posizioni

Miglior Risultato

Variazioni Ranking
```

---

## Compatibilità Profilo Pubblico

Il profilo può mostrare:

```text
Posizione Globale

Top Categoria

Miglior Classifica
```

---

## Compatibilità Gamification

Le classifiche possono assegnare:

```text
Achievement

Badge

Ricompense Stagionali

Titoli Speciali
```

---

## Compatibilità Notifiche

Possono essere inviate notifiche quando:

```text
Ingresso Top 100

Ingresso Top 10

Nuovo Record Personale

Perdita Posizione Importante
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Ricalcolare

Rigenerare

Analizzare
```

le classifiche.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Partecipanti

Distribuzione Punteggi

Top Utenti

Variazione Ranking

Storico Classifiche
```

---

## Esempio Logico

Leaderboard

↓

Collector Score Globale

↓

Leaderboard Entry

↓

Utente A

↓

Rank 1

↓

15000 Punti

---

Leaderboard

↓

Scanner Ranking

↓

Leaderboard Entry

↓

Utente B

↓

Rank 8

↓

2450 Punti

---

Leaderboard

↓

Community Ranking

↓

Utente C

↓

Rank 2

↓

890 Contributi

---

## Motivazione Architetturale

La separazione tra:

```text
leaderboards
```

e

```text
leaderboard_entries
```

consente di mantenere una struttura altamente scalabile e storicizzabile.

Questo approccio permette:

- classifiche multiple
- ranking storici
- statistiche avanzate
- stagioni competitive
- progressione utente

senza modificare direttamente i dati della gamification.

La tabella costituisce il cuore del sistema classifiche di CollectorVerse.

---

# Parte 9 - Notifiche

# Tabella: notifications

## Scopo

Rappresenta una notifica generata dal sistema CollectorVerse.

La tabella costituisce il centro dell'intero sistema notifiche della piattaforma.

Una notifica può essere generata da:

- Marketplace
- Matching
- Wishlist
- Scanner
- Catalogo Collaborativo
- Gamification
- Messaggistica
- Attività amministrative
- Verifiche commerciante

---

## Tipo Tabella

Principale

---

## Nome Tabella

notifications

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo univoco notifica |
| user_id | UUID | SI | Destinatario notifica |
| notification_type | VARCHAR(50) | SI | Tipologia notifica |
| title | VARCHAR(255) | SI | Titolo notifica |
| message | TEXT | SI | Contenuto notifica |
| reference_type | VARCHAR(50) | NO | Tipo entità collegata |
| reference_id | UUID | NO | Entità collegata |
| status | VARCHAR(30) | SI | Stato notifica |
| priority_level | VARCHAR(20) | SI | Priorità |
| read_at | TIMESTAMPTZ | NO | Data lettura |
| expires_at | TIMESTAMPTZ | NO | Data scadenza |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

status = unread

priority_level = normal

---

## Valori Consentiti

### notification_type

```text
marketplace

offer

wishlist

matching

message

review

scanner

achievement

badge

level_up

catalog_contribution

merchant_verification

system

security

administrative
```

---

### status

```text
unread

read

archived
```

---

### priority_level

```text
low

normal

high

critical
```

---

## Significato Notification Type

### marketplace

Attività correlate agli annunci Marketplace.

---

### offer

Nuove offerte e trattative.

---

### wishlist

Oggetti wishlist diventati disponibili.

---

### matching

Nuove opportunità generate dal Matching.

---

### message

Nuovi messaggi ricevuti.

---

### review

Nuove recensioni ricevute.

---

### scanner

Risultati Scanner e aggiornamenti.

---

### achievement

Achievement completato.

---

### badge

Badge ottenuto.

---

### level_up

Avanzamento livello.

---

### catalog_contribution

Aggiornamenti contributi catalogo.

---

### merchant_verification

Aggiornamento stato verifica commerciante.

---

### system

Comunicazioni di sistema.

---

### security

Avvisi di sicurezza.

---

### administrative

Comunicazioni amministrative.

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

notifications

---

notifications (1)

↓

(N)

notification_deliveries

(Futuro)

---

## Vincoli

user_id deve esistere.

title non può essere vuoto.

message non può essere vuoto.

notification_type deve contenere un valore valido.

status deve contenere un valore valido.

priority_level deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (notification_type)

INDEX (status)

INDEX (priority_level)

INDEX (created_at)

INDEX (read_at)

INDEX (expires_at)

---

## Regole Business

Ogni notifica appartiene ad un solo utente.

Un utente può ricevere molte notifiche.

Una notifica può essere:

```text
Non letta

Letta

Archiviata
```

---

## Lettura Notifica

Quando l'utente visualizza la notifica:

```text
status = read
```

e

```text
read_at
```

viene valorizzato.

---

## Archiviazione

Le notifiche archiviate non devono comparire tra quelle attive.

Restano disponibili per finalità storiche.

---

## Entità Collegate

Una notifica può riferirsi ad una entità della piattaforma.

---

### Esempio Marketplace

```text
reference_type

marketplace_listing
```

↓

```text
reference_id

UUID Annuncio
```

---

### Esempio Achievement

```text
reference_type

achievement
```

↓

```text
reference_id

UUID Achievement
```

---

### Esempio Messaggio

```text
reference_type

message
```

↓

```text
reference_id

UUID Messaggio
```

---

## Compatibilità Marketplace

Notifiche possibili:

```text
Nuova Offerta

Offerta Accettata

Offerta Rifiutata

Nuovo Preferito

Annuncio Scaduto
```

---

## Compatibilità Wishlist

Notifiche possibili:

```text
Oggetto Disponibile

Nuovo Annuncio Compatibile

Riduzione Prezzo
```

---

## Compatibilità Matching

Notifiche possibili:

```text
Nuovo Match

Nuovo Trade Match

Nuova Opportunità
```

---

## Compatibilità Scanner

Notifiche possibili:

```text
Scansione Completata

Nuovo Risultato

Conferma Richiesta
```

---

## Compatibilità Catalogo Collaborativo

Notifiche possibili:

```text
Contributo Approvato

Contributo Respinto

Richiesta Revisione
```

---

## Compatibilità Gamification

Notifiche possibili:

```text
Achievement Sbloccato

Badge Ottenuto

Level Up

Nuovo Ranking
```

---

## Compatibilità Sicurezza

Notifiche possibili:

```text
Nuovo Accesso

Password Modificata

Attività Sospetta
```

---

## Compatibilità Dashboard Utente

L'utente deve poter visualizzare:

```text
Notifiche Non Lette

Storico Notifiche

Filtro per Categoria

Archivio Notifiche
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Inviare Notifiche Globali

Inviare Notifiche Mirate

Monitorare Consegne

Analizzare Utilizzo
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Notifiche Generate

Notifiche Letto

Tasso Apertura

Tempo Medio Lettura

Categorie Più Attive
```

---

## Esempio Logico

Marketplace

↓

Nuova Offerta

↓

Notification

↓

Unread

↓

Read

---

Matching

↓

Nuova Opportunità

↓

Notification

↓

Unread

---

Gamification

↓

Achievement Sbloccato

↓

Notification

↓

Unread

↓

Read

---

## Motivazione Architetturale

La tabella notifications rappresenta il centro unico di tutte le comunicazioni automatiche della piattaforma.

Questo approccio consente:

- un sistema notifiche uniforme
- gestione centralizzata
- statistiche globali
- supporto multicanale
- integrazione con tutte le funzionalità

senza duplicare logiche nei singoli moduli.

La tabella costituisce il nucleo del sistema Notifiche di CollectorVerse.

---

# Parte 10 - Messaggistica

# Tabella: conversation_threads

## Scopo

Rappresenta una conversazione tra utenti all'interno della piattaforma.

Una conversazione può essere generata da:

- Marketplace
- Matching
- Wishlist
- Catalogo Collaborativo
- Messaggistica Diretta

La conversazione costituisce il contenitore dei messaggi.

---

## Tipo Tabella

Principale

---

## Nome Tabella

conversation_threads

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo conversazione |
| thread_type | VARCHAR(30) | SI | Tipo conversazione |
| marketplace_listing_id | UUID | NO | Annuncio collegato |
| matching_opportunity_id | UUID | NO | Match collegato |
| created_by_user_id | UUID | SI | Utente creatore |
| status | VARCHAR(30) | SI | Stato conversazione |
| last_message_at | TIMESTAMPTZ | NO | Ultimo messaggio |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |
| closed_at | TIMESTAMPTZ | NO | Data chiusura |

---

## Valori Predefiniti

status = active

---

## Valori Consentiti

### thread_type

```text
marketplace

matching

direct
```

---

### status

```text
active

closed

archived

blocked
```

---

## Foreign Keys

created_by_user_id

→ users.id

---

marketplace_listing_id

→ marketplace_listings.id

---

matching_opportunity_id

→ matching_opportunities.id

---

## Relazioni

conversation_threads (1)

↓

(N)

messages

---

## Vincoli

created_by_user_id deve esistere.

thread_type deve contenere un valore valido.

status deve contenere un valore valido.

---

## Regole Business

Una conversazione può essere collegata a:

```text
Marketplace
```

oppure:

```text
Matching
```

oppure:

```text
Messaggistica Diretta
```

---

## Esempio Marketplace

Annuncio

↓

Charizard Gold

↓

Contatta Venditore

↓

Nuova Conversazione

---

## Esempio Matching

Match

↓

Scambio Possibile

↓

Nuova Conversazione

---

## Motivazione Architetturale

La Conversazione rappresenta il contenitore dei messaggi e permette di mantenere il contesto della comunicazione.

---

# Tabella: conversation_participants

## Scopo

Rappresenta la partecipazione di un utente ad una Conversazione.

La tabella collega:

```text
Utente
```

e

```text
Conversazione
```

e definisce:

- chi può leggere
- chi può scrivere
- chi partecipa
- stato partecipazione
- ultima lettura

---

## Tipo Tabella

Principale

---

## Nome Tabella

conversation_participants

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo partecipazione |
| conversation_thread_id | UUID | SI | Conversazione associata |
| user_id | UUID | SI | Utente partecipante |
| participant_role | VARCHAR(30) | SI | Ruolo partecipante |
| status | VARCHAR(30) | SI | Stato partecipazione |
| last_read_message_id | UUID | NO | Ultimo messaggio letto |
| last_read_at | TIMESTAMPTZ | NO | Data ultima lettura |
| joined_at | TIMESTAMPTZ | SI | Data ingresso conversazione |
| left_at | TIMESTAMPTZ | NO | Data uscita conversazione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

participant_role = member

status = active

---

## Valori Consentiti

### participant_role

```text
owner

member

moderator
```

---

### status

```text
active

archived

blocked

left
```

---

## Significato Ruoli

### owner

Creatore della conversazione.

---

### member

Partecipante standard.

---

### moderator

Partecipante con privilegi speciali.

Attualmente utilizzato principalmente per attività amministrative.

---

## Significato Stati

### active

Partecipazione attiva.

---

### archived

Conversazione archiviata per quell'utente.

---

### blocked

Partecipazione bloccata.

---

### left

L'utente ha lasciato la conversazione.

---

## Foreign Keys

conversation_thread_id

→ conversation_threads.id

---

user_id

→ users.id

---

last_read_message_id

→ messages.id

(Futuro)

---

## Relazioni

conversation_threads (1)

↓

(N)

conversation_participants

---

users (1)

↓

(N)

conversation_participants

---

messages (1)

↓

(N)

conversation_participants

(tramite lettura)

---

## Vincoli

conversation_thread_id deve esistere.

user_id deve esistere.

participant_role deve contenere un valore valido.

status deve contenere un valore valido.

---

## Vincolo Anti-Duplicato

Lo stesso utente può comparire una sola volta nella stessa conversazione.

---

### Regola

```text
UNIQUE
(
conversation_thread_id,
user_id
)
```

---

## Indici

PRIMARY KEY (id)

INDEX (conversation_thread_id)

INDEX (user_id)

INDEX (status)

INDEX (last_read_at)

UNIQUE (conversation_thread_id, user_id)

---

## Regole Business

Una conversazione deve avere almeno due partecipanti attivi.

---

Ogni messaggio può essere visualizzato esclusivamente dai partecipanti della conversazione.

---

## Ultima Lettura

Il sistema utilizza:

```text
last_read_message_id
```

e

```text
last_read_at
```

per determinare:

```text
Messaggi Letti

Messaggi Non Letti
```

---

## Esempio

Conversazione

↓

Messaggi Totali = 50

↓

last_read_message_id = 48

↓

Messaggi Non Letti = 2

---

## Archiviazione Conversazione

Se:

```text
status = archived
```

la conversazione non compare tra quelle attive dell'utente.

---

La conversazione continua ad esistere.

---

## Uscita Conversazione

Se:

```text
status = left
```

↓

```text
left_at valorizzato
```

---

I messaggi storici restano conservati.

---

## Compatibilità Marketplace

Quando un utente contatta un venditore:

```text
Nuova Conversazione
```

↓

```text
2 Partecipanti
```

↓

```text
conversation_participants
```

---

## Compatibilità Matching

Un Match può generare:

```text
Conversazione
```

↓

```text
Partecipanti Coinvolti
```

---

## Compatibilità Notifiche

Le notifiche possono basarsi su:

```text
Nuovo Messaggio

Messaggi Non Letti

Nuova Conversazione
```

---

## Compatibilità Dashboard Utente

L'utente deve poter vedere:

```text
Conversazioni Attive

Conversazioni Archiviate

Messaggi Non Letti
```

---

## Compatibilità Moderazione

Gli amministratori devono poter:

```text
Bloccare Partecipanti

Chiudere Conversazioni

Revisionare Conversazioni Segnalate
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Conversazioni

Numero Partecipanti

Tempo Medio Risposta

Messaggi Non Letti
```

---

## Esempio Logico

Conversation Thread

↓

Marketplace

↓

Charizard Gold

↓

Conversation Participants

↓

Utente A

(owner)

↓

Utente B

(member)

↓

Conversazione Attiva

---

Conversation Thread

↓

Matching

↓

Trade Match

↓

Conversation Participants

↓

Utente C

↓

Utente D

↓

Conversazione Attiva

---

## Motivazione Architetturale

La separazione tra:

```text
conversation_threads
```

e

```text
conversation_participants
```

consente di gestire in modo corretto i partecipanti senza duplicare informazioni nella conversazione.

Questo approccio permette:

- gestione letture
- archivio personale
- supporto multiutente futuro
- moderazione avanzata
- maggiore scalabilità

e costituisce la base necessaria per la successiva tabella:

```text
messages
```

che conterrà il contenuto effettivo della conversazione.

---

# Tabella: messages

## Scopo

Rappresenta un singolo messaggio inviato all'interno di una Conversazione.

La tabella costituisce il cuore operativo del sistema di Messaggistica.

Ogni messaggio appartiene ad una Conversazione ed è inviato da un partecipante autorizzato.

I messaggi possono contenere:

- testo
- riferimenti a Marketplace
- riferimenti a Matching
- allegati

Gli allegati vengono gestiti tramite la tabella:

```text
message_attachments
```

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
| conversation_thread_id | UUID | SI | Conversazione associata |
| sender_user_id | UUID | SI | Mittente messaggio |
| message_type | VARCHAR(30) | SI | Tipo messaggio |
| message_content | TEXT | SI | Contenuto messaggio |
| reply_to_message_id | UUID | NO | Messaggio a cui si risponde |
| edited_at | TIMESTAMPTZ | NO | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Data eliminazione logica |
| created_at | TIMESTAMPTZ | SI | Data invio |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |

---

## Valori Predefiniti

message_type = text

---

## Valori Consentiti

### message_type

```text
text

system

marketplace

matching
```

---

## Significato Tipologie

### text

Messaggio standard inviato da un utente.

---

### system

Messaggio generato automaticamente dal sistema.

---

### marketplace

Messaggio collegato ad attività Marketplace.

---

### matching

Messaggio collegato ad attività Matching.

---

## Foreign Keys

conversation_thread_id

→ conversation_threads.id

---

sender_user_id

→ users.id

---

reply_to_message_id

→ messages.id

---

## Relazioni

conversation_threads (1)

↓

(N)

messages

---

users (1)

↓

(N)

messages

---

messages (1)

↓

(N)

messages

(risposte)

---

messages (1)

↓

(N)

message_attachments

---

## Vincoli

conversation_thread_id deve esistere.

sender_user_id deve esistere.

message_content non può essere vuoto.

message_type deve contenere un valore valido.

---

## Vincolo Partecipazione

Il mittente deve essere un partecipante attivo della conversazione.

---

### Regola

Il sistema deve verificare l'esistenza di:

```text
conversation_participants

↓

conversation_thread_id

+

sender_user_id

+

status = active
```

---

## Vincolo Risposta

Se valorizzato:

```text
reply_to_message_id
```

deve appartenere alla stessa Conversazione.

---

## Indici

PRIMARY KEY (id)

INDEX (conversation_thread_id)

INDEX (sender_user_id)

INDEX (reply_to_message_id)

INDEX (message_type)

INDEX (created_at)

INDEX (deleted_at)

---

## Regole Business

Ogni messaggio appartiene ad una sola conversazione.

Ogni messaggio ha un solo mittente.

Una conversazione può contenere molti messaggi.

---

## Ordine Messaggi

I messaggi devono essere mostrati in ordine di:

```text
created_at
```

---

## Modifica Messaggi

Quando un messaggio viene modificato:

```text
edited_at
```

deve essere valorizzato.

---

## Eliminazione Messaggi

L'eliminazione è logica.

---

### Regola

```text
deleted_at
```

viene valorizzato.

Il record resta disponibile per finalità storiche e di moderazione.

---

## Risposte

Un messaggio può essere una risposta diretta ad un altro messaggio.

---

### Esempio

```text
Messaggio #10

↓

"Ciao, è ancora disponibile?"
```

---

```text
Messaggio #11

↓

Risposta a #10

↓

"Sì, è disponibile."
```

---

## Compatibilità Marketplace

Quando un utente contatta un venditore:

```text
Conversation Thread

↓

Messages
```

---

## Compatibilità Matching

Un Match può generare una conversazione.

I messaggi permettono agli utenti di approfondire la proposta.

---

## Compatibilità Allegati

Un messaggio può contenere:

```text
Fotografie

Screenshot

Documenti

Certificazioni

Immagini Oggetti
```

tramite:

```text
message_attachments
```

---

## Compatibilità Notifiche

Un nuovo messaggio può generare:

```text
Nuovo Messaggio Ricevuto
```

---

## Compatibilità Moderazione

Gli amministratori devono poter:

```text
Visualizzare

Revisionare

Segnalare

Oscurare
```

messaggi in caso di abuso.

---

## Compatibilità Sicurezza

I messaggi devono poter essere sottoposti a:

```text
Filtri Spam

Filtri Linguaggio Abusivo

Moderazione
```

---

## Compatibilità Dashboard Utente

L'utente deve poter visualizzare:

```text
Conversazioni

Ultimi Messaggi

Messaggi Non Letti

Messaggi Inviati
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Messaggi

Messaggi Ricevuti

Messaggi Inviati

Tempo Medio Risposta

Conversazioni Attive
```

---

## Esempio Logico

Conversation Thread

↓

Marketplace

↓

Charizard Gold

↓

Messages

↓

"Ciao, è disponibile?"

↓

"Sì"

↓

"Prezzo trattabile?"

↓

"Possiamo parlarne"

↓

Allegati Fotografici

---

## Motivazione Architetturale

La separazione tra:

```text
conversation_threads
```

```text
conversation_participants
```

```text
messages
```

e

```text
message_attachments
```

consente di mantenere separati:

- contesto conversazione
- partecipanti
- contenuto testuale
- file allegati

garantendo scalabilità, sicurezza e moderazione.

---

# Tabella: message_attachments

## Scopo

Rappresenta un allegato associato ad un Messaggio.

Permette agli utenti di inviare file all'interno delle Conversazioni.

Supporta:

- immagini
- fotografie
- screenshot
- documenti
- certificazioni
- prove fotografiche
- materiale informativo

---

## Tipo Tabella

Principale

---

## Nome Tabella

message_attachments

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo allegato |
| message_id | UUID | SI | Messaggio associato |
| media_file_id | UUID | SI | File associato |
| attachment_type | VARCHAR(30) | SI | Tipologia allegato |
| created_at | TIMESTAMPTZ | SI | Data collegamento |

---

## Valori Consentiti

### attachment_type

```text
image

document

certificate

other
```

---

## Significato Tipologie

### image

Immagine o fotografia.

---

### document

Documento generico.

---

### certificate

Certificato o documento di autenticità.

---

### other

Allegato non classificato.

---

## Foreign Keys

message_id

→ messages.id

---

media_file_id

→ media_files.id

---

## Relazioni

messages (1)

↓

(N)

message_attachments

---

media_files (1)

↓

(N)

message_attachments

---

## Vincoli

message_id deve esistere.

media_file_id deve esistere.

attachment_type deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (message_id)

INDEX (media_file_id)

INDEX (attachment_type)

INDEX (created_at)

---

## Regole Business

Un Messaggio può contenere:

```text
Nessun allegato

Uno

Molti allegati
```

---

Un Allegato appartiene ad un solo Messaggio.

---

## Compatibilità Marketplace

Gli utenti possono inviare:

```text
Foto Oggetti

Dettagli Difetti

Certificazioni

Immagini Aggiuntive
```

---

## Compatibilità Matching

Gli utenti possono condividere:

```text
Immagini Collezione

Verifiche Condizione

Foto Varianti
```

---

## Compatibilità Merchant Verification

I commercianti possono condividere:

```text
Documentazione

Certificati

Materiale Informativo
```

all'interno delle conversazioni.

---

## Compatibilità Moderazione

Gli allegati possono essere:

```text
Revisionati

Segnalati

Oscurati

Disattivati
```

tramite:

```text
media_files
```

e i sistemi di moderazione.

---

## Compatibilità Storage

I file non vengono salvati direttamente nella tabella.

La gestione fisica avviene tramite:

```text
media_files
```

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Numero Allegati

Numero Immagini

Numero Documenti

Spazio Utilizzato

Media Allegati per Conversazione
```

---

## Esempio Logico

Conversation

↓

Message

↓

"Ti allego altre foto del Charizard"

↓

Message Attachments

↓

front.jpg

↓

back.jpg

↓

closeup_holo.jpg

---

Conversation

↓

Message

↓

"Ti allego il certificato"

↓

Message Attachments

↓

certificate.pdf

---

## Motivazione Architetturale

La separazione tra:

```text
messages
```

e

```text
message_attachments
```

consente di gestire file e contenuti testuali in modo indipendente.

Questo approccio:

- evita duplicazioni
- migliora lo storage
- migliora la moderazione
- migliora la scalabilità

e integra perfettamente la messaggistica con il sistema centralizzato:

```text
media_files
```

di CollectorVerse.

---

# Parte 11 - Reputazione e Recensioni

# Tabella: user_reviews

## Scopo

Rappresenta una recensione lasciata da un utente nei confronti di un altro utente.

Le recensioni consentono alla community di valutare:

- affidabilità
- correttezza
- qualità della comunicazione
- esperienza complessiva

Le recensioni possono essere lasciate esclusivamente tra utenti che hanno effettivamente interagito tramite una conversazione sulla piattaforma.

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
| id | UUID | SI | Identificativo recensione |
| reviewer_user_id | UUID | SI | Utente autore recensione |
| reviewed_user_id | UUID | SI | Utente recensito |
| conversation_thread_id | UUID | SI | Conversazione che abilita la recensione |
| rating | INTEGER | SI | Valutazione |
| review_text | TEXT | NO | Testo recensione |
| is_visible | BOOLEAN | SI | Visibilità recensione |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data ultima modifica |
| deleted_at | TIMESTAMPTZ | NO | Soft Delete |

---

## Valori Predefiniti

is_visible = TRUE

---

## Valori Consentiti

### rating

```text
1

2

3

4

5
```

---

## Significato Valutazioni

### 1

Esperienza molto negativa.

---

### 2

Esperienza negativa.

---

### 3

Esperienza neutra.

---

### 4

Esperienza positiva.

---

### 5

Esperienza eccellente.

---

## Foreign Keys

reviewer_user_id

→ users.id

---

reviewed_user_id

→ users.id

---

conversation_thread_id

→ conversation_threads.id

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

conversation_threads (1)

↓

(N)

user_reviews

---

## Vincoli

reviewer_user_id deve esistere.

reviewed_user_id deve esistere.

conversation_thread_id deve esistere.

rating deve essere compreso tra:

```text
1

e

5
```

---

## Vincolo Anti-Autorecensione

Non è consentito:

```text
reviewer_user_id

=

reviewed_user_id
```

---

## Vincolo Conversazione

L'utente recensore e l'utente recensito devono essere partecipanti della Conversazione indicata.

La conversazione deve esistere.

Non è consentito recensire utenti con cui non è mai esistita una conversazione.

---

## Vincolo Anti-Duplicato

Un utente può possedere una sola recensione verso uno specifico utente.

```text
UNIQUE
(
reviewer_user_id,
reviewed_user_id
)
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (reviewer_user_id, reviewed_user_id)

INDEX (reviewer_user_id)

INDEX (reviewed_user_id)

INDEX (conversation_thread_id)

INDEX (rating)

INDEX (is_visible)

INDEX (created_at)

---

## Regole Business

Le recensioni contribuiscono alla reputazione dell'utente.

Le recensioni archiviate devono rimanere nello storico.

Le recensioni possono essere moderate dagli amministratori.

---

## Aggiornamento Recensione

Se un utente tenta di recensire nuovamente lo stesso utente:

```text
NON viene creato un nuovo record.
```

---

Il sistema deve aggiornare il record esistente.

Devono essere aggiornati:

```text
rating

review_text

updated_at

conversation_thread_id
```

---

## Compatibilità Marketplace

Le recensioni possono nascere da conversazioni originate da annunci Marketplace.

---

## Compatibilità Matching

Le recensioni possono nascere da conversazioni originate da opportunità di Matching.

---

## Compatibilità Messaggistica

La Conversazione rappresenta la prova dell'effettiva interazione tra gli utenti.

---

## Compatibilità User Scores

Le recensioni contribuiscono al calcolo di:

```text
reputation_score
```

presente in:

```text
user_scores
```

---

## Compatibilità Profilo Utente

Il profilo può mostrare:

```text
Media Recensioni

Numero Recensioni

Ultime Recensioni
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Moderare

Nascondere

Ripristinare
```

recensioni abusive.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Media Recensioni

Numero Recensioni

Distribuzione Voti

Migliori Utenti

Utenti Più Recensiti
```

---

## Esempio Logico

Conversation Thread

↓

Marketplace

↓

Utente A

↓

Utente B

↓

Recensione

↓

5 Stelle

↓

"Eccellente comunicazione"

---

## Motivazione Architetturale

La recensione è consentita soltanto dopo una reale interazione documentata tramite Conversazione.

Questo approccio:

- riduce recensioni false
- aumenta affidabilità
- migliora reputazione
- protegge gli utenti

e costituisce la base del sistema di fiducia di CollectorVerse.

---

# Tabella: merchant_verifications

## Scopo

Rappresenta una richiesta di verifica professionale effettuata da un utente.

La verifica consente di identificare:

- negozi
- commercianti professionali
- aziende
- rivenditori specializzati
- attività commerciali del settore collezionistico

L'obiettivo è aumentare la fiducia e la trasparenza all'interno della piattaforma.

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
| id | UUID | SI | Identificativo verifica |
| user_id | UUID | SI | Richiedente verifica |
| business_name | VARCHAR(255) | SI | Nome attività |
| business_type | VARCHAR(50) | SI | Tipologia attività |
| website_url | TEXT | NO | Sito web |
| tax_identifier | VARCHAR(100) | NO | Identificativo fiscale |
| country_code | VARCHAR(10) | SI | Paese attività |
| verification_status | VARCHAR(30) | SI | Stato verifica |
| application_notes | TEXT | NO | Note richiedente |
| reviewer_user_id | UUID | NO | Revisore amministratore |
| review_notes | TEXT | NO | Note revisione |
| submitted_at | TIMESTAMPTZ | SI | Data invio |
| reviewed_at | TIMESTAMPTZ | NO | Data revisione |
| approved_at | TIMESTAMPTZ | NO | Data approvazione |
| rejected_at | TIMESTAMPTZ | NO | Data rifiuto |
| expires_at | TIMESTAMPTZ | NO | Scadenza verifica |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |

---

## Valori Predefiniti

verification_status = pending

submitted_at = data corrente

---

## Valori Consentiti

### business_type

```text
store

dealer

collector_shop

company

auction_house

other
```

---

### verification_status

```text
pending

under_review

approved

rejected

expired

revoked
```

---

## Significato Business Type

### store

Negozio fisico o online.

---

### dealer

Rivenditore professionale.

---

### collector_shop

Attività specializzata nel collezionismo.

---

### company

Società registrata.

---

### auction_house

Casa d'aste.

---

### other

Altra attività professionale.

---

## Significato Verification Status

### pending

Richiesta ricevuta.

---

### under_review

Richiesta in fase di verifica.

---

### approved

Verifica approvata.

---

### rejected

Verifica rifiutata.

---

### expired

Verifica scaduta.

---

### revoked

Verifica revocata.

---

## Foreign Keys

user_id

→ users.id

---

reviewer_user_id

→ users.id

---

## Relazioni

users (1)

↓

(0..1)

merchant_verifications

---

users (1)

↓

(N)

merchant_verifications

(revisore)

---

merchant_verifications (1)

↓

(N)

media_usages

---

## Vincoli

user_id deve esistere.

business_name non può essere vuoto.

country_code non può essere vuoto.

verification_status deve contenere un valore valido.

business_type deve contenere un valore valido.

---

## Vincolo Anti-Duplicato

Un utente può avere una sola verifica attiva.

```text
UNIQUE (user_id)
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (user_id)

INDEX (verification_status)

INDEX (business_type)

INDEX (country_code)

INDEX (reviewer_user_id)

INDEX (submitted_at)

INDEX (reviewed_at)

---

## Regole Business

Solo gli utenti che operano come professionisti o attività commerciali devono richiedere la verifica.

Gli utenti privati non sono obbligati a richiederla.

---

## Documentazione Verifica

La documentazione viene gestita tramite:

```text
media_files
```

e

```text
media_usages
```

utilizzando:

```text
entity_type = merchant_verification
```

---

## Esempi Documenti

```text
Visura camerale

Documento fiscale

Partita IVA

Certificato attività

Prove commerciali

Documentazione aziendale
```

---

## Workflow Standard

```text
Utente

↓

Richiesta

↓

Pending

↓

Under Review

↓

Approved
```

---

## Workflow Rifiuto

```text
Utente

↓

Richiesta

↓

Pending

↓

Under Review

↓

Rejected
```

---

## Badge Merchant Verificato

Quando:

```text
verification_status = approved
```

può essere assegnato automaticamente:

```text
Verified Merchant
```

tramite:

```text
user_badges
```

---

## Compatibilità Marketplace

I profili verificati possono mostrare:

```text
Merchant Verificato
```

all'interno degli annunci.

---

## Compatibilità Matching

Gli utenti possono filtrare:

```text
Merchant Verificati
```

all'interno delle opportunità.

---

## Compatibilità Profilo Utente

Il profilo può mostrare:

```text
Stato Verifica

Nome Attività

Tipologia Attività

Badge Merchant
```

---

## Compatibilità Notifiche

La verifica può generare:

```text
Richiesta Ricevuta

Richiesta Approvata

Richiesta Respinta

Verifica Scaduta

Verifica Revocata
```

---

## Compatibilità User Scores

Può contribuire a:

```text
reputation_score
```

secondo le regole applicative.

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Visualizzare

Revisionare

Approvare

Respingere

Revocare

Rinnovare
```

le verifiche.

---

## Compatibilità Statistiche

Statistiche disponibili:

```text
Merchant Verificati

Richieste Approvate

Richieste Respinte

Tempo Medio Revisione

Distribuzione per Paese
```

---

## Esempio Logico

Utente

↓

Merchant Verification

↓

PokéStore Milano

↓

Store

↓

Pending

↓

Approved

↓

Verified Merchant

↓

Documentazione Archiviata

---

## Motivazione Architetturale

La separazione tra:

```text
merchant_verifications
```

e

```text
media_files
```

consente di mantenere separati:

- dati della verifica
- documentazione allegata

Questo approccio:

- migliora la sicurezza
- migliora la moderazione
- migliora la tracciabilità
- supporta audit futuri

e costituisce il sistema ufficiale di verifica professionale di CollectorVerse.

---

# Parte 12 - Moderazione e Sicurezza

# Tabella: user_blocks

## Scopo

Rappresenta il blocco di un utente da parte di un altro utente.

Il blocco consente di interrompere qualsiasi interazione tra due utenti.

Questa funzionalità protegge gli utenti da:

- spam
- molestie
- comportamenti indesiderati
- contatti non graditi

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
| id | UUID | SI | Identificativo blocco |
| blocker_user_id | UUID | SI | Utente che blocca |
| blocked_user_id | UUID | SI | Utente bloccato |
| reason | TEXT | NO | Motivazione opzionale |
| created_at | TIMESTAMPTZ | SI | Data blocco |
| updated_at | TIMESTAMPTZ | SI | Data modifica |
| deleted_at | TIMESTAMPTZ | NO | Data sblocco |

---

## Foreign Keys

blocker_user_id

→ users.id

---

blocked_user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

user_blocks

(bloccante)

---

users (1)

↓

(N)

user_blocks

(bloccato)

---

## Vincoli

blocker_user_id deve esistere.

blocked_user_id deve esistere.

---

## Vincolo Anti-Autoblocco

Non è consentito:

```text
blocker_user_id

=

blocked_user_id
```

---

## Vincolo Anti-Duplicato

```text
UNIQUE
(
blocker_user_id,
blocked_user_id
)
```

---

## Indici

PRIMARY KEY (id)

INDEX (blocker_user_id)

INDEX (blocked_user_id)

UNIQUE (blocker_user_id, blocked_user_id)

---

## Regole Business

Quando un utente viene bloccato:

```text
Nessun nuovo messaggio

Nessun nuovo contatto

Nessuna nuova conversazione

Nessuna opportunità Matching diretta
```

---

## Compatibilità Messaggistica

Le conversazioni esistenti restano archiviate.

Non possono essere inviati nuovi messaggi.

---

## Compatibilità Marketplace

Gli utenti bloccati non possono contattarsi tramite annunci.

---

## Compatibilità Matching

Gli utenti bloccati vengono esclusi dal Matching.

---

## Motivazione Architetturale

Questa tabella costituisce il primo livello di protezione personale tra utenti.

---

# Tabella: moderation_cases

## Scopo

Rappresenta un caso di moderazione aperto sulla piattaforma.

Un caso può essere originato da:

- segnalazioni Marketplace
- segnalazioni utenti
- verifiche amministrative
- controlli automatici

---

## Tipo Tabella

Principale

---

## Nome Tabella

moderation_cases

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo caso |
| case_number | VARCHAR(50) | SI | Codice caso |
| status | VARCHAR(30) | SI | Stato caso |
| priority_level | VARCHAR(20) | SI | Priorità |
| created_by_user_id | UUID | NO | Utente segnalante |
| assigned_to_user_id | UUID | NO | Moderatore assegnato |
| summary | VARCHAR(255) | SI | Titolo caso |
| description | TEXT | NO | Dettagli caso |
| resolution_notes | TEXT | NO | Esito revisione |
| opened_at | TIMESTAMPTZ | SI | Apertura |
| resolved_at | TIMESTAMPTZ | NO | Chiusura |
| created_at | TIMESTAMPTZ | SI | Creazione |
| updated_at | TIMESTAMPTZ | SI | Aggiornamento |

---

## Valori Consentiti

### status

```text
open

under_review

pending_info

resolved

dismissed
```

---

### priority_level

```text
low

normal

high

critical
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (case_number)

INDEX (status)

INDEX (priority_level)

INDEX (assigned_to_user_id)

---

## Regole Business

Ogni caso può coinvolgere:

```text
Utenti

Annunci

Messaggi

Contributi

Recensioni
```

---

## Motivazione Architetturale

Centralizza tutta la moderazione in un'unica struttura.

---

# Tabella: moderation_case_entities

## Scopo

Collega un Caso di Moderazione alle entità coinvolte.

Permette ad un singolo caso di riferirsi a più elementi.

---

## Tipo Tabella

Principale

---

## Nome Tabella

moderation_case_entities

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo collegamento |
| moderation_case_id | UUID | SI | Caso associato |
| entity_type | VARCHAR(50) | SI | Tipo entità |
| entity_id | UUID | SI | Entità coinvolta |
| created_at | TIMESTAMPTZ | SI | Data creazione |

---

## Valori Consentiti

### entity_type

```text
user

marketplace_listing

message

catalog_contribution

review

merchant_verification
```

---

## Foreign Keys

moderation_case_id

→ moderation_cases.id

---

## Indici

PRIMARY KEY (id)

INDEX (moderation_case_id)

INDEX (entity_type)

INDEX (entity_id)

---

## Motivazione Architetturale

Permette di collegare qualsiasi oggetto della piattaforma ad un caso senza modificare il database in futuro.

---

# Tabella: audit_logs

## Scopo

Rappresenta il registro storico delle azioni importanti effettuate nella piattaforma.

La tabella viene utilizzata per:

- sicurezza
- audit
- investigazioni
- conformità
- debugging amministrativo

---

## Tipo Tabella

Principale

---

## Nome Tabella

audit_logs

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo log |
| user_id | UUID | NO | Utente coinvolto |
| action_type | VARCHAR(100) | SI | Azione eseguita |
| entity_type | VARCHAR(50) | SI | Tipo entità coinvolta |
| entity_id | UUID | NO | Record coinvolto |
| metadata_json | JSONB | NO | Dati aggiuntivi |
| ip_address | VARCHAR(100) | NO | IP registrato |
| created_at | TIMESTAMPTZ | SI | Data evento |

---

## Esempi Action Type

```text
login

logout

create_listing

delete_listing

send_message

approve_contribution

reject_contribution

merchant_approved

merchant_revoked

user_blocked
```

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (action_type)

INDEX (entity_type)

INDEX (entity_id)

INDEX (created_at)

---

## Regole Business

I log non devono essere modificati.

I log non devono essere eliminati.

I log rappresentano la fonte ufficiale delle attività storiche.

---

## Motivazione Architetturale

Questa tabella costituisce la memoria operativa della piattaforma e permette di ricostruire qualsiasi evento rilevante.

---

# Parte 13 - Amministrazione e Configurazione

# Tabella: system_settings

## Scopo

Rappresenta le impostazioni globali della piattaforma.

Questa tabella consente agli amministratori di configurare il comportamento generale di CollectorVerse senza effettuare modifiche al codice.

Le impostazioni possono riguardare:

- Marketplace
- Matching
- Scanner
- Gamification
- Registrazione utenti
- Catalogo Collaborativo
- Sicurezza

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

system_settings

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo impostazione |
| setting_key | VARCHAR(150) | SI | Chiave impostazione |
| setting_value | TEXT | SI | Valore impostazione |
| value_type | VARCHAR(20) | SI | Tipo valore |
| category | VARCHAR(50) | SI | Categoria impostazione |
| description | TEXT | NO | Descrizione |
| is_public | BOOLEAN | SI | Visibile lato client |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |

---

## Valori Predefiniti

is_public = FALSE

---

## Valori Consentiti

### value_type

```text
string

integer

decimal

boolean

json
```

---

### category

```text
marketplace

matching

scanner

security

catalog

gamification

notifications

general
```

---

## Vincoli

setting_key deve essere univoco.

setting_key non può essere vuoto.

setting_value non può essere vuoto.

---

## Indici

PRIMARY KEY (id)

UNIQUE (setting_key)

INDEX (category)

INDEX (is_public)

---

## Esempi

### Marketplace

```text
max_active_listings_per_user

100
```

---

### Matching

```text
default_matching_score

50
```

---

### Scanner

```text
minimum_scan_confidence

75
```

---

### Catalogo

```text
community_votes_required

10
```

---

## Motivazione Architetturale

Permette la configurazione centralizzata del sistema senza deploy applicativi.

---

# Tabella: feature_flags

## Scopo

Permette di attivare o disattivare funzionalità della piattaforma.

Le Feature Flag consentono rilasci graduali e gestione controllata delle nuove funzionalità.

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

feature_flags

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo flag |
| feature_key | VARCHAR(150) | SI | Codice funzionalità |
| name | VARCHAR(150) | SI | Nome funzionalità |
| description | TEXT | NO | Descrizione |
| is_enabled | BOOLEAN | SI | Stato attivazione |
| rollout_percentage | INTEGER | SI | Percentuale rilascio |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |

---

## Valori Predefiniti

is_enabled = FALSE

rollout_percentage = 100

---

## Vincoli

feature_key deve essere univoco.

rollout_percentage deve essere compreso tra:

```text
0
e
100
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (feature_key)

INDEX (is_enabled)

---

## Esempi

```text
advanced_scanner
```

---

```text
ai_matching_v2
```

---

```text
merchant_program
```

---

```text
seasonal_leaderboards
```

---

## Regole Business

Se:

```text
is_enabled = FALSE
```

la funzionalità non deve essere disponibile.

---

## Motivazione Architetturale

Permette il rilascio progressivo di nuove funzionalità senza modifiche strutturali.

---

# Tabella: maintenance_windows

## Scopo

Rappresenta le finestre di manutenzione pianificate della piattaforma.

Utilizzata per:

- aggiornamenti
- manutenzioni
- migrazioni database
- deploy importanti
- comunicazioni agli utenti

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

maintenance_windows

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo manutenzione |
| title | VARCHAR(255) | SI | Titolo manutenzione |
| description | TEXT | NO | Descrizione dettagliata |
| starts_at | TIMESTAMPTZ | SI | Inizio manutenzione |
| ends_at | TIMESTAMPTZ | SI | Fine manutenzione |
| status | VARCHAR(30) | SI | Stato manutenzione |
| affects_marketplace | BOOLEAN | SI | Impatta Marketplace |
| affects_scanner | BOOLEAN | SI | Impatta Scanner |
| affects_matching | BOOLEAN | SI | Impatta Matching |
| affects_messaging | BOOLEAN | SI | Impatta Messaggistica |
| created_by_user_id | UUID | SI | Amministratore creatore |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |

---

## Valori Predefiniti

status = scheduled

affects_marketplace = FALSE

affects_scanner = FALSE

affects_matching = FALSE

affects_messaging = FALSE

---

## Valori Consentiti

### status

```text
scheduled

active

completed

cancelled
```

---

## Foreign Keys

created_by_user_id

→ users.id

---

## Vincoli

starts_at deve essere precedente a ends_at.

status deve contenere un valore valido.

---

## Indici

PRIMARY KEY (id)

INDEX (status)

INDEX (starts_at)

INDEX (ends_at)

---

## Regole Business

Le manutenzioni future devono essere comunicate agli utenti tramite notifiche.

---

## Compatibilità Notifiche

Può generare:

```text
Manutenzione Pianificata

Manutenzione In Corso

Manutenzione Terminata
```

---

## Compatibilità Dashboard Admin

Gli amministratori devono poter:

```text
Creare

Modificare

Annullare

Pubblicare
```

le manutenzioni.

---

## Motivazione Architetturale

Centralizza la gestione delle manutenzioni e delle comunicazioni operative verso gli utenti.

---

# Parte 14 - Gestione Media e Storage

# Tabella: media_files

## Scopo

Rappresenta qualsiasi file caricato sulla piattaforma.

La tabella centralizza la gestione di:

- immagini catalogo
- avatar
- copertine profilo
- allegati contributi
- documenti verifica commercianti
- immagini scanner
- icone badge
- icone achievement

---

## Tipo Tabella

Principale

---

## Nome Tabella

media_files

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo file |
| uploaded_by_user_id | UUID | NO | Utente caricatore |
| storage_path | TEXT | SI | Percorso file storage |
| original_filename | VARCHAR(255) | SI | Nome file originale |
| mime_type | VARCHAR(100) | SI | Mime Type |
| file_size_bytes | BIGINT | SI | Dimensione file |
| width | INTEGER | NO | Larghezza |
| height | INTEGER | NO | Altezza |
| file_hash | VARCHAR(255) | NO | Hash file |
| status | VARCHAR(30) | SI | Stato file |
| created_at | TIMESTAMPTZ | SI | Data caricamento |
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

pending_review

blocked

deleted
```

---

## Foreign Keys

uploaded_by_user_id

→ users.id

---

## Vincoli

storage_path non può essere vuoto.

mime_type non può essere vuoto.

file_size_bytes deve essere maggiore di zero.

---

## Indici

PRIMARY KEY (id)

INDEX (uploaded_by_user_id)

INDEX (status)

INDEX (mime_type)

INDEX (file_hash)

---

## Regole Business

Ogni file viene salvato una sola volta.

Lo stesso file può essere utilizzato da molte entità.

---

## Compatibilità Moderazione

I file possono essere:

```text
Revisionati

Bloccati

Archiviati
```

---

## Motivazione Architetturale

Centralizza tutto lo storage della piattaforma.

---

# Tabella: media_usages

## Scopo

Collega un file ad una entità della piattaforma.

Permette di sapere dove viene utilizzato ogni file.

---

## Tipo Tabella

Principale

---

## Nome Tabella

media_usages

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo collegamento |
| media_file_id | UUID | SI | File collegato |
| entity_type | VARCHAR(50) | SI | Tipo entità |
| entity_id | UUID | SI | Entità utilizzatrice |
| usage_type | VARCHAR(50) | SI | Utilizzo specifico |
| created_at | TIMESTAMPTZ | SI | Data collegamento |

---

## Valori Consentiti

### entity_type

```text
user_profile

catalog_image

catalog_contribution

merchant_verification

achievement

badge

scan_session
```

---

### usage_type

```text
avatar

cover

front_image

back_image

attachment

proof

icon

scan_source
```

---

## Foreign Keys

media_file_id

→ media_files.id

---

## Relazioni

media_files (1)

↓

(N)

media_usages

---

## Vincoli

media_file_id deve esistere.

entity_id deve essere valorizzato.

---

## Indici

PRIMARY KEY (id)

INDEX (media_file_id)

INDEX (entity_type)

INDEX (entity_id)

INDEX (usage_type)

---

## Regole Business

Un file può essere riutilizzato più volte.

Una entità può avere più file collegati.

---

## Esempio

media_file

↓

charizard_front.jpg

↓

catalog_image

↓

front_image

---

media_file

↓

avatar_user.jpg

↓

user_profile

↓

avatar

---

## Motivazione Architetturale

Permette di sapere sempre:

- dove è usato un file
- se un file è orfano
- se un file può essere eliminato

senza dipendere da URL sparsi nel database.

---

# Parte 15 - Analytics e Telemetria

# Tabella: analytics_events

## Scopo

Rappresenta un evento generato all'interno della piattaforma.

Questa tabella costituisce la base per:

- statistiche
- dashboard amministrative
- business intelligence
- monitoraggio utilizzo
- metriche prodotto

---

## Tipo Tabella

Principale

---

## Nome Tabella

analytics_events

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo evento |
| user_id | UUID | NO | Utente associato |
| event_type | VARCHAR(100) | SI | Tipologia evento |
| entity_type | VARCHAR(50) | NO | Tipo entità coinvolta |
| entity_id | UUID | NO | Entità coinvolta |
| metadata_json | JSONB | NO | Dati aggiuntivi |
| occurred_at | TIMESTAMPTZ | SI | Momento evento |
| created_at | TIMESTAMPTZ | SI | Data registrazione |

---

## Valori Consentiti

### event_type

```text
login

user_registration

scan_completed

scan_confirmed

item_added

wishlist_added

listing_created

listing_viewed

offer_created

message_sent

match_generated

match_opened

achievement_unlocked

badge_earned

contribution_created

contribution_approved
```

---

## Foreign Keys

user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

analytics_events

---

## Vincoli

event_type non può essere vuoto.

occurred_at non può essere nullo.

---

## Indici

PRIMARY KEY (id)

INDEX (user_id)

INDEX (event_type)

INDEX (entity_type)

INDEX (entity_id)

INDEX (occurred_at)

---

## Regole Business

Gli eventi sono immutabili.

Gli eventi non devono essere modificati.

Gli eventi non devono essere cancellati.

---

## Esempio

Utente

↓

Scansione Oggetto

↓

analytics_event

↓

scan_completed

---

Utente

↓

Nuovo Annuncio

↓

analytics_event

↓

listing_created

---

## Motivazione Architetturale

Costituisce la sorgente primaria di tutte le statistiche della piattaforma.

---

# Tabella: analytics_daily_metrics

## Scopo

Rappresenta metriche aggregate giornaliere generate a partire dagli Analytics Events.

Questa tabella consente di alimentare dashboard e report senza effettuare elaborazioni pesanti in tempo reale.

---

## Tipo Tabella

Aggregazione

---

## Nome Tabella

analytics_daily_metrics

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo metrica |
| metric_date | DATE | SI | Giorno riferimento |
| metric_key | VARCHAR(100) | SI | Nome metrica |
| metric_value | BIGINT | SI | Valore aggregato |
| category | VARCHAR(50) | SI | Categoria |
| created_at | TIMESTAMPTZ | SI | Data calcolo |
| updated_at | TIMESTAMPTZ | SI | Data aggiornamento |

---

## Valori Consentiti

### category

```text
users

marketplace

matching

scanner

catalog

community

gamification

messaging
```

---

## Vincoli

metric_date non può essere vuota.

metric_key non può essere vuota.

metric_value deve essere maggiore o uguale a zero.

---

## Vincolo Anti-Duplicato

```text
UNIQUE
(
metric_date,
metric_key
)
```

---

## Indici

PRIMARY KEY (id)

UNIQUE (metric_date, metric_key)

INDEX (category)

INDEX (metric_date)

---

## Esempi Metriche

### Utenti

```text
daily_active_users

1250
```

---

### Marketplace

```text
listings_created

340
```

---

### Scanner

```text
scans_completed

890
```

---

### Matching

```text
matches_generated

420
```

---

### Catalogo

```text
contributions_created

35
```

---

## Compatibilità Dashboard Admin

Permette di mostrare:

```text
Andamento Utenti

Crescita Marketplace

Uso Scanner

Uso Matching

Attività Community
```

---

## Compatibilità Report

Permette la generazione di:

```text
Report Giornalieri

Report Settimanali

Report Mensili

Report Annuali
```

---

## Motivazione Architetturale

Riduce drasticamente il carico sul database operativo e consente la creazione di dashboard ad alte prestazioni.

---

# Parte 16 - Internazionalizzazione e Localizzazione

# Tabella: languages

## Scopo

Rappresenta le lingue supportate dalla piattaforma.

Questa tabella viene utilizzata per:

- traduzioni catalogo
- traduzioni interfaccia
- contenuti multilingua
- supporto internazionale

---

## Tipo Tabella

Configurazione

---

## Nome Tabella

languages

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo lingua |
| code | VARCHAR(10) | SI | Codice lingua ISO |
| name | VARCHAR(100) | SI | Nome lingua |
| native_name | VARCHAR(100) | SI | Nome lingua nativo |
| is_active | BOOLEAN | SI | Lingua attiva |
| is_default | BOOLEAN | SI | Lingua predefinita |
| sort_order | INTEGER | SI | Ordinamento |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |

---

## Valori Predefiniti

is_active = TRUE

is_default = FALSE

sort_order = 0

---

## Esempi Codici

```text
it

en

fr

de

es

ja
```

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

INDEX (is_default)

---

## Regole Business

Può esistere una sola lingua predefinita.

---

## Esempio

Italiano

```text
it
```

---

Inglese

```text
en
```

---

Giapponese

```text
ja
```

---

## Motivazione Architetturale

Centralizza la gestione delle lingue dell'intera piattaforma.

---

# Tabella: translations

## Scopo

Rappresenta una traduzione associata ad una specifica entità.

Questa tabella consente di tradurre qualsiasi elemento della piattaforma senza modificare le tabelle originali.

---

## Tipo Tabella

Principale

---

## Nome Tabella

translations

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo traduzione |
| language_id | UUID | SI | Lingua |
| entity_type | VARCHAR(50) | SI | Tipo entità |
| entity_id | UUID | SI | Record tradotto |
| field_name | VARCHAR(100) | SI | Campo tradotto |
| translated_value | TEXT | SI | Valore tradotto |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| updated_at | TIMESTAMPTZ | SI | Data modifica |

---

## Foreign Keys

language_id

→ languages.id

---

## Relazioni

languages (1)

↓

(N)

translations

---

## Valori Consentiti

### entity_type

```text
category

collection

rarity

series

item

item_version

item_variant

achievement

badge

system_setting
```

---

### field_name

Esempi:

```text
name

description

title

label
```

---

## Vincoli

language_id deve esistere.

entity_type deve essere valorizzato.

entity_id deve essere valorizzato.

field_name deve essere valorizzato.

translated_value non può essere vuoto.

---

## Vincolo Anti-Duplicato

```text
UNIQUE
(
language_id,
entity_type,
entity_id,
field_name
)
```

---

## Indici

PRIMARY KEY (id)

INDEX (language_id)

INDEX (entity_type)

INDEX (entity_id)

INDEX (field_name)

UNIQUE (
language_id,
entity_type,
entity_id,
field_name
)

---

## Regole Business

Una traduzione può riferirsi a qualsiasi entità della piattaforma.

Le traduzioni non modificano il dato originale.

---

## Esempio

Item

↓

Charizard

↓

Lingua

Italiano

↓

"Charizard"

---

Item

↓

Charizard

↓

Lingua

Francese

↓

"Dracaufeu"

---

Achievement

↓

First Scan

↓

Italiano

↓

"Prima Scansione"

---

## Compatibilità Catalogo Universale

Permette di tradurre:

```text
Categorie

Collezioni

Serie

Item

Versioni

Varianti
```

---

## Compatibilità Gamification

Permette di tradurre:

```text
Achievement

Badge

Messaggi
```

---

## Compatibilità Internazionale

Permette a CollectorVerse di operare su scala globale senza duplicare i dati del catalogo.

---

## Motivazione Architetturale

La separazione delle traduzioni dalle entità originali consente:

- supporto multilingua completo
- aggiunta nuove lingue senza migrazioni
- catalogo unico globale
- scalabilità internazionale

senza modificare la struttura delle tabelle esistenti.

---

# Parte 17 - Storico e Versionamento

# Tabella: entity_versions

## Scopo

Rappresenta lo storico delle modifiche effettuate alle entità principali della piattaforma.

La tabella consente di conservare una copia delle versioni precedenti dei dati.

Viene utilizzata per:

- storico modifiche
- ripristino dati
- audit avanzato
- confronto versioni
- recupero errori

---

## Tipo Tabella

Principale

---

## Nome Tabella

entity_versions

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo versione |
| entity_type | VARCHAR(50) | SI | Tipo entità |
| entity_id | UUID | SI | Record versionato |
| version_number | INTEGER | SI | Numero versione |
| changed_by_user_id | UUID | NO | Utente autore modifica |
| change_type | VARCHAR(30) | SI | Tipo modifica |
| snapshot_json | JSONB | SI | Stato completo entità |
| change_summary | TEXT | NO | Descrizione modifica |
| created_at | TIMESTAMPTZ | SI | Data modifica |

---

## Valori Consentiti

### entity_type

```text
collection

series

item

item_version

item_variant

catalog_contribution

user_profile

system_setting
```

---

### change_type

```text
create

update

restore

merge

delete
```

---

## Foreign Keys

changed_by_user_id

→ users.id

---

## Relazioni

users (1)

↓

(N)

entity_versions

---

## Vincoli

entity_type deve contenere un valore valido.

entity_id deve essere valorizzato.

version_number deve essere maggiore di zero.

snapshot_json non può essere vuoto.

---

## Vincolo Anti-Duplicato

```text
UNIQUE
(
entity_type,
entity_id,
version_number
)
```

---

## Indici

PRIMARY KEY (id)

INDEX (entity_type)

INDEX (entity_id)

INDEX (version_number)

INDEX (changed_by_user_id)

INDEX (created_at)

UNIQUE (
entity_type,
entity_id,
version_number
)

---

## Regole Business

Ogni modifica genera una nuova versione.

Le versioni precedenti non devono essere modificate.

Le versioni precedenti non devono essere eliminate.

---

## Esempio

Item

↓

Charizard

↓

Versione 1

↓

Versione 2

↓

Versione 3

---

## Compatibilità Catalogo Collaborativo

Permette di recuperare:

```text
Versioni precedenti

Correzioni errate

Modifiche vandaliche
```

---

## Compatibilità Audit

Consente di ricostruire completamente la cronologia.

---

## Motivazione Architetturale

Introduce il versionamento senza modificare le tabelle operative.

---

# Tabella: data_restore_requests

## Scopo

Rappresenta una richiesta di ripristino dati.

Utilizzata quando è necessario recuperare:

- contributi eliminati
- collezioni eliminate
- dati modificati per errore
- record archiviati

---

## Tipo Tabella

Principale

---

## Nome Tabella

data_restore_requests

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo richiesta |
| requester_user_id | UUID | SI | Richiedente |
| entity_type | VARCHAR(50) | SI | Tipo entità |
| entity_id | UUID | SI | Entità interessata |
| reason | TEXT | SI | Motivazione |
| status | VARCHAR(30) | SI | Stato richiesta |
| reviewed_by_user_id | UUID | NO | Revisore |
| review_notes | TEXT | NO | Esito revisione |
| created_at | TIMESTAMPTZ | SI | Data richiesta |
| reviewed_at | TIMESTAMPTZ | NO | Data revisione |

---

## Valori Consentiti

### status

```text
pending

approved

rejected

restored
```

---

## Foreign Keys

requester_user_id

→ users.id

---

reviewed_by_user_id

→ users.id

---

## Indici

PRIMARY KEY (id)

INDEX (requester_user_id)

INDEX (status)

INDEX (entity_type)

---

## Regole Business

Ogni richiesta deve essere valutata da un amministratore.

---

## Motivazione Architetturale

Permette il recupero controllato dei dati senza operazioni dirette sul database.

---

# Tabella: system_snapshots

## Scopo

Rappresenta i riferimenti ai backup logici della piattaforma.

Non contiene i dati del backup.

Contiene esclusivamente i metadati dei backup disponibili.

---

## Tipo Tabella

Amministrazione

---

## Nome Tabella

system_snapshots

---

## Primary Key

id UUID PRIMARY KEY

---

## Colonne

| Colonna | Tipo | Obbligatorio | Descrizione |
|----------|----------|----------|----------|
| id | UUID | SI | Identificativo snapshot |
| snapshot_name | VARCHAR(255) | SI | Nome snapshot |
| snapshot_type | VARCHAR(30) | SI | Tipo snapshot |
| storage_reference | TEXT | SI | Riferimento storage |
| file_size_bytes | BIGINT | NO | Dimensione |
| created_by_user_id | UUID | NO | Creatore snapshot |
| created_at | TIMESTAMPTZ | SI | Data creazione |
| expires_at | TIMESTAMPTZ | NO | Data eliminazione prevista |

---

## Valori Consentiti

### snapshot_type

```text
full

catalog

marketplace

analytics
```

---

## Foreign Keys

created_by_user_id

→ users.id

---

## Indici

PRIMARY KEY (id)

INDEX (snapshot_type)

INDEX (created_at)

INDEX (expires_at)

---

## Regole Business

Gli snapshot rappresentano backup logici disponibili per attività amministrative.

---

## Motivazione Architetturale

Permette la tracciabilità dei backup senza memorizzare i dati direttamente nel database operativo.

---

# Mappatura Completa Database CollectorVerse

## Obiettivo

Questa sezione descrive tutte le relazioni tra le tabelle del database CollectorVerse.

Serve per:

- verificare la coerenza architetturale
- identificare le dipendenze
- preparare la generazione DDL PostgreSQL
- preparare Supabase
- preparare Prisma/ORM futuri

---

## Legenda

```text
(1)
=
Un Record

(N)
=
Molti Record
```

Esempio:

```text
users (1)
↓
(N)
user_items
```

significa:

Un Utente possiede molti Oggetti.

---

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

