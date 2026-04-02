### External Recon and Enumeration Principles (Summary)

External reconnaissance serve a raccogliere informazioni pubbliche sul target prima del pentest, verificando lo scope e individuando possibili dati esposti.  
Aiuta a evitare errori operativi e a garantire che le attività siano condotte sugli asset corretti.  
L’obiettivo è ottenere una visione generale dell’ambiente e scoprire eventuali leak (credenziali, repository, documenti, link interni).

### What Are We Looking For? (Summary)

Durante la fase di external reconnaissance cerchiamo informazioni pubbliche utili per comprendere l’infrastruttura del target e facilitare eventuali accessi.  
Questi dati possono includere credenziali esposte, servizi pubblici e configurazioni dell’ambiente.  
L’obiettivo è ottenere vantaggi pratici per il pentest (es. accesso VPN, enumerazione utenti, attacchi password-based).

---

### Key Data Points

|----Data Point----|----------------------------------------------------------- Description ------------------------------------------------------------|
|------------------|------------------------------------------------------------------------------------------------------------------------------------|
| IP Space         | ASN, netblock, infrastruttura pubblica, cloud, DNS e provider di hosting utilizzati dall’organizzazione. --------------------------|
| Domain Info      | Informazioni sui domini: subdomain, servizi esposti (mail, VPN, web), amministrazione dominio e difese attive (SIEM, AV, IDS/IPS). |
| Schema Format    | Formato username/email, account AD e policy password per costruire wordlist e attacchi (spraying, brute force, stuffing). ---------|
| Data Disclosures | File pubblici (.pdf, .docx, .xlsx) contenenti informazioni interne (intranet, metadata, share, software, credenziali). ------------|
| Breach Data      | Credenziali e dati sensibili esposti pubblicamente utili per ottenere accesso iniziale. -------------------------------------------|
