1. Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(*) AS `iscritti`, YEAR(`enrolment_date`) AS `anno` 
FROM `students`
GROUP BY `anno`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(*) AS `num_insegnanti`, `office_address` AS `ufficio` 
FROM `teachers`
GROUP BY `ufficio`;

3. Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`vote`) AS `voto`, `exam_id`
FROM `exam_student`
GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(*) AS `corsi_laurea`, `departments`.`name` AS `dipartimento`
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
GROUP BY `department_id`;