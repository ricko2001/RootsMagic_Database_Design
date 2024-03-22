# URLTable

## Table DDL

```
CREATE TABLE URLTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, OwnerID INTEGER, LinkType INTEGER, Name TEXT, URL TEXT, Note TEXT, UTCModDate FLOAT );
```

## Columns List

| #  | Name          | Type      |
|----|---------------|-----------|
| 1  | LinkID        | INTEGER   |
| 2  | OwnerType     | INTEGER   |
| 3  | OwnerID       | INTEGER   |
| 4  | LinkType      | INTEGER   |
| 5  | Name          | TEXT      |
| 6  | URL           | TEXT      |
| 7  | Note          | TEXT      |
| 8  | UTCModDate    | FLOAT     |

## Notes

| #  | Name          | Note      |
|----|---------------|-----------|
| 1  | LinkID        | _PK
| 2  | OwnerType     | _PFK-TYPE
| 3  | OwnerID       | _PFK
| 4  | LinkType      | _NOT-IMP  (all 0) ?
| 5  | Name          | _TEXT-SL
| 6  | URL           | _TEXT-SL
| 7  | Note          | _TEXT-ML
| 8  | UTCModDate    | _STD

## Open Questions

