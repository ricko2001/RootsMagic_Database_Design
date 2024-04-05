# AddressLinkTable

## Purpose

Links Address/Repositories to the objects that use them. People or Sources.

## Table DDL

``` SQL
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
| 6   | Details    | _NOT-IMPL                       |
| 7   | UTCModDate | _STD                           |

OwnerType is either 0, 1,3 or 6

In person edit window, can attach an address to the person, his spouse (family) and parents (family)

Address of AddressType 0 links to people 0 or 1 family, address/repository of type 1 links to sources.

## Open Questions

What is AddressNum  TODO

### DONE 1
