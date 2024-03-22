# AddressLinkTable

## Table DDL

```
CREATE TABLE AddressLinkTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, AddressID INTEGER, OwnerID INTEGER, AddressNum INTEGER, Details TEXT, UTCModDate FLOAT );
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | OwnerType  | INTEGER |
| 3   | AddressID  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | AddressNum | INTEGER |
| 6   | Details    | TEXT    |
| 7   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                           |
| --- | ---------- | ------------------------------ |
| 1   | LinkID     | _PK                            |
| 2   | OwnerType  | _PFK-TYPE                      |
| 3   | AddressID  | _FK ==> AddressTable.AddressID |
| 4   | OwnerID    | _PFK                           |
| 5   | AddressNum |                                |
| 6   | Details    | _TEXT-ML                       |
| 7   | UTCModDate | _STD                           |

## Open Questions

What is AddressNum  TODO

### DONE 1
