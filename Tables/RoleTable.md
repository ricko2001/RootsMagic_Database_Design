# RoleTable

## Table DDL

```
CREATE TABLE RoleTable (RoleID INTEGER PRIMARY KEY, RoleName TEXT COLLATE RMNOCASE, EventType INTEGER, RoleType INTEGER, Sentence TEXT, UTCModDate FLOAT );

CREATE INDEX idxRoleEventType ON RoleTable (EventType);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | RoleID     | INTEGER |
| 2   | RoleName   | TEXT    |
| 3   | EventType  | INTEGER |
| 4   | RoleType   | INTEGER |
| 5   | Sentence   | TEXT    |
| 6   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                 |
| --- | ---------- | -------------------- |
| 1   | RoleID     | _PK                  |
| 2   | RoleName   | _TEXT-SL             |
| 3   | EventType  | _NOT-IMP (all 0)     |
| 4   | RoleType   | FK ==> FactTypeTable |
| 5   | Sentence   | _TEXT-SL             |
| 6   | UTCModDate | _STD                 |

RoleName  Used in GUI in Edit person window when a fact is shared, eg Spouse-Census

EventType   point to FactTypeTable
Eact FactType may have mulitple Roles. Each role has a name and a sentence.

RoleType   not used. All 0
Sentence  The template for the narative sentence.



## Open Questions


### DONE 1
