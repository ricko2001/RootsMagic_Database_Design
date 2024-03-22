# PlaceTable

## Table DDL

```
CREATE TABLE PlaceTable (PlaceID INTEGER PRIMARY KEY, PlaceType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, Normalized TEXT, Latitude INTEGER, Longitude INTEGER, LatLongExact INTEGER, MasterID INTEGER, Note TEXT, Reverse TEXT COLLATE RMNOCASE, fsID INTEGER, anID INTEGER, UTCModDate FLOAT );

CREATE INDEX idxPlaceName ON PlaceTable (Name);

CREATE INDEX idxPlaceAbbrev ON PlaceTable (Abbrev);

CREATE INDEX idxReversePlaceName ON PlaceTable (Reverse);
```

## Columns List

| #   | Name         | Type    |
| --- | ------------ | ------- |
| 1   | PlaceID      | INTEGER |
| 2   | PlaceType    | INTEGER |
| 3   | Name         | TEXT    |
| 4   | Abbrev       | TEXT    |
| 5   | Normalized   | TEXT    |
| 6   | Latitude     | INTEGER |
| 7   | Longitude    | INTEGER |
| 8   | LatLongExact | INTEGER |
| 9   | MasterID     | INTEGER |
| 10  | Note         | TEXT    |
| 11  | Reverse      | TEXT    |
| 12  | fsID         | INTEGER |
| 13  | anID         | INTEGER |
| 14  | UTCModDate   | FLOAT   |

## Notes

| #   | Name         | Note                                       |
| --- | ------------ | ------------------------------------------ |
| 1   | PlaceID      | _PK                                        |
| 2   | PlaceType    | _LOOKUP                                     |
| 3   | Name         | _TEXT-SL                                   |
| 4   | Abbrev       | _TEXT-SL                                   |
| 5   | Normalized   | _TEXT-SL                                   |
| 6   | Latitude     | _STD                                       |
| 7   | Longitude    | _STD                                       |
| 8   | LatLongExact | _NOT-IMP  (all 0)                            |
| 9   | MasterID     | _FK ==> PlaceTable.PlaceID                 |
| 10  | Note         | _TEXT-ML                                   |
| 11  | Reverse      | _TEXT-SL                                   |
| 12  | fsID         | _NOT-IMP  (all NULL) FamilySearch place ID ? |
| 13  | anID         | _NOT-IMP  (all NULL)  Ancestry place ID ?    |
| 14  | UTCModDate   | _STD                                       |


MasterID only used in for PlaceDetail records. Points to owning Master Place.

Reverse de-normalized (?) reverse Name for master place, not populated for place detail records.

## Lookup Tables

| PlaceType | meaning         |
| --------- | --------------- |
| 0         | Top level place |
| 1         | Builtin (LDS)   |
| 2         | Place Detail    |


## Open Questions

What is LatLongExact  TODO

### DONE 1
