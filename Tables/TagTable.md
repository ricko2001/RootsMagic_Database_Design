# TagTable

## Table DDL

## Purpose

Stores names used by other objects- Groups, task folders.

``` SQL
CREATE TABLE TagTable (TagID INTEGER PRIMARY KEY, TagType INTEGER, TagValue INTEGER, TagName TEXT COLLATE RMNOCASE, Description TEXT, UTCModDate FLOAT );

CREATE INDEX idxTagType ON TagTable (TagType);
```

## Columns List

| #   | Name        | Type    |
| --- | ----------- | ------- |
| 1   | TagID       | INTEGER |
| 2   | TagType     | INTEGER |
| 3   | TagValue    | INTEGER |
| 4   | TagName     | TEXT    |
| 5   | Description | TEXT    |
| 6   | UTCModDate  | FLOAT   |

## Notes
 
| #   | Name        | Note            |
| --- | ----------- | --------------- |
| 1   | TagID       | _PK             |
| 2   | TagType     | _LOOKUP         |
| 3   | TagValue    |                 |
| 4   | TagName     | _TEXT-SL  _RMNC |
| 5   | Description | _TEXT-SL        |
| 6   | UTCModDate  | _STD            |

TagID\
is pointed to by TaskLinkTable, as expected.

TagValue\
GroupID in GroupTable points to TagValue, not TagID
so it's an identifier specific to group names

TagName\
simple name, used according to TagType


## Lookup Tables

| TagType | meaning          |
| :------ | :--------------- |
| 0       | group name       |
| 1       | task folder name |


## Open Questions
