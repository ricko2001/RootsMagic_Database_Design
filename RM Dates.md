# RM Date format

## Date information goes though several stages

* A text date is entered by the user into the GUI in a Date field.\
 As the user types, the text is validated. The field is highlighted with an error color as the user types until the text can be interpreted as a valid RM date. Input date format is specified in the RM Preferences.\
* The data that is stored in the database in a RM date field. (Database TEXT field) and a Sort date is created and stored in a RM SortDate field (database INTEGER (BIGINT) field)\
* When the date is displayed by the GUI, the text is generated from the database date. The output is in the canonical date format as specified by in the preferences.\
(the last is also displayed immediately after leaving the entry field before database update.)\

If we call the database data the "stored date"-\
There may be more than one set of characters that can be entered into the RM GUI that generate the same stored date. That text in the GUI is converted to the canonical form.\
There are several ways to display the saved date depending on the format selected in preferences.\


## Double Date has two meanings

Most commonly a date is a single date, Jan 1 1970, herein called a "One Part Date".
A date can also indicate a range or interval, e.g.
```
From Jan 1 1970 to Feb 4 1975
or
Between 8 May 1973 and 8 Jun 1975 
```
herein named a "Two Part Date" since the RM Date has to encode both the start and end dates.\
A second use of the term Double Dates regards the formatting of a date that occurred in the
transition between Julian and Gregorian calendars in the West. This doc calls them "Double JG Dates", they are also called "slash dates".. 

Double JG Dates usually look like this 04 Feb 1740/1 or 14 February 1699/1700  The year is julian/Gregorian and enough digits are used for the Gregorian portion to make it unambiguous. Dates may only to be written as double if they occur between 1 January and 25 March in the years from 1582 until the year of full conversion. (1753 in the old British Empire). RM allows modern dates to be in double JG date format\

Double Date  Julian Gregorian  Old Style - New Style 

<https://www.familysearch.org/en/wiki/Julian_and_Gregorian_Calendars>

<https://news.legacyfamilytree.com/legacy_news/2020/01/tuesdays-tip-double-dating-intermediate.html>

<http://www.searchforancestors.com/utility/gregorian.html>

<https://stevemorse.org/jcal/julian.html>

An example transition (two consecutive days)-

| Country                     | Last Julian Date | First Gregorian Date |
| :-------------------------- | :--------------- | :------------------- |
| Germany, Catholic (Bavaria) | Oct 5, 1583      | Oct 16, 1583         |


In historical sources created when dates were in transition, Julian data was sometimes/often  followed with O.S. and Gregorian dates followed by N.S.( old and new style)


```
                                 GREGORIAN
  2   2   2   2   2   2   2   2   2   2   2   2   3   3   3   3   3   3   3   3   3   3   3   3
  1   2   3   4   5   6   7   8   9  10  11  12   1   2   3   4   5   6   7   8   9  10  11  12 
Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec
 11  12   1   2   3   4   5   6   7   8   9  10  11  12   1   2   3   4   5   6   7   8   9  10   
  1   1   2   2   2   2   2   2   2   2   2   2   2   2   3   3   3   3   3   3   3   3   3   3
                                  JULIIAN
  X   X                                           X   X  
```

## Quarter dates

enter- Q1 2014\
displays- March Quarter 2014   (long format, what about other formats?)\
sort      January 2014\
      Q1 - 2014,  Q2 - June, Q3 - September, Q4 - December \

March Quarter 2014   long format\
Mar Q 2014           short format

sort date is as if it was standard \
Q1 2014 => sort date Jan 2014 same sort date as entering Jan 2014 in date

## Quaker dates

questions
Do quaker dates just have a different canonical input/output but stored date is simple Gregorian?


## Date validation:

General
must be a valid Gregorian date (# days in month, leap year rules etc?) (do double dates jave to be valid Julian dates (leap years were different)\
Ambiguous date parts are interpreted by the sequence as specified in preferences.\
For a Two-Part Date, the first date must be earlier than second.\

Double JG Dates
Month-day must be between Jan 1 and Mar 24 inclusive. 
Year must be 1583 or greater


Canonical date format
Double JG Dates- the Gregorian date after the slash may only contain a year. 
And only the minimum number of digits required is included that show the main year +1.
so: 1 Feb 1755/6     1 Feb 1759/60     1 Feb 1798/9    1 Feb 1799/1800
There is no accounting for the 10 days "eliminated"


## Database RM Date format

Most RM database format dates are 24 bytes long, except '.' type dates which are one character and 'T' dates which can be any length.

```
schematic of an RM Date
origin 0 based indexing

0123456789A123456789B123
TS+YYYYMMDDJC+YYYYMMDDJC
```

Python style string slicing

|        | char  | range  | mea              |
| ------ | :---- | :----- | :--------------- |
| Part 0 | ===== | ====== | ======           |
|        | T     | 0:1    | Type             |
|        | S     | 1:2    | Structure        |
| Part 1 | ===== | ====== | =======          |
|        | +     | 2:3    | BC/AD -/+        |
|        | YYY   | 3:7    |                  |
|        | MM    | 7:9    |                  |
|        | DD    | 9:11   |                  |
|        | J     | 11:12  | Julian/Gregorian |
|        | C     | 12:13  | certainty        |
| Part 2 | ===== | ====== | =======          |
|        | +     | 13:14  | BC/AD -/+        |
|        | YYY   | 14:18  |                  |
|        | MM    | 18:20  |                  |
|        | DD    | 20:22  |                  |
|        | J     | 22:23  | Julian/Gregorian |
|        | C     | 23:24  | certainty        |

from 
<https://docs.google.com/spreadsheets/d/1yOb8klovt6UXStcD_S2g7wkkKh4S12AZJ9zSo1Dz_-g/edit#gid=2014317360>\
accessed: 2021-04-17\
and investigations by RJ Otter

### Full date type
The position 1 character describes the entire date.
other modifiers affect ony the first or second date.
Even JG double date flag (positions 12 & 23) affects its own part of the date

This section uses origin 1 indexing

| Position 1 | function      |
| :--------: | ------------- |
|     .      | Empty Date    |
|     D      | Standard Date |
|     Q      | Quaker Date   |
|     R      | Quarter Date  |
|     T      | Text Date     |
|            |               |

D, Q, and R dates may be One Part or Two Part Dates.

| Position 2 | meaning     | number of date parts |
| :--------: | :---------- | :------------------: |
|     B      | Bef         |        1 part        |
|     Y      | By          |        1 part        |
|     T      | To          |        1 part        |
|     U      | Until       |        1 part        |
|     .      | On          |        1 part        |
|     R      | Bet/And     |        2 part        |
|     S      | From/To     |        2 part        |
|     -      | – (em dash) |        2 part        |
|     O      | Or          |        2 part        |
|     F      | From        |        1 part        |
|     I      | Since       |        1 part        |
|     A      | After       |        1 part        |

### Part One date

| Position 3 | meaning   |
| :--------: | :-------- |
|     -      | BC or BCE |
|     +      | AD or CE  |

| Position 4-7 | meaning                                   |
| :----------: | ----------------------------------------- |
|     YYYY     | 4 digit Year or 0000 if no year specified |


|           | Position 8-9 | meaning                                    |
| --------- | :----------: | ------------------------------------------ |
| if D date |              |                                            |
|           |      MM      | 2 digit month, or 00 if no month specified |
| if R date |              |                                            |
|           |      01      | Q1                                         |
|           |      02      | Q2                                         |
|           |      03      | Q3                                         |
|           |      04      | Q4                                         |


|           | Position 10-11 | meaning                                       |
| --------- | -------------- | --------------------------------------------- |
| if D date |                |                                               |
|           | DD             | 2 digit day of month, 00 if day not specified |
| if R date |                | -                                             |
|           | 00             | always                                        |

| Position 12 | meaning                        |
| :---------: | ------------------------------ |
|      /      | Double date (Julian/Gregorian) |
|      .      | otherwise                      |

| Position 13 | meaning   |
| ----------- | --------- |
| ?           | Maybe     |
| 1           | Prhps     |
| 2           | Appar     |
| 3           | Lkly      |
| 4           | Poss      |
| 5           | Prob      |
| 6           | Cert      |
| A           | Abt       |
| C           | Ca        |
| E           | Est       |
| L           | Calc      |
| S           | Say       |
| .           | otherwise |


### Part Two Date

| Position 14 | meaning                   |
| :---------- | :------------------------ |
| -           | BC or BCE for second date |
| +           | AD or CE for second date  |


| Position 15-18 | meaning                                   |
| -------------- | ----------------------------------------- |
| YYYY           | 4 digit Year or 0000 if no year specified |


|           | Position 19-20 | meaning                                    |
| --------- | -------------- | ------------------------------------------ |
| if D date |                |                                            |
|           | MM             | 2 digit month, or 00 if no month specified |
| if R date |                |                                            |
|           | 01             | Q1                                         |
|           | 02             | Q2                                         |
|           | 03             | Q3                                         |
|           | 04             | Q4                                         |


|           | Position 21-22 | meaning                                       |
| --------- | -------------- | --------------------------------------------- |
| if D date |                |                                               |
|           | DD             | 2 digit day of month, 00 if day not specified |
| if R date |                |                                               |
|           | 00             | always                                        |

| Position 23 | meaning                         |
| :---------: | ------------------------------- |
|      /      | Double date  (Julian/Gregorian) |
|      .      | otherwise                       |


| Position 24 | meaning   |
| :---------: | --------- |
|      ?      | Maybe     |
|      1      | Prhps     |
|      2      | Appar     |
|      3      | Lkly      |
|      4      | Poss      |
|      5      | Prob      |
|      6      | Cert      |
|      A      | Abt       |
|      C      | Ca        |
|      E      | Est       |
|      L      | Calc      |
|      S      | Say       |
|      .      | otherwise |


### starting attempt at Bachus-Naur form Date spec (not even close yet)

https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form

```
RMdate ::= <RM_Type_EM_Date> | <RM_Type_T_Date> | <RM_Type_D_Date> | <RM_Type_R_Date> |<RM_Type_Q_Date> 

<RM_Type_EM_Date> ::= "."

<RM_Type_T_Date> ::= "T" <UTF-8 character>+

<RM_Type_D_Date> ::= 'D' <struct> <DatePart> " | 'D' <struct> <DatePart> <DatePart> 

<RM_Type_R_Date> ::= 'R' <struct> <DatePart> " | 'R' <struct> <DatePart> <DatePart> 

<RM_Type_Q_Date> ::= 'Q' <struct> <DatePart> " | 'Q' <struct> <DatePart> <DatePart> 


<DatePart> ::= <AD or BC FLAG> <YYYY> <MM> <DD> <confidence FLAG> <JG DD FLAG>

<YYYY> ::= <digit> digit> <digit> <digit>
<MM>   ::= <digit> <digit>
<DD>    ::= <digit> <digit>

etc.  TODO

```

confidence does not affect sort date

===========================================DIV50==

Tested in RM 9.1.3
created a date of-
24 March 1924/5
in database, it is stored as-
D.+19240324/.+00000000/.
with a sort date of-
6713296958983766028

the Julian date is stored in the DB !!!
