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
| 2   | RecType    | _LOOKUP  |
| 3   | OwnerType  | _PFK-TYP |
| 4   | OwnerID    | _PFK     |
| 5   | Title      |          |
| 6   | DataRec    | XML      |
| 7   | UTCModDate | _STD     |


PayloadTable
New table added in support of Saved Criteria Search and Saved Criteria Group.

In RM GUI, 
* Saved Search Criteria
Advanced search, list show by clicking button "Saved searches".\
OwnerType =8 OwnerID=0  _SPECIAL-CASE
* Saved Group Criteria\
Groups window/ Edit an existing group/ Saved criteria.



Sample XML RecType=1
```
<Root>
    <MatchCase>false</MatchCase>
    <Criteria0>
        <Join>0</Join>
        <Field>10001</Field>
        <FieldType>2</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>2</Compare>
        <Value>1922</Value>
    </Criteria0>
    <Criteria1>
        <Join>0</Join>
        <Field>10002</Field>
        <FieldType>6</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria1>
    <Criteria2>
        <Join>0</Join>
        <Field>7002</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>1</Compare>
        <Value></Value>
    </Criteria2>
    <Criteria3>
        <Join>0</Join>
        <Field>10001</Field>
        <FieldType>3</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>2</Compare>
        <Value>deutschland</Value>
    </Criteria3>
    <Criteria4>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria4>
    <Criteria5>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria5>
</Root>
```

Sample XML RecType=2 OwnerType=20
OwnerID ==> TagTable.TagValue, GroupTable.GroupID
```
<Root>
    <MatchCase>false</MatchCase>
    <Criteria0>
        <Join>0</Join>
        <Field>10001</Field>
        <FieldType>6</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria0>
    <Criteria1>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria1>
    <Criteria2>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria2>
    <Criteria3>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria3>
    <Criteria4>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria4>
    <Criteria5>
        <Join>0</Join>
        <Field>0</Field>
        <FieldType>0</FieldType>
        <OwnerType>0</OwnerType>
        <Compare>0</Compare>
        <Value></Value>
    </Criteria5>
</Root>
```

## Lookup Tables

| RecType | meaning               |
| :------ | :-------------------- |
| 1       | saved search criteria |
| 2       | saved group criteria  |



## Open Questions

