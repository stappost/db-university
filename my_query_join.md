1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `degrees`.`name` AS `nome_corso`, `degrees`.`level` AS `livello_corso`, `degrees`.`address` AS `indirizzo`, `students`.`name` AS `nome_studente`, `students`.`surname` AS `cognome_studente`, `students`.`registration_number` AS `matricola`
FROM `degrees`
JOIN `students` 
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

SELECT `degrees`.*
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `teachers`.`name` AS `nome_insegnante`, `teachers`.`surname` AS `cognome_insegnante`, `courses`.`name` AS `nome_corso`, `courses`.`description` AS `destrizione_corso`, `courses`.`period` AS `periodo`,`courses`.`cfu`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

SELECT `students`.`name` AS `nome_studente`, `students`.`surname` AS `cognome_studente`, `students`.`registration_number` AS `matricola`, `degrees`.`name` AS `nome_corso`, `degrees`.`level` AS `livello_corso`, `degrees`.`address` AS `indirizzo_corso`, `degrees`.`email` AS `email_corso`, `departments`.`name` AS `nome_dipartimento`
FROM `students`
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`name` AS `nome_corso_laurea`, `degrees`.`level` AS `livello_corso`, `degrees`.`address` AS `indirizzo_corso`, `degrees`.`email` AS `email_corso`, `courses`.`name` AS `nome_corso`, `courses`.`cfu`, `courses`.`year`, `courses`.`period`, `teachers`.`name` AS `nome_insegnante`, `teachers`.`surname` AS `cognome_insegnante`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

SELECT DISTINCT `teachers`.`name` AS `nome_insegnante`, `teachers`.`surname` AS `cognome_insegnante`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

SELECT `students`.`name` AS `nome_studente`, `students`.`surname`, `courses`.`name`, COUNT(`exam_student`.`exam_id`) AS `tentativi_esame`, MAX(`exam_student`.`vote`) AS `voto_massimo`
FROM `exam_student` 
JOIN `students` ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses` ON `courses`.`id` = exams.course_id
GROUP BY `students`.`id`, `exams`.`course_id`;