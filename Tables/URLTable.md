# URLTable

## Purpose

Stores web URL items. These link directly to using objects.

## Table DDL

``` SQL
CREATE TABLE URLTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, OwnerID INTEGER, LinkType INTEGER, Name TEXT, URL TEXT, Note TEXT, UTCModDate FLOAT );
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | OwnerType  | INTEGER |
| 3   | OwnerID    | INTEGER |
| 4   | LinkType   | INTEGER |
| 5   | Name       | TEXT    |
| 6   | URL        | TEXT    |
| 7   | Note       | TEXT    |
| 8   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                |
| --- | ---------- | ------------------- |
| 1   | LinkID     | _PK                 |
| 2   | OwnerType  | _PFK-TYPE           |
| 3   | OwnerID    | _PFK                |
| 4   | LinkType   | _NOT-IMP  (all 0) ? |
| 5   | Name       | _TEXT-SL            |
| 6   | URL        | _TEXT-SL            |
| 7   | Note       | _STD                |
| 8   | UTCModDate | _STD                |
 

Possible OwnerType
3 = SourceTable.SourceID
4 = CitationTable.CitationID
5 = PlaceTable.PlaceID
6 = Tasktable.TaskID
14 = PlaceTable.PlaceID     (either Place or Place Detail)


## Open Questions

