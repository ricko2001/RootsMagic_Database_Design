# ExclusionTable

## Purpose

Hold info on people who are not duplicates, used by auto merge feature and people who have problems to ignore.

## Table DDL

``` SQL
CREATE TABLE ExclusionTable (RecID INTEGER PRIMARY KEY, ExclusionType INTEGER, ID1 INTEGER, ID2 INTEGER, UTCModDate FLOAT );

CREATE UNIQUE INDEX idxExclusionIndex ON ExclusionTable (ExclusionType, ID1, ID2);
```

## Columns List

| #   | Name          | Type    |
| --- | ------------- | ------- |
| 1   | RecID         | INTEGER |
| 2   | ExclusionType | INTEGER |
| 3   | ID1           | INTEGER |
| 4   | ID2           | INTEGER |
| 5   | UTCModDate    | FLOAT   |

## Notes

| #   | Name          | Note |
| --- | ------------- | ---- |
| 1   | RecID         | _PK  |
| 2   | ExclusionType |      |
| 3   | ID1           |      |
| 4   | ID2           |      |
| 5   | UTCModDate    | _STD |


```
Type
1        PersonID    PersonIPD        not a match
2        PersonID    problem flag to ignore

    problem flag to ignore
```

## Open Questions

