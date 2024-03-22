# GroupTable

## Table DDL

```
CREATE TABLE GroupTable (RecID INTEGER PRIMARY KEY, GroupID INTEGER, StartID INTEGER, EndID INTEGER, UTCModDate FLOAT );
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | RecID      | INTEGER |
| 2   | GroupID    | INTEGER |
| 3   | StartID    | INTEGER |
| 4   | EndID      | INTEGER |
| 5   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                         |
| --- | ---------- | ---------------------------- |
| 1   | RecID      | _PK                          |
| 2   | GroupID    | _FK ==> TagTable.TagValue    |
| 3   | StartID    | _FK ==> PersonTable.PersonID |
| 4   | EndID      | _FK ==> PersonTable.PersonID |
| 5   | UTCModDate | _STD                         |

## Open Questions

If the groups are only witten by code, then one can always use StartID == EndID
The table will be bigger, but who cares.

### DONE 1
