# TaskLinkTable

## Table DDL

``` SQL
CREATE TABLE TaskLinkTable (LinkID INTEGER PRIMARY KEY, TaskID INTEGER, OwnerType INTEGER, OwnerID INTEGER, UTCModDate FLOAT );

CREATE INDEX idxTaskOwnerID ON TaskLinkTable (OwnerID);
```

## Purpsoe

Handles linking of Tasks to owning - Person, Event etc
and 
linking of task to a folder name (TagTable)


## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | TaskID     | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                     |
| --- | ---------- | ------------------------ |
| 1   | LinkID     | _PK                      |
| 2   | TaskID     | _FK ==> TaskTable.TaskID |
| 3   | OwnerType  | _PFK-TYPE                |
| 4   | OwnerID    | _PFK                     |
| 5   | UTCModDate | _STD                     |

Links Tasks to the object the task is for, usually a person or a fact.
But now, also puts the Task in a Task Folder

if OwnerType = 18 (Task Folder name)
OwnerID ==> TagTable.TagID


Note that for OwnerType=18
TaskTable.OwnerID ==> TagTable.TagID  
which is what would be expected.
TagTable.TagValue seems to be used for Group names only.


## Open Questions

How are tasks linked to sources ?

They are linked in a backwards way. A citation is linked to a Task and
the source is linked through the citation.

Not the same way tasks are linked to other objects.


### DONE 1


