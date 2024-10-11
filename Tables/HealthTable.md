# HealthTable

## Purpose

Stores information displayed in heath info

## Table DDL

``` SQL
CREATE TABLE HealthTable (RecID INTEGER PRIMARY KEY, OwnerID INTEGER, Condition INTEGER, SubCondition TEXT, Date FLOAT, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxHealthOwnerId ON HealthTable (OwnerID);
```

## Columns List

| #   | Name          | Type    |
| --- | ------------- | ------- |
| 1   | RecID         | INTEGER |
| 2   | OwnerID       | INTEGER |
| 3   | Condition     | INTEGER |
| 4   | SubCondition  | TEXT    |
| 5   | Date          | FLOAT   |
| 6   | Note          | TEXT    |
| 7   | UTCModDate    | FLOAT   |


## Notes

| #   | Name          | Note                         |
| --- | ------------- | ---------------------------- |
| 1   | RecID         |                              |
| 2   | OwnerID       |                              |
| 3   | Condition     |                              |
| 4   | SubCondition  |                              |
| 5   | Date          |                              |
| 6   | Note          |                              |
| 7   | UTCModDate    |                              |