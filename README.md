# PowerQuery: Auto Generating Date Parameters for PowerBI and Excel
DatesM

--Copy from line 6 to line 23--

 let
    Source = List.Dates(#date(2014,1,1),Duration.Days(#date(2016,12,31)-#date(2014,1,1
)),#duration(1,0,0,0)),
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Renamed Columns" = Table.RenameColumns(#"Converted to Table",{{"Column1", "DateKey"}}),
    #"Added Custom" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([DateKey])),
    #"Added Custom1" = Table.AddColumn(#"Added Custom", "Month Num", each Date.Month([DateKey])),
    #"Added Custom2" = Table.AddColumn(#"Added Custom1", "Month Num2", each Date.ToText([DateKey],"MM")),
    #"Added Custom3" = Table.AddColumn(#"Added Custom2", "Day", each 
Date.Day([DateKey])),
    #"Added Custom4" = Table.AddColumn(#"Added Custom3", "Day Name", each Date.ToText([DateKey],"ddd")),
    #"Added Custom5" = Table.AddColumn(#"Added Custom4", "Month Name", each Date.ToText([DateKey],"MMM")),
    #"Added Custom6" = Table.AddColumn(#"Added Custom5", "Quarter Num", each Date.QuarterOfYear([DateKey])),
    #"Added Custom7" = Table.AddColumn(#"Added Custom6", "QuarterName", each "Qtr"& Number.ToText([Quarter Num])),
    #"Added Custom8" = Table.AddColumn(#"Added Custom7", "WeekMonth", each Date.WeekOfMonth([DateKey])),
    #"Added Custom9" = Table.AddColumn(#"Added Custom8", "Week", each "Week"& Number.ToText([WeekMonth]))
in
    #"Added Custom9"
