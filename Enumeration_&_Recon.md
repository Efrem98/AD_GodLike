### External Recon and Enumeration Principles

External reconnaissance serve a raccogliere informazioni pubbliche sul target prima del pentest, verificando lo scope e individuando possibili dati esposti.  
Aiuta a evitare errori operativi e a garantire che le attività siano condotte sugli asset corretti.  
L’obiettivo è ottenere una visione generale dell’ambiente e scoprire eventuali leak (credenziali, repository, documenti, link interni).

### What Are We Looking For? (Parte 1)

Durante la fase di external reconnaissance cerchiamo informazioni pubbliche utili per comprendere l’infrastruttura del target e facilitare eventuali accessi.  
Questi dati possono includere credenziali esposte, servizi pubblici e configurazioni dell’ambiente.  
L’obiettivo è ottenere vantaggi pratici per il pentest (es. accesso VPN, enumerazione utenti, attacchi password-based).

---

### Key Data Points

| Data Point | Description |
|------------------|------------------|
| IP Space         | ASN, netblock, infrastruttura pubblica, cloud, DNS e provider di hosting utilizzati dall’organizzazione.|
| Domain Info      | Informazioni sui domini: subdomain, servizi esposti (mail, VPN, web), amministrazione dominio e difese attive (SIEM, AV, IDS/IPS).|
| Schema Format    | Formato username/email, account AD e policy password per costruire wordlist e attacchi (spraying, brute force, stuffing).|
| Data Disclosures | File pubblici (.pdf, .docx, .xlsx) contenenti informazioni interne (intranet, metadata, share, software, credenziali).|
| Breach Data      | Credenziali e dati sensibili esposti pubblicamente utili per ottenere accesso iniziale.|

### Where Are We Looking? (Parte 2)

Le informazioni di external reconnaissance possono essere raccolte tramite diversi tool e fonti pubbliche online.  
Queste risorse permettono di ottenere dati su infrastruttura, domini, utenti e possibili credenziali esposte.  
L’obiettivo è sfruttare fonti OSINT per costruire una visione completa del target.

---

### Key Resources

| Resource                     | Examples |
|-----------------------------|----------|
| ASN / IP registrars         | IANA, ARIN (Americas), RIPE (Europe), BGP Toolkit |
| Domain Registrars & DNS     | DomainTools, PTRArchive, ICANN, query DNS manuali (es. 8.8.8.8) |
| Social Media                | LinkedIn, Twitter, Facebook, news e informazioni pubbliche sull’organizzazione |
| Public-Facing Company Websites | Sito aziendale, pagine About/Contact, documenti e contenuti pubblici |
| Cloud & Dev Storage Spaces  | GitHub, AWS S3, Azure Blob, Google Dorks |
| Breach Data Sources         | HaveIBeenPwned, Dehashed, credenziali leakate utilizzabili per accessi (VPN, OWA, Citrix, ecc.) |

### Finding Address Spaces

<img width="967" height="459" alt="image" src="https://github.com/user-attachments/assets/9c71d67a-bf7a-4cbb-ac5f-adb3ccc5b766" />

Il BGP Toolkit (es. Hurricane Electric) permette di identificare ASN e blocchi IP associati a un’organizzazione, distinguendo tra infrastruttura self-hosted e cloud/terze parti.  
È fondamentale capire dove risiedono i sistemi per evitare di testare asset fuori scope, soprattutto in ambienti condivisi (AWS, Azure, Cloudflare).  
Durante il pentest bisogna rispettare rigorosamente lo scope e verificare eventuali autorizzazioni anche da provider terzi.  
In caso di dubbi, è sempre necessario fermarsi e chiarire prima di procedere per evitare impatti legali o su altre organizzazioni.

### DNS

<img width="1336" height="736" alt="image" src="https://github.com/user-attachments/assets/14e1ece5-57c6-4600-a5b3-9465a0f0f7b5" />

Il DNS è fondamentale per validare lo scope e scoprire host raggiungibili non dichiarati dal cliente.  
Tool come DomainTools e ViewDNS permettono di ottenere record DNS, subdomain e informazioni utili sull’infrastruttura.  
Possiamo identificare asset interessanti (anche fuori scope) da discutere con il cliente o subdomain validi su IP in scope.  
È buona pratica verificare sempre i dati raccolti, perché le informazioni DNS potrebbero non essere aggiornate.

### Public Data

Le informazioni pubbliche (es. LinkedIn, Indeed, Glassdoor) possono rivelare struttura aziendale, tecnologie e possibili vulnerabilità.  
Siti aziendali e documenti pubblici possono esporre email, contatti, intranet e dettagli su software (es. SharePoint).  
Piattaforme come GitHub, AWS S3 e Azure Blob possono contenere leak di credenziali o dati sensibili.  
Tool come TruffleHog e Greyhat Warfare aiutano a trovare queste esposizioni, facilitando l’accesso iniziale.

### Example Enumeration Process (Operative Idea)

L’approccio è **step-by-step e sempre validato**, partendo da informazioni base fino a ottenere dati utili per accesso iniziale:

1. **Raccolta iniziale (DNS / IP / ASN)**  
   - Usare tool come BGP Toolkit, ViewDNS e nslookup per ottenere IP, nameserver, mail server.  
   - Validare sempre i dati trovati (mai fidarsi di una sola fonte).  
   - Aggiungere nuovi IP/domains alla lista target (solo se in scope).

2. **Validazione e ampliamento superficie**  
   - Reverse IP lookup (ViewDNS) per scoprire altri domini collegati.  
   - Enumerare nameserver → nuovi IP → possibile nuova superficie.  
   - Sempre controllare lo scope prima di interagire.

3. **OSINT su sito e contenuti pubblici**  
   - Google Dorks:
     - `filetype:pdf inurl:domain`
     - `intext:"@domain"`  
   - Scaricare documenti → analizzare metadata / link interni.  
   - Cercare email → capire naming convention (es. `nome.cognome`).

4. **User enumeration (utenti reali)**  
   - LinkedIn → scraping con tool tipo linkedin2username  
   - Costruzione wordlist utenti (first.last, f.last, ecc.)

5. **Credential hunting (leak)**  
   - Tool: DeHashed  
   - Cercare credenziali leakate (password, hash)  
   - Anche vecchie credenziali possono funzionare → riuso password
   <img width="980" height="771" alt="image" src="https://github.com/user-attachments/assets/f8269023-f1fb-4e9a-9ffd-2568050f5a93" />

6. **Preparazione accesso iniziale**  
   - Unire:
     - lista utenti
     - naming convention
     - eventuali password leakate  
   - Usare per:
     - password spraying
     - login su VPN / OWA / portali esterni

---
