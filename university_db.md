## Consegna
1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)



## ES.1

SELECT *
FROM students
WHERE  date_of_birth >= '1990-01-01' AND date_of_birth <= '1990-12-31'; 


## ES.2

SELECT *
FROM courses
WHERE cfu > 10;


## ES.3

SELECT * 
FROM students 
WHERE timestampdiff(YEAR, date_of_birth, '2025-04-10') > 30;


## ES.4

SELECT *
FROM courses
WHERE period = 'I semestre' AND year = 1;


## ES.5

SELECT *
FROM exams
WHERE hour > '14:00:00' AND `date` = '2020-06-20';

## ES.6


SELECT *
FROM degrees
WHERE level = 'magistrale';


## ES.7


SELECT *
FROM departments


## ES. 8


SELECT *
FROM teachers
WHERE phone IS NULL 