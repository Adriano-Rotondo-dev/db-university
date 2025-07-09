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
SELECT * 
FROM `students`
JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = `Corso di Laurea in Economia` 
```
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT * 
FROM `departments`
JOIN `degrees`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` ='magistrale'
``` 
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT * 
FROM `courses`
JOIN `course_teacher` 
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = '44'
```
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome 
```sql
SELECT * 
FROM `students`
JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
on `degrees`.`department_id` = `departments`.`id`
order by `students`.`surname`, `students`.`name`
```
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti 
```sql
SELECT *
FROM `degrees`
JOIN `courses` 
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` 
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` 
ON `teachers`.`id` = `course_teacher`.`teacher_id`
```
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54) 
```sql
SELECT *
FROM `teachers`
JOIN `course_teacher` 
ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses`
ON `ourses`.`id`=`course_teacher`.`course_id`
JOIN `degrees` 
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
```
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
```sql
SELECT COUNT(*) AS `attempts`, 
MAX(`vote`) as `max_vote`
FROM `exams`
JOIN `exam_student`
on `exam_student`.`exam_id` = `exams.id`
JOIN `students`
on `students`.`id`=`exam_student`.`student_id`
WHERE `vote` >= 18
GROUP BY `student_id`, `exam_id`
```