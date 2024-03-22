# ChildTable

## Table DDL

```
CREATE TABLE ChildTable (RecID INTEGER PRIMARY KEY, ChildID INTEGER, FamilyID INTEGER, RelFather INTEGER, RelMother INTEGER, ChildOrder INTEGER, IsPrivate INTEGER, ProofFather INTEGER, ProofMother INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxChildOrder ON ChildTable (ChildOrder);

CREATE INDEX idxChildID ON ChildTable (ChildID);

CREATE INDEX idxChildFamilyID ON ChildTable (FamilyID);
```

## Columns List

| #   | Name        | Type    |
| --- | ----------- | ------- |
| 1   | RecID       | INTEGER |
| 2   | ChildID     | INTEGER |
| 3   | FamilyID    | INTEGER |
| 4   | RelFather   | INTEGER |
| 5   | RelMother   | INTEGER |
| 6   | ChildOrder  | INTEGER |
| 7   | IsPrivate   | INTEGER |
| 8   | ProofFather | INTEGER |
| 9   | ProofMother | INTEGER |
| 10  | Note        | TEXT    |
| 11  | UTCModDate  | FLOAT   |

## Notes

| #   | Name        | Type                         |
| --- | ----------- | ---------------------------- |
| 1   | RecID       | _PK                          |
| 2   | ChildID     | _FK ==> PersonTable.PersonID |
| 3   | FamilyID    | _FK ==> FamilyTable.FamilyID |
| 4   | RelFather   | _LOOKUP                      |
| 5   | RelMother   | _LOOKUP                      |
| 6   | ChildOrder  | _GUI_LAB=order in lists      |
| 7   | IsPrivate   | _STD _GUI_LAB=none           |
| 8   | ProofFather | _STD (Proof)                 |
| 9   | ProofMother | _STD (Proof)                 |
| 10  | Note        | _TEXT-ML                     |
| 11  | UTCModDate  | _STD                         |

The ChildTable and FamilyTable are the basis for all family relationships
see below


RecID       primary key (NOT LinkID, as expected)

ChildID     ChildTable.ChildID ==> PersonTable.PersonID

FamilyID    ChildTable.FamilyID ==> FamilyTable.FamilyID

RelFather / RelMother      relationship type of child to parent

ChildOrder    used to sort children in some (all ?) lists.
              For records pointing to the same FamilyID, gives order within set.

IsPrivate   not in RM user interface.

Proof- Note that there is a separate proof value for father & mother


Complaint
CitationLinkTable not allowed to link to ChildTable record, but that is where evidence for a connection should go.
It already has proof values for mother father, so citations should back it up.

### Traversing the tree

ChildTable is a link table between Family and Person
not really because ChildTable has PersonID. so no need to use the Person Table directly
ChildTable is a link table between FamilyTable and itself (ft)


How to link parents and offspring
I the person was linked directly to his parents (the family object) then
there would not be an opportunity to allow mulitple sets of parents - Birth, adopted, alternate possiblie Birth parents, etc.


Actual method allows multiple families for a person. 
Person-1   <== ChildLink-1 ==> Family-1
Person-1   <== ChildLink-2 ==> Family-1

A single Person can point to multiple ChildTable entries.
PersonTable.PersonID => ChildTable.ChildID *1) and  ChildTable.ChildID *2)
    Each ChildTable entry points to a family.



## Lookup Tables

| Rel-Father/Mother | type     |
| ----------------- | -------- |
| 0                 | Birth    |
| 1                 | Adopted  |
| 2                 | Step     |
| 3                 | Foster   |
| 4                 | Related  |
| 5                 | Guardian |
| 6                 | Sealed   |
| 7                 | Unknown  |


## Open Questions


