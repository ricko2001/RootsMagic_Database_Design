# CitationLinkTable

## Purpose

Links Citations to objects that can use them, facts, Person, Family, Task etc?

## Table DDL

``` SQL
CREATE TABLE CitationLinkTable (LinkID INTEGER PRIMARY KEY, CitationID INTEGER, OwnerType INTEGER, OwnerID INTEGER, SortOrder INTEGER, Quality TEXT, IsPrivate INTEGER, Flags INTEGER, UTCModDate FLOAT );

CREATE INDEX idxCitationLinkOwnerID ON CitationLinkTable (OwnerID);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | CitationID | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | SortOrder  | INTEGER |
| 6   | Quality    | TEXT    |
| 7   | IsPrivate  | INTEGER |
| 8   | Flags      | INTEGER |
| 9   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                                                     |
| --- | ---------- | -------------------------------------------------------- |
| 1   | LinkID     | _PK                                                      |
| 2   | CitationID | _FK ==> CitationTable.CitationID                         |
| 3   | OwnerType  | _PFK-TYPE                                                |
| 4   | OwnerID    | _PFK                                                     |
| 5   | SortOrder  | _NOT-IMP (all null)                                      |
| 6   | Quality    | _LOOKUP _GUI-LAB="Source", "Information", "Evidence"     |
| 7   | IsPrivate  | _STD _NOT-IMP (all 0)                                    |
| 8   | Flags      | _NOT-IMP (all 0)                                         |
| 9   | UTCModDate | _STD                                                     |

OwnerType values seen in DB: 

| OwnerType | Links to       |
| --------- | -------------- |
| 0         | a person       |
| 1         | a family       |
| 2         | a fact/event   |
| 6         | a task         |
| 7         | a name         |
| 19        | an association |

A citation must have only Source, but via the CitationLinkTable, may be pointed to by many objects of many types. See below- Polymorphic Foreign Key type.

Link to association is new and different. It gives evidence for a relationship.


SortOrder does not appear in the RM GUI, but the column values is indeed used in v9.1.3 for sorting citations in lists,
but not in reports when the citation is converted to a footnote, and not in the "slide-in workflow" citation listing.
Utility app and SQL statement exist to exploit this field even in v9.1.3.

In RM GUI
Quality is shown in three separate fields in the Citation display:
Source, Information, and Evidence. See below for values.


## Lookup Tables

Quality has three positions 

| Char # | GUI field   | Possible values |
| ------ | ----------- | --------------- |
| 1      | Information | P S ~           |
| 2      | Evidence    | D I N ~         |
| 3      | Source      | O X ~           |

| Source | _GUI-LAB   |
| ------ | ---------- |
| O      | Original   |
| X      | Derivative |
| ~      | Don't know |

| Information | _GUI-LAB   |
| ----------- | ---------- |
| P           | Primary    |
| S           | Secondary  |
| ~           | Don't know |

| Evidence | _GUI-LAB   |
| -------- | ---------- |
| D        | Direct     |
| I        | Indirect   |
| N        | Negative   |
| ~        | Don't know |


## Open Questions

## DONE 1