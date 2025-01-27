# FamilySearchTable

## Purpose

Stores linage information between a RootsMagic person and a FamilySearch Family Tree person.

## Table DDL

``` SQL
CREATE TABLE FamilySearchTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, fsID TEXT, Modified INTEGER, fsVersion TEXT, fsDate FLOAT, Status INTEGER, UTCModDate FLOAT , TreeID TEXT);

CREATE INDEX idxLinkRmId ON FamilySearchTable (rmID);

CREATE INDEX idxLinkfsID ON FamilySearchTable (fsID);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | LinkType   | INTEGER |
| 3   | rmID       | INTEGER |
| 4   | fsID       | TEXT    |
| 5   | Modified   | INTEGER |
| 6   | fsVersion  | TEXT    |
| 7   | fsDate     | FLOAT   |
| 8   | Status     | INTEGER |
| 9   | UTCModDate | FLOAT   |
| 10  | TreeID     | TEXT    |

## Notes

| #   | Name       | Note |
| --- | ---------- | ---- |
| 1   | LinkID     | _PK  |
| 2   | LinkType   |      |
| 3   | rmID       |      |
| 4   | fsID       |      |
| 5   | Modified   |      |
| 6   | fsVersion  |      |
| 7   | fsDate     |      |
| 8   | Status     |      |
| 9   | UTCModDate | _STD |
| 10  | TreeID     | TEXT |

## Open Questions
