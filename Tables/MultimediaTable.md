# MultimediaTable

## Table DDL

```
CREATE TABLE MultimediaTable (MediaID INTEGER PRIMARY KEY, MediaType INTEGER, MediaPath TEXT, MediaFile TEXT COLLATE RMNOCASE, URL TEXT, Thumbnail BLOB, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate BIGINT, Description TEXT, UTCModDate FLOAT );

CREATE INDEX idxMediaFile ON MultimediaTable (MediaFile);

CREATE INDEX idxMediaURL ON MultimediaTable (URL);
```

## Columns List

| #   | Name        | Type    |
| --- | ----------- | ------- |
| 1   | MediaID     | INTEGER |
| 2   | MediaType   | INTEGER |
| 3   | MediaPath   | TEXT    |
| 4   | MediaFile   | TEXT    |
| 5   | URL         | TEXT    |
| 6   | Thumbnail   | BLOB    |
| 7   | Caption     | TEXT    |
| 8   | RefNumber   | TEXT    |
| 9   | Date        | TEXT    |
| 10  | SortDate    | BIGINT  |
| 11  | Description | TEXT    |
| 12  | UTCModDate  | FLOAT   |

## Notes

| #   | Name        | Note           |
| --- | ----------- | -------------- |
| 1   | MediaID     | _PK            |
| 2   | MediaType   | _LOOKUP        |
| 3   | MediaPath   | _TEXT-SL       |
| 4   | MediaFile   | _TEXT-SL  _RNC |
| 5   | URL         | _NOT-IMP       |
| 6   | Thumbnail   | image          |
| 7   | Caption     | _TEXT-SL  _RNC |
| 8   | RefNumber   | _TEXT-SL  _RNC |
| 9   | Date        | _STD           |
| 10  | SortDate    | _STD           |
| 11  | Description | _TEXT-SL       |
| 12  | UTCModDate  | _STD           |



MediaPath  Case insensitive\
    path with optional relative path anchor character\
    RM 8&9 Relative path symbols (expanded when found in the first position of the stored path)\
    `?`    media folder as set in RM preferences\
    `~`    home directory  (%USERPROFILE%)\
    `*`    RM main database file location

Uses backslash `"\"` as directory separator on Win and MacOS

MediaFile   Case insensitive


## Lookup Tables

MeidaType


## Open Questions

Thumbnail  format ?, size ?



