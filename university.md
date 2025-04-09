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

- id
- name

## Table name `degree_courses`

**columns**:

- id_degree_course
- id_department
- name

## Table name `courses`

**columns**:

- id_course
- id_degree_course
- name

## Table name `teachers`

**columns**:

- id_teacher
- name
- lastname

## Table name `exams`

**columns**:

- id_exam
- id_course
- date_exam

## Table name `students`

**columns**:

- id_student
- name
- lastname