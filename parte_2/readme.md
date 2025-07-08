## Consegna

1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

## Esecuzione

1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT * FROM `students` LIKE '1990%';
```
    Result:
    160 rows

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT * FROM `courses` WHERE `cfu` > 10;
```
    Result:
    479 rows

3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT * FROM `students` WHERE `date_of_birth` <= '1995-07-08';
SELECT * FROM `students` WHERE `date_of_birth` = DATE_BIRTH(CURDATE(), INTERVAL 30 YEARS);
```
    Result:
    3860 rows

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql
SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;
```
    Result:
    286 rows

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT * FROM `exams` WHERE `date` = '2020-06-20' AND `hour` > '13:59:59';
```
    Result:
    21 rows

6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT * FROM `degrees` WHERE `name` LIKE '%Magistrale%';
```
    Result:
    38 rows