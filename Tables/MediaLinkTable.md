# MediaLinkTable

## Table DDL

```
CREATE TABLE MediaLinkTable (LinkID INTEGER PRIMARY KEY, MediaID INTEGER, OwnerType INTEGER, OwnerID INTEGER, IsPrimary INTEGER, Include1 INTEGER, Include2 INTEGER, Include3 INTEGER, Include4 INTEGER, SortOrder INTEGER, RectLeft INTEGER, RectTop INTEGER, RectRight INTEGER, RectBottom INTEGER, Comments TEXT, UTCModDate FLOAT );

CREATE INDEX idxMediaOwnerID ON MediaLinkTable (OwnerID);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | MediaID    | INTEGER |
| 3   | OwnerType  | INTEGER |
| 4   | OwnerID    | INTEGER |
| 5   | IsPrimary  | INTEGER |
| 6   | Include1   | INTEGER |
| 7   | Include2   | INTEGER |
| 8   | Include3   | INTEGER |
| 9   | Include4   | INTEGER |
| 10  | SortOrder  | INTEGER |
| 11  | RectLeft   | INTEGER |
| 12  | RectTop    | INTEGER |
| 13  | RectRight  | INTEGER |
| 14  | RectBottom | INTEGER |
| 15  | Comments   | TEXT    |
| 16  | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                                     |
| --- | ---------- | ---------------------------------------- |
| 1   | LinkID     | _PK                                      |
| 2   | MediaID    | _FK ==> MultimediaTable.MediaID          |
| 3   | OwnerType  | _PFK-TYPE                                |
| 4   | OwnerID    | _PFK                                     |
| 5   | IsPrimary  | _STD                                     |
| 6   | Include1   | _01-FLAG _GUI-LAB="Include in scrapbook" |
| 7   | Include2   | _NOT-IMP  (all 0)                        |
| 8   | Include3   | _NOT-IMP  (all 0)                        |
| 9   | Include4   | _NOT-IMP  (all 0)                        |
| 10  | SortOrder  | _NOT_IMP except for person media gallery |
| 11  | RectLeft   | _NOT-IMP                                 |
| 12  | RectTop    | _NOT-IMP                                 |
| 13  | RectRight  | _NOT-IMP                                 |
| 14  | RectBottom | _NOT-IMP                                 |
| 15  | Comments   | _TEXT-ML                                 |
| 16  | UTCModDate | _STD                                     |

OwnerType's seen in database

| OwnerType | object       |
| :-------- | :----------- |
| 14        | Place Detail |
| 7         | Name         |
| 5         | Place        |
| 4         | Citation     |
| 3         | Source       |
| 2         | Fact         |
| 0         | Person       |

OTHERS ?

IsPrimary  Used only for an image attached to a Person. Indicates it is the profile image.

Include1  In the GUI, it is "Include in scrapbook" checkbox
Include2 & Include3 & Include4     not shown in GUI.

SortOrder  Implemented only in the Person media gallery. (on Person edit windows, icon in left side)

Unimplemented feature would allow a tag to represent a subset of the full image.
RectLeft, RectTop, RectRight, RectBottom


## Open Questions

IsPrimary  Used only for an image attached to a Person.(?) Indicates it is the profile image.

### DONE 1
