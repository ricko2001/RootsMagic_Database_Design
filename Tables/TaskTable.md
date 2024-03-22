# TaskTable

## Table DDL

```
CREATE TABLE TaskTable (TaskID INTEGER PRIMARY KEY, TaskType INTEGER, RefNumber TEXT, Name TEXT COLLATE RMNOCASE, Status INTEGER, Priority INTEGER, Date1 TEXT, Date2 TEXT, Date3 TEXT, SortDate1 BIGINT, SortDate2 BIGINT, SortDate3 BITINT, Filename TEXT, Details TEXT, Results TEXT, UTCModDate FLOAT, Exclude INTEGER );

CREATE INDEX idxTaskName ON TaskTable (Name);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | TaskID     | INTEGER |
| 2   | TaskType   | INTEGER |
| 3   | RefNumber  | TEXT    |
| 4   | Name       | TEXT    |
| 5   | Status     | INTEGER |
| 6   | Priority   | INTEGER |
| 7   | Date1      | TEXT    |
| 8   | Date2      | TEXT    |
| 9   | Date3      | TEXT    |
| 10  | SortDate1  | BIGINT  |
| 11  | SortDate2  | BIGINT  |
| 12  | SortDate3  | BITINT  |
| 13  | Filename   | TEXT    |
| 14  | Details    | TEXT    |
| 15  | Results    | TEXT    |
| 16  | UTCModDate | FLOAT   |
| 17  | Exclude    | INTEGER |

## Notes

| #   | Name       | Note           |
| --- | ---------- | -------------- |
| 1   | TaskID     | _PK            |
| 2   | TaskType   | _LOOKUP        |
| 3   | RefNumber  | _TEXT-SL       |
| 4   | Name       | _TEXT-SL  _RNC |
| 5   | Status     | _LOOKUP        |
| 6   | Priority   | _LOOKUP        |
| 7   | Date1      | _STD           |
| 8   | Date2      | _STD           |
| 9   | Date3      | _STD           |
| 10  | SortDate1  | BIGINT         |
| 11  | SortDate2  | BIGINT         |
| 12  | SortDate3  | BIGINT         |
| 13  | Filename   | _TEXT-SL       |
| 14  | Details    | _TEXT-ML       |
| 15  | Results    | _TEXT-ML       |
| 16  | UTCModDate | _STD           |
| 17  | Exclude    |                |


Filename      | A path to a file, absolute path. Not connected to media gallery

TODO SortDate1 to SortDate3\
    not std dates or sort dates
My database has a variety of formats. Latest seem to be standard Sort dates.


## Lookup Tables

| TaskType | Name           |
| -------- | -------------- |
| 0        | <blank>        |
| 1        | Research       |
| 2        | To-Do          |
| 3        | Correspondence |


| Status | Name        |
| ------ | ----------- |
| 0      | New         |
| 1      | In progress |
| 2      | Completed   |
| 3      | On hold     |
| 4      | Problem     |
| 5      | Canceled    |


| Priority | Name          |
| -------- | ------------- |
| 0        | 1 (Highest)   |
| 1        | 2 (Very high) |
| 2        | 3 (High)      |
| 3        | 4 (Med high)  |
| 4        | 5 (Medium)    |
| 5        | 6 (Med low)   |
| 6        | 7 (Low)       |
| 7        | 8 (Very low)  |
| 8        | 9 (Lowest)    |


## Open Questions


