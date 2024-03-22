# ConfigTable

## Table DDL

```
CREATE TABLE ConfigTable (RecID INTEGER PRIMARY KEY, RecType INTEGER, Title TEXT, DataRec BLOB, UTCModDate FLOAT );

CREATE INDEX idxRecType ON ConfigTable (RecType);
```

## Columns List

| #   | Name       | Type    |
| --- | ---------- | ------- |
| 1   | RecID      | INTEGER |
| 2   | RecType    | INTEGER |
| 3   | Title      | TEXT    |
| 4   | DataRec    | BLOB    |
| 5   | UTCModDate | FLOAT   |

## Notes

| #   | Name       | Note |
| --- | ---------- | ---- |
| 1   | RecID      | _PK  |
| 2   | RecType    |      |
| 3   | Title      |      |
| 4   | DataRec    |      |
| 5   | UTCModDate | _STD |


```
RecType 1,3,4,5,6,7   no 2, mostly 5
Title TEXT
DataRec BLOB
UTCModDate FLOAT


RecType
1    main config                    Title=<blank>
3    custom report settings        Title=custom report user specified name
4    ??                            Title=MAIN & 1            
5    predefined report settings    Title=report name
6                                Title=WEB1
7    problem sttings                Title=PROB1 & POB2


    ===========================================DIV50==
    rowid    RecID    RecType    Title    DataRec    UTCModDate
    1    1    1        [BLOB_DATA]    45147.1934720255
    22    22    3    test    [BLOB_DATA]    
    28    28    3    immigrat    [BLOB_DATA]    
    52    52    3    FG proto    [BLOB_DATA]    44916.1396773032
    2    2    4    MAIN    [BLOB_DATA]    
    30    30    4    1    [BLOB_DATA]    45144.9324915394
    3    3    5    MEDIALIST    [BLOB_DATA]    
    4    4    5    KINSHIPLIST    [BLOB_DATA]    
    5    5    5    LDSLIST    [BLOB_DATA]    
    6    6    5    DUPLIST    [BLOB_DATA]    
    7    7    5    DESCLIST    [BLOB_DATA]    
    8    8    5    BOXCHART    [BLOB_DATA]    
    9    9    5    PEDCHART    [BLOB_DATA]    
    10    10    5    RELATECHART    [BLOB_DATA]    
    11    11    5    HOURGLASS    [BLOB_DATA]    
    12    12    5    INDIVSUMMARY    [BLOB_DATA]    
    13    13    5    SURNAMESTATS    [BLOB_DATA]    
    14    14    5    AHNENTAFEL    [BLOB_DATA]    
    15    15    5    FACTLIST    [BLOB_DATA]    
    16    16    5    INDIVLIST    [BLOB_DATA]    
    17    17    5    PLACELIST    [BLOB_DATA]    
    18    18    5    COUNTYCHECK    [BLOB_DATA]    
    19    19    5    STATISTICSLIST    [BLOB_DATA]    
    20    20    5    GROUPSHEET    [BLOB_DATA]    
    21    21    5    WEBTAGSLIST    [BLOB_DATA]    
    23    23    5    CUSTOMRPT    [BLOB_DATA]    
    24    24    5    BLANKREPORTS    [BLOB_DATA]    
    25    25    5    SOURCELIST    [BLOB_DATA]    
    26    26    5    ADDRLABELS    [BLOB_DATA]    
    29    29    5    rptTaskList    [BLOB_DATA]    44484.1527710185
    31    31    5    rptSurnameStatistics    [BLOB_DATA]    44484.1528169676
    32    32    5    rptSourceList    [BLOB_DATA]    45103.1695091088
    33    33    5    rptRelationshipChart    [BLOB_DATA]    45055.8186694097
    34    34    5    rptIndividualSummary    [BLOB_DATA]    44985.8273894444
    35    35    5    rptMultimediaList    [BLOB_DATA]    44565.9921435648
    36    36    5    rptAddressLabels    [BLOB_DATA]    44567.8425340162
    37    37    5    rptWhoWasThereList    [BLOB_DATA]    44628.7059010185
    38    38    5    rptFGS    [BLOB_DATA]    44997.9758127778
    39    39    5    rptPedigreeChart    [BLOB_DATA]    44640.0540819792
    42    42    5    rptCustomReport    [BLOB_DATA]    44916.1402024884
    43    43    5    rptFactList    [BLOB_DATA]    45087.1351957639
    44    44    5    rptDuplicateList    [BLOB_DATA]    44758.0270608681
    45    45    5    rptStatisticsList    [BLOB_DATA]    45089.9363217245
    46    46    5    rptIndividualList    [BLOB_DATA]    44997.9751678819
    47    47    5    rptWebTagsList    [BLOB_DATA]    44804.1184123727
    48    48    5    rptCountTrees    [BLOB_DATA]    44881.7024156713
    49    49    5    rptBoxChart    [BLOB_DATA]    45120.7562170486
    50    50    5    chartAncestorFan    [BLOB_DATA]    44884.2265676736
    51    51    5    rptPlaceList    [BLOB_DATA]    44907.7932423958
    53    53    5    chartAncestor    [BLOB_DATA]    45144.9324913542
    54    54    5    rptProblemList    [BLOB_DATA]    45029.9301888079
    55    55    5    chartDescendant    [BLOB_DATA]    45120.7568479861
    56    56    5    rptDescendantList    [BLOB_DATA]    45120.7564016088
    57    57    5    rptKinshipList    [BLOB_DATA]    45069.2003108912
    58    58    5    rptCountyCheck    [BLOB_DATA]    45089.9441190741
    40    40    6    WEB1    [BLOB_DATA]    45088.0334241204
    27    27    7    PROB1    [BLOB_DATA]    44986.7116882407
    41    41    7    PROB2    [BLOB_DATA]    45078.171658912
    
    ===========================================DIV50==



RecType=1    Title= <blank>

data=

    <Root>
    <Version>9000</Version>
    <STVersion>700</STVersion>
    <UniqueID>E8841905B21D49D79D2E878E0AC690B87147</UniqueID>
    <RootPerson>1</RootPerson>
    <LastPerson>18013</LastPerson>
    <LastView>1</LastView>
    <LastSideView>0</LastSideView>
    <StartPerson>1</StartPerson>
    <StartView>1</StartView>
    <StartSideView>0</StartSideView>
    <SurnameUp>false</SurnameUp>
    <LDSOptions>false</LDSOptions>
    <DateFormat>0</DateFormat>
    <RecNumber>1</RecNumber>
    <PreparerName>Richard J Otter</PreparerName>
    <PreparerAddr1>4232 Wilshire Blvd.</PreparerAddr1>
    <PreparerAddr2>Oakland, California 94602 USA</PreparerAddr2>
    <PreparerAddr3/>
    <PreparerPhone/>
    <PreparerCellPhone>+1 510-604-1498</PreparerCellPhone>
    <PreparerEmail>Richard.J.Otter@gmail.com</PreparerEmail>
    <PreparerFax/>
    <PreparerWeb/>
    <LiveProblems>true</LiveProblems>
    <WebHintStatus>1</WebHintStatus>
    <WebHints>false</WebHints>
    <MHHints>true</MHHints>
    <FSHints>true</FSHints>
    <FMPHints>false</FMPHints>
    <AncHints>true</AncHints>
    <AncRecordHints>true</AncRecordHints>
    <AncPersonHints>true</AncPersonHints>
    <AncPhotoHints>true</AncPhotoHints>
    <AncColorCode>true</AncColorCode>
    <MHRecordMatches>false</MHRecordMatches>
    <MHSmartMatches>true</MHSmartMatches>
    <MHConfidence>10</MHConfidence>
    <MHUserEmail>rjo7@columbia.edu</MHUserEmail>
    <FilterAncestryList>1</FilterAncestryList>
    <FSConfidence>50</FSConfidence>
    <FSFixes>0</FSFixes>
    <APFT1>1</APFT1>
    <APFT2>2</APFT2>
    <APFT3>4</APFT3>
    <APFT4>1065</APFT4>
    <APFT5>30</APFT5>
    <RECST0>10037</RECST0>
    <RECST1>10057</RECST1>
    <RECST2>10057</RECST2>
    <RECST3>10057</RECST3>
    <RECST4>10038</RECST4>
    <RECST5>10038</RECST5>
    <RECST6>10038</RECST6>
    <RECST7>10038</RECST7>
    <RECST8>10038</RECST8>
    <RECST9>10038</RECST9>
    <RECST10>10038</RECST10>
    <RECST11>10038</RECST11>
    <RECST12>10037</RECST12>
    <RECST13>10037</RECST13>
    <RECST14>10038</RECST14>
    <RECST15>10038</RECST15>
    <RECST16>10038</RECST16>
    <RECST17>10037</RECST17>
    <RECST18>10037</RECST18>
    <RECST19>10038</RECST19>
    <RECST20>10037</RECST20>
    <RECST21>10033</RECST21>
    <RECST22>10026</RECST22>
    <RECST23>10026</RECST23>
    <RECST24>10036</RECST24>
    <RECST25>157</RECST25>
    <RECST26>10008</RECST26>
    <RECST27>10033</RECST27>
    <RECST28>10033</RECST28>
    <RECST29>10008</RECST29>
    <RECST30>10008</RECST30>
    <RECST31>10008</RECST31>
    <RECST32>10033</RECST32>
    <RECST33>10033</RECST33>
    <RECST34>10033</RECST34>
    <RECST35>10033</RECST35>
    <RECST36>229</RECST36>
    <RECST37>229</RECST37>
    <RECST38>10008</RECST38>
    <RECST39>10008</RECST39>
    <RECST40>10008</RECST40>
    <RECST41>10008</RECST41>
    <RECST42>10008</RECST42>
    <RECST43>10008</RECST43>
    <RECST44>229</RECST44>
    <RECST45>229</RECST45>
    <RECST46>229</RECST46>
    <RECST47>229</RECST47>
    <RECST48>10008</RECST48>
    <RECST49>10008</RECST49>
    <RECRPT0>chartAncestor</RECRPT0>
    <RECRPT1>rptPedigreeChart</RECRPT1>
    <RECRPT2>rptFGS</RECRPT2>
    <RECRPT3>rptNarrativeReport</RECRPT3>
    <MemCitID>117450</MemCitID>
    <NicknameDelim>0</NicknameDelim>
    <IGIUserName/>
    <IGIPassword/>
    <PedGens>5</PedGens>
    <DescGens>7</DescGens>
    <DescBEPS>false</DescBEPS>
    <AltNamesInSideList>true</AltNamesInSideList>
    <AltNamesInExplorer>true</AltNamesInExplorer>
    <AltNamesInPersonView>false</AltNamesInPersonView>
    <ShowPictures>true</ShowPictures>
    <ShowAvatars>true</ShowAvatars>
    <DBColor>0</DBColor>
    <BirthInSideList>true</BirthInSideList>
    <RecNoInSideList>true</RecNoInSideList>
    <PersViewSortCol>4</PersViewSortCol>
    <PersViewCol0>
        <FieldType>2</FieldType>
        <EventType>0</EventType>
        <DataType>0</DataType>
        <ColWidth>40</ColWidth>
    </PersViewCol0>
    <PersViewCol1>
        <FieldType>10000</FieldType>
        <EventType>4</EventType>
        <DataType>1</DataType>
        <ColWidth>132</ColWidth>
    </PersViewCol1>
    <PersViewCol2>
        <FieldType>10000</FieldType>
        <EventType>1065</EventType>
        <DataType>3</DataType>
        <ColWidth>100</ColWidth>
    </PersViewCol2>
    <PersViewCol3>
        <FieldType>10000</FieldType>
        <EventType>18</EventType>
        <DataType>3</DataType>
        <ColWidth>100</ColWidth>
    </PersViewCol3>
    <PersViewCol4>
        <FieldType>10000</FieldType>
        <EventType>1</EventType>
        <DataType>2</DataType>
        <ColWidth>200</ColWidth>
    </PersViewCol4>
    <PersViewCol5>
        <FieldType>10000</FieldType>
        <EventType>1</EventType>
        <DataType>1</DataType>
        <ColWidth>80</ColWidth>
    </PersViewCol5>
    <PersViewCol6>
        <FieldType>10000</FieldType>
        <EventType>2</EventType>
        <DataType>2</DataType>
        <ColWidth>200</ColWidth>
    </PersViewCol6>
    <PersViewCol7>
        <FieldType>3</FieldType>
        <EventType>0</EventType>
        <DataType>0</DataType>
        <ColWidth>80</ColWidth>
    </PersViewCol7>
    <PersViewNameColWidth>205</PersViewNameColWidth>
    <CplViewFathWidth>187</CplViewFathWidth>
    <CplViewMothWidth>150</CplViewMothWidth>
    <CplViewDateWidth>80</CplViewDateWidth>
    <CplViewPlaceWidth>180</CplViewPlaceWidth>
    <FanViewRelationWidth>100</FanViewRelationWidth>
    <FanViewRole1Width>100</FanViewRole1Width>
    <FanViewP1Width>180</FanViewP1Width>
    <FanViewRole2Width>100</FanViewRole2Width>
    <FanViewP2Width>180</FanViewP2Width>
    <FanViewDateWidth>80</FanViewDateWidth>
    <FanViewPlaceWidth>180</FanViewPlaceWidth>
    <TreeShareFactType1Width>80</TreeShareFactType1Width>
    <TreeShareFactType2Width>80</TreeShareFactType2Width>
    <TreeShareDate1Width>80</TreeShareDate1Width>
    <TreeShareDate2Width>80</TreeShareDate2Width>
    <EditPersEventWidth>119</EditPersEventWidth>
    <EditPersonDateWidth>105</EditPersonDateWidth>
    <SideListBirthWidth>40</SideListBirthWidth>
    <SideListDeathWidth>40</SideListDeathWidth>
    <DescViewNameWidth>300</DescViewNameWidth>
    <DescViewArrowWidth>24</DescViewArrowWidth>
    <DescViewSexWidth>24</DescViewSexWidth>
    <DescViewBDateWidth>115</DescViewBDateWidth>
    <DescViewBPlaceWidth>300</DescViewBPlaceWidth>
    <DescViewDDateWidth>100</DescViewDDateWidth>
    <DescViewDPlaceWidth>300</DescViewDPlaceWidth>
    <EditPersonSourceWidth>250</EditPersonSourceWidth>
    <FSMatchPersonWidth>150</FSMatchPersonWidth>
    <FSMatchBDWidth>119</FSMatchBDWidth>
    <FSMatchBPWidth>150</FSMatchBPWidth>
    <FSMatchDDWidth>139</FSMatchDDWidth>
    <FSMatchDPWidth>150</FSMatchDPWidth>
    <FSMatchFatherWidth>150</FSMatchFatherWidth>
    <FSMatchMotherWidth>150</FSMatchMotherWidth>
    <FSMatchSpouseWidth>150</FSMatchSpouseWidth>
    <FSMatchFSIDWidth>80</FSMatchFSIDWidth>
    <CitationsCollapsed>false</CitationsCollapsed>
    <CitationsCollapsed_Tasks>false</CitationsCollapsed_Tasks>
    <WitnessesCollapsed>false</WitnessesCollapsed>
    <MediaCollapsed>false</MediaCollapsed>
    <MediaCollapsed_Places>false</MediaCollapsed_Places>
    <MediaCollapsed_Citations>false</MediaCollapsed_Citations>
    <MediaCollapsed_Sources>false</MediaCollapsed_Sources>
    <MediaCollapsed_Tasks>false</MediaCollapsed_Tasks>
    <TasksCollapsed>false</TasksCollapsed>
    <TasksCollapsed_Places>false</TasksCollapsed_Places>
    <AddressesCollapsed>false</AddressesCollapsed>
    <AddressesCollapsed_Sources>false</AddressesCollapsed_Sources>
    <AddressesCollapsed_Citations>false</AddressesCollapsed_Citations>
    <AddressesCollapsed_TasksAddr>false</AddressesCollapsed_TasksAddr>
    <AddressesCollapsed_TasksRepo>false</AddressesCollapsed_TasksRepo>
    <EnableFS>true</EnableFS>
    <FSCheckDupOrds>false</FSCheckDupOrds>
    <FSFilterType>All</FSFilterType>
    <FSFilterGroupID>0</FSFilterGroupID>
    <FSFilterGenerations>11</FSFilterGenerations>
    <FSFilterStartPerson>2361</FSFilterStartPerson>
    <TimelineReversePlaceNames>false</TimelineReversePlaceNames>
    <TimelinePlaceDetails>true</TimelinePlaceDetails>
    <TimelineSharedEvents>true</TimelineSharedEvents>
    <TimelineAssociations>true</TimelineAssociations>
    <TimelineRelatives>false</TimelineRelatives>
    <TimelineParents>false</TimelineParents>
    <TimelineSiblings>false</TimelineSiblings>
    <TimelineChildren>true</TimelineChildren>
    <TimelineSpouses>true</TimelineSpouses>
    <TimelineDblRows>true</TimelineDblRows>
    <TimelineSortBy>0</TimelineSortBy>
    <NameSpacing>false</NameSpacing>
    <NameInvalidCharacters>false</NameInvalidCharacters>
    <NamePunctuation>false</NamePunctuation>
    <NameAllUppercase>false</NameAllUppercase>
    <NameCapitalization>false</NameCapitalization>
    <NameAbbreviation>false</NameAbbreviation>
    <NameDescription>false</NameDescription>
    <NameMisplacedNickname>false</NameMisplacedNickname>
    <NameMisplacedPrefix>false</NameMisplacedPrefix>
    <NameMisplacedSuffix>false</NameMisplacedSuffix>
    <NameAlternateName>false</NameAlternateName>
    <NameWifeHasHusbandSurname>false</NameWifeHasHusbandSurname>
    <PlaceSpacing>false</PlaceSpacing>
    <PlaceInvalidCharacters>false</PlaceInvalidCharacters>
    <PlacePunctuation>false</PlacePunctuation>
    <PlaceAllUppercase>false</PlaceAllUppercase>
    <PlaceCapitalization>false</PlaceCapitalization>
    <PlaceAbbreviation>false</PlaceAbbreviation>
    <PlaceBlankPieces>false</PlaceBlankPieces>
    <PlaceMisplacedDetails>false</PlaceMisplacedDetails>
    <PlaceAddCountry>false</PlaceAddCountry>
    <PlaceRemoveCountry>false</PlaceRemoveCountry>
    <PlaceReplaceBrackets>false</PlaceReplaceBrackets>
    <ColorCodeSet>1</ColorCodeSet>
    <ColorCode0>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10>Couseins of CAO</FieldName10>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode0>
    <ColorCode1>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode1>
    <ColorCode2>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode2>
    <ColorCode3>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode3>
    <ColorCode4>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode4>
    <ColorCode5>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode5>
    <ColorCode6>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode6>
    <ColorCode7>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode7>
    <ColorCode8>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode8>
    <ColorCode9>
        <Name/>
        <FieldName0/>
        <FieldName1/>
        <FieldName2/>
        <FieldName3/>
        <FieldName4/>
        <FieldName5/>
        <FieldName6/>
        <FieldName7/>
        <FieldName8/>
        <FieldName9/>
        <FieldName10/>
        <FieldName11/>
        <FieldName12/>
        <FieldName13/>
        <FieldName14/>
        <FieldName15/>
        <FieldName16/>
        <FieldName17/>
        <FieldName18/>
        <FieldName19/>
        <FieldName20/>
        <FieldName21/>
        <FieldName22/>
        <FieldName23/>
        <FieldName24/>
        <FieldName25/>
        <FieldName26/>
        <FieldName27/>
    </ColorCode9>
</Root>


RecType=4    Title=MAIN
data=

...<?xml version="1.0" encoding="UTF-8"?>.<styles>
    <style>
        <code>AhnHead</code>
        <font>
            <name>Arial</name>
            <size>14</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>AhnText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>BoxChartText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>CalendarDate</code>
        <font>
            <name>Arial</name>
            <size>12</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>CalendarMonth</code>
        <font>
            <name>Arial</name>
            <size>18</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>CalendarSubtitle</code>
        <font>
            <name>Arial</name>
            <size>14</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>CalendarText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>Dummy</code>
        <font>
            <name>Verdana</name>
            <size>24</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>FamGroupEvents</code>
        <font>
            <name>Times New Roman</name>
            <size>9</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>FamGroupLabels</code>
        <font>
            <name>Arial</name>
            <size>7</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>FamGroupNames</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>Footnote</code>
        <font>
            <name>Times New Roman</name>
            <size>8</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>LabelText</code>
        <font>
            <name>Arial</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ListHeader</code>
        <font>
            <name>Arial</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ListText</code>
        <font>
            <name>Courier New</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>NarrHead</code>
        <font>
            <name>Arial</name>
            <size>14</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>NarrText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>OTDHeaders</code>
        <font>
            <name>Arial</name>
            <size>12</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>OTDText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>OTDTitle</code>
        <font>
            <name>Arial</name>
            <size>14</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PedChartEvents</code>
        <font>
            <name>Times New Roman</name>
            <size>8</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PedChartLabels</code>
        <font>
            <name>Arial</name>
            <size>7</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PedChartNames</code>
        <font>
            <name>Times New Roman</name>
            <size>9</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PhotoTreeName</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PublisherSubtitle</code>
        <font>
            <name>Arial</name>
            <size>14</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PublisherText</code>
        <font>
            <name>Arial</name>
            <size>12</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>PublisherTitle</code>
        <font>
            <name>Arial</name>
            <size>16</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>RelateChartNames</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>RelateChartText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ResearchComments</code>
        <font>
            <name>Times New Roman</name>
            <size>11</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ResearchDatePlace</code>
        <font>
            <name>Arial</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ResearchText</code>
        <font>
            <name>Times New Roman</name>
            <size>11</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ScrapbookCaption</code>
        <font>
            <name>Arial</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>ScrapbookDescription</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>SummaryText</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>WallchartData</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>False</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>WallchartName</code>
        <font>
            <name>Times New Roman</name>
            <size>10</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
    <style>
        <code>WallchartTitle</code>
        <font>
            <name>Arial</name>
            <size>18</size>
            <bold>True</bold>
            <underline>False</underline>
            <italic>False</italic>
            <strikeout>False</strikeout>
        </font>
    </style>
</styles>.



RecType=6    Title=WEB1
data=

<Root>
    <Extension>0</Extension>
    <Generations>2</Generations>
    <WebsiteType>0</WebsiteType>
    <HomePage>index</HomePage>
    <Project>Otter-saito</Project>
    <DateFormat>0</DateFormat>
    <Title>Otter-Saito Family Tree</Title>
    <Introduction/>
    <PhotoFile/>
    <Name/>
    <Street/>
    <CityStateZip/>
    <Country/>
    <Email/>
    <HomePagePhoto>0</HomePagePhoto>
    <NavBarPosition>0</NavBarPosition>
    <Header/>
    <Footer/>
    <SideBkColor>$FF008080</SideBkColor>
    <SideTextColor>$FFFFFFFF</SideTextColor>
    <MainBkColor>$FFFFFFFF</MainBkColor>
    <MainTextColor>$FF000000</MainTextColor>
    <LinkColor>$FF0000FF</LinkColor>
    <HoverColor>$FFFF0000</HoverColor>
    <IncGedcom>false</IncGedcom>
    <IncNotes>true</IncNotes>
    <IncPhotos>true</IncPhotos>
    <PrivacyNames>1</PrivacyNames>
    <PrivacyFacts>0</PrivacyFacts>
    <Privatize>true</Privatize>
    <IncPrivateFacts>false</IncPrivateFacts>
    <IncPrivateNotes>false</IncPrivateNotes>
    <StripBrackets>true</StripBrackets>
    <Link0/>
    <LinkText0/>
    <Link1/>
    <LinkText1/>
    <Link2/>
    <LinkText2/>
    <Link3/>
    <LinkText3/>
    <Link4/>
    <LinkText4/>
    <Link5/>
    <LinkText5/>
    <Link6/>
    <LinkText6/>
    <Link7/>
    <LinkText7/>
    <Link8/>
    <LinkText8/>
    <Link9/>
    <LinkText9/>
    <PrintSourceType>1</PrintSourceType>
    <IncCitationText>true</IncCitationText>
    <IncCitationComments>true</IncCitationComments>
    <ReuseDups>true</ReuseDups>
    <ProjectPath>C:\Users\rotter\Documents\Genealogy\GeneDB\HTML</ProjectPath>
</Root>


RecType=7    Title=PROB1
data=

<Root>
    <NoSex>true</NoSex>
    <EventOrder>true</EventOrder>
    <ParentsMarriage>true</ParentsMarriage>
    <AgeAtDeath>true</AgeAtDeath>
    <AgeAtMarriage>true</AgeAtMarriage>
    <BornBeforeParents>true</BornBeforeParents>
    <FathersDeath>true</FathersDeath>
    <MothersDeath>true</MothersDeath>
    <FathersAge>true</FathersAge>
    <MothersAge>true</MothersAge>
    <MaxAgeAtDeath>100</MaxAgeAtDeath>
    <MinAgeAtMarriage>14</MinAgeAtMarriage>
    <MaxAgeAtMarriage>70</MaxAgeAtMarriage>
    <MinFathersAge>14</MinFathersAge>
    <MaxFathersAge>70</MaxFathersAge>
    <MinMothersAge>14</MinMothersAge>
    <MaxMothersAge>50</MaxMothersAge>
    <DeathBurial>true</DeathBurial>
    <MaxDeathBurial>30</MaxDeathBurial>
    <MissingGiven>true</MissingGiven>
    <MissingSurname>true</MissingSurname>
</Root>


RecType=7    Title=PROB2

<Root>
    <NoSex>true</NoSex>
    <EventOrder>true</EventOrder>
    <ParentsMarriage>true</ParentsMarriage>
    <AgeAtDeath>true</AgeAtDeath>
    <AgeAtMarriage>true</AgeAtMarriage>
    <BornBeforeParents>true</BornBeforeParents>
    <FathersDeath>true</FathersDeath>
    <MothersDeath>true</MothersDeath>
    <FathersAge>true</FathersAge>
    <MothersAge>true</MothersAge>
    <MaxAgeAtDeath>104</MaxAgeAtDeath>
    <MinAgeAtMarriage>14</MinAgeAtMarriage>
    <MaxAgeAtMarriage>75</MaxAgeAtMarriage>
    <MinFathersAge>14</MinFathersAge>
    <MaxFathersAge>70</MaxFathersAge>
    <MinMothersAge>14</MinMothersAge>
    <MaxMothersAge>50</MaxMothersAge>
    <DeathBurial>true</DeathBurial>
    <MaxDeathBurial>652</MaxDeathBurial>
    <MissingGiven>true</MissingGiven>
    <MissingSurname>true</MissingSurname>
    <MissingGivenAlt>false</MissingGivenAlt>
    <MissingSurnameAlt>false</MissingSurnameAlt>
    </Root>

```

## Open Questions

