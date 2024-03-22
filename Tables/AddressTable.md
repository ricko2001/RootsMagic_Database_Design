# AddressTable

## Table DDL

```
CREATE TABLE AddressTable (AddressID INTEGER PRIMARY KEY, AddressType INTEGER, Name TEXT COLLATE RMNOCASE, Street1 TEXT, Street2 TEXT, City TEXT, State TEXT, Zip TEXT, Country TEXT, Phone1 TEXT, Phone2 TEXT, Fax TEXT, Email TEXT, URL TEXT, Latitude INTEGER, Longitude INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE INDEX idxAddressName ON AddressTable (Name);
```

## Columns List

| #   | Name        | Type    |
| --- | ----------- | ------- |
| 1   | AddressID   | INTEGER |
| 2   | AddressType | INTEGER |
| 3   | Name        | TEXT    |
| 4   | Street1     | TEXT    |
| 5   | Street2     | TEXT    |
| 6   | City        | TEXT    |
| 7   | State       | TEXT    |
| 8   | Zip         | TEXT    |
| 9   | Country     | TEXT    |
| 10  | Phone1      | TEXT    |
| 11  | Phone2      | TEXT    |
| 12  | Fax         | TEXT    |
| 13  | Email       | TEXT    |
| 14  | URL         | TEXT    |
| 15  | Latitude    | INTEGER |
| 16  | Longitude   | INTEGER |
| 17  | Note        | TEXT    |
| 18  | UTCModDate  | FLOAT   |

## Notes

| #   | Name        | Type           |
| --- | ----------- | -------------- |
| 1   | AddressID   | _PK            |
| 2   | AddressType | _LOOKUP        |
| 3   | Name        | _TEXT-SL       |
| 4   | Street1     | _TEXT-SL       |
| 5   | Street2     | _TEXT-SL       |
| 6   | City        | _TEXT-SL       |
| 7   | State       | _TEXT-SL       |
| 8   | Zip         | _TEXT-SL       |
| 9   | Country     | _TEXT-SL       |
| 10  | Phone1      | _TEXT-SL       |
| 11  | Phone2      | _TEXT-SL       |
| 12  | Fax         | _TEXT-SL       |
| 13  | Email       | _TEXT-SL       |
| 14  | URL         | _TEXT-SL       |
| 15  | Latitude    | _STD  _NOT-IMP |
| 16  | Longitude   | _STD  _NOT-IMP |
| 17  | Note        | _TEXT-ML       |
| 18  | UTCModDate  | _STD           |


| AddressType | Type                   |
| ----------- | ---------------------- |
| 0           | address for person     |
| 1           | address for repository |


## Open Questions

### DONE 1