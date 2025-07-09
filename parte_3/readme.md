## Consegna

### Group by:
1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

### Join:  
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
7. **BONUS**: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

## Esecuzione

### Group by:
1. Contare quanti iscritti ci sono stati ogni anno

**RAGIONAMENTO:**  

'Contare quanti' --> SELECT COUNT()  
'iscritti' --> tabella di riferimento: `students`  
'ogni anno' --> ho bisogno di individuare ogni singola distinta istanza di YEAR(`enrolment_date`) e usarla per il raggruppamento

**SVOLGIMENTO:**
```sql
SELECT DISTINCT YEAR(`enrolment_date`) AS `anno_iscrizione`, COUNT(`id`) AS `iscritti_per_anno` FROM `students` GROUP BY `anno_iscrizione`;
```
**Result:**

| anno_iscrizione | iscritti_per_anno |
| ------------- | ------------- |
| 2018 | 912 |
| 2019 | 1709 |
| 2020 | 1645 |
| 2021 | 734 |

---

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

**RAGIONAMENTO:**  

'Contare' --> SELECT COUNT()  
'insegnanti' --> tabella di riferimento: `teachers`  
'ufficio' --> colonna di riferimento: `office_address`  
'nello stesso edificio' --> stesso valore in `office_address`  
poiché voglio contare solo gli insegnanti che condividono l'edificio, dovrò ignorare i distinti valori di `office_address` che ricorrono solo una volta.

**SVOLGIMENTO:**
```sql
SELECT DISTINCT `office_address` AS `edificio`, COUNT(`id`) AS `insegnanti_per_edificio` FROM `teachers` GROUP BY `edificio` HAVING `insegnanti_per_edificio` > 1;
```
**Result:**

| edificio | insegnanti_per_edificio |
| ------------- | ------------- |
| Contrada Penelope 73 |	4 |
| Incrocio Marini 9 |	3 |
| Strada Vitali 8 Piano 0 |	5 |
| Via Mariano 48 |	4 |
| Borgo Martino 82 Appartamento 07 |	3 |
| Rotonda Martinelli 309 |	9 |
| Contrada Amato 58 Piano 2 |	5 |
| Borgo Elga 89 |	8 |
| Piazza Ferretti 619 |	3 |
| Strada Kociss 997 Piano 8 |	5 |
| Via Eusebio 167 Appartamento 28 |	6 |
| Contrada Rita 5 Appartamento 71 |	3 |
| Piazza Demian 856 Appartamento 63 |	3 |
| Strada Neri 577 |	3 |
| Borgo Elio 234 Piano 4 |	4 |
| Contrada Santoro 17 Appartamento 30 |	3 |
| Rotonda Carmela 10 Piano 1 |	6 |
| Via Giacinto 11 Piano 8 |	3 |
| Strada Concetta 6 |	3 |
| Via Maika 491 |	3 |
| Piazza Pellegrino 613 Piano 8 |	2 |
| Strada Lombardi 855 |	3 |
| Incrocio Testa 142 Piano 7 |	2 |
| Rotonda Teseo 9 |	2 |