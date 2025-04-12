# University

## JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`id` AS `degrees_id`, `degrees`.`name` AS `degrees_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT `degrees`.`id`, `degrees`.`name`, `degrees`.`level`, `departments`.`id` AS `departments_id`, `departments`.`name` AS `departments_name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = 'magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT `courses`.`id`, `courses`.`name`, `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`
FROM `courses`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `students`.`id` AS `students_id`, `students`.`surname`, `students`.`name`, `students`.`registration_number`, `degrees`.`id` AS `degrees_id`, `degrees`.`name`, `degrees`.`level`, `departments`.`id`, `departments`.`name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT `degrees`.`id` AS `degrees_id`, `degrees`.`name`, `degrees`.`level`, `courses`.`id` AS `courses_id`, `courses`.`name`, `teachers`.`id` AS `teachers_id`, `teachers`.name, `teachers`.`surname`
FROM `degrees`
JOIN `courses` ON `courses`.`degree_id` = `degrees`.id
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT `teachers`.*, `departments`.`name`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
SELECT `students`.`name`, `students`.`surname`, `courses`.`name` AS `courses_name`, COUNT(*) AS `exam_chance`, MAX(`exam_student`.`vote`)
FROM `exam_student`
JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`


## GROUP BY
1. Contare quanti iscritti ci sono stati ogni anno
SELECT YEAR(`enrolment_date`) AS `year`, COUNT(`id`) AS `total_registered`
FROM `students`
GROUP BY `enrolment_date`

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) AS `teacher_with_same_office`
FROM `teachers`
GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d'esame
SELECT `exam_student`.`exam_id`, AVG(`exam_student`.`vote`) AS `vote_average`
FROM `exam_student`
GROUP BY `exam_student`.`exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT `departments`.`name` AS `department_name`, COUNT(`degrees`.`id`) AS `how_much_courses`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
GROUP BY `departments`.`name`

## SELECT
1. Selezionare tutti gli insegnanti
SELECT * 
FROM `teachers`;

2. Selezionare tutti i referenti per ogni dipartimento
SELECT `head_of_department`
FROM `departments`

3. Selezionare tutti gli studenti il cui nome inizia per "E" (373)
SELECT * 
FROM `students`
WHERE `students`.`name` LIKE 'E%';

4. Selezionare tutti gli studenti che si sono iscritti nel 2021 (734)
SELECT *
FROM `students`
WHERE YEAR(`enrolment_date`) = 2021

5. Selezionare tutti i corsi che non hanno un sito web (676)
SELECT * 
FROM `courses`
WHERE `courses`.`website` IS NULL

6. Selezionare tutti gli insegnanti che hanno un numero di telefono (50)
SELECT *
FROM `teachers`
WHERE `teachers`.`phone`;

7. Selezionare tutti gli appelli d'esame dei mesi di giugno e luglio 2020 (2634)
SELECT *
FROM `exams`
WHERE `exams`.`date` LIKE '2020-06-%' OR `exams`.`date` LIKE '2020-07-%';

8. Qual è il numero totale degli studenti iscritti? (5000)
SELECT COUNT(*) AS `total_registered_students`
FROM `students`
