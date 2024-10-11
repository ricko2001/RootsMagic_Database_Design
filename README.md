# RootsMagic_Database_Design
This branch of the repo describes the ver 9 database schema
See the main ranch for the current (or latest) schema version

## Overview

RootsMagic software, published by RootsMagic Inc. <https://RootsMagic.com>
is a genealogy research project organizational tool
used by amateur and professional genealogists and ordinary hobbyists who want to
build their family tree.

This dataset was created by the community of RootsMagic users.

RootsMagic is distinguished by its use of an unencrypted SQLite database as its
storage file format. That makes the user's data available to third party tools
and applications. One won't have to worry about one's data being locked up in 
a proprietary storage format.

If you are interested in SQL access to the RootsMagic database, you must become
familiar with the web site <https://SQLiteToolsForRootsMagic.com>

There is a user forum where interesting questions are posed and answered.

The forum format allows a easy exchange of ideas and posting of SQL statements, but it
does not lend itself towards creating documentation and keeping it current and fixing errors.
That's why I am starting this project where anyone can contribute, fix errors, and fill in the gaps.
Everything is under version control, so we can keep current docs for all future RM releases
in separate branches or perhaps create point-in-time "releases" that may be more easily accessed.

## Content

Currently, most content is in the Tables folder, which contains one file for 
each RM database table plus one file, "+ General.md", containing information used by the 
table files.
Each table file has:
* Table name at the top.
* Purpose section. A one liner giving summary of what this table does.
* the DDL used to create the table, as generated by the "SQLite Expert" app.
* a list of the columns with the datatype.
* a Notes section which includes another list of the columns with column type notes, and then, 
free form notes another list.
* A Lookup Tables section, if the table has a field that uses pre-defined values.
* An Open Questions section which makes uncertainty more obvious.
* A DONE marker with a level number. starting at 1 and increasing, 
here to help order what needs to be fixed next.

Some more general topics are included in this root folder, alongside this ReadMe file..

Also- a disclaimer- I have not investigated the RootsMagic "LDS Options".


## File format

In case it's not obvious, the table files, like this file are in MarkDown format (file extension.md)
<https://github.github.com/gfm/#what-is-github-flavored-markdown->

The easiest way to view these files in the rendered form is by opening then from a GitHub repository.
To edit them, open the raw format version.
There are lots of text editors that will also display them in the rendered form.
e.g. Visual Studio Code, NotePad++ with a MarkDown plugin.

