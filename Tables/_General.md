# RM v9.1.3 full schema

## Controlled Vocabulary

| token         | meaning                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------ |
| _PK           | primary key                                                                                |
| _FK           | foreign key                                                                                |
| _PFK          | polymorphic foreign key                                                                    |
| _PFK-TYPE     | polymorphic foreign key type (where does PFFK point)                                       |
| _STD          | standard colum described here                                                              |
| _TEXT-SL      | text field designed for a single line string                                               |
| _TEXT-ML      | text field designed for a multiple lines of text. Uses CR LF end of line for Win and MacOS |
| _RNC          | column is used in an index collated with proprietory collation RMNOCAASE                   |
| _01-FLAG      | SQLite Integer column with a value of 0 or 1                                               |
| _3CAHR-FLAG   | text field containing 3 characters (CitationLinkTable.Quality)                             |
| _SPECIAL-CASE | marker used to describe special case of _FK, usually 0.                                    |
| _GUI-LAB      | set to the string used to label the data in the RM GUI                                     |
| _NOT-IMP      | Not Implemented. No obvious use as of current release.                                     |
| ### DONE 1    | marker indicating work is completed for that file to standard "1"                          |


## Notes

The column types-
_01-FLAG, _3CAHR-FLAG
should be thought of as _LOOKUP type  TODO

Polymorphic Associations. Using this design, can't use relational database refential integrity mechanisms.


Could use-\
unique indexes to enforce IsPrimary\
Triggers to do update of de-normalized data (BDate, DDate, Reverse (place), NameMP cols


## Standard Columns  _STD

UTCModDate	FLOAT
Modified Julian date
see: <https://en.wikipedia.org/wiki/Julian_day?>

using SQLite-
to generate current UTCModDate
SELECT julianday('now') - 2415018.5 AS UTCModDate

to convert UTCModDate to standard format date/time
SELECT UTCModDate,
DATE(UTCModDate + 2415018.5) AS Date,
TIME(UTCModDate + 2415018.5) AS Time,
DATETIME(UTCModDate + 2415018.5) AS DateTime
FROM EventTable



Date		TEXT
See other document

SortDate	BIGINT
See other document


Latitude     INTEGER
Longitude    INTEGER
values stored as a signed integer with a scale factor
for example- Oakland, CA
stored value   scale    actual
378044389   * 10e-7  = 37.8044389
-1222697194 * 10e-7  = -122.2697194
W adn S are nedative


## Lookup tables

below from  https://sqlitetoolsforrootsmagic.com/rm9-data-definitions/

| Table    | RecType | OwnerType             | OwnerID |
| -------- | ------- | --------------------- | ------- |
| Payload  | 1       | (SavedCriteriaSearch) | 8       | 0
| Payload  | 2       | (SavedCriteriaGroup)  | 20      | TagTable.TagValue, GroupTable.GroupID
| FANTable |         |                       | 19      | CitationLinkTable, MediaLinkTable,...


Polymorphic Foreign Key Type

| OwnerType | Links to     | Table.row                |
| --------- | ------------ | ------------------------ |
| 0         | person       | PersonTable.PersonID     |
| 1         | couple       | FamilyTable.FamilyID     |
| 2         | fact/event   | EventTable.EventID       |
| 3         | source       | SourceTable.SourceID     |
| 4         | citation     | CitationTable.CitationID |
| 5         | place        | PlaceTable.PlaceID       |
| 6         | task         | TaskTable.TaskID         |
| 7         | name         | NameTable.NameID         |
| 8         |              |                          |
| 14        | place detail | PlaceTable.PlaceID       |
| 19        | association  | FANTable.FanID           |
| 20        |              |                          |

5 & 14 both point to PlaceTable.PlaceID \
PlaceTable.PlaceType distinguishes the 3 types of places.


| Proof | level     |
| ----- | --------- |
| 0     | <blank>   |
| 1     | Proven    |
| 2     | Disproven |
| 3     | Disputed  |

| IsPrimary | primary ? |
| --------- | --------- |
| 0         | No        |
| 1         | Yes       |

| IsPrivate | private? |
| --------- | -------- |
| 0         | No       |
| 1         | Yes      |



## References

https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form

## Table DDL

For full database

```
CREATE TABLE AddressLinkTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, AddressID INTEGER, OwnerID INTEGER, AddressNum INTEGER, Details TEXT, UTCModDate FLOAT );

CREATE TABLE AddressTable (AddressID INTEGER PRIMARY KEY, AddressType INTEGER, Name TEXT COLLATE RMNOCASE, Street1 TEXT, Street2 TEXT, City TEXT, State TEXT, Zip TEXT, Country TEXT, Phone1 TEXT, Phone2 TEXT, Fax TEXT, Email TEXT, URL TEXT, Latitude INTEGER, Longitude INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE TABLE AncestryTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, anID TEXT, Modified INTEGER, anVersion TEXT, anDate FLOAT, Status INTEGER, UTCModDate FLOAT );

CREATE TABLE ChildTable (RecID INTEGER PRIMARY KEY, ChildID INTEGER, FamilyID INTEGER, RelFather INTEGER, RelMother INTEGER, ChildOrder INTEGER, IsPrivate INTEGER, ProofFather INTEGER, ProofMother INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE TABLE CitationLinkTable (LinkID INTEGER PRIMARY KEY, CitationID INTEGER, OwnerType INTEGER, OwnerID INTEGER, SortOrder INTEGER, Quality TEXT, IsPrivate INTEGER, Flags INTEGER, UTCModDate FLOAT );

CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT COLLATE RMNOCASE );

CREATE TABLE ConfigTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );

CREATE TABLE EventTable (EventID INTEGER PRIMARY KEY, EventType INTEGER, OwnerType INTEGER, OwnerID INTEGER, FamilyID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Status INTEGER, Sentence TEXT, Details TEXT, Note TEXT, UTCModDate FLOAT );

CREATE TABLE ExclusionTable (RecID INTEGER PRIMARY KEY, ExclusionType INTEGER, ID1 INTEGER, ID2 INTEGER, UTCModDate FLOAT );

CREATE TABLE FactTypeTable (FactTypeID INTEGER PRIMARY KEY, OwnerType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, GedcomTag TEXT, UseValue INTEGER, UseDate INTEGER, UsePlace INTEGER, Sentence TEXT, Flags INTEGER, UTCModDate FLOAT );

CREATE TABLE FamilySearchTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, fsID TEXT, Modified INTEGER, fsVersion TEXT, fsDate FLOAT, Status INTEGER, UTCModDate FLOAT );

CREATE TABLE FamilyTable (FamilyID INTEGER PRIMARY KEY, FatherID INTEGER, MotherID INTEGER, ChildID INTEGER, HusbOrder INTEGER, WifeOrder INTEGER, IsPrivate INTEGER, Proof INTEGER, SpouseLabel INTEGER, FatherLabel INTEGER, MotherLabel INTEGER, SpouseLabelStr TEXT, FatherLabelStr TEXT, MotherLabelStr TEXT, Note TEXT, UTCModDate FLOAT );

CREATE TABLE FANTable (FanID INTEGER PRIMARY KEY, ID1 INTEGER, ID2 INTEGER, FanTypeID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, Description TEXT, Note TEXT, UTCModDate FLOAT );

CREATE TABLE FANTypeTable (FANTypeID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Role1 TEXT, Role2 TEXT, Sentence1 TEXT, Sentence2 TEXT, UTCModDate FLOAT );

CREATE TABLE GroupTable (RecID INTEGER PRIMARY KEY, GroupID INTEGER, StartID INTEGER, EndID INTEGER, UTCModDate FLOAT );

CREATE TABLE MediaLinkTable (LinkID INTEGER PRIMARY KEY, MediaID INTEGER, OwnerType INTEGER, OwnerID INTEGER, IsPrimary INTEGER, Include1 INTEGER, Include2 INTEGER, Include3 INTEGER, Include4 INTEGER, SortOrder INTEGER, RectLeft INTEGER, RectTop INTEGER, RectRight INTEGER, RectBottom INTEGER, Comments TEXT, UTCModDate FLOAT );

CREATE TABLE MultimediaTable (MediaID INTEGER PRIMARY KEY, MediaType INTEGER, MediaPath TEXT, MediaFile TEXT COLLATE RMNOCASE, URL TEXT, Thumbnail BLOB, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate BIGINT, Description TEXT, UTCModDate FLOAT );

CREATE TABLE NameTable (NameID INTEGER PRIMARY KEY, OwnerID INTEGER, Surname TEXT COLLATE RMNOCASE, Given TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, Nickname TEXT COLLATE RMNOCASE, NameType INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Sentence TEXT, Note TEXT, BirthYear INTEGER, DeathYear INTEGER, Display INTEGER, Language TEXT, UTCModDate FLOAT, SurnameMP TEXT, GivenMP TEXT, NicknameMP TEXT );

CREATE TABLE PayloadTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, OwnerType INTEGER, OwnerID INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );

CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Color1 INTEGER, Color2 INTEGER, Color3 INTEGER, Color4 INTEGER, Color5 INTEGER, Color6 INTEGER, Color7 INTEGER, Color8 INTEGER, Color9 INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note TEXT, UTCModDate FLOAT );

CREATE TABLE PlaceTable (PlaceID INTEGER PRIMARY KEY, PlaceType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, Normalized TEXT, Latitude INTEGER, Longitude INTEGER, LatLongExact INTEGER, MasterID INTEGER, Note TEXT, Reverse TEXT COLLATE RMNOCASE, fsID INTEGER, anID INTEGER, UTCModDate FLOAT );

CREATE TABLE RoleTable (RoleID INTEGER PRIMARY KEY, RoleName TEXT COLLATE RMNOCASE, EventType INTEGER, RoleType INTEGER, Sentence TEXT, UTCModDate FLOAT );

CREATE TABLE SourceTable (SourceID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, RefNumber TEXT, ActualText TEXT, Comments TEXT, IsPrivate INTEGER, TemplateID INTEGER, Fields BLOB, UTCModDate FLOAT );

CREATE TABLE SourceTemplateTable (TemplateID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Description TEXT, Favorite INTEGER, Category TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, FieldDefs BLOB, UTCModDate FLOAT );

CREATE TABLE TagTable (TagID INTEGER PRIMARY KEY, TagType INTEGER, TagValue INTEGER, TagName TEXT COLLATE RMNOCASE, Description TEXT, UTCModDate FLOAT );

CREATE TABLE TaskLinkTable (LinkID INTEGER PRIMARY KEY, TaskID INTEGER, OwnerType INTEGER, OwnerID INTEGER, UTCModDate FLOAT );

CREATE TABLE TaskTable (TaskID INTEGER PRIMARY KEY, TaskType INTEGER, RefNumber TEXT, Name TEXT COLLATE RMNOCASE, Status INTEGER, Priority INTEGER, Date1 TEXT, Date2 TEXT, Date3 TEXT, SortDate1 BIGINT, SortDate2 BIGINT, SortDate3 BITINT, Filename TEXT, Details TEXT, Results TEXT, UTCModDate FLOAT, Exclude INTEGER );

CREATE TABLE URLTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, OwnerID INTEGER, LinkType INTEGER, Name TEXT, URL TEXT, Note TEXT, UTCModDate FLOAT );

CREATE TABLE WitnessTable (WitnessID INTEGER PRIMARY KEY, EventID INTEGER, PersonID INTEGER, WitnessOrder INTEGER, Role INTEGER, Sentence TEXT, Note TEXT, Given TEXT COLLATE RMNOCASE, Surname TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, UTCModDate FLOAT );

CREATE INDEX idxAddressName ON AddressTable (Name);

CREATE INDEX idxChildFamilyID ON ChildTable (FamilyID);

CREATE INDEX idxChildID ON ChildTable (ChildID);

CREATE INDEX idxChildOrder ON ChildTable (ChildOrder);

CREATE INDEX idxCitationLinkOwnerID ON CitationLinkTable (OwnerID);

CREATE INDEX idxCitationName ON CitationTable (CitationName);

CREATE INDEX idxCitationSourceID ON CitationTable (SourceID);

CREATE UNIQUE INDEX idxExclusionIndex ON ExclusionTable (ExclusionType, ID1, ID2);

CREATE INDEX idxFactTypeAbbrev ON FactTypeTable (Abbrev);

CREATE INDEX idxFactTypeGedcomTag ON FactTypeTable (GedcomTag);

CREATE INDEX idxFactTypeName ON FactTypeTable (Name);

CREATE INDEX idxFamilyFatherID ON FamilyTable (FatherID);

CREATE INDEX idxFamilyMotherID ON FamilyTable (MotherID);

CREATE INDEX idxFanId1 ON FANTable (ID1);

CREATE INDEX idxFanId2 ON FANTable (ID2);

CREATE INDEX idxFANTypeName ON FANTypeTable (Name);

CREATE INDEX idxGiven ON NameTable (Given);

CREATE INDEX idxGivenMP ON NameTable (GivenMP);

CREATE INDEX idxLinkAncestryanID ON AncestryTable (anID);

CREATE INDEX idxLinkAncestryRmId ON AncestryTable (rmID);

CREATE INDEX idxLinkfsID ON FamilySearchTable (fsID);

CREATE INDEX idxLinkRmId ON FamilySearchTable (rmID);

CREATE INDEX idxMediaFile ON MultimediaTable (MediaFile);

CREATE INDEX idxMediaOwnerID ON MediaLinkTable (OwnerID);

CREATE INDEX idxMediaURL ON MultimediaTable (URL);

CREATE INDEX idxNameOwnerID ON NameTable (OwnerID);

CREATE INDEX idxNamePrimary ON NameTable (IsPrimary);

CREATE INDEX idxOwnerDate ON EventTable (OwnerID,SortDate);

CREATE INDEX idxOwnerEvent ON EventTable (OwnerID,EventType);

CREATE INDEX idxPayloadType ON PayloadTable (RecType);

CREATE INDEX idxPlaceAbbrev ON PlaceTable (Abbrev);

CREATE INDEX idxPlaceName ON PlaceTable (Name);

CREATE INDEX idxRecType ON ConfigTable (RecType);

CREATE INDEX idxReversePlaceName ON PlaceTable (Reverse);

CREATE INDEX idxRoleEventType ON RoleTable (EventType);

CREATE INDEX idxSourceName ON SourceTable (Name COLLATE RMNOCASE) ;

CREATE INDEX idxSourceTemplateName ON SourceTemplateTable (Name);

CREATE INDEX idxSurname ON NameTable (Surname);

CREATE INDEX idxSurnameGiven ON NameTable (Surname, Given, BirthYear, DeathYear);

CREATE INDEX idxSurnameGivenMP ON NameTable (SurnameMP, GivenMP, BirthYear, DeathYear);

CREATE INDEX idxSurnameMP ON NameTable (SurnameMP);

CREATE INDEX idxTagType ON TagTable (TagType);

CREATE INDEX idxTaskName ON TaskTable (Name);

CREATE INDEX idxTaskOwnerID ON TaskLinkTable (OwnerID);

CREATE INDEX idxWitnessEventID ON WitnessTable (EventID);

CREATE INDEX idxWitnessPersonID ON WitnessTable (PersonID);
```


## RMNOCASE - found in DDL here

(ignore Line  NN)
```
	Line   7: CREATE TABLE AddressTable (AddressID INTEGER PRIMARY KEY, AddressType INTEGER, Name TEXT COLLATE RMNOCASE, Street1 TEXT, Street2 TEXT, City TEXT, State TEXT, Zip TEXT, Country TEXT, Phone1 TEXT, Phone2 TEXT, Fax TEXT, Email TEXT, URL TEXT, Latitude INTEGER, Longitude INTEGER, Note TEXT, UTCModDate FLOAT );

	Line  15: CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT COLLATE RMNOCASE );

	Line  23: CREATE TABLE FactTypeTable (FactTypeID INTEGER PRIMARY KEY, OwnerType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, GedcomTag TEXT, UseValue INTEGER, UseDate INTEGER, UsePlace INTEGER, Sentence TEXT, Flags INTEGER, UTCModDate FLOAT );

	Line  31: CREATE TABLE FANTypeTable (FANTypeID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Role1 TEXT, Role2 TEXT, Sentence1 TEXT, Sentence2 TEXT, UTCModDate FLOAT );

	Line  37: CREATE TABLE MultimediaTable (MediaID INTEGER PRIMARY KEY, MediaType INTEGER, MediaPath TEXT, MediaFile TEXT COLLATE RMNOCASE, URL TEXT, Thumbnail BLOB, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate BIGINT, Description TEXT, UTCModDate FLOAT );

	Line  39: CREATE TABLE NameTable (NameID INTEGER PRIMARY KEY, OwnerID INTEGER, Surname TEXT COLLATE RMNOCASE, Given TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, Nickname TEXT COLLATE RMNOCASE, NameType INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Sentence TEXT, Note TEXT, BirthYear INTEGER, DeathYear INTEGER, Display INTEGER, Language TEXT, UTCModDate FLOAT, SurnameMP TEXT, GivenMP TEXT, NicknameMP TEXT );

	Line  45: CREATE TABLE PlaceTable (PlaceID INTEGER PRIMARY KEY, PlaceType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, Normalized TEXT, Latitude INTEGER, Longitude INTEGER, LatLongExact INTEGER, MasterID INTEGER, Note TEXT, Reverse TEXT COLLATE RMNOCASE, fsID INTEGER, anID INTEGER, UTCModDate FLOAT );

	Line  47: CREATE TABLE RoleTable (RoleID INTEGER PRIMARY KEY, RoleName TEXT COLLATE RMNOCASE, EventType INTEGER, RoleType INTEGER, Sentence TEXT, UTCModDate FLOAT );

	Line  49: CREATE TABLE SourceTable (SourceID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, RefNumber TEXT, ActualText TEXT, Comments TEXT, IsPrivate INTEGER, TemplateID INTEGER, Fields BLOB, UTCModDate FLOAT );

	Line  51: CREATE TABLE SourceTemplateTable (TemplateID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Description TEXT, Favorite INTEGER, Category TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, FieldDefs BLOB, UTCModDate FLOAT );

	Line  53: CREATE TABLE TagTable (TagID INTEGER PRIMARY KEY, TagType INTEGER, TagValue INTEGER, TagName TEXT COLLATE RMNOCASE, Description TEXT, UTCModDate FLOAT );

	Line  57: CREATE TABLE TaskTable (TaskID INTEGER PRIMARY KEY, TaskType INTEGER, RefNumber TEXT, Name TEXT COLLATE RMNOCASE, Status INTEGER, Priority INTEGER, Date1 TEXT, Date2 TEXT, Date3 TEXT, SortDate1 BIGINT, SortDate2 BIGINT, SortDate3 BITINT, Filename TEXT, Details TEXT, Results TEXT, UTCModDate FLOAT, Exclude INTEGER );

	Line  61: CREATE TABLE WitnessTable (WitnessID INTEGER PRIMARY KEY, EventID INTEGER, PersonID INTEGER, WitnessOrder INTEGER, Role INTEGER, Sentence TEXT, Note TEXT, Given TEXT COLLATE RMNOCASE, Surname TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, UTCModDate FLOAT );

	Line 133: CREATE INDEX idxSourceName ON SourceTable (Name COLLATE RMNOCASE) ;
```
