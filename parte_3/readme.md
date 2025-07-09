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

'Co by:
1. Contare quanti ntare' --> SELECT COUNT()  
'corsi di laurea' --> tabella di riferimento: `degrees`    
'per ogni dipartimento' --> dovrò raggruppare per DISTINCT(`department_id`)

**SVOLGIMENTO:**
```sql
SELECT DISTINCT(`department_id`) AS `id_dipartimento`, COUNT(`id`) AS `corsi_laurea` FROM `degrees` GROUP BY `id_dipartimento`;
```
**Result:**

[Tabella](./results/gb4.html)

---

### Join
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

**RAGIONAMENTO:**  

'Selezionare tutti' --> SELECT *  
'studenti' --> prima tabella di riferimento: `students`  
'Corso di Laurea in Economia' --> seconda tabella di riferimento: `degrees`  
devo individuare l'id del corso di laurea la cui colonna `name` = 'Corso di Laurea in Economia' e selezionare gli studenti la cui colonna `degree_id` corrisponde a quell'id.

**SVOLGIMENTO:**
```sql
SELECT * FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```
**Result:**

[Tabella](./results/j1.html)

---

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

**RAGIONAMENTO:**  

'Selezionare tutti' --> SELECT *  
'Corsi di Laurea Magistrale' --> prima tabella di riferimento: `degrees`  
'Dipartimento di Neuroscienze' --> seconda tabella di riferimento: `departments`  
devo individuare l'id del dipartimento la cui colonna `name` = 'Dipartimento di Neuroscienze' e selezionare i corsi di laurea la cui colonna `department_id` corrisponde a quell'id e la cui colonna `level` = 'magistrale'.

**SVOLGIMENTO:**
```sql
SELECT * FROM `degrees`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';
```
**Result:**

[Tabella](./results/j2.html)

---

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

**RAGIONAMENTO:**  

'Selezionare tutti' --> SELECT *  
'corsi' --> prima tabella di riferimento: `courses`  
'in cui insegna Fulvio Amato' --> seconda tabella di riferimento: `teachers`  
mi servirà anche la tabella `course_teacher` per associare gli id.
Devo quindi individuare l'id del teacher la cui colonna `name` = 'Fulvio' e la cui colonna `surname` = 'Amato' e selezionare gli id dei corsi che gli sono associati nella tabella `course_teacher`. Poi seleziono i corsi dalla tabella `courses` partendo dall'id.

**SVOLGIMENTO:**
```sql
SELECT * 
FROM `courses`
LEFT JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
LEFT JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`name` = 'Fulvio'
AND `teachers`.`surname` = 'Amato';
```
**Result:**

[Tabella](./results/j3.html)

---
