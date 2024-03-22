# EventTable

## Table DDL

```
CREATE TABLE EventTable (EventID INTEGER PRIMARY KEY, EventType INTEGER, OwnerType INTEGER, OwnerID INTEGER, FamilyID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Status INTEGER, Sentence TEXT, Details TEXT, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxOwnerEvent ON EventTable (OwnerID,EventType);

CREATE INDEX idxOwnerDate ON EventTable (OwnerID,SortDate);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | EventID    | INTEGER |
| 2   | EventType  | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | FamilyID   | INTEGER |
| 6   | PlaceID    | INTEGER |
| 7   | SiteID     | INTEGER |
| 8   | Date       | TEXT    |
| 9   | SortDate   | BIGINT  |
| 10  | IsPrimary  | INTEGER |
| 11  | IsPrivate  | INTEGER |
| 12  | Proof      | INTEGER |
| 13  | Status     | INTEGER |
| 14  | Sentence   | TEXT    |
| 15  | Details    | TEXT    |
| 16  | Note       | TEXT    |
| 17  | UTCModDate | FLOAT   |


## Notes

| #   | Name       | Note                             |
| --- | ---------- | -------------------------------- |
| 1   | EventID    | _PK                              |
| 2   | EventType  | _FK ==> FactTypeTable.FactTypeID |
| 3   | OwnerType  | _PFK-TYPE                        |
| 4   | OwnerID    | _PFK                             |
| 5   | FamilyID   | _NOT-IMP (all 0)                 |
| 6   | PlaceID    | _FK ==> PlaceTable.PlaceID       |
| 7   | SiteID     | _FK ==> PlaceTable.PlaceID       |
| 8   | Date       | _STD                             |
| 9   | SortDate   | _STD                             |
| 10  | IsPrimary  | _STD                             |
| 11  | IsPrivate  | _STD                             |
| 12  | Proof      | _STD                             |
| 13  | Status     | _NOT-IMP (all 0)                 |
| 14  | Sentence   | _TEXT-SL                         |
| 15  | Details    | _TEXT-SL                         |
| 16  | Note       | _TEXT-ML                         |
| 17  | UTCModDate | _STD                             |


OwnerType
Types seen in database-
0 Person, 1 Family/couple 

FamilyID        no longer used in current design

PlaceID   points to place
SiteID    points to place deatil
SiteID ,  0 if no detail specified
          HOWEVER, due to TMG import by RM, SiteID was set to -1 when no Place Deatail specified.

OwnerEventType  This is redundant with the EventType which also says what kind of event it is.

Sentence    if not null, use this as sentence for fact


## Lookup Tables

| OwnerEventType | type         |
| :------------- | :----------- |
| 0              | person event |
| 1              | family event |


## Open Questions

is FamilyID really not used ?  TODO

