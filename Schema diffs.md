# Ver 8 to ver 9

## New Tables

## Modified Tables

```
$  diff ver\ 8.txt ver\ 9.txt
11c11
< CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT );
---
> CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT COLLATE RMNOCASE );
24a25,28
> CREATE TABLE FANTable (FanID INTEGER PRIMARY KEY, ID1 INTEGER, ID2 INTEGER, FanTypeID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, Description TEXT, Note TEXT, UTCModDate FLOAT );
>
> CREATE TABLE FANTypeTable (FANTypeID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Role1 TEXT, Role2 TEXT, Sentence1 TEXT, Sentence2 TEXT, UTCModDate FLOAT );
>
33c37,39
< CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note TEXT, UTCModDate FLOAT );
---
> CREATE TABLE PayloadTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, OwnerType INTEGER, OwnerID INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );
>
> CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Color1 INTEGER, Color2 INTEGER, Color3 INTEGER, Color4 INTEGER, Color5 INTEGER, Color6 INTEGER, Color7 INTEGER, Color8 INTEGER, Color9 INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note TEXT, UTCModDate FLOAT );
78a85,90
> CREATE INDEX idxFanId1 ON FANTable (ID1);
>
> CREATE INDEX idxFanId2 ON FANTable (ID2);
>
> CREATE INDEX idxFANTypeName ON FANTypeTable (Name);
>
104a117,118
> CREATE INDEX idxPayloadType ON PayloadTable (RecType);
>
115c129
< CREATE INDEX idxSourceName ON SourceTable (Name);
---
> CREATE INDEX idxSourceName ON SourceTable (Name COLLATE RMNOCASE) ;
```

# Ver 7 to ver 8

## New Tables

## Modified Tables

```
$  diff ver\ 7.txt ver\ 8.txt
1c1
< CREATE TABLE AddressLinkTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, AddressID INTEGER, OwnerID INTEGER, AddressNum INTEGER, Details TEXT );
---
> CREATE TABLE AddressLinkTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, AddressID INTEGER, OwnerID INTEGER, AddressNum INTEGER, Details TEXT, UTCModDate FLOAT );
3c3
< CREATE TABLE AddressTable (AddressID INTEGER PRIMARY KEY, AddressType INTEGER, Name TEXT COLLATE RMNOCASE, Street1 TEXT, Street2 TEXT, City TEXT, State TEXT, Zip TEXT, Country TEXT, Phone1 TEXT, Phone2 TEXT, Fax TEXT, Email TEXT, URL TEXT, Latitude INTEGER, Longitude INTEGER, Note BLOB );
---
> CREATE TABLE AddressTable (AddressID INTEGER PRIMARY KEY, AddressType INTEGER, Name TEXT COLLATE RMNOCASE, Street1 TEXT, Street2 TEXT, City TEXT, State TEXT, Zip TEXT, Country TEXT, Phone1 TEXT, Phone2 TEXT, Fax TEXT, Email TEXT, URL TEXT, Latitude INTEGER, Longitude INTEGER, Note TEXT, UTCModDate FLOAT );
5c5
< CREATE TABLE ChildTable (RecID INTEGER PRIMARY KEY, ChildID INTEGER, FamilyID INTEGER, RelFather INTEGER, RelMother INTEGER, ChildOrder INTEGER, IsPrivate INTEGER, ProofFather INTEGER, ProofMother INTEGER, Note BLOB );
---
> CREATE TABLE AncestryTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, anID TEXT, Modified INTEGER, anVersion TEXT, anDate FLOAT, Status INTEGER, UTCModDate FLOAT );
7c7
< CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, OwnerType INTEGER, SourceID INTEGER, OwnerID INTEGER, Quality TEXT, IsPrivate INTEGER, Comments BLOB, ActualText BLOB, RefNumber TEXT, Flags INTEGER, Fields BLOB );
---
> CREATE TABLE ChildTable (RecID INTEGER PRIMARY KEY, ChildID INTEGER, FamilyID INTEGER, RelFather INTEGER, RelMother INTEGER, ChildOrder INTEGER, IsPrivate INTEGER, ProofFather INTEGER, ProofMother INTEGER, Note TEXT, UTCModDate FLOAT );
9c9
< CREATE TABLE ConfigTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, Title TEXT, DataRec BLOB );
---
> CREATE TABLE CitationLinkTable (LinkID INTEGER PRIMARY KEY, CitationID INTEGER, OwnerType INTEGER, OwnerID INTEGER, SortOrder INTEGER, Quality TEXT, IsPrivate INTEGER, Flags INTEGER, UTCModDate FLOAT );
11c11
< CREATE TABLE EventTable (EventID INTEGER PRIMARY KEY, EventType INTEGER, OwnerType INTEGER, OwnerID INTEGER, FamilyID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate INTEGER, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Status INTEGER, EditDate FLOAT, Sentence BLOB, Details BLOB, Note BLOB );
---
> CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT );
13c13
< CREATE TABLE ExclusionTable (RecID INTEGER PRIMARY KEY, ExclusionType INTEGER, ID1 INTEGER, ID2 INTEGER );
---
> CREATE TABLE ConfigTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );
15c15
< CREATE TABLE FactTypeTable (FactTypeID INTEGER PRIMARY KEY, OwnerType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, GedcomTag TEXT, UseValue INTEGER, UseDate INTEGER, UsePlace INTEGER, Sentence BLOB, Flags INTEGER );
---
> CREATE TABLE EventTable (EventID INTEGER PRIMARY KEY, EventType INTEGER, OwnerType INTEGER, OwnerID INTEGER, FamilyID INTEGER, PlaceID INTEGER, SiteID INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Status INTEGER, Sentence TEXT, Details TEXT, Note TEXT, UTCModDate FLOAT );
17c17
< CREATE TABLE FamilyTable (FamilyID INTEGER PRIMARY KEY, FatherID INTEGER, MotherID INTEGER, ChildID INTEGER, HusbOrder INTEGER, WifeOrder INTEGER, IsPrivate INTEGER, Proof INTEGER, SpouseLabel INTEGER, FatherLabel INTEGER, MotherLabel INTEGER, Note BLOB );
---
> CREATE TABLE ExclusionTable (RecID INTEGER PRIMARY KEY, ExclusionType INTEGER, ID1 INTEGER, ID2 INTEGER, UTCModDate FLOAT );
19c19
< CREATE TABLE GroupTable (RecID INTEGER PRIMARY KEY, GroupID INTEGER, StartID INTEGER, EndID INTEGER );
---
> CREATE TABLE FactTypeTable (FactTypeID INTEGER PRIMARY KEY, OwnerType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, GedcomTag TEXT, UseValue INTEGER, UseDate INTEGER, UsePlace INTEGER, Sentence TEXT, Flags INTEGER, UTCModDate FLOAT );
21c21
< CREATE TABLE LabelTable (LabelID INTEGER PRIMARY KEY, LabelType INTEGER, LabelValue INTEGER, LabelName TEXT COLLATE RMNOCASE, Description TEXT );
---
> CREATE TABLE FamilySearchTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, fsID TEXT, Modified INTEGER, fsVersion TEXT, fsDate FLOAT, Status INTEGER, UTCModDate FLOAT );
23c23
< CREATE TABLE LinkAncestryTable (LinkID INTEGER PRIMARY KEY, extSystem INTEGER, LinkType INTEGER, rmID INTEGER, extID TEXT, Modified INTEGER, extVersion TEXT, extDate FLOAT, Status INTEGER, Note BLOB );
---
> CREATE TABLE FamilyTable (FamilyID INTEGER PRIMARY KEY, FatherID INTEGER, MotherID INTEGER, ChildID INTEGER, HusbOrder INTEGER, WifeOrder INTEGER, IsPrivate INTEGER, Proof INTEGER, SpouseLabel INTEGER, FatherLabel INTEGER, MotherLabel INTEGER, SpouseLabelStr TEXT, FatherLabelStr TEXT, MotherLabelStr TEXT, Note TEXT, UTCModDate FLOAT );
25c25
< CREATE TABLE LinkTable (LinkID INTEGER PRIMARY KEY, extSystem INTEGER, LinkType INTEGER, rmID INTEGER, extID TEXT, Modified INTEGER, extVersion TEXT, extDate FLOAT, Status INTEGER, Note BLOB );
---
> CREATE TABLE GroupTable (RecID INTEGER PRIMARY KEY, GroupID INTEGER, StartID INTEGER, EndID INTEGER, UTCModDate FLOAT );
27c27
< CREATE TABLE MediaLinkTable (LinkID INTEGER PRIMARY KEY, MediaID INTEGER, OwnerType INTEGER, OwnerID INTEGER, IsPrimary INTEGER, Include1 INTEGER, Include2 INTEGER, Include3 INTEGER, Include4 INTEGER, SortOrder INTEGER, RectLeft INTEGER, RectTop INTEGER, RectRight INTEGER, RectBottom INTEGER, Note TEXT, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate INTEGER, Description BLOB );
---
> CREATE TABLE MediaLinkTable (LinkID INTEGER PRIMARY KEY, MediaID INTEGER, OwnerType INTEGER, OwnerID INTEGER, IsPrimary INTEGER, Include1 INTEGER, Include2 INTEGER, Include3 INTEGER, Include4 INTEGER, SortOrder INTEGER, RectLeft INTEGER, RectTop INTEGER, RectRight INTEGER, RectBottom INTEGER, Comments TEXT, UTCModDate FLOAT );
29c29
< CREATE TABLE MultimediaTable (MediaID INTEGER PRIMARY KEY, MediaType INTEGER, MediaPath TEXT, MediaFile TEXT COLLATE RMNOCASE, URL TEXT, Thumbnail BLOB, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate INTEGER, Description BLOB );
---
> CREATE TABLE MultimediaTable (MediaID INTEGER PRIMARY KEY, MediaType INTEGER, MediaPath TEXT, MediaFile TEXT COLLATE RMNOCASE, URL TEXT, Thumbnail BLOB, Caption TEXT COLLATE RMNOCASE, RefNumber TEXT COLLATE RMNOCASE, Date TEXT, SortDate BIGINT, Description TEXT, UTCModDate FLOAT );
31c31
< CREATE TABLE NameTable (NameID INTEGER PRIMARY KEY, OwnerID INTEGER, Surname TEXT COLLATE RMNOCASE, Given TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, Nickname TEXT COLLATE RMNOCASE, NameType INTEGER, Date TEXT, SortDate INTEGER, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, EditDate FLOAT, Sentence BLOB, Note BLOB, BirthYear INTEGER, DeathYear INTEGER );
---
> CREATE TABLE NameTable (NameID INTEGER PRIMARY KEY, OwnerID INTEGER, Surname TEXT COLLATE RMNOCASE, Given TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, Nickname TEXT COLLATE RMNOCASE, NameType INTEGER, Date TEXT, SortDate BIGINT, IsPrimary INTEGER, IsPrivate INTEGER, Proof INTEGER, Sentence TEXT, Note TEXT, BirthYear INTEGER, DeathYear INTEGER, Display INTEGER, Language TEXT, UTCModDate FLOAT, SurnameMP TEXT, GivenMP TEXT, NicknameMP TEXT );
33c33
< CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, EditDate FLOAT, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note BLOB );
---
> CREATE TABLE PersonTable (PersonID INTEGER PRIMARY KEY, UniqueID TEXT, Sex INTEGER, ParentID INTEGER, SpouseID INTEGER, Color INTEGER, Relate1 INTEGER, Relate2 INTEGER, Flags INTEGER, Living INTEGER, IsPrivate INTEGER, Proof INTEGER, Bookmark INTEGER, Note TEXT, UTCModDate FLOAT );
35c35
< CREATE TABLE PlaceTable (PlaceID INTEGER PRIMARY KEY, PlaceType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, Normalized TEXT, Latitude INTEGER, Longitude INTEGER, LatLongExact INTEGER, MasterID INTEGER, Note BLOB );
---
> CREATE TABLE PlaceTable (PlaceID INTEGER PRIMARY KEY, PlaceType INTEGER, Name TEXT COLLATE RMNOCASE, Abbrev TEXT, Normalized TEXT, Latitude INTEGER, Longitude INTEGER, LatLongExact INTEGER, MasterID INTEGER, Note TEXT, Reverse TEXT COLLATE RMNOCASE, fsID INTEGER, anID INTEGER, UTCModDate FLOAT );
37c37
< CREATE TABLE ResearchItemTable (ItemID INTEGER PRIMARY KEY, LogID INTEGER, Date TEXT, SortDate INTEGER, RefNumber TEXT, Repository TEXT, Goal TEXT, Source TEXT, Result TEXT );
---
> CREATE TABLE RoleTable (RoleID INTEGER PRIMARY KEY, RoleName TEXT COLLATE RMNOCASE, EventType INTEGER, RoleType INTEGER, Sentence TEXT, UTCModDate FLOAT );
39c39
< CREATE TABLE ResearchTable (TaskID INTEGER PRIMARY KEY, TaskType INTEGER, OwnerID INTEGER, OwnerType INTEGER, RefNumber TEXT, Name TEXT COLLATE RMNOCASE, Status INTEGER, Priority INTEGER, Date1 TEXT, Date2 TEXT, Date3 TEXT, SortDate1 INTEGER, SortDate2 INTEGER, SortDate3 INTEGER, Filename TEXT, Details BLOB );
---
> CREATE TABLE SourceTable (SourceID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, RefNumber TEXT, ActualText TEXT, Comments TEXT, IsPrivate INTEGER, TemplateID INTEGER, Fields BLOB, UTCModDate FLOAT );
41c41
< CREATE TABLE RoleTable (RoleID INTEGER PRIMARY KEY, RoleName TEXT COLLATE RMNOCASE, EventType INTEGER, RoleType INTEGER, Sentence TEXT );
---
> CREATE TABLE SourceTemplateTable (TemplateID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Description TEXT, Favorite INTEGER, Category TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, FieldDefs BLOB, UTCModDate FLOAT );
43c43
< CREATE TABLE SourceTable (SourceID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, RefNumber TEXT, ActualText TEXT, Comments TEXT, IsPrivate INTEGER, TemplateID INTEGER, Fields BLOB );
---
> CREATE TABLE TagTable (TagID INTEGER PRIMARY KEY, TagType INTEGER, TagValue INTEGER, TagName TEXT COLLATE RMNOCASE, Description TEXT, UTCModDate FLOAT );
45c45
< CREATE TABLE SourceTemplateTable (TemplateID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Description TEXT, Favorite INTEGER, Category TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, FieldDefs BLOB );
---
> CREATE TABLE TaskLinkTable (LinkID INTEGER PRIMARY KEY, TaskID INTEGER, OwnerType INTEGER, OwnerID INTEGER, UTCModDate FLOAT );
47c47
< CREATE TABLE URLTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, OwnerID INTEGER, LinkType INTEGER, Name TEXT, URL TEXT, Note BLOB );
---
> CREATE TABLE TaskTable (TaskID INTEGER PRIMARY KEY, TaskType INTEGER, RefNumber TEXT, Name TEXT COLLATE RMNOCASE, Status INTEGER, Priority INTEGER, Date1 TEXT, Date2 TEXT, Date3 TEXT, SortDate1 BIGINT, SortDate2 BIGINT, SortDate3 BITINT, Filename TEXT, Details TEXT, Results TEXT, UTCModDate FLOAT, Exclude INTEGER );
49c49,51
< CREATE TABLE WitnessTable (WitnessID INTEGER PRIMARY KEY, EventID INTEGER, PersonID INTEGER, WitnessOrder INTEGER, Role INTEGER, Sentence TEXT, Note BLOB, Given TEXT COLLATE RMNOCASE, Surname TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE );
---
> CREATE TABLE URLTable (LinkID INTEGER PRIMARY KEY, OwnerType INTEGER, OwnerID INTEGER, LinkType INTEGER, Name TEXT, URL TEXT, Note TEXT, UTCModDate FLOAT );
>
> CREATE TABLE WitnessTable (WitnessID INTEGER PRIMARY KEY, EventID INTEGER, PersonID INTEGER, WitnessOrder INTEGER, Role INTEGER, Sentence TEXT, Note TEXT, Given TEXT COLLATE RMNOCASE, Surname TEXT COLLATE RMNOCASE, Prefix TEXT COLLATE RMNOCASE, Suffix TEXT COLLATE RMNOCASE, UTCModDate FLOAT );
59c61,63
< CREATE INDEX idxCitationOwnerID ON CitationTable (OwnerID);
---
> CREATE INDEX idxCitationLinkOwnerID ON CitationLinkTable (OwnerID);
>
> CREATE INDEX idxCitationName ON CitationTable (CitationName);
77,79c81
< CREATE INDEX idxLabelType ON LabelTable (LabelType);
<
< CREATE INDEX idxLinkAncestryExtId ON LinkAncestryTable (extID);
---
> CREATE INDEX idxGivenMP ON NameTable (GivenMP);
81c83
< CREATE INDEX idxLinkAncestryRmId ON LinkAncestryTable (rmID);
---
> CREATE INDEX idxLinkAncestryanID ON AncestryTable (anID);
83c85
< CREATE INDEX idxLinkExtId ON LinkTable (extID);
---
> CREATE INDEX idxLinkAncestryRmId ON AncestryTable (rmID);
85c87
< CREATE INDEX idxLinkRmId ON LinkTable (rmID);
---
> CREATE INDEX idxLinkfsID ON FamilySearchTable (fsID);
87c89
< CREATE INDEX idxMediaCaption ON MediaLinkTable (Caption);
---
> CREATE INDEX idxLinkRmId ON FamilySearchTable (rmID);
109,113c111
< CREATE INDEX idxResearchItemLogID ON ResearchItemTable (LogID);
<
< CREATE INDEX idxResearchName ON ResearchTable (Name);
<
< CREATE INDEX idxResearchOwnerID ON ResearchTable (OwnerID);
---
> CREATE INDEX idxReversePlaceName ON PlaceTable (Reverse);
125c123,131
< CREATE INDEX idxURLOwnerID ON URLTable (OwnerID);
---
> CREATE INDEX idxSurnameGivenMP ON NameTable (SurnameMP, GivenMP, BirthYear, DeathYear);
>
> CREATE INDEX idxSurnameMP ON NameTable (SurnameMP);
>
> CREATE INDEX idxTagType ON TagTable (TagType);
>
> CREATE INDEX idxTaskName ON TaskTable (Name);
>
> CREATE INDEX idxTaskOwnerID ON TaskLinkTable (OwnerID);
```