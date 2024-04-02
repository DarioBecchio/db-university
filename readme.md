# Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
  Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Entità Departments

- department_id (Primary Key)| TINYINT | UNIQUE |
- department name | VARCHAR (255)|NOTNULL

## Entità DegreeCourses

- degree_course_id (Primary Key)|TINYINT |UNIQUE|
- course_name |VARCHAR (255)|
- department_id (Foreign key)
- duration_years |TINYINT

## Entità Courses

- course_id (Primary Key) |TINYINT | UNIQUE
- course_name |VARCHAR (255) |
- degree_course_id (Foreign key)

## Entità Teachers

- teacher_id (Primary Key) |SMALLINT | UNIQUE
- teacher_name |VARCHAR(50)

## Entità Course_Teachers

- course_id (Foreign key)
- teacher_id (Foreign key)

## Entità Exam_Session

- session_id (Primary Key) | MEDIUMINT | UNIQUE
- session_date | DATETIME
- course_id (Foreign key)

## Entità Students

- student_id (Primary Key) | MEDIUMINT | UNIQUE | AI
- student_name | VARCHAR(50)
- degree_course_id (Foreign key)

## Entità Exam_Registration

- registration_id (Primary Key)| MEDIUMINT | UNIQUE | AI
- student_id (Foreign key)
- session_id (Foreign Key)
- grade | TINYINT

### Queries 1

# Selezionare tutti gli studenti nati nel 1990 (160)

- SELECT \* FROM `students` WHERE YEAR (date_of_birth) = 1990;
  Showing rows 0 - 24 (160 total, Query took 0.0031 seconds.)

# Selezionare tutti i corsi che valgono più di 10 crediti (479)

- SELECT \* FROM `courses` WHERE `cfu` > '10';
  Showing rows 0 - 24 (479 total, Query took 0.0020 seconds.)

# Selezionare tutti gli studenti che hanno più di 30 anni

SELECT \* FROM `students` WHERE DATEDIFF(NOW(), `date_of_birth`)/365 > 30;
Showing rows 0 - 24 (3693 total, Query took 0.0028 seconds.)

SELECT \*
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) > 30;
Showing rows 0 - 24 (3531 total, Query took 0.0032 seconds.)

SELECT \* FROM `students` WHERE YEAR (NOW()) - YEAR(`date_of_birth`) > 30;
Showing rows 0 - 24 (3646 total, Query took 0.0012 seconds.)

SELECT \* FROM `students`
WHERE DATEDIFF(NOW(), `date_of_birth`) /365.25 > 30;
Showing rows 0 - 24 (3690 total, Query took 0.0011 seconds.)

### Queries 2

- Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(id), `enrolment_date`
FROM `students`
GROUP BY `enrolment_date`;

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(id), `office_address`
FROM `teachers`
GROUP BY `office_address`;

- Calcolare la media dei voti di ogni appello d'esame

SELECT `exam_id`,
AVG(`vote`) AS `average_vote`
FROM `exam_student`
GROUP BY `exam_id`;

- Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT `department_id`,
COUNT(`id`) AS `number_of_courses`
FROM `degrees`
GROUP BY `department_id`;
