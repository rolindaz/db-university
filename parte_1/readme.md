## Consegna

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. 

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.drawio.com/ per la creazione dello schema.

Esportare quindi il diagramma in pnge caricarlo nella repo come visto in classe.

## Esecuzione

### Entità e tabelle

In base alla consegna, queste sono le entità e relative tabelle che ho individuato:

- dipartimenti
- corsi_laurea
- insegnamenti
- insegnanti
- appelli
- studenti

### Relazioni

- dipartimenti <-> corsi_laurea = one to many
- corsi_laurea <-> insegnamenti = one to many
- insegnamenti <-> insegnanti = many to many
- insegnamenti <-> appelli = one to many
- corsi_laurea <-> studenti = one to many
- studenti <-> appelli = many to many

### Colonne e relativi data-types

- dipartimenti
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - nome [VARCHAR(255), UNIQUE, NOT_NULL] [es.: 'Dipartimento di Filosofia e Scienze dell'Educazione']
    - sede_centrale [VARCHAR(255)] [es.: 'Via S. Ottavio, 20, 10124, Torino']
    - direttore [VARCHAR(255)] [es.: 'Graziano Lingua']
    - email [VARCHAR(255)] [es.: 'direzione.dfe@unito.it']
    - sito_web [VARCHAR(255)] [es.: 'https://www.dfe.unito.it/do/home.pl']
    - centralino [VARCHAR(25)] [es.: '+39 011 6703608']

- corsi_laurea
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - dipartimento_id [INTEGER] [es.: 1234]
    - nome [VARCHAR(255), UNIQUE, NOT_NULL] [es.: 'Filosofia']
    - tipo [VARCHAR(255)] [es.: 'Laurea triennale']
    - accesso [VARCHAR(255)] [es.: 'Libero']
    - crediti_totali [SMALLINT, NOT_NULL] [es.: 180]
    - modalità_didattica [VARCHAR(255)] [es.: 'Convenzionale']
    - durata [VARCHAR(255)] [es.: '3 anni']
    - sede [VARCHAR(255)][es.: 'Torino']

- insegnamenti
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - corso_laurea_id [INTEGER] [es.: 1234]
    - nome [VARCHAR(255), UNIQUE, NOT_NULL] [es.: 'Storia della Filosofia Russa']
    - anno_corso [TINYINT] [es.: 1]
    - crediti [TINYINT, NOT_NULL] [es.: 6]
    - tipo_esame [VARCHAR(255)] [es.: 'Orale']
    - periodo_didattico [VARCHAR(255)] [es.: 'Primo semestre']
    - data_inizio [DATE, NOT_NULL] [es.: 21/09/2025]
    - data_fine [DATE, NOT_NULL] [es.: 19/12/2025]
    - obbligatorietà [VARCHAR(255)] [es.: 'Non obbligatorio']
    - monte_ore [SMALLINT] [es.: 36]
    - sede [VARCHAR(255)] [es.: 'Torino']

- insegnanti
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - nome [VARCHAR(255), NOT_NULL] [es.: 'Daniela']
    - cognome [VARCHAR(255), NOT_NULL] [es.: 'Steila']
    - telefono [VARCHAR(25), NOT_NULL] [es.: '+39 011 6708218']
    - email [VARCHAR(255), NOT_NULL] [es.: 'daniela.steila@unito.it']
    - livello_accademico [VARCHAR(255)] [es.: 'Prima fascia']
    - contratto [VARCHAR(255)] [es.: 'Professoressa ordinaria']

- appelli
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - insegnamento_id [INTEGER] [es.: 1234]
    - data_inizio [DATE, NOT_NULL] [es.: 10/01/2026]
    - data_fine [DATE, NOT_NULL] [es.: 30/01/2026]
    - tipo_sessione [VARCHAR(255)] [es.: 'Ordinaria']

- studenti
    - id [INTEGER, NOT_NULL, UNIQUE, AUTO_INCREMENT] [es.: 1234]
    - corso_laurea_id [INTEGER] [es.: 1234]
    - nome [VARCHAR(255), NOT_NULL] [es.: 'Daniela']
    - cognome [VARCHAR(255), NOT_NULL] [es.: 'Steila']
    - matricola [VARCHAR(255), UNIQUE, NOT_NULL] [es.: 1234AA]
    - data_iscrizione [DATE, NOT_NULL] [es.: 01/09/2024]
    - email [VARCHAR(255), UNIQUE, NOT_NULL] [es.: 'daniela.steila@unito.it']
    - telefono [VARCHAR(25), UNIQUE, NOT_NULL] [es.: '+39 011 6708218']





