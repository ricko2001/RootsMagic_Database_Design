# WitnessTable

## Table DDL

```
CREATE TABLE WitnessTable (WitnessID INTEGER PRIMARY KEY, EventID INTEGER, PersonID INTEGER, WitnessOrder INTEGER, Role INTEGER, Sentence TEXT, Note TEXT, Given TEXT COLLATE RMNOCASE, Surname TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, UTCModDate FLOAT );

CREATE INDEX idxWitnessPersonID ON WitnessTable (PersonID);

CREATE INDEX idxWitnessEventID ON WitnessTable (EventID);
```

## Columns List

| #   | Name         | Type    |
| --- | ------------ | ------- |
| 1   | WitnessID    | INTEGER |
| 2   | EventID      | INTEGER |
| 3   | PersonID     | INTEGER |
| 4   | WitnessOrder | INTEGER |
| 5   | Role         | INTEGER |
| 6   | Sentence     | TEXT    |
| 7   | Note         | TEXT    |
| 8   | Given        | TEXT    |
| 9   | Surname      | TEXT    |
| 10  | Prefix       | TEXT    |
| 11  | Suffix       | TEXT    |
| 12  | UTCModDate   | FLOAT   |

## Notes

| #   | Name         | Note                         |
| --- | ------------ | ---------------------------- |
| 1   | WitnessID    | _PK                          |
| 2   | EventID      | _FK ==> EventTable.EventID   |
| 3   | PersonID     | _FK ==> PersonTable.PersonID |
| 4   | WitnessOrder | _NOT-IMP        sort order   |
| 5   | Role         | _FK ==> RoleTable.RoleID     |
| 6   | Sentence     | _TEXT-SL                     |
| 7   | Note         | _TEXT-ML                     |
| 8   | Given        | _TEXT-SL                     |
| 9   | Surname      | _TEXT-SL                     |
| 10  | Prefix       | _TEXT-SL                     |
| 11  | Suffix       | _TEXT-SL                     |
| 12  | UTCModDate   | _STD                         |


````
Person edit window, list of items:
    events
    witnessed events
    names
    associations
    relative events (which events, which relatives?)

````

EventID       | _FK ==> EventTable.EventID   fact that is witnessed

PersonID      | _FK ==> PersonTable.PersonID  person this is attached to\
_SPECIAL-CASE if 0, use name in this table

WitnessOrder  | _NOT-IMP        sort order  Test this TODO

Sentence      If not NULL, custom sentence used instead of the RoleTable's sentence



| col     | use                                   |
| ------- | ------------------------------------- |
| Given   | used for "just type in witness names" |
| Surname | used for "just type in witness names" |
| Prefix  | used for "just type in witness names" |
| Suffix  | used for "just type in witness names" |


## Open Questions


