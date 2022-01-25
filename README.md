Query SQL

1) SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;
2) SELECT * FROM `courses` WHERE `cfu` > 10;
3) SELECT * FROM `students` WHERE `date_of_birth` <= 19920125;
4) SELECT * FROM `courses` WHERE `period` LIKE '__semestre' AND `year` = 1;
5) SELECT * FROM `exams` WHERE `date` = 20200620 AND `hour` > 140000 ORDER BY `hour` ASC;
6) SELECT * FROM `degrees` WHERE `level` LIKE 'm%' AND `name` LIKE '%Magistrale%';
7) SELECT COUNT('id') AS 'dipartimenti' FROM `departments`;
8) SELECT COUNT('id') AS 'Senza Telefono' FROM `teachers` WHERE `phone` IS NULL
