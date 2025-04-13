## Consegna
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

## ES 1

 SELECT students.name, students.surname, degrees.name AS 'Nome del corso'
 FROM students
 JOIN degrees ON students.degree_id = degrees.id
 WHERE degrees.name = 'Corso di Laurea in Economia'

 ## ES 2

  SELECT degrees.name, degrees.level, departments.name
 FROM degrees
 JOIN departments ON degrees.department_id = departments.id
 WHERE degrees.level = 'Magistrale'
 AND departments.name = 'Dipartimento di Neuroscienze'

 ## ES 3

 SELECT teachers.name, teachers.surname, courses.name, courses.description
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON teacher_id = teachers.id
WHERE teacher_id = 44 


## ES 4

SELECT *
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.name

## ES 5

SELECT teachers.name, teachers.surname, degrees.name AS degree_name, courses.name AS course_name
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id

## ES 6

SELECT DISTINCT teachers.name, teachers.surname, departments.name
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name LIKE '%Matematica'

## ES 7

SELECT student_id, course_id, COUNT(*) AS Attempts, MAX(exam_student.vote) AS 'Voto massimo'
FROM students
JOIN exam_student ON exam_student.student_id = students.id
JOIN exams ON exam_student.exam_id = exams.id
WHERE exam_student.vote >= 18
GROUP BY student_id, course_id

## GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento


## ES 1

SELECT YEAR(enrolment_date) AS anno, COUNT(*) AS iscritti
FROM students
GROUP BY YEAR(enrolment_date)
ORDER BY YEAR(enrolment_date)

## ES 2
SELECT office_address, COUNT(*) AS 'N insegnanti'
FROM teachers
GROUP BY office_address

## ES 3
SELECT exam_id, ROUND(AVG(vote), 0) AS media
FROM exam_student
GROUP BY exam_id;

## ES 4
SELECT department_id, COUNT(*) AS degrees_courses
FROM degrees
GROUP BY department_id