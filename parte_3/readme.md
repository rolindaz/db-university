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

[Tabella](./results/gb1.html)

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

[Tabella](./results/gb2.html)

---

3. Calcolare la media dei voti di ogni appello d'esame

**RAGIONAMENTO:**  

'Calcolare la media' --> SELECT AVG()  
'voti' --> tabella di riferimento: `exam_student`    
'di ogni appello d'esame' --> dovrò raggruppare per DISTINCT(`exam_id`)

**SVOLGIMENTO:**
```sql
SELECT DISTINCT(`exam_id`) AS `appello_esame`, AVG(`vote`) AS `media_voti` FROM `exam_student` GROUP BY `appello_esame`;
```
**Result:**

[Tabella](./results/gb3.html)

---

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

**RAGIONAMENTO:**  

'Contare' --> SELECT COUNT()  
'corsi di laurea' --> tabella di riferimento: `degrees`    
'per ogni dipartimento' --> dovrò raggruppare per DISTINCT(`department_id`)

**SVOLGIMENTO:**
```sql
SELECT DISTINCT(`department_id`) AS `id_dipartimento`, COUNT(`id`) AS `corsi_laurea` FROM `degrees` GROUP BY `id_dipartimento`;
```
**Result:**

[Tabella](./results/gb4.html)