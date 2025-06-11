##  Relazioni principali

- 1 `department` → molti `degree_courses`
- 1 `degree_course` → molti `courses`
- 1 `degree_course` → molti `students`
- molti `courses` ↔ molti `teachers` (tabella ponte `course_teacher`)
- 1 `course` → molti `exam_sessions`
- molti `students` ↔ molti `exam_sessions` (tabella ponte `exam_registrations`, con voto)

## Tabella: `departments`

| Colonna | Tipo           | Note                 |
|---------|----------------|----------------------|
| `id`    | INT            | Primary Key (PK)     |
| `name`  | VARCHAR(100)   | Nome del dipartimento|


---

##  Tabella: `degree_courses`

| Colonna         | Tipo         | Note                                 |
|-----------------|--------------|--------------------------------------|
| `id`            | INT          | Primary Key (PK)                     |
| `name`          | VARCHAR(100) | Nome del corso di laurea             |
| `department_id` | INT          | Foreign Key (FK) → departments.id    |

---

##  Tabella: `courses`

| Colonna           | Tipo         | Note                                 |
|-------------------|--------------|--------------------------------------|
| `id`              | INT          | Primary Key (PK)                     |
| `name`            | VARCHAR(100) | Nome della materia                   |
| `degree_course_id`| INT          | Foreign Key (FK) → degree_courses.id |

---

##  Tabella: `teachers`

| Colonna      | Tipo         | Note             |
|--------------|--------------|------------------|
| `id`         | INT          | Primary Key (PK) |
| `first_name` | VARCHAR(50)  | Nome             |
| `last_name`  | VARCHAR(50)  | Cognome          |

---

##  Tabella: `course_teacher` (relazione molti-a-molti)

| Colonna      | Tipo | Note                                 |
|--------------|------|--------------------------------------|
| `id`         | INT  | Primary Key (PK)                     |
| `course_id`  | INT  | Foreign Key (FK) → courses.id        |
| `teacher_id` | INT  | Foreign Key (FK) → teachers.id       |

---

##  Tabella: `exam_sessions`

| Colonna     | Tipo | Note                             |
|-------------|------|----------------------------------|
| `id`        | INT  | Primary Key (PK)                 |
| `course_id` | INT  | Foreign Key (FK) → courses.id    |
| `date`      | DATE | Data dell'appello                |

---

##  Tabella: `students`

| Colonna           | Tipo         | Note                                |
|-------------------|--------------|-------------------------------------|
| `id`              | INT          | Primary Key (PK)                    |
| `first_name`      | VARCHAR(50)  | Nome dello studente                 |
| `last_name`       | VARCHAR(50)  | Cognome dello studente              |
| `degree_course_id`| INT          | Foreign Key (FK) → degree_courses.id|

---

##  Tabella: `exam_registrations` (relazione molti-a-molti + voto)

| Colonna            | Tipo     | Note                                     |
|--------------------|----------|------------------------------------------|
| `id`               | INT      | Primary Key (PK)                         |
| `student_id`       | INT      | Foreign Key (FK) → students.id           |
| `exam_session_id`  | INT      | Foreign Key (FK) → exam_sessions.id      |
| `grade`            | TINYINT  | Voto ottenuto (0–30, anche insufficiente) |