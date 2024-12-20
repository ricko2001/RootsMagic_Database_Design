
# SORT DATE

Still in the discovery phase

```
Standard/Recognized Dates							Date
	Complete and Partial Dates
			1 Jan 1900						D.+19000101..+00000000..
			1 Jan 1900 BC					D.-19000101..+00000000..
			Jan 1900						D.+19000100..+00000000..
			1900							D.+19000000..+00000000..
			1 Jan							D.+00000101..+00000000..
			Jan								D.+00000100..+00000000..
			1 ??? 1900						D.+19000001..+00000000..

		Double Dates
			1 Jan 1583/84					D.+15830101/.+00000000..

		Quaker Dates
			12da 5mo 1588					Q.+15880512..+00000000..

		Quarter Dates

	Date Modifiers and Date Qualifiers
		Single Date Directional Modifiers
			Bef 1 Jan 1900					DB+19000101..+00000000..
			By 1 Jan 1900					DY+19000101..+00000000..
			To 1 Jan 1900					DT+19000101..+00000000..
			Until 1 Jan 1900				DU+19000101..+00000000..
			From 1 Jan 1900					DF+19000101..+00000000..
			Since 1 Jan 1900				DI+19000101..+00000000..
			Aft 1 Jan 1900					DA+19000101..+00000000..

		Date-Range Directional Modifiers
			Bet 1 Jan 1900 and 5 Jan 1900		DR+19000101..+19000105..
			From 1 Jan 1900 to 5 Jan 1900		DS+19000101..+19000105..
			1 Jan 1900–5 Jan 1900				D-+19000101..+19000105..
			1 Jan 1900 or 5 Jan 1900			DO+19000101..+19000105..

		Date Qualifiers
			Abt 1 Jan 1900					D.+19000101.A+00000000..
			Est 1 Jan 1900					D.+19000101.E+00000000..
			Calc 1 Jan 1900					D.+19000101.L+00000000..
			Ca 1 Jan 1900					D.+19000101.C+00000000..
			Say 1 Jan 1900					D.+19000101.S+00000000..

		Qualitative Modifiers
			Cert 1 Jan 1900					D.+19000101.6+00000000..
			Prob 1 Jan 1900					D.+19000101.5+00000000..
			Poss 1 Jan 1900					D.+19000101.4+00000000..
			Lkly 1 Jan 1900					D.+19000101.3+00000000..
			Appar 1 Jan 1900				D.+19000101.2+00000000..
			Prhps 1 Jan 1900				D.+19000101.1+00000000..
			Maybe 1 Jan 1900				D.+19000101.?+00000000..

Empty Dates			empty					.

Text Dates			the first Wednesday		TFirst Wednesday
```
=========================================================================
=========================================================================

from-\
https://sqlitetoolsforrootsmagic.com/dates-sortdate-algorithm/\
accessed: 2021-04-17\
minor edits for clarity by RJO

```
Advanced Date Algorithms by R. Steven Turley
Here are the algorithms for decoding RM5 dates. These may be the same as RM4, but I haven’t tested them (ve3meo Dec 31, 2012 tested in RM6 and okay). They work for all normal dates, but I haven’t tested them on old dates or Quaker dates. I’m hoping those will just translate to their Julian equivalents and work okay. I’ll report those tests later. These dates are best understood in terms of bit fields on a long (64 bit) integer. Bit 0 is the least significant bit.

bits	value
0-9		flag indicating date modifiers (see table below)
10-15	day for the second date; 0 if no second date
16-19	month for the second date (1=Jan, 2=Feb, etc), 0 if no second date
20-33	year for the second date+10,000; 0x3fff if no second date
34-38	these were always zero in my tests, must be reserved for something else
39-44	day for the first date; 0 if no day is supplied
45-48	month for the first date; 0 if no month is supplied
49-64	year for the first date + 10,000

If the date is missing, the value 0xffffffff (2^65-1) is stored. This makes an event with no date, the last date in the list as far as the sort order is concerned.

The flag fields tell what kind of modifiers the date has.
Certainty modifiers are not included in SortDates since they don’t affect the sort order.
Here are the possible flag values:

flag value	meaning
0	before
3	by
6	to
9	until
12	normal date (no modifier)
15	between/and
18	from/to
21	dash (25 Oct 2011-28 Oct 2011)
24	or
27	from
30	since
31	after
Note that the value of these flags determines the sort order for dates as listed above.
Since dates that don’t have ranges store their year as 0x3fff, they will always come after dates with ranges that have a year less than this.

Algorithms
For almost all compilers, shift and bit-wise mask operators are faster than the division and remainder operations outlines above.
If your system supports it, I recommend the following algorithms to extract the dates and flag from sort dates.
In these formulas i>>j is the operation of shifting the number i j bits to the right.
The operation i<<j shifts the number i j bits to the left.
The operation i&j performs a bitwise and of the two numbers.
This is the notation used in C, C++, C#, and python.
I’m not sure about other languages. Let Ds be the sort date, as above, Y1 be the year of the first date,
M1 be the month of the first date, D1 be the day of the first date, Y2 be the year of the second date,
 M2 be the month of the second date, D2 by the day of the second date, and F by the flag.

Ds = ((Y1 + 10000)<<49) & (M1<<45) & (D1<<39) & (Y2<<20) & (M2<<16) & (D2<<10) & F ??
Ds = If no Date then
9223372036854775807
else
((Y1 + 10000)<<49) + (M1<<45) + (D1<<39) + (If Date2 then (Y2 + 10000)<<20 else
17178820608) + (M2<<16) + (D2<<10) + F

Y1 = (Ds>>49) – 10000
M1 = (Ds>>45) & 0xf
D1 = (Ds>>39) & 0x3f
Y2 = (Ds>>20) & 0x3fff – 10000
M2 = (Ds>>16) & 0xf
D2 = (Ds>>10) & 0x3f
F = Ds & 0x3ff

```
Downloads
SortDateDecodeDev.sql an example decoder using Steve’s algorithm
SortDateEncoderDev2.sql an encoding example using the modified version of Steve’s algorithm; streamlined, faster and more readable code than SortDateEncoderDev.sql.
SortDates (2013-01-01).rmgb
RM6 database with samples of most date formats for testing with above.

=========================================================================
=========================================================================
from same as above-

SortDateEncoderDev2.sql an encoding example using the modified version of Steve’s algorithm; streamlined, faster and more readable code than SortDateEncoderDev.sql.

```
-- SortDateEncoderDev2.sql

/*
2013-01-02 Tom Holden ve3meo

Streamlined version of SortDateEncoderDev.sql that is easier to read, maybe faster because of fewer operations.
Calculates SortDates from event dates, based on algorithms adapted from R. Steven Turley
and compares to the RM generated SortDates for errors.
See http://sqlitetoolsforrootsmagic.wikispaces.com/Dates%3E+SortDate+Algorithm#Advanced Date Decoder

Encode SortDate for regular non-Quaker dates
Ds = If no Date then 9223372036854775807
     else ((Y1 + 10000)<<49) + (M1<<45) + (D1<<39) +
     (If Date2 then (Y2 + 10000)<<20 else 17178820608) + (M2<<16) + (D2<<10) + F
where Ds = SortDate, Y = Year, M = Month, D = Day, F = modifier flag.

Also handles Quaker dates and slash dates, separately and in combination, at least in part.

*/

SELECT EventID, Date, Details, SortDate, CalcDate, SortDate-CalcDate AS Error
FROM
(
SELECT EventID, DATE, Details, SortDate,
  CASE Typ
		WHEN 'D'
			THEN --non-Quaker date
				CASE
					WHEN Y1 = 0
						AND M1 + D1 != 0
						THEN 16383 << 49 -- a date with no year
					ELSE ((Y1 + 10000 + (Slsh = '/')) << 49) -- Slash date increments year by 1
					END + --Y1
				(M1 << 45) + --M1
				(D1 << 39) + --D1
				CASE Y2
					WHEN 0
						THEN 17178820608 -- x'03 FF F0 00 00' or (2^34 - 2^20)  SELECT (1<<34)-(1<<20)
					ELSE ((Y2 + 10000) << 20) --Y2
					END + (M2 << 16) + --M2
				(D2 << 10) + --D2
				Flag -- Flag
		WHEN 'Q'
			THEN --Quaker date
				CASE
					WHEN M1 > 10
						AND Y1 < 1752 -- month 1=Mar, 12=Feb of next year, before 1752
						THEN (Y1 + 10001 + (Slsh = '/')) << 49
					ELSE (Y1 + 10000 + (Slsh = '/')) << 49
					END + -- Y1
				CASE
					WHEN Y1 < 1752
						THEN CASE
								WHEN M1 = 0
									THEN 0
								WHEN M1 < 11
									THEN (M1 + 2) << 45
								WHEN M1 > 10
									THEN (M1 - 10) << 45  -- SELECT Date,SUBSTR(Date,8,2)-10 FROM EventTable WHERE ABS(SUBSTR(Date,8,2))>10
								END
					ELSE (M1 << 45)
					END + --M1
				(D1 << 39) + --D1
				CASE Y2
					WHEN 0
						THEN 17178820608 -- x'03 FF F0 00 00' or (2^34 - 2^20)  SELECT (1<<34)-(1<<20)
					ELSE CASE
							WHEN M2 > 10
								AND Y2 < 1752
								THEN (Y2 + 10001) << 20
							ELSE (Y2 + 10000) << 20
							END
					END + --Y2
				CASE
					WHEN Y2 < 1752
						THEN --
							CASE
								WHEN M2 = 0
									THEN 0
								WHEN M2 < 11
									THEN (M2 + 2) << 16 -- SELECT 11%12
								WHEN M2 > 10
									THEN (M2 - 10) << 16 -- SELECT Date,SUBSTR(Date,8,2)-10 FROM EventTable WHERE ABS(SUBSTR(Date,8,2))>10
								END
					ELSE (M2 << 16)
					END + --M2
				(D2 << 10) + --D2
				Flag -- Flag
	--  WHEN '.' OR 'T' --blank or text date
		ELSE 9223372036854775807 --x'7F FF FF FF FF FF FF FF' (2^63-1)
		END AS CalcDate
FROM (
	SELECT
    EventID,
    DATE,
    SortDate,
    Details,
    SUBSTR(DATE, 1, 1) AS Typ,
    CAST(SUBSTR(DATE, 3, 5) AS INT) AS Y1,
    CAST(SUBSTR(DATE, 8, 2) AS INT) AS M1,
    CAST(SUBSTR(DATE, 10, 2) AS INT) AS D1,
    SUBSTR(DATE, 12, 1) AS Slsh,
    CAST(SUBSTR(DATE, 14, 5) AS INT) AS Y2,
    CAST(SUBSTR(DATE, 19, 2) AS INT) AS M2,
    CAST(SUBSTR(DATE, 21, 2) AS INT) AS D2,

				CASE SUBSTR(DATE, 2, 1) -- Flag
					WHEN 'B'
						THEN 0 --Before
					WHEN 'Y'
						THEN 3 --By
					WHEN 'T'
						THEN 6 --To
					WHEN 'U'
						THEN 9 --Until
					WHEN '.'
						THEN 12 --On
					WHEN 'R'
						THEN 15 --Between x and y
					WHEN 'S'
						THEN 18 --From x to y
					WHEN '-'
						THEN 21 --Hyphen x-y
					WHEN 'O'
						THEN 24 --x Or y
					WHEN 'F'
						THEN 1047579 --From    (27 + x'FFC00')
					WHEN 'I'
						THEN 1047582 --Since   (30 + x'FFC00')
					WHEN 'A'
						THEN 1047583 --After   (31 + x'FFC00')
					ELSE 0
					END  AS Flag
	FROM EventTable
	)
)
;
```

=========================================================================
=========================================================================

-- SortDateDecodeDev.sql
/*
2012-11-03 Tom Holden ve3meo, based on the following algorithm by R. Steven Turley
see http://sqlitetoolsforrootsmagic.wikispaces.com/Dates%3E+SortDate+Algorithm#Advanced Date Decoder

Encode SortDate
Ds = ((Y1 + 10000)<<49) & (M1<<45) & (D1<<39) & (Y2<<20) & (M2<<16) & (D2<<10) & F
where Ds = SortDate, Y = Year, M = Month, D = Day, F = modifier flag.

Decode SortDate
Y1 = (Ds>>49) - 10000
M1 = (Ds>>45) & 0xf
D1 = (Ds>>39) & 0x3f
Y2 = (Ds>>20) & 0x3fff - 10000
M2 = (Ds>>16) & 0xf
D2 = (Ds>>10) & 0x3f
F = Ds & 0x3ff
*/

/* SortDateDecode */


/*
SELECT Date, 
       (Ds >> 49) - 10000 AS Y1, 
       (Ds >> 45) & 15  AS M1,  
       (Ds >> 39) & 63  AS D1, 
       ((Ds >> 20) & 16383) - 10000 AS Y2,
       (Ds >> 16) & 15 AS M2,
       (Ds >> 10) & 63 AS D2,
        Ds & 1023 AS F
FROM (SELECT Date, SortDate AS Ds FROM EventTable) 
;
*/

SELECT Date, 
       (Ds >> 49) - 10000 AS Y1, 
       (Ds >> 45) & 15  AS M1,  
       (Ds >> 39) & 63  AS D1, 
       ((Ds >> 20) & 16383) - 10000 AS Y2,
       (Ds >> 16) & 15 AS M2,
       (Ds >> 10) & 63 AS D2,
        Ds & 1023 AS F,
CASE (Ds & 1023) IN (0,3,6,9,12,15,18,21,24,27,30,31)
 WHEN 1 THEN  
  CASE Ds & 1023
   WHEN 0 THEN 'before '
   WHEN 3 THEN 'by '
   WHEN 6 THEN 'to '
   WHEN 9 THEN 'until '
   WHEN 15 THEN 'between '
   WHEN 18 THEN 'from '
   WHEN 27 THEN 'from '
   WHEN 30 THEN 'since '
   WHEN 31 THEN 'after '
   ELSE ''
  END
  ||
  CAST((Ds >> 49) - 10000 AS TEXT) || '-'
  ||
  CAST((Ds >> 45) & 15 AS TEXT) || '-'
  ||
  CAST((Ds >> 39) & 63 AS TEXT)
  ||
  CASE Ds & 1023 IN (15,18,21,24)
   WHEN 1
   THEN
    CASE Ds & 1023
     WHEN 15 THEN ' and '
     WHEN 18 THEN ' to '
     WHEN 21 THEN ' - '
     WHEN 24 THEN ' or '
     ELSE ''
    END
    ||
    CAST(((Ds >> 20) & 16383) - 10000 AS TEXT) || '-'
    ||
    CAST((Ds >> 16) & 15 AS TEXT) || '-'
    ||
    CAST((Ds >> 10) & 63 AS TEXT)
   ELSE ''
  END
 ELSE ''
END
AS SortDateDecoded, Ds, Date

 FROM (SELECT Date, SortDate AS Ds FROM EventTable) 

;
=========================================================================
=========================================================================

copy data from db using sql

sample database (original)
select Details, Date, SortDate from EventTable order by SortDate


Details								Date	SortDate
1 Jan 1583/84 double date							D.+15830101/.+00000000..	6521248011739201548
12da 2mo 1588										Q.+15880212..+00000000..	6523611411983106060
Bet 12da 11mo 1588 and 1da 12mo 1588 Quaker			QR+15881112..+15881201..	6524068803793519631
12da 11mo 1588 Quaker Date							Q.+15881112..+00000000..	6524068808820260876
2da 1mo 1588/9 Quaker double-date					Q.+15880102/.+00000000..	6524133680006299660
2da 11mo 1588/9										Q.+15881102/.+00000000..	6524626261215543308
31da 10mo 1751 Quaker date pre-1752					Q.+17511031..+00000000..	6615664174727954444
1da 1mo 1752 Quaker date post-1751					Q.+17520101..+00000000..	6615823603913981964
1921												D.+19210000..+00000000..	6710926411914280972
13 ??? 1921											D.+19210013..+00000000..	6710933558739861516
Jan 1921											D.+19210100..+00000000..	6710961596286369804
Bet 13 Jan 1921 and 25 Jan 1922						DR+19210113..+19220125..	6710968738434343951
From 13 Jan 1921 to 25 Jan 1922						DS+19210113..+19220125..	6710968738434343954
13 Jan 1921-25 Jan 1922								D-+19210113..+19220125..	6710968738434343957
13 Jan 1921 or 25 Jan 1922							DO+19210113..+19220125..	6710968738434343960
Bef 13 Jan 1921										DB+19210113..+00000000..	6710968743111950336
By 13 Jan 1921										DY+19210113..+00000000..	6710968743111950339
To 13 Jan 1921										DT+19210113..+00000000..	6710968743111950342
Until 13 Jan 1921									DU+19210113..+00000000..	6710968743111950345
13 Jan 1921											D.+19210113..+00000000..	6710968743111950348
Abt 13 Jan 1921										D.+19210113.A+00000000..	6710968743111950348
Est 13 Jan 1921										D.+19210113.E+00000000..	6710968743111950348
Calc 13 Jan 1921									D.+19210113.L+00000000..	6710968743111950348
Ca 13 Jan 1921										D.+19210113.C+00000000..	6710968743111950348
Say 13 Jan 1921										D.+19210113.S+00000000..	6710968743111950348
From 13 Jan 1921									DF+19210113..+00000000..	6710968743112997915
Since 13 Jan 1921									DI+19210113..+00000000..	6710968743112997918
Aft 13 Jan 1921										DA+19210113..+00000000..	6710968743112997919
Jan													D.+00000100..+00000000..	9222844288452263948
Jan-Mar    no-year range							D-+00000100..+00000300..	9222844288452460565
13 Jan												D.+00000113..+00000000..	9222851435277844492
blank date											.							9223372036854775807
Text date											TText date					9223372036854775807

=========================================================================
=========================================================================


Added MISC_2 facts with "-N"at end of sort date.
"-N" not valid for all date types
date	sort date display		"-N" valid ?

Bet and		same				no
From to		same				no
-			same				no
or			same				no
bef			same				no
by			same				no
to			same				no
until		same				no
est 		no prefix			yes
std date	no prefix			yes
abt			no prefix			yes
say			no prefix			yes
calc		no prefix			yes
ca			no prefix			yes
from		same				no
since		same				no
aft			same				no
MMM			same				no
MMM-MMM		same				no
DD MMM		same				no
double date			second year only (gregorian)
all quake dates		converted to gregorian equiv. single dates, range, etc (not checked)
blank date	blank				no
text date	blank				no

seems like stuct flag- pos 2 "-" is always used with double date and the
date -n  format usually used for sort dates, also uses the same struct flag.
the N is considered a year number in the second date.

the sort date is calculated the same for all 2 date formats, even the -N style.


same means sort date displayed same as date.

Add some more

select EventType, Details, Date, SortDate from EventTable order by SortDate

EventType	Details	Date	SortDate
1000	date is blank, sort date=10					.							5635129050926153740
1000	date is blank, sort date=11					.							5635692000879575052

999		1 Jan 1583/84 double date					D.+15830101/.+00000000..	6521248011739201548
999		12da 2mo 1588								Q.+15880212..+00000000..	6523611411983106060
999		Bet 12da 11mo 1588 and 1da 12mo 1588 Quaker	QR+15881112..+15881201..	6524068803793519631
999		12da 11mo 1588 Quaker Date					Q.+15881112..+00000000..	6524068808820260876
999		2da 1mo 1588/9 Quaker double-date			Q.+15880102/.+00000000..	6524133680006299660
999		2da 11mo 1588/9								Q.+15881102/.+00000000..	6524626261215543308
999		31da 10mo 1751 Quaker date pre-1752			Q.+17511031..+00000000..	6615664174727954444
999		1da 1mo 1752 Quaker date post-1751			Q.+17520101..+00000000..	6615823603913981964

1000	1921 ( sort date=1921-1 )					D.+19210000..+00000000..	6710926405222268949
1000	1921 ( sort date=1921-2 )					D.+19210000..+00000000..	6710926405223317525
1000	1921 ( sort date=1921-10 )					D.+19210000..+00000000..	6710926405231706133
999		1921										D.+19210000..+00000000..	6710926411914280972
999		13 ??? 1921									D.+19210013..+00000000..	6710933558739861516
999		Jan 1921									D.+19210100..+00000000..	6710961596286369804
1000	13 Jan 1921  ( sort date 13 Jan 1921-1 )	D.+19210113..+00000000..	6710968736419938325
1000	13 Jan 1921  ( sort date 13 Jan 1921-2 )	D.+19210113..+00000000..	6710968736420986901
1000	13 Jan 1921  ( sort date 13 Jan 1921-10 )	D.+19210113..+00000000..	6710968736429375509
999		Bet 13 Jan 1921 and 25 Jan 1922				DR+19210113..+19220125..	6710968738434343951
999		From 13 Jan 1921 to 25 Jan 1922				DS+19210113..+19220125..	6710968738434343954
999		13 Jan 1921-25 Jan 1922						D-+19210113..+19220125..	6710968738434343957
999		13 Jan 1921 or 25 Jan 1922					DO+19210113..+19220125..	6710968738434343960
1000	13 Jan 1921 or 25 Jan 1925					DO+19210113..+19250125..	6710968738437489688
999		Bef 13 Jan 1921								DB+19210113..+00000000..	6710968743111950336
999		By 13 Jan 1921								DY+19210113..+00000000..	6710968743111950339
999		To 13 Jan 1921								DT+19210113..+00000000..	6710968743111950342
999		Until 13 Jan 1921							DU+19210113..+00000000..	6710968743111950345
999		13 Jan 1921									D.+19210113..+00000000..	6710968743111950348
999		Abt 13 Jan 1921								D.+19210113.A+00000000..	6710968743111950348
999		Est 13 Jan 1921								D.+19210113.E+00000000..	6710968743111950348
999		Calc 13 Jan 1921							D.+19210113.L+00000000..	6710968743111950348
999		Ca 13 Jan 1921								D.+19210113.C+00000000..	6710968743111950348
999		Say 13 Jan 1921								D.+19210113.S+00000000..	6710968743111950348
999		From 13 Jan 1921							DF+19210113..+00000000..	6710968743112997915
999		Since 13 Jan 1921							DI+19210113..+00000000..	6710968743112997918
999		Aft 13 Jan 1921								DA+19210113..+00000000..	6710968743112997919
999		Jan											D.+00000100..+00000000..	9222844288452263948
999		Jan-Mar    no-year range					D-+00000100..+00000300..	9222844288452460565
999		13 Jan										D.+00000113..+00000000..	9222851435277844492
999		blank date									.							9223372036854775807
999		Text date									TText date					9223372036854775807


The SQL code above works for all of the original MISC entries i n the sortdate database.
see output below. Rightmost column is error
It takes the date and calculates the sort date.
It is not designed to use the sort date modified with a "-N"

EventID	DATE	Details	SortDate	CalcDate	Error
41	.							date is blank, sort date=10						5635129050926153740	9223372036854775807		-3588242985928622067
42	.							date is blank, sort date=11						5635692000879575052	9223372036854775807		-3587680035975200755
19	D.+15830101/.+00000000..	1 Jan 1583/84 double date						6521248011739201548	6521248011739201548		0
22	Q.+15880212..+00000000..	12da 2mo 1588									6523611411983106060	6523611411983106060		0
21	QR+15881112..+15881201..	Bet 12da 11mo 1588 and 1da 12mo 1588 Quaker		6524068803793519631	6524068803793519631		0
20	Q.+15881112..+00000000..	12da 11mo 1588 Quaker Date						6524068808820260876	6524068808820260876		0
31	Q.+15880102/.+00000000..	2da 1mo 1588/9 Quaker double-date				6524133680006299660	6524133680006299660		0
33	Q.+15881102/.+00000000..	2da 11mo 1588/9									6524626261215543308	6524626261215543308		0
25	Q.+17511031..+00000000..	31da 10mo 1751 Quaker date pre-1752				6615664174727954444	6615664174727954444		0
23	Q.+17520101..+00000000..	1da 1mo 1752 Quaker date post-1751				6615823603913981964	6615823603913981964		0
35	D.+19210000..+00000000..	1921 ( sort date=1921-1 )						6710926405222268949	6710926411914280972		-6692012023
36	D.+19210000..+00000000..	1921 ( sort date=1921-2 )						6710926405223317525	6710926411914280972		-6690963447
37	D.+19210000..+00000000..	1921 ( sort date=1921-10 )						6710926405231706133	6710926411914280972		-6682574839
28	D.+19210000..+00000000..	1921											6710926411914280972	6710926411914280972		0
26	D.+19210013..+00000000..	13 ??? 1921										6710933558739861516	6710933558739861516		0
27	D.+19210100..+00000000..	Jan 1921										6710961596286369804	6710961596286369804		0
38	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-1 )		6710968736419938325	6710968743111950348		-6692012023
39	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-2 )		6710968736420986901	6710968743111950348		-6690963447
40	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-10 )		6710968736429375509	6710968743111950348		-6682574839
14	DR+19210113..+19220125..	Bet 13 Jan 1921 and 25 Jan 1922					6710968738434343951	6710968738434343951		0
15	DS+19210113..+19220125..	From 13 Jan 1921 to 25 Jan 1922					6710968738434343954	6710968738434343954		0
16	D-+19210113..+19220125..	13 Jan 1921-25 Jan 1922							6710968738434343957	6710968738434343957		0
17	DO+19210113..+19220125..	13 Jan 1921 or 25 Jan 1922						6710968738434343960	6710968738434343960		0
43	DO+19210113..+19250125..	13 Jan 1921 or 25 Jan 1925						6710968738437489688	6710968738437489688		0
2	DB+19210113..+00000000..	Bef 13 Jan 1921									6710968743111950336	6710968743111950336		0
3	DY+19210113..+00000000..	By 13 Jan 1921									6710968743111950339	6710968743111950339		0
4	DT+19210113..+00000000..	To 13 Jan 1921									6710968743111950342	6710968743111950342		0
5	DU+19210113..+00000000..	Until 13 Jan 1921								6710968743111950345	6710968743111950345		0
1	D.+19210113..+00000000..	13 Jan 1921										6710968743111950348	6710968743111950348		0
9	D.+19210113.A+00000000..	Abt 13 Jan 1921									6710968743111950348	6710968743111950348		0
10	D.+19210113.E+00000000..	Est 13 Jan 1921									6710968743111950348	6710968743111950348		0
11	D.+19210113.L+00000000..	Calc 13 Jan 1921								6710968743111950348	6710968743111950348		0
12	D.+19210113.C+00000000..	Ca 13 Jan 1921									6710968743111950348	6710968743111950348		0
13	D.+19210113.S+00000000..	Say 13 Jan 1921									6710968743111950348	6710968743111950348		0
6	DF+19210113..+00000000..	From 13 Jan 1921								6710968743112997915	6710968743112997915		0
7	DI+19210113..+00000000..	Since 13 Jan 1921								6710968743112997918	6710968743112997918		0
8	DA+19210113..+00000000..	Aft 13 Jan 1921									6710968743112997919	6710968743112997919		0
30	D.+00000100..+00000000..	Jan												9222844288452263948	9222844288452263948		0
32	D-+00000100..+00000300..	Jan-Mar    no-year range						9222844288452460565	9222844288452460565		0
29	D.+00000113..+00000000..	13 Jan											9222851435277844492	9222851435277844492		0
18	.							blank date										9223372036854775807	9223372036854775807		0
34								TText date	Text date							9223372036854775807	9223372036854775807		0



Question- how does "-N" affect sort date?
How big can N be without overflow?

displayed SD		actual SD
13 Jan 1921-1		6,710,968,736,419,938,325
13 Jan 1921-2		6,710,968,736,420,986,901
13 Jan 1921-10		6,710,968,736,429,375,509
13 Jan 1921			6,710,968,743,111,950,348

displayed SD		actual SD								-K
13 Jan 1921-1		6,710,968,7  36,419,938,325
13 Jan 1921-2		6,710,968,7  36,420,986,901
13 Jan 1921-10		6,710,968,7  36,429,375,509
13 Jan 1921			6,710,968,7  43,111,950,348		36,420,986,901


plain - plain_1   = 43,111,950,348 - 36,419,938,325 =  6,692,012,023


K = 6,692,012,023
2^20 = 1,048,576

plain_N  = plain -K + (N-1) * 2^20

plain_1  = plain -K  + 0* 2^20 =	36,419,938,325
plain_2  = plain -K +  1* 2^20  =	36,420,986,901
plain_10 = plain -K +  9* 2^20   =	36,429,375,509


Or, change offset so multiple of 2^20 is N  (orign =1)

K - 6,690,963,447
2^20 = 1,048,576

plain-N  = plain -K + N * 2^20     N=1, ~1920

plain-1  = plain -K  + 1* 2^20  =	36,419,938,325
plain-2  = plain -K +  2* 2^20  =	36,420,986,901
plain-10 = plain -K + 10* 2^20  =	36,429,375,509



what is K  6,690,963,447

2^32 = 4,294,967,296
2^33  will be too big

sort order
date-1					6,710,968,736,419,938,325
date-2
between x and Y date 	6,710,968,738,434,343,951
date					6,710,968,743,111,950,348

how much space between date-1 and between x and Y date?
6,710,968,738,434,343,951 - 6,710,968,736,419,938,325  = 2,014,405,626    =  1,921.0869083
looks like -N can get to about 1920 before it overflows into the other spaces.


Now try the other known case
displayed SD					actual SD
1921 ( sort date=1921-1 )		6710926405222268949
1921 ( sort date=1921-2 )		6710926405223317525
1921 ( sort date=1921-10 )		6710926405231706133
1921							6710926411914280972

displayed SD					actual SD
1921 ( sort date=1921-1 )		6,710,926, 405,222,268,949
1921 ( sort date=1921-2 )		6,710,926, 405,223,317,525
1921 ( sort date=1921-10 )		6,710,926, 405,231,706,133
1921							6,710,926, 411,914,280,972

plain_N  = plain -K + N * 2^20

plain_N -plain -2^20 = -K
N=1
K= plain - plain_1 + 2*20

plain - plainN1 + 2^20 =  6,690,963,447  same K as above



=========================================================================
=========================================================================
63 events

calculates internal sort date from the internal date
will always fail comparison when sort date is overridden by modiefication in UI


EventID	DATE	Details	SortDate	CalcDate	Error
57	D.-10000000..+00000000..	1000 BC   [BC dates, for my Neanderthal cousins]		5066549597970628620	5066549597970628620	0
55	D.+00050000..+00000000..	5  [sort date=5]										5632314301159047180	5632314301159047180	0
41	.	date is blank [sort date=10]													5635129050926153740	9223372036854775807	-3588242985928622067
42	.	date is blank [sort date=11]													5635692000879575052	9223372036854775807	-3587680035975200755
45	D.+00300000..+00000000..	30   [date/number only]									5646388049994579980	5646388049994579980	0
46	D.+03000000..+00000000..	300    [number, too big for day of month[				5798384537418334220	5798384537418334220	0
19	D.+15830101/.+00000000..	1 Jan 1583/84 [double date]								6521248011739201548	6521248011739201548	0
22	Q.+15880212..+00000000..	12da 2mo 1588   [quaker, neeeds further investigation]	6523611411983106060	6523611411983106060	0
21	QR+15881112..+15881201..	Bet 12da 11mo 1588 and 1da 12mo 1588 [quaker, not investigated]		6524068803793519631	6524068803793519631	0
20	Q.+15881112..+00000000..	12da 11mo 1588  [quaker date]							6524068808820260876	6524068808820260876	0
31	Q.+15880102/.+00000000..	2da 1mo 1588/9   [quaker double-date]					6524133680006299660	6524133680006299660	0
33	Q.+15881102/.+00000000..	2da 11mo 1588/9  [quaker double-date]					6524626261215543308	6524626261215543308	0
25	Q.+17511031..+00000000..	31da 10mo 1751 [quaker date pre-1752]					6615664174727954444	6615664174727954444	0
23	Q.+17520101..+00000000..	1da 1mo 1752  [quaker date post-1751]					6615823603913981964	6615823603913981964	0
35	D-+19210000..+00010000..	1921-1   [ sort date=1921-1 ]							6710926405222268949	6710926405222268949	0
36	D-+19210000..+00020000..	1921-2  [ sort date=1921-2 ]							6710926405223317525	6710926405223317525	0
47	D-+19210000..+00030000..	1921-3   [ sort date=1921-3 ]							6710926405224366101	6710926405224366101	0
37	D-+19210000..+00100000..	1921-10  [sort date=1921-10 ]							6710926405231706133	6710926405231706133	0
28	D.+19210000..+00000000..	1921   [std date- year only]							6710926411914280972	6710926411914280972	0
48	D-+19210000..+99990000..	1921–9999  [sort date=1921–9999]						6710926415705931797	6710926415705931797	0
26	D.+19210013..+00000000..	13 ??? 1921												6710933558739861516	6710933558739861516	0
27	D.+19210100..+00000000..	Jan 1921												6710961596286369804	6710961596286369804	0
38	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-1 )				6710968736419938325	6710968743111950348	-6692012023
50	D-+19210113.E+00010000..	Est 13 Jan 1921-1    [prefix ignored in sort date]		6710968736419938325	6710968736419938325	0
51	D-+19210113.A+00010000..	Abt 13 Jan 1921-1    [prefix ignored in sort date]		6710968736419938325	6710968736419938325	0
52	D-+19210113.S+00010000..	Say 13 Jan 1921-1  [prefix ignored in sort date]		6710968736419938325	6710968736419938325	0
53	D-+19210113.L+00010000..	Calc 13 Jan 1921–1 [prefix ignored in sort date]		6710968736419938325	6710968736419938325	0
54	D-+19210113.C+00010000..	Ca 13 Jan 1921–1 [prefix ignored in sort date]			6710968736419938325	6710968736419938325	0
62	D-+19210113..+00010000..	13 Jan 1921–10000  [N=10000 changed to 1 in both dates]	6710968736419938325	6710968736419938325	0
39	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-2 )				6710968736420986901	6710968743111950348	-6690963447
40	D.+19210113..+00000000..	13 Jan 1921  ( sort date 13 Jan 1921-10 )				6710968736429375509	6710968743111950348	-6682574839
58	D-+19210113..+10000000..	13 Jan 1921–1000										6710968737467465749	6710968737467465749	0
14	DR+19210113..+19220125..	Bet 13 Jan 1921 and 25 Jan 1922							6710968738434343951	6710968738434343951	0
15	DS+19210113..+19220125..	From 13 Jan 1921 to 25 Jan 1922							6710968738434343954	6710968738434343954	0
16	D-+19210113..+19220125..	13 Jan 1921-25 Jan 1922									6710968738434343957	6710968738434343957	0
17	DO+19210113..+19220125..	13 Jan 1921 or 25 Jan 1922								6710968738434343960	6710968738434343960	0
43	DO+19210113..+19250125..	13 Jan 1921 or 25 Jan 1925								6710968738437489688	6710968738437489688	0
61	D-+19210113..+49990000..	13 Jan 1921–4999   [largest N]							6710968741660721173	6710968741660721173	0
63	D-+19210113..+50000000..	13 Jan 1921–5000   [N too big, ignored in sort date]	6710968741661769749	6710968741661769749	0
2	DB+19210113..+00000000..	Bef 13 Jan 1921											6710968743111950336	6710968743111950336	0
3	DY+19210113..+00000000..	By 13 Jan 1921											6710968743111950339	6710968743111950339	0
4	DT+19210113..+00000000..	To 13 Jan 1921											6710968743111950342	6710968743111950342	0
5	DU+19210113..+00000000..	Until 13 Jan 1921										6710968743111950345	6710968743111950345	0
49	DU+19210113..+00000000..	Until 13 Jan 1921-1										6710968743111950345	6710968743111950345	0
1	D.+19210113..+00000000..	13 Jan 1921												6710968743111950348	6710968743111950348	0
9	D.+19210113.A+00000000..	Abt 13 Jan 1921   [prefix ignored in sort date]			6710968743111950348	6710968743111950348	0
10	D.+19210113.E+00000000..	Est 13 Jan 1921   [prefix ignored in sort date]			6710968743111950348	6710968743111950348	0
11	D.+19210113.L+00000000..	Calc 13 Jan 1921   [prefix ignored in sort date]		6710968743111950348	6710968743111950348	0
12	D.+19210113.C+00000000..	Ca 13 Jan 1921     [prefix ignored in sort date]		6710968743111950348	6710968743111950348	0
13	D.+19210113.S+00000000..	Say 13 Jan 1921   [prefix ignored in sort date]			6710968743111950348	6710968743111950348	0
6	DF+19210113..+00000000..	From 13 Jan 1921										6710968743112997915	6710968743112997915	0
7	DI+19210113..+00000000..	Since 13 Jan 1921										6710968743112997918	6710968743112997918	0
8	DA+19210113..+00000000..	Aft 13 Jan 1921											6710968743112997919	6710968743112997919	0
59	D-+19210113..+90000000..	13 Jan 1921–9000										6710968745856073749	6710968745856073749	0
56	D-+19210113..+99990000..	13 Jan 1921-9999										6710968746903601173	6710968746903601173	0
60	D.+19210114..+00000000..	14 Jan 1921												6710969292867764236	6710969292867764236	0
30	D.+00000100..+00000000..	Jan   [std date - month only]							9222844288452263948	9222844288452263948	0
32	D-+00000100..+00000300..	Jan-Mar   [month range, no year]						9222844288452460565	9222844288452460565	0
29	D.+00000113..+00000000..	13 Jan   [no year]										9222851435277844492	9222851435277844492	0
44	D.+00000300..+00000000..	Mar  [month only]										9222914657196441612	9222914657196441612	0
18	.	blank date																		9223372036854775807	9223372036854775807	0
34	TText date	Text date																9223372036854775807	9223372036854775807	0



# Large sort date problems
< 5000  acts normally
5000 -6383- is accepted but is deleted when fact is saved
> 6383  the fact is displayed at the top of the edit screen and 
displayed as a BC date

Repeated entry of these large numbers cause app failure by not allowing sort date entry- no save check ark etc.

