# CitationTable

## Table DDL

```
CREATE TABLE CitationTable (CitationID INTEGER PRIMARY KEY, SourceID INTEGER, Comments TEXT, ActualText TEXT, RefNumber TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, Fields BLOB, UTCModDate FLOAT, CitationName TEXT COLLATE RMNOCASE );

CREATE INDEX idxCitationName ON CitationTable (CitationName);

CREATE INDEX idxCitationSourceID ON CitationTable (SourceID);
```

## Columns List

| #   | Name          | Type    |
| --- | ------------- | ------- |
| 1   | CitationID    | INTEGER |
| 2   | SourceID      | INTEGER |
| 3   | Comments      | TEXT    |
| 4   | ActualText    | TEXT    |
| 5   | RefNumber     | TEXT    |
| 6   | Footnote      | TEXT    |
| 7   | ShortFootnote | TEXT    |
| 8   | Bibliography  | TEXT    |
| 9   | Fields        | BLOB    |
| 10  | UTCModDate    | FLOAT   |
| 11  | CitationName  | TEXT    |

## Notes

| #   | Name          | Note                         |
| --- | ------------- | ---------------------------- |
| 1   | CitationID    | _PK                          |
| 2   | SourceID      | _FK ==> SourceTable.SourceID |
| 3   | Comments      | _TEXT-ML                     |
| 4   | ActualText    | _TEXT-ML                     |
| 5   | RefNumber     | _TEXT-SL                     |
| 6   | Footnote      | _TEXT-SL                     |
| 7   | ShortFootnote | _TEXT-SL                     |
| 8   | Bibliography  | _TEXT-SL                     |
| 9   | Fields        | BLOB XML                     |
| 10  | UTCModDate    | _STD                         |
| 11  | CitationName  | _RNC                         |


Columns: Footnote, ShortFootnote, and Bibliography are used for custom sentences.

Haven't tested, but its plain text, so probably exactly the same as the Footnote, ShortFootnote, and Bibliography columns in SourceTemplateTable

CitationName can be automatically generated or can be edited by the user.
Defailt is:
```
Separator ::= "; "
CitationName ::= <Cit-filed-1-value> <Separator> <Cit-filed-2-value> <Separator> ... <Cit-filed-N-value> \
```
The order is set by the listing position in the Source Template.

Fields = contains XML as shown below. All XML data is in one line, nor CR LF. (not pretty printed as shown here.)\
Field name from SourceTemplate, goes in the Name element.
Text goes in the Value element. 

Name and Value element content are designed to be single line text.

```
<Root>
  <Fields>
    <Field>
      <Name>
        a field name
      </Name>
      <Value>
        field name content
      </Value>
    </Field>
    <Field>
      <Name>
        another field name
      </Name>
      <Value>
        more content
      </Value>
    </Field>
  </Fields>
</Root>
```
Newly created XML field column data RM ver>=8 starts with <Root>.
Old style started with a BOM, an XML declaration statement, a LF, then <Root> and ended with a LF.

Builtin SourceTemplates in v 9.1.3 still have old style XML

 ## Open Questions

 In v8 why wasn't CitationName moved further forward and last coluim set to UTCModDate ?

 Why isn't the Fields column a text field, it will always be UTF-8. 
 