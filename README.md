Query SQL

1) SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;
2) SELECT * FROM `courses` WHERE `cfu` > 10;
3) SELECT * FROM `students` WHERE `date_of_birth` <= 19920125;
4) SELECT * FROM `courses` WHERE `period` LIKE '__semestre' AND `year` = 1;
5) SELECT * FROM `exams` WHERE `date` = 20200620 AND `hour` > 140000 ORDER BY `hour` ASC;
6) SELECT * FROM `degrees` WHERE `level` LIKE 'm%' AND `name` LIKE '%Magistrale%';
7) SELECT COUNT('id') AS 'dipartimenti' FROM `departments`;
8) SELECT COUNT('id') AS 'Senza Telefono' FROM `teachers` WHERE `phone` IS NULL


Query SQL Group by:
1) Iscritti per anno : SELECT COUNT(`id`) FROM `students` GROUP BY YEAR(`enrolment_date`);
2) Insegnanti per edificio : SELECT COUNT(`id`) FROM `teachers` GROUP BY `office_address`;
3) media voti per esame : SELECT `exam_student`.`exam_id`, AVG(`vote`) AS 'media voti' FROM `exam_student` GROUP BY `exam_id`;
4) Corsi di laurea per ogni dipartimento: SELECT COUNT(`id`) FROM `courses` GROUP BY `degree_id`;

Query SQL Join;

1) Filtro strudenti Corso di Economia: 
  SELECT `students`.`name`,`students`.`surname`,`degrees`.`name` 
  FROM `students` 
  JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
  WHERE `degrees`.`name` LIKE '%Economia';

2) Degrees in dipartimento di Neuroscienze:
  SELECT `degrees`.`name`,`degrees`.`level`,`departments`.`name` AS 'Dipartimento',`departments`.`head_of_department`AS 'Responsabile' 
  FROM `degrees` 
  JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
  WHERE `departments`.`name` LIKE '%Neuroscienze';

3) corsi di Fulvio Amato (id = 44):
  SELECT `teachers`.`name`,`teachers`.`surname`,`courses`.`name`,`courses`.`cfu`,`courses`.`website` 
  FROM `teachers` 
  JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
  JOIN `courses` ON `courses`.`id` = course_teacher.course_id 
  WHERE `teachers`.`id` = 44;

4) Lista Ordinata per name e surname con dati del dipartimento e corso di laurea:
  SELECT `students`.`name`,`students`.`surname`,`students`.`registration_number`,`departments`.`name`,`degrees`.`name` 
  FROM `students` 
  JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
  JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
  ORDER BY `students`.`name`,`students`.`surname` ASC

5) Lista dei corsi con i relativi corsi ed insegnati:
  SELECT `degrees`.`name`,`courses`.`name`,`teachers`.`name`,`teachers`.`surname` 
  FROM `degrees` 
  JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
  JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
  JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` 
  ORDER BY `degrees`.`name` ASC;

6) insegnati nel dipartimento di matematica:
  SELECT DISTINCT `teachers`.`name`,`teachers`.`surname`,`departments`.`name`,`teachers`.`id`
  FROM `departments` 
  JOIN `degrees` ON `degrees`.`department_id` = `departments`.`id` 
  JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` 
  JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
  JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
  WHERE `departments`.`name` LIKE '%Matematica'

7) Studenti e Tutti i tentivi per ogni esame:
  SELECT `students`.`name`,`students`.`surname`,`courses`.`name` AS 'Corso',COUNT(`exams`.`id`) AS 'Tentativi'
  FROM `students`
  JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
  JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
  JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
  GROUP BY `courses`.`id`,`students`.`id`
  ORDER BY `students`.`name`, `students`.`surname` ASC
 
