# FANTypeTable

## Table DDL

```
CREATE TABLE FANTypeTable (FANTypeID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Role1 TEXT, Role2 TEXT, Sentence1 TEXT, Sentence2 TEXT, UTCModDate FLOAT );

CREATE INDEX idxFANTypeName ON FANTypeTable (Name);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | FANTypeID  | INTEGER |
| 2   | Name       | TEXT    |
| 3   | Role1      | TEXT    |
| 4   | Role2      | TEXT    |
| 5   | Sentence1  | TEXT    |
| 6   | Sentence2  | TEXT    |
| 7   | UTCModDate | FLOAT   |
 
## Notes

| #   | Name       | Note     |
| --- | ---------- | -------- |
| 1   | FANTypeID  | _PK      |
| 2   | Name       | _TEXT-SL |
| 3   | Role1      | _TEXT-SL |
| 4   | Role2      | _TEXT-SL |
| 5   | Sentence1  | _TEXT-SL |
| 6   | Sentence2  | _TEXT-SL |
| 7   | UTCModDate | _STD     |

A FAN type relationship has a name and a name for each of the two roles.

There is a sentence template used to constuct the sentence used in a narative report.


## Open Questions
