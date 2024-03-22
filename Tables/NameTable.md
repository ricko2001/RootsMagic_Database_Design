# NameTable

## Table DDL

```
CREATE TABLE NameTable (NameID INTEGER PRIMARY KEY, OwnerID INTEGER, Surname TEXT COLLATE RMNOCASE, Given TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, Nickname TEXT COLLATE RMNOCASE, NameType INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Sentence TEXT, Note TEXT, BirthYear INTEGER, DeathYear INTEGER, Display INTEGER, Language TEXT, UTCModDate FLOAT, SurnameMP TEXT, GivenMP TEXT, NicknameMP TEXT );

CREATE INDEX idxSurnameGiven ON NameTable (Surname, Given, BirthYear, DeathYear);

CREATE INDEX idxSurnameGivenMP ON NameTable (SurnameMP, GivenMP, BirthYear, DeathYear);

CREATE INDEX idxNamePrimary ON NameTable (IsPrimary);

CREATE INDEX idxGivenMP ON NameTable (GivenMP);

CREATE INDEX idxNameOwnerID ON NameTable (OwnerID);

CREATE INDEX idxGiven ON NameTable (Given);

CREATE INDEX idxSurname ON NameTable (Surname);

CREATE INDEX idxSurnameMP ON NameTable (SurnameMP);
```

# Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | NameID     | INTEGER |
| 2   | OwnerID    | INTEGER |
| 3   | Surname    | TEXT    |
| 4   | Given      | TEXT    |
| 5   | Prefix     | TEXT    |
| 6   | Suffix     | TEXT    |
| 7   | Nickname   | TEXT    |
| 8   | NameType   | INTEGER |
| 9   | Date       | TEXT    |
| 10  | SortDate   | BIGINT  |
| 11  | IsPrimary  | INTEGER |
| 12  | IsPrivate  | INTEGER |
| 13  | Proof      | INTEGER |
| 14  | Sentence   | TEXT    |
| 15  | Note       | TEXT    |
| 16  | BirthYear  | INTEGER |
| 17  | DeathYear  | INTEGER |
| 18  | Display    | INTEGER |
| 19  | Language   | TEXT    |
| 20  | UTCModDate | FLOAT   |
| 21  | SurnameMP  | TEXT    |
| 22  | GivenMP    | TEXT    |
| 23  | NicknameMP | TEXT    |

## Notes

| #   | Name       | Note                         |
| --- | ---------- | ---------------------------- |
| 1   | NameID     | _PK                          |
| 2   | OwnerID    | _FK ==> PersonTable.PersonID |
| 3   | Surname    | _TEXT-SL  _RNC               |
| 4   | Given      | _TEXT-SL  _RNC               |
| 5   | Prefix     | _TEXT-SL  _RNC               |
| 6   | Suffix     | _TEXT-SL  _RNC               |
| 7   | Nickname   | _TEXT-SL  _RNC               |
| 8   | NameType   | _LOOKUP                       |
| 9   | Date       | _STD                         |
| 10  | SortDate   | _STD                         |
| 11  | IsPrimary  | _STD                         |
| 12  | IsPrivate  | _STD                         |
| 13  | Proof      | _STD                  |
| 14  | Sentence   | _TEXT-SL                     |
| 14  | Sentence   | _TEXT-SL                     |
| 15  | Note       | _TEXT-ML                     |
| 16  | BirthYear  | _TEXT-SL                     |
| 17  | DeathYear  | _TEXT-SL                     |
| 18  | Display    | _NOT-IMP                     |
| 19  | Language   | _NOT-IMP                     |
| 20  | UTCModDate | _STD                         |
| 21  | SurnameMP  | _NOT-IMP                     |
| 22  | GivenMP    | _NOT-IMP                     |
| 23  | NicknameMP | _NOT-IMP                     |


### MP Columns
these columns have an 'ASCIIized' version of the data in the corresponding column without the MP.

Here are several examples-

| Surname        | SurnameMP      |
| -------------- | -------------- |
| Öhring         | Ohring         |
| Rüb            | Rub            |
| \[wife of Rüb] | \[wife of Rub] |

The Japanese names in my database aren't changed, so ASCIIized is not at 
all a correct description of the transformation. It could also involve using the normalized version of names containing Unicode combining characters.

The columns were not populated at upgrade time, but are filled when a name is now added or edited.

The new columns are not declared with a collation, so the indexes that exist were created using the default binary collation.

## Lookup Tables

| NameType | Type           |
| -------- | -------------- |
| 1        | AKA            |
| 2        | Birth          |
| 3        | Immigrant      |
| 4        | Maiden         |
| 5        | Married        |
| 6        | Nickname       |
| 7        | Other Spelling |


## Open Questions
De-normalized Birth and death dates should go in the PersonTable.
A person can have multiple names, can each name have a dif B & D date in the index?

### DONE 1

