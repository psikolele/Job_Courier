# jobs.ch – Analisi per Web Scraping (Competitor: jobs.ch)  
_Last update: 02/03/2026_

## 1. Panoramica del sito

jobs.ch è una delle principali, se non la principale, piattaforme di ricerca lavoro in Svizzera, con posizionamento chiaro come “leading job search platform” a livello nazionale.[web:20][web:22][web:23]  
Il portale offre annunci di lavoro, profili aziendali, un calcolatore salariale, recensioni sulle aziende e servizi aggiuntivi come pool di talenti (“Spotted by jobs.ch”) e app mobile dedicata.[page:3][web:23]

---

## 2. Struttura dei contenuti rilevante per lo scraping

### 2.1 Homepage

La homepage internazionale (versione EN) presenta una sezione “Interesting services for your job search” con blocchi dedicati a profilo, raccomandazioni personalizzate, calcolatore salariale e talent pool.[page:3]  
Sotto questa sezione, il sito elenca:

- Servizi chiave per la ricerca (profilo, raccomandazioni, app, talent pool).[page:3]  
- Sezione “Explore companies that suit you” con carousel di aziende con rating, badge (es. no dress code, working from home, free fruits) e elementi di employer branding.[page:3]  
- Navigazione alternativa “Another way to start your job search” basata su campi professionali, regioni, ricerche più frequenti e città principali.[page:3]  

Questa struttura suggerisce che il portale è fortemente segmentato per settore e regione, simile a JobCourier ma con maggiore enfasi su servizi collaterali (salari, recensioni).

### 2.2 Pagine di lista annunci

La pagina di ricerca annunci usa URL del tipo `https://www.jobs.ch/de/stellenangebote/?term=` con parametri per keyword, regione e filtri.[page:4][web:27]  
Il contenuto testuale estratto mostra:

- Form di ricerca con campi “Beruf oder Stichwort” (professione o parola chiave) e “Städte oder Regionen”.[page:4]  
- Filtri avanzati: data di pubblicazione, percentuale di lavoro (pensum), campo professionale, tipo di contratto, lingua, modalità di impiego.[page:4]  
- Un elenco di risultati (“Suchergebnisliste”) accessibile con link o anchor, da cui estrarre singoli annunci.[page:4]  

La struttura HTML dettagliata dei risultati non è esplicitata nel testo, ma sulla base del layout tipico:

- Ogni annuncio è rappresentato da una “card” con titolo, azienda, località, percentuale e tag.[web:27]  
- Spesso è presente un link alla pagina dettaglio annuncio e un link al profilo aziendale.

### 2.3 Tassonomie: campi professionali e regioni

La homepage elenca numerosi **occupational fields** con il numero di annunci per ciascuno.[page:3]  
Esempi di campi (estratti):

- Admin / HR / Consulting / CEO – 6607 annunci.[page:3]  
- Banking / Insurance – 2359.[page:3]  
- Information Technology / Telecom. – 2857.[page:3]  
- Medicine / Care / Therapy – 6809.[page:3]  
- Sales / Customer Service / Admin – 4578.[page:3]  

Analogamente, il sito raggruppa annunci per **regioni**:

- German part of Switzerland – 41432 annunci, Region of Zurich / Schaffhausen – 12410, Ticino – 417, Western Switzerland – 5061, ecc.[page:3]  

Queste tassonomie sono cruciali per definire loop di scraping basati su combinazioni campo professionale + regione, usando i link che la homepage fornisce come entry point.

### 2.4 Servizi e contenuti aggiuntivi

Oltre agli annunci, jobs.ch offre:

- **Salary Calculator** per calcolo e confronto del reddito annuale lordo.[page:3]  
- **Company Search** con profili aziendali, recensioni, informazioni su benefit, cultura, ecc.[page:3]  
- Accesso a piattaforme correlate (jobup.ch per la Romandia, topjobs.ch, jobwinner.ch, jobs4sales.ch, financejobs.ch, ingjobs.ch, ictcareer.ch, alpha.ch), tutte parte dell’ecosistema JobCloud.[web:20][web:23][web:28]  

Questi contenuti sono potenzialmente interessanti da mappare come network di portali, ma lo scraping sistematico di piattaforme multiple aumenta complessità e necessità di attenzione ai termini d’uso.

---

## 3. Link e pattern di navigazione

### 3.1 Link principali per la ricerca annunci

Dalla homepage e dalla pagina di ricerca risulta che le principali vie d’accesso ai job sono:[page:3][page:4][web:27]

- Ricerca per parola chiave e regione via form di ricerca.  
- Link “Jobs by occupational fields” con elenco di campi professionali, ciascuno probabilmente collegato a una pagina filtrata.  
- Link “Jobs by region” per regioni geografiche svizzere (Zurigo, Romandia, Ticino, ecc.).  
- Link “Most searched” e “Top cities” con pre-configurazioni di ricerca pronte all’uso.  

Per lo scraping:

- Conviene partire dai link “occupational fields” e “jobs by region” per generare combinazioni campo + regione.  
- In alternativa, usare la ricerca generale con query vuota o generica (`term=`) e filtri impostati via parametri URL.

### 3.2 Struttura di lista e paginazione

La pagina `stellenangebote/?term=` supporta filtri multipli e verosimilmente un parametro di paginazione (es. `page=`, `pageNum=` o simile), da verificare via ispezione HTML e URL durante l’uso normale del sito.[page:4][web:27]  
Per evitare carico eccessivo:

- Limitare il numero di pagine per combinazione di filtro.  
- Introdurre sleep casuali tra le richieste.  

---

## 4. Immagini e asset visivi

Sulla homepage sono presenti:

- Immagini collegate alle aziende in evidenza nel carousel (“Explore companies that suit you”), con loghi, rating e tag visivi (es. “No dress code”, “Working from home”, “Free fruits”, “Training”).[page:3]  
- Icone o illustrazioni per i servizi (profilo, calcolatore salariale, talent pool, app).[page:3]  

Per uno scraping focalizzato sugli asset visivi:

- Selezionare gli `<img>` all’interno della sezione carousel aziende e associare il file alle entità aziendali (nome, rating, benefit).[page:3]  
- Valutare se recuperare le immagini di icone o solo quelle di brand, a seconda dell’uso finale (analisi brand, comparazione employer branding, ecc.).

---

## 5. Metodo di comunicazione e stile di scrittura

### 5.1 Tono e posizionamento

jobs.ch si presenta come **leader svizzero** nel recruiting online, con tono istituzionale ma orientato al supporto del candidato.[web:20][web:22][web:23]  
Frasi come “Switzerland’s leading job search platform, where your perfect job is just a few clicks away” enfatizzano facilità, vicinanza e ampiezza di offerta.[web:23]

### 5.2 Struttura e linguaggio

Lo stile usa:

- Headline esplicite “Finding a job with the Swiss leader in online recruitment: jobs.ch”.[page:3][web:22][web:23]  
- Paragrafi che combinano descrizione del servizio con esempi concreti (“Explore our IT job listings…”, “Healthcare professionals can find various positions…”).[page:3]  
- Linguaggio inclusivo e orientato al beneficio (“Finding your ideal job has never been easier.”, “Join our community today and take the next step in your career”).[page:3][web:23]  

Rispetto a JobCourier, jobs.ch ha un tono più globale e strutturato, meno local-oriented e con maggiore enfasi su ecosistema di servizi (salary, aziende, app).[page:3][web:13]

---

## 6. Considerazioni tecniche per lo scraping

### 6.1 Entità da modellare

In un contesto di scraping del competitor jobs.ch, le entità più rilevanti sono:

- **Offerta di lavoro**: titolo, azienda, località, percentuale (pensum), data, descrizione breve, tag, URL dettaglio.[page:4][web:27]  
- **Pagina dettaglio annuncio**: descrizione estesa, requisiti, benefit, tipo di contratto, settore, lingua, eventuale salario indicato.  
- **Campo professionale**: nome e numero di annunci (come da lista sulla homepage).[page:3]  
- **Regione**: nome regione e numero di annunci.[page:3]  
- **Azienda**: nome, rating, benefit (no dress code, lavoro da casa, frutta gratis, formazione, ecc.), logo.[page:3]  
- **Strumenti**: link al Salary Calculator, Company Search, eventuale API o endpoint interno (se esistente e legittimo da usare).[page:3]  

### 6.2 Nota su termini d’uso ed etica

jobs.ch appartiene all’ecosistema JobCloud, che include diversi portali premium e tecnologie di recruiting.[web:28]  
Prima di implementare scraping intensivo è consigliabile:

- Verificare i Terms of Use e robots.txt per restrizioni su crawling automatico.  
- Limitare il crawling a uso interno/analitico e non redistribuire contenuti protetti (descrizioni, testi) in forma pubblica o commerciale.

---

## 7. Specifiche operative di scraping (bozza)

Questa sezione è pensata per essere usata in IDE AI come Antigravity come “spec” operativa.

### 7.1 Obiettivo

Estrarre un dataset di offerte di lavoro da jobs.ch per analizzare il posizionamento del competitor rispetto a JobCourier (volumi per settore e regione, tipi di ruoli, employer branding).[page:3][web:13][web:27]  

### 7.2 Campi minimi per listing

Per ogni job nella pagina di lista:

- `title`: titolo annuncio.  
- `company`: nome azienda.  
- `location`: città/area.  
- `region`: regione macro (se presente).  
- `occupational_field`: campo professionale (se deducibile dalla pagina o dal filtro).  
- `workload`: percentuale (es. 80–100%).  
- `published_at`: data pubblicazione.  
- `detail_url`: URL della pagina dettaglio.  

### 7.3 Campi aggiuntivi per dettaglio

Per ogni job, dalla pagina dettaglio:

- `description`: testo completo dell’annuncio.  
- `requirements`: elenco requisiti (se strutturati).  
- `benefits`: lista benefit (se presenti).  
- `contract_type`: tipo di contratto (tempo indeterminato, temporaneo, stage, ecc.).  
- `language`: lingua principale dell’annuncio.  

### 7.4 Pseudopiano di scraping

1. Raccogli i link per “Jobs by occupational fields” dalla homepage.[page:3]  
2. Per ogni campo, raccogli i link “Jobs by region” o filtra per regione tramite parametri URL.[page:3][page:4]  
3. Per ogni combinazione (campo, regione), richiama la pagina lista con parametri appropriati, gestendo la paginazione.  
4. Per ogni annuncio in lista, estrai i campi di base e metti in coda gli URL di dettaglio.  
5. Visita le pagine di dettaglio per arricchire i campi avanzati (descrizione, requisiti, benefit).  
6. Deduplica per `detail_url` o ID interno dell’annuncio.

---

## 8. Titolo del file e uso

- Nome file consigliato: `jobs.ch.md` (competitor diretto rispetto a JobCourier).[web:20][web:22][web:23]  
- Questo file può essere salvato come artifact in Antigravity per guidare agenti di scraping, analisi e confronto competitivo contro `jobcourier.ch.md` già creato.[page:3][web:28]
