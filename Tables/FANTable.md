# FANTable

## Table DDL

```
CREATE TABLE FANTable (FanID INTEGER PRIMARY KEY, ID1 INTEGER, ID2 INTEGER, FanTypeID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, Description TEXT, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxFanId2 ON FANTable (ID2);

CREATE INDEX idxFanId1 ON FANTable (ID1);
```

## Columns List

| #   | Name        | Type    |
| --- | ----------- | ------- |
| 1   | FanID       | INTEGER |
| 2   | ID1         | INTEGER |
| 3   | ID2         | INTEGER |
| 4   | FanTypeID   | INTEGER |
| 5   | PlaceID     | INTEGER |
| 6   | SiteID      | INTEGER |
| 7   | Date        | TEXT    |
| 8   | SortDate    | BIGINT  |
| 9   | Description | TEXT    |
| 10  | Note        | TEXT    |
| 11  | UTCModDate  | FLOAT   |

## Notes

| #   | Name        | Note                           |
| --- | ----------- | ------------------------------ |
| 1   | FanID       | _PK                            |
| 2   | ID1         | _FK ==> PersonTable.PersonID   |
| 3   | ID2         | _FK ==> PersonTable.PersonID   |
| 4   | FanTypeID   | _FK ==> FANTypeTable.FANTypeID |
| 5   | PlaceID     | _FK ==> PlaceTable.PlaceID     |
| 6   | SiteID      | _FK ==> PlaceTable.PlaceID     |
| 7   | Date        | _STD                           |
| 8   | SortDate    | _STD                           |
| 9   | Description | _TEXT-SL                       |
| 10  | Note        | _TEXT-ML                       |
| 11  | UTCModDate  | _STD                           |

## Open Questions

Why doesn't FANTable have a value for Proof ?  TODO
