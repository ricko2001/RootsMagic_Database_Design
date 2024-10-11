# DNATable

## Purpose

Stores DNA match information

## Table DDL

``` SQL
CREATE TABLE DNATable (RecID INTEGER PRIMARY KEY, ID1 INTEGER, ID2 INTEGER, Label1 TEXT, Label2 TEXT, DNAProvider INTEGER, SharedCM FLOAT, SharedPercent FLOAT, LargeSeg FLOAT, SharedSegs INTEGER, Date TEXT, Relate1 INTEGER, Relate2 INTEGER, CommonAnc INTEGER, CommonAncType INTEGER, Verified INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxDnaId1 ON DNATable (ID1);

CREATE INDEX idxDnaId2 ON DNATable (ID2);
```

## Columns List

| #   | Name          | Type    |
| --- | ------------- | ------- |
| 1   | CitationID    | INTEGER |
| 1   | RecID         | INTEGER |
| 2   | ID1           | INTEGER |
| 3   | ID2           | INTEGER |
| 4   | Label1        | TEXT    |
| 5   | Label2        | TEXT    |
| 6   | DNAProvider   | INTEGER |
| 7   | SharedCM      | FLOAT   |
| 8   | SharedPercent | FLOAT   |
| 9   | LargeSeg      | FLOAT   |
| 10  | SharedSegs    | INTEGER |
| 11  | Date          | TEXT    |
| 12  | Relate1       | INTEGER |
| 13  | Relate2       | INTEGER |
| 14  | CommonAnc     | INTEGER |
| 15  | CommonAncType | INTEGER |
| 16  | Verified      | INTEGER |
| 17  | Note          | TEXT    |
| 18  | UTCModDate    | FLOAT   |
|

## Notes

| #   | Name          | Note                         |
| --- | ------------- | ---------------------------- |
| 1   | CitationID    |                              |
| 1   | RecID         |                              |
| 2   | ID1           |                              |
| 3   | ID2           |                              |
| 4   | Label1        |                              |
| 5   | Label2        |                              |
| 6   | DNAProvider   |                              |
| 7   | SharedCM      |                              |
| 8   | SharedPercent |                              |
| 9   | LargeSeg      |                              |
| 10  | SharedSegs    |                              |
| 11  | Date          |                              |
| 12  | Relate1       |                              |
| 13  | Relate2       |                              |
| 14  | CommonAnc     |                              |
| 15  | CommonAncType |                              |
| 16  | Verified      |                              |
| 17  | Note          |                              |
| 18  | UTCModDate    |                              |

