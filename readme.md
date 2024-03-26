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
- department name | VARCHAR (255)|

## Entità DegreeCourses

- degree_course_id (Primary Key)|TINYINT |UNIQUE|
- course_name |VARCHAR (255)|
- department_id (Foreign key) |
- duration_years |TINYINT

## Entità Courses

- course_id (Primary Key) |TINYINT | UNIQUE
- course_name |VARCHAR (255) |
- degree_course_id (Foreign key)|

## Entità Teachers

- teacher_id (Primary Key) |SMALLINT | UNIQUE
- teacher_name |VARCHAR(50)|

## Entità Course_Teachers

- course_id (Foreign key)
- teacher_id (Foreign key)

## Entità Exam Session

- session_id (Primary Key) | MEDIUMINT | UNIQUE
- session_date
- course_id (Foreign key)

## Entità Students

- student_id (Primary Key) | MEDIUMINT | UNIQUE | AI
- student_name | VARCHAR(50)
- degree_course_id (Foreign key)

## Entità Exam_Registration

- registration_id (Primary Key)
- student_id (Foreign key)
- session_id (Foreign Key)
- grade
