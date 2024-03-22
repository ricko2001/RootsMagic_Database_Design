# TaskLinkTable

## Table DDL

```
CREATE TABLE TaskLinkTable (LinkID INTEGER PRIMARY KEY, TaskID INTEGER, OwnerType INTEGER, OwnerID INTEGER, UTCModDate FLOAT );

CREATE INDEX idxTaskOwnerID ON TaskLinkTable (OwnerID);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | TaskID     | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note |
| --- | ---------- | ---- |
| 1   | LinkID     | _PK  |
| 2   | TaskID     |      |
| 3   | OwnerType  |      |
| 4   | OwnerID    |      |
| 5   | UTCModDate | _STD |

## Lookup Tables

OwnerType

0    TaskTable.TaskID ==> PersonTable.PersonID

1    TaskTable.TaskID ==> FamilyTable.FamilyID

2    TaskTable.TaskID ==> EventTable.EventID

18    TaskTable.TaskID ==> TagTable.TagID            TagValue not used



Handle linking of Tasks to owning object

and 

linking of task to a folder name (TagTable)


## Open Questions

How are tasks linked to sources ?

They are linked in a backwards way. A citation is linked to a Task and
the source is linked through the citation.

Not the same way tasks are linked to other objects.





