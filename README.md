## Anteprima della piattaforma

### Dashboard

Panoramica della struttura e dei principali indicatori.
<img width="1440" height="813" alt="Screenshot 2026-10-10 alle 13 47 10" src="https://github.com/user-attachments/assets/293e6c79-97be-4697-97e6-480c1347b35c" />
<img width="1440" height="813" alt="Screenshot 2026-10-10 alle 13 47 31" src="https://github.com/user-attachments/assets/0e7f2dab-2a43-48b5-ac4b-4f47738517ef" />
<img width="1440" height="812" alt="Screenshot 2026-10-10 alle 12 46 04" src="https://github.com/user-attachments/assets/9cbcb33c-9e50-4ae3-8003-36ad86c1f3cf" />



# StayBase

### Piattaforma SaaS multi-tenant per hospitality, gestione operativa e vendita diretta.

**StayBase** è una piattaforma che ho ideato e sviluppato per integrare la gestione di hotel, B&B e case vacanze con la loro distribuzione commerciale e presenza digitale.

Il progetto riunisce PMS, Booking Engine, Channel Manager, strumenti Revenue e RMS, gestione della vetrina, SEO progressiva e servizi dedicati alle esperienze sul territorio.

L’obiettivo è costruire un ambiente nel quale prenotazioni, camere, disponibilità, tariffe, contenuti e attività dello staff condividano dati e processi coerenti.

Sono **Gerardo Fortino, Founder e CTO di StayBase**. Mi occupo della progettazione del prodotto, dell’architettura applicativa, dello sviluppo full-stack, delle integrazioni e della SEO tecnica.

[Visita StayBase](https://staybase.it) · [Contattami](mailto:info@staybase.it)

---

## Indice

- [Anteprima della piattaforma](#anteprima-della-piattaforma)
- [Il problema](#il-problema)
- [La visione del prodotto](#la-visione-del-prodotto)
- [Destinatari](#destinatari)
- [Architettura applicativa](#architettura-applicativa)
- [Modello multi-tenant](#modello-multi-tenant)
- [Ruoli e autorizzazioni](#ruoli-e-autorizzazioni)
- [Moduli funzionali](#moduli-funzionali)
- [Integrazioni](#integrazioni)
- [Stack tecnologico](#stack-tecnologico)
- [Sicurezza](#sicurezza)
- [Qualità e validazione](#qualità-e-validazione)
- [Deployment e configurazione](#deployment-e-configurazione)
- [Scelte di sviluppo](#scelte-di-sviluppo)
- [Il mio contributo](#il-mio-contributo)
- [Stato del progetto](#stato-del-progetto)
- [Repository e codice sorgente](#repository-e-codice-sorgente)
- [Contatti](#contatti)

---

## Il problema
<img width="1440" height="811" alt="Screenshot 2026-10-10 alle 13 38 31" src="https://github.com/user-attachments/assets/dcff391d-8c33-40a2-a4f5-21a4d569d1ca" />

Una struttura ricettiva utilizza spesso strumenti diversi per gestire:

- prenotazioni e soggiorni;
- camere e disponibilità;
- prezzi e restrizioni;
- distribuzione sui portali;
- pagamenti;
- attività di reception;
- housekeeping;
- comunicazione con gli ospiti;
- sito web e contenuti;
- analisi delle performance.

Questa frammentazione introduce passaggi manuali, duplicazione delle informazioni e difficoltà nel mantenere allineati sistemi diversi.

Una modifica alla disponibilità, per esempio, può avere conseguenze sul planning interno, sulla vendita diretta e sui canali OTA. Gestire questi passaggi separatamente aumenta il rischio di incoerenze.

StayBase nasce per affrontare questa complessità attraverso un prodotto verticale, progettato intorno ai processi dell’ospitalità.

## La visione del prodotto

Sto costruendo StayBase come un sistema che collega tre dimensioni della stessa attività:

1. **Operatività:** gestire strutture, camere, soggiorni e lavoro quotidiano.
2. **Distribuzione:** coordinare disponibilità, tariffe e prenotazioni sui canali di vendita.
3. **Acquisizione diretta:** sviluppare una presenza digitale capace di trasformare visite e contatti in prenotazioni.

La vendita diretta è centrale nel progetto. L’obiettivo è dare alle strutture maggiore controllo sulla relazione con gli ospiti, sui contenuti e sui propri canali commerciali.

L’integrazione con le OTA completa questa strategia, permettendo alla struttura di gestire la distribuzione esterna all’interno dello stesso ambiente operativo.

## Destinatari
<img width="1440" height="813" alt="Screenshot 2026-10-10 alle 13 38 15" src="https://github.com/user-attachments/assets/18b3fab4-cca3-4df1-80be-a7efe60e48ef" />


StayBase è progettato per:

| Destinatario | Esigenza |
|---|---|
| Hotel | Coordinare operatività, camere, distribuzione e performance |
| B&B | Gestire prenotazioni e presenza digitale con strumenti integrati |
| Case vacanze | Organizzare disponibilità, soggiorni e vendita diretta |
| Gestori di più strutture | Lavorare su più sedi con accessi e responsabilità differenziati |
| Staff operativo | Accedere alle funzioni necessarie al proprio lavoro |
| Operatori di esperienze | Gestire e vendere attività legate al territorio |
| Content creator | Collaborare con le strutture attraverso un’area dedicata |

## Architettura applicativa

StayBase utilizza un’architettura con frontend separato dal backend e comunicazione attraverso API.

### Frontend

Il frontend è sviluppato in **React**, con **Tailwind CSS** per la costruzione delle interfacce.

Il perimetro comprende:

- pannelli gestionali;
- navigazione tra strutture e sedi;
- interfacce differenziate per ruolo;
- vetrine pubbliche;
- percorsi di prenotazione;
- ambienti dedicati a esperienze e operatori.

Le restrizioni nell’interfaccia aiutano l’utente a orientarsi tra le funzioni disponibili. L’autorizzazione effettiva viene applicata anche sul backend.

### Backend

Il backend è sviluppato in **Python con FastAPI**.

Gestisce:

- autenticazione;
- risoluzione del contesto utente;
- autorizzazioni;
- logica applicativa;
- accesso ai dati;
- integrazioni con servizi esterni;
- endpoint per le interfacce pubbliche e gestionali.

L’organizzazione in router e servizi permette di separare le responsabilità dei diversi domini applicativi.

### Persistenza

Il database è **MongoDB**.

Il modello dei dati comprende entità legate a organizzazioni, strutture, utenti, membership e processi operativi del prodotto.

La separazione tra tenant viene applicata attraverso il contesto di accesso e i controlli delle operazioni sul backend.

## Modello multi-tenant

Il multi-tenant è una parte centrale dell’architettura.

StayBase distingue:

- **organizzazione:** il contesto aziendale;
- **struttura o sede:** l’unità operativa;
- **utente:** l’identità che accede al sistema;
- **membership:** la relazione tra utente, organizzazione, ruolo e ambito di accesso.

Il backend risolve un contesto che determina:

- tenant di appartenenza;
- ruolo;
- sedi accessibili;
- ambito operativo;
- accesso ai dati economici;
- permessi applicabili.

Questo modello permette di gestire utenti con responsabilità differenti e organizzazioni con più strutture.

La selezione di una sede nell’interfaccia deve rimanere coerente con le autorizzazioni dell’utente e con i dati restituiti dalle API.

## Ruoli e autorizzazioni

Il modello di accesso distingue tre ruoli principali.

| Ruolo | Ambito |
|---|---|
| **Owner** | Gestione dell’organizzazione, delle sedi e delle autorizzazioni |
| **Manager** | Gestione operativa, con accesso economico configurabile |
| **Operatore** | Attività quotidiane previste dai permessi assegnati |

Le autorizzazioni seguono un principio di **default deny**: una funzione richiede un permesso esplicito.

Il controllo riguarda sia l’azione richiesta sia il contesto nel quale viene eseguita.

Tra i casi gestiti rientrano:

- membership sospese o revocate;
- accesso alle sole sedi autorizzate;
- limitazioni sui dati economici;
- restrizioni sulle operazioni amministrative;
- protezione dell’ultimo Owner attivo.

La protezione dell’ultimo Owner comprende controlli sulla concorrenza, per evitare che modifiche simultanee lascino un’organizzazione senza un responsabile attivo.

## Moduli funzionali

I moduli seguenti descrivono il perimetro del prodotto. Lo stato di completamento e validazione viene valutato per ciascun flusso.

### PMS — Property Management System

Il PMS costituisce il nucleo gestionale di StayBase.

Il suo perimetro comprende:

- gestione delle strutture;
- gestione delle camere e delle relative tipologie;
- prenotazioni e soggiorni;
- planning;
- disponibilità;
- informazioni operative degli ospiti;
- condizioni e politiche di prenotazione;
- coordinamento con tariffe e distribuzione.

Il principio è mantenere una relazione coerente tra prenotazione, periodo di soggiorno, camera e disponibilità vendibile.

### Front Desk

Il Front Desk porta il prodotto nel lavoro quotidiano della reception.

Il perimetro comprende:

- consultazione delle prenotazioni;
- gestione degli arrivi e delle partenze;
- accesso alle informazioni del soggiorno;
- aggiornamento degli stati operativi;
- coordinamento con camere e disponibilità.

L’obiettivo è rendere accessibili le informazioni necessarie durante il servizio, riducendo i passaggi tra schermate e strumenti separati.

### Housekeeping

Il modulo housekeeping collega il lavoro operativo allo stato delle camere.

Il perimetro comprende:

- consultazione degli stati delle camere;
- organizzazione delle attività;
- aggiornamento delle informazioni operative;
- coordinamento tra reception e personale;
- accesso secondo ruolo e sede.

### Booking Engine

Il Booking Engine gestisce il percorso di prenotazione sul canale diretto della struttura.
<img width="1440" height="814" alt="Screenshot 2026-10-10 alle 13 48 20" src="https://github.com/user-attachments/assets/5c7c9071-7cde-44e7-a7d0-67eb761fd33b" />


Il perimetro comprende:

- ricerca delle disponibilità;
- selezione del soggiorno;
- consultazione delle opzioni di vendita;
- raccolta dei dati necessari alla prenotazione;
- applicazione delle condizioni previste;
- collegamento con i flussi di pagamento;
- registrazione della prenotazione nel gestionale.

La disponibilità esposta al cliente deve essere coerente con quella utilizzata dal PMS e dalla distribuzione.

### Channel Manager

L’integrazione con **Channex** gestisce lo scambio dei dati con i canali OTA collegati.

I flussi comprendono:

- disponibilità;
- tariffe;
- restrizioni;
- ricezione delle prenotazioni;
- aggiornamenti delle prenotazioni;
- mapping tra camere e piani tariffari.

Una parte rilevante dello sviluppo riguarda la precisione degli aggiornamenti.

Tra i casi verificati:

- aggiornamento di una singola camera;
- aggiornamento di una singola data;
- aggiornamento di intervalli;
- esclusione delle camere non coinvolte;
- trattamento corretto del giorno di checkout;
- coerenza tra dati locali e richieste inviate al provider.

L’attivazione di un canale per una struttura comprende configurazione, mapping e verifica del collegamento.

### Revenue e RMS

Il perimetro Revenue e RMS comprende strumenti per gestire prezzi e leggere l’andamento commerciale della struttura.

Le aree includono:

- tariffe;
- restrizioni di vendita;
- prezzi dinamici;
- aggiornamenti massivi;
- politiche commerciali;
- ricavi;
- occupazione;
- andamento delle prenotazioni;
- confronto delle performance di camere e tariffe.

L’accesso alle informazioni economiche dipende dai permessi dell’utente.

### Vetrina della struttura

La vetrina pubblica collega presentazione e vendita.

Il perimetro comprende:

- descrizione della struttura;
- camere e servizi;
- contenuti fotografici;
- informazioni territoriali;
- contatti;
- condizioni;
- collegamento al percorso di prenotazione.

La gestione delle immagini prevede categorie utili a organizzare la presentazione, come camere, bagni, ambienti comuni, esterni e viste.

### SEO progressiva

La SEO progressiva è il percorso di sviluppo della presenza organica della struttura.

Il progetto comprende:

- organizzazione dei contenuti;
- pagine dedicate;
- pagine territoriali;
- informazioni coerenti tra struttura, servizi e destinazione;
- titoli e descrizioni;
- FAQ;
- collegamento con strumenti di misurazione e gestione della presenza sui motori di ricerca.

L’obiettivo è permettere alla presenza digitale di crescere insieme ai contenuti e all’attività della struttura.

### Analytics

Il perimetro analitico comprende:

- ricavi;
- occupazione;
- prenotazioni;
- performance di camere e tariffe;
- traffico;
- acquisizione;
- funnel di prenotazione;
- performance dei contenuti.

Le metriche servono a collegare attività operative, distribuzione e risultati del canale diretto.

### Health Score

Il progetto comprende un indicatore sintetico dello stato del tenant.

Il suo scopo è aiutare l’operatore a individuare aree della configurazione e della presenza digitale che richiedono attenzione.

### Comunicazione con gli ospiti

Il perimetro comprende strumenti per:

- messaggistica;
- informazioni utili al soggiorno;
- FAQ;
- richieste di contatto;
- comunicazioni collegate ai processi della struttura.

L’obiettivo è mantenere le comunicazioni nel contesto operativo al quale appartengono.

### Experiences

L’area Experiences estende StayBase alle attività e ai servizi legati al territorio.

Il perimetro comprende:

- vetrine delle esperienze;
- gestione dei contenuti;
- ambienti gestionali dedicati agli operatori;
- vendita diretta;
- gestione dei processi di prenotazione.

Questo permette di collegare l’offerta ricettiva a ciò che l’ospite può vivere nella destinazione.

### Content creator

Il progetto comprende un’area dedicata ai professionisti della produzione di contenuti.

L’obiettivo è facilitare il collegamento tra strutture e creator, con profili e strumenti gestionali dedicati.

Fotografia, video e contenuti editoriali diventano così parte del percorso di sviluppo della presenza digitale della struttura.

## Integrazioni

Le integrazioni vengono gestite come componenti del prodotto, con configurazioni e verifiche dedicate.

| Servizio | Ambito | Aspetti da validare |
|---|---|---|
| **Channex** | Distribuzione ricettiva e collegamento alle OTA | Mapping, sincronizzazione, prenotazioni e webhook |
| **Stripe** | Pagamenti | Configurazione degli account, eventi, conferme e rimborsi |
| **tRavio** | Perimetro travel e distribuzione | Flussi e copertura previsti dall’integrazione |
| **Postmark** | Email transazionali | Configurazione del provider e consegna delle email |
| **Google e LinkedIn** | Autenticazione federata | Configurazione OAuth/OIDC e completamento dei percorsi di accesso |

L’integrazione di un provider richiede sia la logica applicativa sia la configurazione dell’ambiente nel quale il prodotto viene eseguito.

Per ciascun servizio distinguo:

1. implementazione;
2. validazione nell’ambiente di test;
3. configurazione di produzione;
4. verifica del flusso completo.

## Stack tecnologico

| Livello | Tecnologie |
|---|---|
| Interfaccia | React, Tailwind CSS |
| API e logica applicativa | Python, FastAPI |
| Persistenza | MongoDB |
| Sessioni | JWT |
| Protezione delle password | bcrypt |
| Autenticazione federata | OAuth 2.0, OpenID Connect |
| Distribuzione ricettiva | Channex |
| Pagamenti | Stripe |
| Email transazionali | Integrazione predisposta per Postmark |
| Containerizzazione | Docker, Docker Compose |
| Ambiente server | Hetzner |
| Versionamento | Git, GitHub |
| Verifiche dell’interfaccia | Playwright |

## Sicurezza

La sicurezza viene applicata ai diversi livelli del sistema.

### Autenticazione e account

Il lavoro comprende:

- policy delle password;
- protezione delle credenziali;
- verifica dell’email tramite OTP;
- scadenza e consumo dei codici;
- limiti sui tentativi e sugli invii;
- recupero della password;
- invalidazione delle sessioni dopo il reset;
- registrazione dell’accettazione dei termini e della relativa versione.

### Autorizzazione

Il backend verifica:

- identità dell’utente;
- validità della membership;
- tenant;
- sedi accessibili;
- ruolo;
- permessi;
- accesso ai dati economici.

Questi controlli vengono applicati alle operazioni protette, comprese quelle che possono essere richiamate direttamente attraverso le API.

### Autenticazione federata

Il lavoro sui provider social comprende flussi OAuth/OIDC con controlli su:

- `state`;
- `nonce`;
- firma del token;
- issuer;
- audience;
- scadenza;
- PKCE nel flusso Google.

Il collegamento di un’identità social a un account esistente richiede un contesto autenticato.

## Qualità e validazione

I test vengono concentrati sui comportamenti che possono compromettere dati, accessi o operatività.

Le aree di verifica comprendono:

- isolamento tra tenant;
- accesso alle sedi;
- ruoli e permessi;
- registrazione e verifica dell’email;
- recupero della password;
- invalidazione delle sessioni;
- protezione dell’ultimo Owner;
- concorrenza nelle modifiche amministrative;
- disponibilità e intervalli di soggiorno;
- sincronizzazione con Channex;
- pagamenti e rimborsi;
- percorsi dell’interfaccia.

### Verifica delle integrazioni

Per i flussi esterni confronto, dove applicabile:

- operazione richiesta dall’utente;
- dati registrati nel database;
- payload inviato al provider;
- risposta ricevuta;
- stato risultante nei sistemi coinvolti.

Questo permette di verificare anche errori che possono rimanere invisibili nell’interfaccia, come l’aggiornamento di camere o date estranee all’operazione.

## Deployment e configurazione

StayBase utilizza servizi containerizzati con **Docker Compose** nell’ambiente server.

Il deployment comprende più elementi:

- versione del codice;
- build del frontend;
- servizi backend;
- database;
- variabili d’ambiente;
- credenziali dei provider;
- webhook;
- configurazione dei domini;
- verifiche dopo la pubblicazione.

Codice, dati persistenti e configurazione vengono gestiti come componenti distinti del rilascio.

Il trasferimento del repository, da solo, non trasferisce il database né configura automaticamente i servizi esterni.

La verifica del deployment deve quindi includere i flussi effettivamente utilizzati dal prodotto.

## Scelte di sviluppo

### Dominio hospitality

Ho organizzato il prodotto intorno alle entità e ai processi dell’ospitalità: strutture, camere, soggiorni, disponibilità, tariffe e distribuzione.

Questa scelta mantiene le funzioni aderenti al lavoro degli operatori.

### Contesto di accesso centralizzato

La risoluzione del contesto utente permette di applicare regole coerenti tra moduli differenti.

Tenant, sedi e permessi accompagnano la richiesta lungo il percorso di elaborazione.

### Backend organizzato per responsabilità

Router e servizi separano le aree applicative e rendono più leggibili i flussi.

Questa organizzazione aiuta a individuare dove applicare una regola e come verificarne gli effetti.

### Coerenza tra gestione e vendita

Il prodotto collega informazioni operative e commerciali.

Una prenotazione, per esempio, deve produrre effetti coerenti sul soggiorno, sul planning e sulla disponibilità distribuita.

### Validazione dei casi limite

Dedico attenzione agli intervalli temporali, alle modifiche concorrenti e alle operazioni parziali.

Nel dominio ricettivo, un singolo giorno o una camera aggiornata per errore possono produrre conseguenze operative concrete.

### Crescita modulare

I moduli condividono il contesto della struttura, mantenendo responsabilità funzionali riconoscibili.

Questo permette di estendere il prodotto senza perdere la relazione tra dati, autorizzazioni e processi.

## Il mio contributo

Come Founder e CTO mi occupo di:

- definizione della visione e del perimetro del prodotto;
- analisi dei processi delle strutture ricettive;
- progettazione dell’architettura;
- modellazione dei dati;
- sviluppo frontend e backend;
- progettazione delle API;
- autenticazione e autorizzazioni;
- integrazioni con servizi esterni;
- SEO tecnica e organizzazione dei contenuti;
- deployment;
- verifica dei flussi critici.

Il confronto con professionisti dell’ospitalità contribuisce a trasformare esigenze operative reali in decisioni di prodotto.

## Stato del progetto

StayBase è in sviluppo e validazione operativa.

Il prodotto comprende moduli con livelli differenti di completamento. Le verifiche vengono effettuate per singolo flusso, distinguendo:

| Stato | Significato |
|---|---|
| **Implementato** | La funzione è presente nell’applicazione |
| **Validato in test** | Il comportamento è stato verificato nell’ambiente di test |
| **Configurato in produzione** | Dati, credenziali e servizi necessari sono disponibili |
| **Validato in produzione** | Il percorso completo è stato verificato nell’ambiente operativo |

Le attività di consolidamento comprendono il completamento delle configurazioni, la validazione delle integrazioni e la verifica dei percorsi utilizzati dalle strutture.

## Repository e codice sorgente

Questo repository è la presentazione pubblica di StayBase.

Raccoglie:

- descrizione del prodotto;
- architettura;
- perimetro funzionale;
- stack tecnologico;
- scelte di sviluppo;
- aggiornamenti condivisibili sul progetto.

Il codice sorgente, la documentazione interna e le configurazioni operative sono mantenuti in repository privati.

## Contatti

**Gerardo Fortino**  
Founder & CTO — StayBase

- **Sito:** [staybase.it](https://staybase.it)
- **Email:** [info@staybase.it](mailto:info@staybase.it)

Per confronti tecnici, collaborazioni e partecipazione ai test del prodotto, puoi contattarmi via email.
