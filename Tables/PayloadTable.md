# PayloadTable

## Table DDL

```
CREATE TABLE PayloadTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, OwnerType INTEGER, OwnerID INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );

CREATE INDEX idxPayloadType ON PayloadTable (RecType);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | RecID      | INTEGER |
| 2   | RecType    | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | Title      | TEXT    |
| 6   | DataRec    | BLOB    |
| 7   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note     |
| --- | ---------- | -------- |
| 1   | RecID      | _PK      |
| 2   | RecType    | _LOOKUP   |
| 3   | OwnerType  | _PFK-TYP |
| 4   | OwnerID    | _PFK     |
| 5   | Title      |          |
| 6   | DataRec    |          |
| 7   | UTCModDate | _STD     |


PayloadTable
New table added in support of Saved Criteria Search and Saved Criteria Group.

OwnerType
New OwnerType values have been added in support of the new tables. These will be identified as encountered through usage and testing.

https://sqlitetoolsforrootsmagic.com/rm9-data-definitions/

## Lookup Tables

```
Table    RecType                  OwnerType    OwnerID    
Payload    1 (SavedCriteriaSearch)    8    0    
Payload    2 (SavedCriteriaGroup)    20    TagTable.TagValue, GroupTable.GroupID    
FANTable        19    CitationLinkTable, MediaLinkTable,…    
```



## Open Questions

