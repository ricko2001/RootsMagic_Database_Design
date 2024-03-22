# PersonTable

## Table DDL

```
CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Color1 INTEGER, Color2 INTEGER, Color3 INTEGER, Color4 INTEGER, Color5 INTEGER, Color6 INTEGER, Color7 INTEGER, Color8 INTEGER, Color9 INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note TEXT, UTCModDate FLOAT );
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | PersonID   | INTEGER |
| 2   | UniqueID   | TEXT    |
| 3   | Sex        | INTEGER |
| 4   | ParentID   | INTEGER |
| 5   | SpouseID   | INTEGER |
| 6   | Color      | INTEGER |
| 7   | Color1     | INTEGER |
| 8   | Color2     | INTEGER |
| 9   | Color3     | INTEGER |
| 10  | Color4     | INTEGER |
| 11  | Color5     | INTEGER |
| 12  | Color6     | INTEGER |
| 13  | Color7     | INTEGER |
| 14  | Color8     | INTEGER |
| 15  | Color9     | INTEGER |
| 16  | Relate1    | INTEGER |
| 17  | Relate2    | INTEGER |
| 18  | Flags      | INTEGER |
| 19  | Living     | INTEGER |
| 20  | IsPrivate  | INTEGER |
| 21  | Proof      | INTEGER |
| 22  | Bookmark   | INTEGER |
| 23  | Note       | TEXT    |
| 24  | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                                    |
| --- | ---------- | --------------------------------------- |
| 1   | PersonID   | _PK                                     |
| 2   | UniqueID   | _TEXT-SL                                |
| 3   | Sex        | _LOOKUP                                  |
| 4   | ParentID   | _FK ==> FamilyTable.FamilyID            |
| 5   | SpouseID   | _FK ==> FamilyTable.FamilyID            |
| 6   | Color      | Color set info                          |
| 7   | Color1     | Color set info                          |
| 8   | Color2     | Color set info                          |
| 9   | Color3     | Color set info                          |
| 10  | Color4     | Color set info                          |
| 11  | Color5     | Color set info                          |
| 12  | Color6     | Color set info                          |
| 13  | Color7     | Color set info                          |
| 14  | Color8     | Color set info                          |
| 15  | Color9     | Color set info                          |
| 16  | Relate1    | Relationship info                       |
| 17  | Relate2    | Relationship info                       |
| 18  | Flags      | _NOT-IMP                                |
| 19  | Living     | _LOOKUP                                  |
| 20  | IsPrivate  | _STD _GUI-LAB=not present               |
| 21  | Proof      | _STD                                    |
| 22  | Bookmark   | _LOOKUP _GUI-LAB name is in Bookmark tab |
| 23  | Note       | _TEXT-ML _GUI-LAB="Note" person         |
| 24  | UTCModDate | _STD                                    |

No indexes created for this table.

UniqueID  looks like a GUID. Not clear how they are generated. TODO


Both ParentID and  SpouseID are _FK =>FamilyTable.FamilyID 
These point to a parent family and spouse family.\
Probably these are the relationships used in reports and display as default.\
Just changing the display to show another spouse will presumably update SpouseID.\


Color columns\ 
Each column, "" to 9 represents one of the 10 possible color "sets"\
The column contains the color of the person when the corresponding color set is active.
Where are color number definitions stored? in ConfigTable?  TODO


TODO
Relate1 1 -> 12 & 999 (7 o these)
Relate2 2 -> 12


Flags


Each name has a proof
Do all items in edit screen have proof fields?


## Lookup Tables

| Sex | meaning |
| --- | ------- |
| 0   | Male    |
| 1   | Female  |
| 2   | unknown |

| Living | Alive |
| ------ | ----- |
| 0      | No    |
| 1      | Yes   |

| Bookmark | meaning |
| -------- | ------- |
| 0        | No      |
| 1        | Yes     |

## Open Questions

UniqueID appears to be a GUID varient. Haven't seen documentation. Not tested:\
What algorithm is used to create them.\
When one is assigned, how they differ between database.

Date Edited in RM GUI\
Is it simply the UTCModDate of the PersonTable row?

or does it depend on other rows pointing to thie person?
Do all fields in PersonTable cause UTCModDate to update?
