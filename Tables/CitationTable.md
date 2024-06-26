# CitationTable

## Purpose

Stores citation information, mainly in the XML column, as well as citation notes and comments.

## Table DDL

``` SQL
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
| 3   | Comments      | _STD                         |
| 4   | ActualText    | _STD                         |
| 5   | RefNumber     | _TEXT-SL                     |
| 6   | Footnote      | _STD                         |
| 7   | ShortFootnote | _STD                         |
| 8   | Bibliography  | _STD                         |
| 9   | Fields        | _STD XML                     |
| 10  | UTCModDate    | _STD                         |
| 11  | CitationName  | _TEXT-SL  _RMNC              |


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


 ## Open Questions

 In v8 why wasn't CitationName moved further forward and last coluim set to UTCModDate ?

 Why isn't the Fields column a text field, it will always be UTF-8. 
 