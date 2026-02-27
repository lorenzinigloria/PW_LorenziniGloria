Guida all'Installazione (Deployment)
Per configurare il database in ambiente PostgreSQL, si raccomanda di eseguire gli script SQL singolarmente seguendo l'ordine numerico. Al fine di gestire correttamente le dipendenze e i vincoli di integrità, è preferibile lanciare le istruzioni CREATE in modo individuale all'interno di ogni file:

01_schema.sql: Creazione di tabelle, chiavi primarie (PK), chiavi esterne (FK) e indici. Questo script definisce la struttura normalizzata (3NF) necessaria per eliminare dati ridondanti tra i reparti IT e Compliance.

02_triggers.sql: Attivazione della logica di versioning per lo storico delle modifiche. Viene implementato il sistema di tracciabilità immutabile tramite PL/pgSQL, registrando ogni variazione nella catena di fornitura per finalità forensi.

03_views.sql: Generazione dello strato logico per l'esportazione del profilo ACN. Le viste aggregano i dati tecnici (Asset, Fornitori, Servizi) nel formato richiesto per gli audit di conformità.

04_mock_data.sql: Inserimento di un set di dati simulato per verificare la solidità del sistema e la corretta gestione delle relazioni N:M (come nel caso di asset condivisi tra più processi).

Il sistema permette l'estrazione immediata del report strutturato (CSV) utile per l'invio all'autorità competente. Per visualizzare i dati aggregati, utilizzare il comando:

SQL
SELECT * FROM v_export_profilo_acn;