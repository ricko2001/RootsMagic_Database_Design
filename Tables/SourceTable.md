# SourceTable

## Table DDL

```
CREATE TABLE SourceTable (SourceID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, RefNumber TEXT, ActualText TEXT, Comments TEXT, IsPrivate INTEGER, TemplateID INTEGER, Fields BLOB, UTCModDate FLOAT );

CREATE INDEX idxSourceName ON SourceTable (Name COLLATE RMNOCASE) ;
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | SourceID   | INTEGER |
| 2   | Name       | TEXT    |
| 3   | RefNumber  | TEXT    |
| 4   | ActualText | TEXT    |
| 5   | Comments   | TEXT    |
| 6   | IsPrivate  | INTEGER |
| 7   | TemplateID | INTEGER |
| 8   | Fields     | BLOB    |
| 9   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note                                 |
| --- | ---------- | ------------------------------------ |
| 1   | SourceID   | _PK                                  |
| 2   | Name       | _TEXT-SL _RNC                        |
| 3   | RefNumber  | _TEXT-SL                             |
| 4   | ActualText | _TEXT-ML                             |
| 5   | Comments   | _TEXT-ML                             |
| 6   | IsPrivate  | _STD                                 |
| 7   | TemplateID | _FK =>SourceTemplateTable.TemplateID |
| 8   | Fields     | XML                                  |
| 9   | UTCModDate | _STD                                 |


Name is the source name and it is collated with RMNOCASE, _GUI-LAB="Source Name"

_SPECIAL-CASE
TemplateID points to the SourceTemplateTable.TemplateID, except when it is 0, then use Free Form source. See below.


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


_SPECIAL-CASE\
if TemplateID = 0, for free form templated sources, \
In the SourceTable.Fields has special requirements\
Name element contents must be
```
Footnote
ShortFootnote
Bibliography
```
for example, 
```
<Root><Fields>

<Field><Name>Footnote</Name>
<Value>Journal of Genealogy, entry for John Smith, p12 (1987)</Value></Field>

<Field><Name>ShortFootnote</Name>
<Value>Journal of Genealogy, p12</Value></Field>

<Field><Name>Bibliography</Name>
<Value>Journal of Genealogy</Value></Field>

</Fields></Root>
```

## Open Questions
Why are so many of my sources marked Private ? (IsPrivate=1)
