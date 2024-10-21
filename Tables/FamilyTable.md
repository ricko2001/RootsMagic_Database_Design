# FamilyTable

## Purpose

Stores info on all families/couples.

## Table DDL

``` SQL
CREATE TABLE FamilyTable (FamilyID INTEGER PRIMARY KEY, FatherID INTEGER, MotherID INTEGER, ChildID INTEGER, HusbOrder INTEGER, WifeOrder INTEGER, IsPrivate INTEGER, Proof INTEGER, SpouseLabel INTEGER, FatherLabel INTEGER, MotherLabel INTEGER, SpouseLabelStr TEXT, FatherLabelStr TEXT, MotherLabelStr TEXT, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxFamilyMotherID ON FamilyTable (MotherID);

CREATE INDEX idxFamilyFatherID ON FamilyTable (FatherID);
```

## Columns List

| #   | Name           | Type    |
| --- | -------------- | ------- |
| 1   | FamilyID       | INTEGER |
| 2   | FatherID       | INTEGER |
| 3   | MotherID       | INTEGER |
| 4   | ChildID        | INTEGER |
| 5   | HusbOrder      | INTEGER |
| 6   | WifeOrder      | INTEGER |
| 7   | IsPrivate      | INTEGER |
| 8   | Proof          | INTEGER |
| 9   | SpouseLabel    | INTEGER |
| 10  | FatherLabel    | INTEGER |
| 11  | MotherLabel    | INTEGER |
| 12  | SpouseLabelStr | TEXT    |
| 13  | FatherLabelStr | TEXT    |
| 14  | MotherLabelStr | TEXT    |
| 15  | Note           | TEXT    |
| 16  | UTCModDate     | FLOAT   |

## Notes

| #   | Name           | Note                         |
| --- | -------------- | ---------------------------- |
| 1   | FamilyID       | _PK                          |
| 2   | FatherID       | _FK ==> PersonTable.PersonID |
| 3   | MotherID       | _FK ==> PersonTable.PersonID |
| 4   | ChildID        | _FK ==> ChildTable.ChildID   |
| 5   | HusbOrder      | _NOT-IMP                     |
| 6   | WifeOrder      | _NOT-IMP                     |
| 7   | IsPrivate      | _STD                         |
| 8   | Proof          | _STD                         |
| 9   | SpouseLabel    | _TEXT-SL                     |
| 10  | FatherLabel    | _TEXT-SL                     |
| 11  | MotherLabel    | _TEXT-SL                     |
| 12  | SpouseLabelStr | _TEXT-SL                     |
| 13  | FatherLabelStr | _TEXT-SL                     |
| 14  | MotherLabelStr | _TEXT-SL                     |
| 15  | Note           | _STD                         |
| 16  | UTCModDate     | _STD                         |

More details- see ChildTable
FatherID and MotherID may be 0, which means the person does not exist
(why not use null?)

There is not supposed to be a personID = 0 in PersonTable.


Thanks to SQLliteToolsForRootsMagic for the following:
The FamilyTable.ChildID points to PersonTable.PersonID of Child last active as the root person in Pedigree view,
0 = No Children in family or no child displayed as root in Pedigree view.

HusbOrder, WifeOrder
from People View, Edit Menu, Rearrange Spouses:
0 if never rearranged




Proof is in regards to them being a couple. (?)  Is 
Note is displayed in Person edit window when either spouse or parent family selected.
Proof and Edit are describing the FamilyTable record.

## Open Questions


