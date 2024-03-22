# SourceTemplateTable

## Table DDL

```
CREATE TABLE SourceTemplateTable (TemplateID INTEGER PRIMARY KEY, Name TEXT COLLATE RMNOCASE, Description TEXT, Favorite INTEGER, Category TEXT, Footnote TEXT, ShortFootnote TEXT, Bibliography TEXT, FieldDefs BLOB, UTCModDate FLOAT );

CREATE INDEX idxSourceTemplateName ON SourceTemplateTable (Name);
```

## Columns List

| #   | Name          | Type    |
| --- | ------------- | ------- |
| 1   | TemplateID    | INTEGER |
| 2   | Name          | TEXT    |
| 3   | Description   | TEXT    |
| 4   | Favorite      | INTEGER |
| 5   | Category      | TEXT    |
| 6   | Footnote      | TEXT    |
| 7   | ShortFootnote | TEXT    |
| 8   | Bibliography  | TEXT    |
| 9   | FieldDefs     | BLOB    |
| 10  | UTCModDate    | FLOAT   |

## Notes

| #   | Name          | Type     |
| --- | ------------- | -------- |
| 1   | TemplateID    | _PK      |
| 2   | Name          | _TEXT-SL |
| 3   | Description   | _TEXT-SL |
| 4   | Favorite      | _LOOKUP   |
| 5   | Category      | _TEXT-SL |
| 6   | Footnote      | _TEXT-SL |
| 7   | ShortFootnote | _TEXT-SL |
| 8   | Bibliography  | _TEXT-SL |
| 9   | FieldDefs     | XML      |
| 10  | UTCModDate    | _STD     |

No prohibition against duplicate Names.\
Names may have leading, trailing, embedded spaces.

Favorite- records with Favorite=1 show their names in the drop down list from the Favorites button at top of RM GUI window- Source templates. Not clear how "recents" list is saved.

No info in documentation on how to use category field.
It is in the RM GUI in SourceTemplate list window.
All the builtin templates use the fields to cite Evidence Explained and other books.

Footnote, ShortFootnote, & Bibliography are the template to use for creation of the corresponding output using the values of the constituent fields from the source and citation records.

FieldDefs is the XML that encodes all of the information editable in the RM SourceTemplates window.

A sample of FieldDefs - only 1 source field nad only 1 citation field. Shown as XML pretty print format, the actual data is all one line. (not clear if long hint can have new lines.)

```
<Root>
    <Fields>
        <Field>
            <FieldName>DateSource</FieldName>
            <DisplayName>DateSource</DisplayName>
            <Type>Date</Type>
            <Hint></Hint>
            <LongHint></LongHint>
            <CitationField>False</CitationField>
        </Field>
        <Field>
            <FieldName>DateMarker</FieldName>
            <DisplayName>DateMarker</DisplayName>
            <Type>Date</Type>
            <Hint></Hint>
            <LongHint></LongHint>
            <CitationField>True</CitationField>
        </Field>
    </Fields>
</Root>
```


## Lookup Tables

| Favorite | meaning |
| :------- | :------ |
| 0        | no      |
| 1        | Yes     |

## Open Questions

### DONE 1