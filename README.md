# DatabaseHW
# 1: Create Database
- **mongosh**: Create database
```
use MyDatabase
```
- **mongosh**: Create collection & document
```
db.scores.insertMany([
    { "name": "Ramesh", "subject": "maths", "marks": 87 }, { "name": "Ramesh", "subject": "english", "marks": 59 }, { "name": "Ramesh", "subject": "science", "marks": 77 }, { "name": "Rav", "subject": "maths", "marks": 62 }, { "name": "Rav", "subject": "english", "marks": 83 }, { "name": "Rav", "subject": "science", "marks": 71 }, { "name": "Alison", "subject": "maths", "marks": 84 }, { "name": "Alison", "subject": "english", "marks": 82 }, { "name": "Alison", "subject": "science", "marks": 86 }, { "name": "Steve", "subject": "maths", "marks": 81 }, { "name": "Steve", "subject": "english", "marks": 89 }, { "name": "Steve", "subject": "science", "marks": 77 }, { "name": "Jan", "subject": "english", "marks": 0, "reason": "absent" }
])
```
# 2: Read data
- **mongosh**: Find without condition
```
db.movies.find()
```
- Find the total marks for each student across all subjects
```
db.students.aggregate([
{$group: { _id: "$name", totalMarks: { $sum: "$marks" }}}
])
```

- Find the maximum marks scored in each subject
```
db.students.aggregate([
{$group: { _id: "$subject", maxMarks: { $max: "$marks" } } }
])
```

- Find the minimum marks scored by each student
```
db.students.aggregate([
{$group: { _id: "$name", minMarks: { $min: "$marks" } } }
])
```

- Find the top two subjects based on average marks
```
db.students.aggregate([
{ $group: {_id: "$subject", avgMarks: {$avg: "$marks" } } }, { $sort: {avgMarks: -1 } }, {$limit: 2}
])
```
