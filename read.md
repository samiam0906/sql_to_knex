## SQL To Knex

For this assignment, you'll combine your knowledge of SQL and Knex. To get started, fork and clone this repository.

### Assignment

Transform the following SQL commands into Knex expressions. You can write your Knex expressions underneath each SQL command using [highlighted code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/). For example:

```sql
SELECT * FROM students;
```

```javascript
knex('students');
```

To check your answers, use the [Knex Query Lab](http://michaelavila.com/knex-querylab/).

```sql
SELECT * FROM students WHERE id = 1;
```

``` javascript
knex('students').where({
  id: 1
});
```
---

```sql
SELECT * FROM students WHERE gpa = 3 LIMIT 1;
```
``` javascript
knex('students').where({gpa: 3}).limit(1);
```


---

```sql
SELECT COUNT(*) FROM students;
```

``` javascript
knex('students').count();
```
---

```sql
SELECT MAX('gpa') FROM students;
```

``` javascript
knex('students').max('gpa');
```
---

```sql
SELECT * FROM students WHERE name IS NOT NULL;
```

``` javascript
knex('students').whereNotNull('name');
```
---

```sql
SELECT * FROM students WHERE id IN (1, 2, 3) OR gpa IN (3, 4);
```

``` javascript
knex('students')
.whereIn('id', [1, 2, 3])
.orWhereIn('gpa', [3, 4]);
```
---

```sql
SELECT * FROM students LIMIT 10 OFFSET 30;
```
``` javascript
knex('students').limit(10).offset(30);
```

---

```sql
INSERT INTO students (name, fav_color) VALUES ('Prince', 'purple');
```

``` javascript
knex('students').insert({'name': 'Prince', 'fav_color': 'purple'});
```

---

```sql
INSERT INTO students (name, fav_color) VALUES ('Liz', 'blue') RETURNING *;
```

``` javascript
knex('students')
.insert({
  name: 'Liz',
  fav_color: 'blue'
})
.returning('name', 'fav_color');
```

---

```sql
UPDATE students SET name = 'Cho' WHERE id = 5;
```

``` javascript
knex('students')
.where({
  id: 5
})
.update('name', 'Cho');
```

---

```sql
DELETE FROM students WHERE gpa = 0;
```

``` javascript
knex('students')
.where({
  gpa: 0
})
.del();
```

---

```sql
UPDATE students SET gpa = gpa + 1 WHERE id = 4;
```

``` javascript
knex('students')
.where({
  id: 4
})
.increment('gpa', 1);
```

---

```sql
SELECT * FROM students INNER JOIN homeworks ON homeworks.student_id = students.id;
```

``` javascript
knex('students')
.join('homeworks', 'homeworks.student_id', 'students.id');
```
---

```sql
SELECT DISTINCT students.name, homework.title, grades.score
FROM students
INNER JOIN homeworks ON homeworks.student_id = students.id
INNER JOIN grades ON grades.id = homeworks.grade_id
WHERE grades.score > 3;
```

``` javascript
knex('students')
.where('grades.score', '>', 3)
.distinct('students.name', 'homework.title', 'grades.score')
.join('homeworks', "homeworks.student_id", 'students.id')
.join('grades', 'grades.id', 'homeworks.grade_id');
```

### Bonus

To answer the following questions, see the [Knex.js documentation](http://knexjs.org/).

##### How would you use a method like `pluck()`?


##### How would you use a method like `raw()`?
