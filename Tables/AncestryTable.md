# AncestryTable

## Table DDL

```
CREATE TABLE AncestryTable (LinkID INTEGER PRIMARY KEY, LinkType INTEGER, rmID INTEGER, anID TEXT, Modified INTEGER, anVersion TEXT, anDate FLOAT, Status INTEGER, UTCModDate FLOAT );

CREATE INDEX idxLinkAncestryRmId ON AncestryTable (rmID);

CREATE INDEX idxLinkAncestryanID ON AncestryTable (anID);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | LinkID     | INTEGER |
| 2   | LinkType   | INTEGER |
| 3   | rmID       | INTEGER |
| 4   | anID       | TEXT    |
| 5   | Modified   | INTEGER |
| 6   | anVersion  | TEXT    |
| 7   | anDate     | FLOAT   |
| 8   | Status     | INTEGER |
| 9   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note |
| --- | ---------- | ---- |
| 1   | LinkID     | _PK  |
| 2   | LinkType   |      |
| 3   | rmID       |      |
| 4   | anID       |      |
| 5   | Modified   |      |
| 6   | anVersion  |      |
| 7   | anDate     |      |
| 8   | Status     |      |
| 9   | UTCModDate | _STD |

## Open Questions


<pre>
LinkType  

LinkType   count(*)   for my DB of 10922 people, look like it was synced when it had 7987 people
0          7987
4          58548
1          14045


rmID    seems to be RM PersonID
typical format
0          202242350006:1030:173150824
4          702343252726:9000:173150824
11         CDAC665497294FEC8C8BC95145093D70


for a rmID =1 (me)
linkType       anID
0              202242349975:1030:173150824
4              702343257427:9000:173150824
11             AF711847193744D2A9707A8CD25ECDF0
11             0DAE392A008B423A9EA3D97ED9856D28


https://www.ancestry.com/family-tree/person/tree/173150824/person/202242349975/facts
https://www.ancestry.com/family-tree/tree/173150824/family?cfpid=202242349975

person 1 unique id= C8D78EB337724572B26801A1C6D694C5F13C

so, linkType=1 gives the ancestry person ID


AncestryTable
LinkID just a primary key, same as rowid

rm ID corresponds to RIN
an ID  identifier used at Ancestry

LinkType
0   links people.       202242349975:1030:173150824
4                       702343257427:9000:173150824
11                      0DAE392A008B423A9EA3D97ED9856D28


LinkType = 0
example for RJO
rmID 1
anID 202242349975:1030:173150824
anID  personID:localeID:treeID

localeID 1030 = English-USA

RJO profile
https://www.ancestry.com/family-tree/person/tree/173150824/person/202242349975/facts


RJO profile in Otter-Saito-RM tree

14 images linked to RJO

lots, say 60 items uploaded from RM
citations, Fact notes

5 citations native to ancestry, probably added via ANC GUI


one source linked is NY Birth index
https://www.ancestry.com/discoveryui-content/view/8310107:61457?ssrc=pt&tid=173150824&pid=202242349975

8310107:61457           recordID:collectionID
tid=173150824           treeID
pid=202242349975        personID

</pre>
