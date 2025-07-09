## Group by:

1. Contare quanti iscritti ci sono stati ogni anno 
```sql
SELECT COUNT(*) AS `total_enrollments`,YEAR(`enrolment_date`) AS `year` 
FROM `students`
GROUP BY YEAR(`enrolment_date`)
```
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio 
```sql
SELECT COUNT(*) AS `same_office_same_building`, `office_address` AS `building` 
FROM `teachers`
GROUP BY (`building`)
```
3. Calcolare la media dei voti di ogni appello d'esame 
```sql
SELECT ROUND(AVG(`vote`),2) AS `average_vote`
FROM `exam_student`
GROUP BY `exam_id`
```
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT COUNT(*), `name` AS `department_name`
FROM `degrees`
GROUP BY `name`
```

## Join:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
```
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
```
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
``` 
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome 
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti 
```sql
```
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54) 
```sql
```
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
```sql
```