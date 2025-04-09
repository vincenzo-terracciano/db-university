# University

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi **Dipartimenti** (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni **Dipartimento** offre più **Corsi di Laurea** (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni **Corso di Laurea** prevede diversi **Corsi** (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni **Corso** può essere tenuto da diversi **Insegnanti**;
- ogni **Corso** prevede più appelli d'**Esame**;
- ogni **Studente** è iscritto ad un solo **Corso di Laurea**;
- ogni **Studente** può iscriversi a più appelli di **Esame**;
- per ogni appello d'**Esame** a cui lo **Studente** ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Table name `departments`

**columns**:

- id_department (BIGINT) - primary key - auto_increment - NOT NULL
- name (VARCHAR(100)) - NOT NULL

## Table name `degree_courses`

**columns**:

- id_degree_course (BIGINT) - primary key - auto_increment - NOT NULL
- id_department (BIGINT) - foreign key - NOT NULL
- name (VARCHAR(100)) - NOT NULL

## Table name `courses`

**columns**:

- id_course (BIGINT) - primary key - auto_increment - NOT NULL
- id_degree_course (BIGINT) - foreign key - NOT NULL
- name (VARCHAR(100)) - NOT NULL

## Table name `teachers`

**columns**:

- id_teacher (BIGINT) - primary key - auto_increment - NOT NULL
- name (VARCHAR(100)) - NOT NULL
- lastname (VARCHAR(100)) - NOT NULL

## Table name `teacher_course`

**columns**:

- id_teacher (BIGINT) - foreign key - NOT NULL
- id_course (BIGINT) - foreign key - NOT NULL

## Table name `exams`

**columns**:

- id_exam (BIGINT) - primary key - auto_increment - NOT NULL
- id_course (BIGINT) - foreign key - NOT NULL
- date_exam (DATETIME()) - NOT NULL

## Table name `students`

**columns**:

- id_student (BIGINT) - primary key - auto_increment - NOT NULL
- id_degree_course (BIGINT) - foreign key - NOT NULL
- name (VARCHAR(100)) - NOT NULL
- lastname (VARCHAR(100)) - NOT NULL

## Table name `student_exam`

**columns**:

- id_student (BIGINT) - foreign key - NOT NULL
- id_exam (BIGINT) - foreign key - NOT NULL
- vote (TINYINT) - NOT NULL