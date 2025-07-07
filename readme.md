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
    - id
    - nome [VARCHAR(255)]
    - direttore [VARCHAR(255)]
    - sede_centrale [VARCHAR(255)]
    - email [VARCHAR(255)]
    - pec [VARCHAR(255)]
    - centralino [VARCHAR(25)]

- corsi_laurea
    - id
    - dipartimento_id []
    - tipo []
    - accesso []
    - crediti_totali []
    - modalità_didattica []
    - durata []
    - sede []   

- insegnamenti
    - id
    - corso_laurea_id []
    - anno []
    - crediti []
    - tipo_esame []
    - periodo_didattico []
    - obbligatorietà []
    - monte_ore []
    - sede []

- insegnanti
    - id []
    - nome []
    - cognome []
    - telefono []
    - email []
    - livello_accademico []
    - contratto []

- appelli
    - id []
    - insegnamento_id []
    - data_inizio []
    - data_fine []
    - tipo_sessione []

- studenti
    - id []
    - nome []
    - cognome []
    - email []
    - telefono []





