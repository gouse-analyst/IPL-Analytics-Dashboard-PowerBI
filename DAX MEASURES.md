# **DAX MEASURES:**

**---------------------------------**



#### **1)season winner:-**



**season winner =** 



**VAR selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season]) --2025**



**VAR finalmatchdate = CALCULATE(max(ipl\_matches\_data\[match\_date]),**

&#x20;                    **ipl\_matches\_data\[season]=selectedseason)                                    --- date of final match**



**VAR finalmatchwinner = CALCULATE(max(ipl\_matches\_data\[match\_winner]),**

&#x20;                     **ipl\_matches\_data\[season]= selectedseason,** 

&#x20;                     **ipl\_matches\_data\[match\_date] = finalmatchdate)                             ----winner team**

&#x20;                     

**Return finalmatchwinner**



#### **2)season winner logo:-**



**season winner logo =** 



**VAR selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season]) --2025**



**VAR finalmatchdate = CALCULATE(max(ipl\_matches\_data\[match\_date]),**

&#x20;                    **ipl\_matches\_data\[season]=selectedseason)                                    --- date of final match**



**VAR finalmatchwinner = CALCULATE(max(ipl\_matches\_data\[match\_winner]),**

&#x20;                     **ipl\_matches\_data\[season]= selectedseason,** 

&#x20;                     **ipl\_matches\_data\[match\_date] = finalmatchdate)                             ----winner team**



**RETURN**



**LOOKUPVALUE(teams\_data\[image\_url],**

&#x20;           **teams\_data\[team\_name],finalmatchwinner)**



#### **3)Runner Up:-**



**RUNNER UP =** 



**VAR selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season]) --2025**



**VAR finalmatchdate = CALCULATE(max(ipl\_matches\_data\[match\_date]),**

&#x20;                    **ipl\_matches\_data\[season]=selectedseason)                                    --- date of final match**



**VAR finalmatchwinner = CALCULATE(max(ipl\_matches\_data\[match\_winner]),**

&#x20;                     **ipl\_matches\_data\[season]= selectedseason,** 

&#x20;                     **ipl\_matches\_data\[match\_date] = finalmatchdate)                             ----winner team**

**VAR TEAM1 = CALCULATE(MAX(ipl\_matches\_data\[team1]),**

&#x20;                 **ipl\_matches\_data\[season] = selectedseason,**

&#x20;                 **ipl\_matches\_data\[match\_date] = finalmatchdate)**



**VAR TEAM2 = CALCULATE(MAX(ipl\_matches\_data\[team2]),**

&#x20;                 **ipl\_matches\_data\[season] = selectedseason,**

&#x20;                 **ipl\_matches\_data\[match\_date] = finalmatchdate)**



&#x20;                              

**Return** 

**IF(finalmatchwinner = TEAM1,TEAM2,TEAM1)**



#### **4)Runner Up Logo:-**



**RUnner up logo =** 



**VAR selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season]) --2025**



**VAR finalmatchdate = CALCULATE(max(ipl\_matches\_data\[match\_date]),**

&#x20;                    **ipl\_matches\_data\[season]=selectedseason)                                    --- date of final match**



**VAR finalmatchwinner = CALCULATE(max(ipl\_matches\_data\[match\_winner]),**

&#x20;                     **ipl\_matches\_data\[season]= selectedseason,** 

&#x20;                     **ipl\_matches\_data\[match\_date] = finalmatchdate)                             ----winner team**

**VAR TEAM1 = CALCULATE(MAX(ipl\_matches\_data\[team1]),**

&#x20;                 **ipl\_matches\_data\[season] = selectedseason,**

&#x20;                 **ipl\_matches\_data\[match\_date] = finalmatchdate)**



**VAR TEAM2 = CALCULATE(MAX(ipl\_matches\_data\[team2]),**

&#x20;                 **ipl\_matches\_data\[season] = selectedseason,**

&#x20;                 **ipl\_matches\_data\[match\_date] = finalmatchdate)**



&#x20;                              

**Return** 

**LOOKUPVALUE(teams\_data\[image\_url],teams\_data\[team\_name],\[RUNNER UP])**



#### **5)Total SIX's secondary KPI:-**



**total 6 =** 

**CALCULATE(COUNTROWS(ball\_by\_ball\_data),ball\_by\_ball\_data\[batter\_runs]=6,**

&#x20;        **KEEPFILTERS(VALUES(ipl\_matches\_data\[season])))**



#### **6)Total Four's secondary KPI:-**



**total 4 =** 

**CALCULATE(COUNTROWS(ball\_by\_ball\_data),ball\_by\_ball\_data\[batter\_runs]=4,**

&#x20;        **KEEPFILTERS(VALUES(ipl\_matches\_data\[season])))**



#### **7)Total Teams secondary KPI:-**



**total teams = CALCULATE(DISTINCTCOUNT(ipl\_matches\_data\[team1]))**



#### **8)Total Matches secondary KPI:-**



**total matches = CALCULATE(DISTINCTCOUNT(ball\_by\_ball\_data\[match\_id]))**



#### **9)Half Centuries secondary KPI:-**



**half centuries =** 

**var selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondata = FILTER(ball\_by\_ball\_data, RELATED(ipl\_matches\_data\[season])=selectedseason)**



**var batterruns = SUMMARIZE(seasondata,ball\_by\_ball\_data\[match\_id], ball\_by\_ball\_data\[batter],"total runs" , sum(ball\_by\_ball\_data\[batter\_runs]))**



**var halfcenturycount = FILTER(batterruns,\[total runs]>=50 \&\& \[total runs]<100)**



**return COUNTROWS(halfcenturycount)**



#### **10)Centuries secondary KPI:-**



**centuries =** 

**var selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondata = FILTER(ball\_by\_ball\_data, RELATED(ipl\_matches\_data\[season])=selectedseason)**



**var batterruns = SUMMARIZE(seasondata,ball\_by\_ball\_data\[match\_id], ball\_by\_ball\_data\[batter],"total runs" , sum(ball\_by\_ball\_data\[batter\_runs]))**



**var centurycount = FILTER(batterruns,\[total runs]>=100)**



**return COUNTROWS(centurycount)**



#### **11)Total Venus secondary KPI:-**



**TOTAL VENUS =** 

**CALCULATE(DISTINCTCOUNT(ipl\_matches\_data\[venue]))**



#### **12)ORANGE CAP HOLDER NAME:-**



**ORANGE CAP HOLDER =** 



**VAR SELECTEDSEASON = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondataonly = FILTER(ball\_by\_ball\_data,RELATED(ipl\_matches\_data\[season]) = SELECTEDSEASON)**



**VAR RUNSUMMARY = SUMMARIZE(seasondataonly,ball\_by\_ball\_data\[batter],"TOTAL RUNS", SUM (ball\_by\_ball\_data\[batter\_runs]))**



**var maxruns = MAXX(RUNSUMMARY,\[TOTAL RUNS])**



**var topscorer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),FILTER(RUNSUMMARY,\[TOTAL RUNS]=maxruns))**



**return maxx (topscorer,ball\_by\_ball\_data\[batter])**



#### **12)ORANGE CAP HOLDER TOTAL RUNS:-**



**ORANGE CAP RUNS =** 



**VAR SELECTEDSEASON = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondataonly = FILTER(ball\_by\_ball\_data,RELATED(ipl\_matches\_data\[season]) = SELECTEDSEASON)**



**VAR RUNSUMMARY = SUMMARIZE(seasondataonly,ball\_by\_ball\_data\[batter],"TOTAL RUNS", SUM (ball\_by\_ball\_data\[batter\_runs]))**



**var maxruns = MAXX(RUNSUMMARY,\[TOTAL RUNS])**



**return maxruns**



#### **13)ORANGE CAP HOLDER TEAM NAME:-**



**ORANGE CAP TEAM =** 



**VAR SELECTEDSEASON = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondataonly = FILTER(ball\_by\_ball\_data,RELATED(ipl\_matches\_data\[season]) = SELECTEDSEASON)**



**VAR RUNSUMMARY = SUMMARIZE(seasondataonly,ball\_by\_ball\_data\[batter],"TOTAL RUNS", SUM (ball\_by\_ball\_data\[batter\_runs]))**



**var maxruns = MAXX(RUNSUMMARY,\[TOTAL RUNS])**



**var topscorer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),FILTER(RUNSUMMARY,\[TOTAL RUNS]=maxruns))**



**VAR FULLTEAMNAME = CALCULATE(MAX(ball\_by\_ball\_data\[team\_batting]),FILTER(seasondataonly,ball\_by\_ball\_data\[batter] = MAXX(topscorer,ball\_by\_ball\_data\[batter])))**



**RETURN FULLTEAMNAME**



#### **14)ORANGE CAP LOGO:-**



**ORANGE CAP LOGO =** 



**VAR SELECTEDSEASON = SELECTEDVALUE(ipl\_matches\_data\[season])**



**var seasondataonly = FILTER(ball\_by\_ball\_data,RELATED(ipl\_matches\_data\[season]) = SELECTEDSEASON)**



**VAR RUNSUMMARY = SUMMARIZE(seasondataonly,ball\_by\_ball\_data\[batter],"TOTAL RUNS", SUM (ball\_by\_ball\_data\[batter\_runs]))**



**var maxruns = MAXX(RUNSUMMARY,\[TOTAL RUNS])**



**var topscorer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),FILTER(RUNSUMMARY,\[TOTAL RUNS]=maxruns))**



**return**



**LOOKUPVALUE('players-data-updated'\[player\_image],'players-data-updated'\[player\_name],MAXX(topscorer,ball\_by\_ball\_data\[batter]))**



#### **15)Purple Cap Holder:-**



**PurpleCapHolder =** 

**VAR SelectedSeason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**-- Filter: wickets in selected season, exclude non-bowler dismissals**

**VAR SeasonWickets =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[is\_wicket] = TRUE() \&\&**

&#x20;       **NOT ball\_by\_ball\_data\[wicket\_kind] IN {**

&#x20;           **"run out",**

&#x20;           **"retired hurt",**

&#x20;           **"obstructing the field",**

&#x20;           **"retired out"**

&#x20;       **}**

&#x20;   **)**



**-- Summarize bowler and count wickets**

**VAR WicketSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonWickets,**

&#x20;       **ball\_by\_ball\_data\[bowler],**

&#x20;       **"WicketCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonWickets,**

&#x20;               **ball\_by\_ball\_data\[bowler] = EARLIER(ball\_by\_ball\_data\[bowler])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**-- Find highest wicket count**

**VAR MaxWickets =**

&#x20;   **MAXX(WicketSummary, \[WicketCount])**



**-- Get the bowler(s) with that wicket count**

**VAR TopBowler =**

&#x20;   **CALCULATETABLE(**

&#x20;       **VALUES(ball\_by\_ball\_data\[bowler]),**

&#x20;       **FILTER(WicketSummary, \[WicketCount] = MaxWickets)**

&#x20;   **)**



**-- Return the name (if multiple, it picks one alphabetically)**

**RETURN**

&#x20;   **MAXX(TopBowler, ball\_by\_ball\_data\[bowler])**



#### **16)Purple Cap WICKETS:-**



**PurpleCapWKTS =** 

**VAR SelectedSeason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**-- Filter: wickets in selected season, exclude non-bowler dismissals**

**VAR SeasonWickets =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[is\_wicket] = TRUE() \&\&**

&#x20;       **NOT ball\_by\_ball\_data\[wicket\_kind] IN {**

&#x20;           **"run out",**

&#x20;           **"retired hurt",**

&#x20;           **"obstructing the field",**

&#x20;           **"retired out"**

&#x20;       **}**

&#x20;   **)**



**-- Summarize bowler and count wickets**

**VAR WicketSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonWickets,**

&#x20;       **ball\_by\_ball\_data\[bowler],**

&#x20;       **"WicketCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonWickets,**

&#x20;               **ball\_by\_ball\_data\[bowler] = EARLIER(ball\_by\_ball\_data\[bowler])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**-- Find highest wicket count**

**VAR MaxWickets =**

&#x20;   **MAXX(WicketSummary, \[WicketCount])**



**RETURN**

&#x20;   **MaxWickets**



#### **17)Purple Cap TEAM NAME:-**



**Purple Cap TEAM =** 

**VAR SelectedSeason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**-- Filter: wickets in selected season, exclude non-bowler dismissals**

**VAR SeasonWickets =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[is\_wicket] = TRUE() \&\&**

&#x20;       **NOT ball\_by\_ball\_data\[wicket\_kind] IN {**

&#x20;           **"run out",**

&#x20;           **"retired hurt",**

&#x20;           **"obstructing the field",**

&#x20;           **"retired out"**

&#x20;       **}**

&#x20;   **)**



**-- Summarize bowler and count wickets**

**VAR WicketSummary =**

&#x20;   **ADDCOLUMNS(**

&#x20;       **SUMMARIZE(**

&#x20;           **SeasonWickets,**

&#x20;           **ball\_by\_ball\_data\[bowler],**

&#x20;           **ball\_by\_ball\_data\[team\_bowling]**

&#x20;       **),**

&#x20;       **"WICKETCOUNT",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(SeasonWickets,**

&#x20;           **ball\_by\_ball\_data\[bowler]=EARLIER(ball\_by\_ball\_data\[bowler])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**-- Find highest wicket count**



**VAR MaxWickets =**

&#x20;   **MAXX(WicketSummary, \[WicketCount])**



**-- Return the name (if multiple, it picks one alphabetically)**

**RETURN**

**MAXX(FILTER(WicketSummary,\[WICKETCOUNT] = MaxWickets),ball\_by\_ball\_data\[team\_bowling])**

&#x20;   

#### **18)Purple Cap LOGO:-**



**PurpleCaplogo =** 

**VAR SelectedSeason = SELECTEDVALUE(ipl\_matches\_data\[season])**



**-- Filter: wickets in selected season, exclude non-bowler dismissals**

**VAR SeasonWickets =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[is\_wicket] = TRUE() \&\&**

&#x20;       **NOT ball\_by\_ball\_data\[wicket\_kind] IN {**

&#x20;           **"run out",**

&#x20;           **"retired hurt",**

&#x20;           **"obstructing the field",**

&#x20;           **"retired out"**

&#x20;       **}**

&#x20;   **)**



**-- Summarize bowler and count wickets**

**VAR WicketSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonWickets,**

&#x20;       **ball\_by\_ball\_data\[bowler],**

&#x20;       **"WicketCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonWickets,**

&#x20;               **ball\_by\_ball\_data\[bowler] = EARLIER(ball\_by\_ball\_data\[bowler])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**-- Find highest wicket count**

**VAR MaxWickets =**

&#x20;   **MAXX(WicketSummary, \[WicketCount])**



**-- Get the bowler(s) with that wicket count**

**VAR TopBowler =**

&#x20;   **CALCULATETABLE(**

&#x20;       **VALUES(ball\_by\_ball\_data\[bowler]),**

&#x20;       **FILTER(WicketSummary, \[WicketCount] = MaxWickets)**

&#x20;   **)**



**-- Return the name (if multiple, it picks one alphabetically)**

**RETURN**

**LOOKUPVALUE('players-data-updated'\[player\_image],'players-data-updated'\[player\_name],MAXX(TopBowler,ball\_by\_ball\_data\[bowler]))**





#### **19)Top FOURS BATSMAN NAME:-**



**Top FOURS BATSMAN =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonFours =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 4**

&#x20;   **)**



**VAR FourSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonFours,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"FoursCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonFours,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxFours =**

&#x20;   **MAXX(FourSummary, \[FoursCount])**



**var topfoursplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(FourSummary,\[FoursCount]=MaxFours))**





**RETURN MAXX(topfoursplayer,ball\_by\_ball\_data\[batter])**  



#### **20)Top FOUR COUNT:-**



**Top FOUR COUNT =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonFours =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 4**

&#x20;   **)**



**VAR FourSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonFours,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"FoursCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonFours,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxFours =**

&#x20;   **MAXX(FourSummary, \[FoursCount])**



**RETURN**

&#x20;   **MaxFours**



#### **21)Top FOURS PLAYER TEAM NAME:-**



**Top FOURS team =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonFours =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 4**

&#x20;   **)**



**VAR FourSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonFours,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"FoursCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonFours,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxFours =**

&#x20;   **MAXX(FourSummary, \[FoursCount])**



**var topfoursplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(FourSummary,\[FoursCount]=MaxFours))**



**VAR BATTERTEAM = CALCULATE(MAX(ball\_by\_ball\_data\[team\_batting]),**

&#x20;                         **FILTER(SeasonFours,ball\_by\_ball\_data\[batter] =MAXX(topfoursplayer,ball\_by\_ball\_data\[batter])))**





**RETURN**

&#x20;   **BATTERTEAM**



#### **22)Top FOURS PLAYER LOGO:-**



**Top FOURSLOGO =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonFours =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 4**

&#x20;   **)**



**VAR FourSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonFours,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"FoursCount",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonFours,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxFours =**

&#x20;   **MAXX(FourSummary, \[FoursCount])**



**var topfoursplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(FourSummary,\[FoursCount]=MaxFours))**





**RETURN** 

**LOOKUPVALUE(**

&#x20;   **'players-data-updated'\[player\_image],**

&#x20;   **'players-data-updated'\[player\_name],MAXX(topfoursplayer,ball\_by\_ball\_data\[batter]))**





#### **22)Top SIX COUNT:-**



**Top SIX COUNT =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonSIXES =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 6**

&#x20;   **)**



**VAR SIXSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonSIXES,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"SIXESCOUNT",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonSIXES,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxSIXES =**

&#x20;   **MAXX(SIXSummary, \[SIXESCOUNT])**



**RETURN**

&#x20;   **MaxSIXES**



#### **23)Top SIXES BATSMAN NAME:-**



**Top SIXES BATSMAN =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonSIXES =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 6**

&#x20;   **)**



**VAR SIXSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonSIXES,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"SIXESCOUNT",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonSIXES,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxSIXES =**

&#x20;   **MAXX(SIXSummary, \[SIXESCOUNT])**



**var topSIXESplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(SIXSummary,\[SIXESCOUNT]=MaxSIXES))**





**RETURN MAXX(topSIXESplayer,ball\_by\_ball\_data\[batter])**



#### **24)Top SIXES team NAME:-**



**Top SIXES team =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonSIXES =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 6**

&#x20;   **)**



**VAR SIXSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonSIXES,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"SIXESCOUNT",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonSIXES,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxSIXES =**

&#x20;   **MAXX(SIXSummary, \[SIXESCOUNT])**



**var topSIXESplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(SIXSummary,\[SIXESCOUNT]=MaxSIXES))**



**VAR BATTERTEAM = CALCULATE(MAX(ball\_by\_ball\_data\[team\_batting]),**

&#x20;                         **FILTER(SeasonSIXES,ball\_by\_ball\_data\[batter] =MAXX(topSIXESplayer,ball\_by\_ball\_data\[batter])))**





**RETURN**

&#x20;   **BATTERTEAM**



#### **25)Top SIXES PLAYER LOGO:-**



**Top SIXES LOGO =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR SeasonSIXES =**

&#x20;   **FILTER(**

&#x20;       **ball\_by\_ball\_data,**

&#x20;       **RELATED(ipl\_matches\_data\[season]) = SelectedSeason \&\&**

&#x20;       **ball\_by\_ball\_data\[batter\_runs] = 6**

&#x20;   **)**



**VAR SIXSummary =**

&#x20;   **SUMMARIZE(**

&#x20;       **SeasonSIXES,**

&#x20;       **ball\_by\_ball\_data\[batter],**

&#x20;       **"SIXESCOUNT",**

&#x20;       **COUNTROWS(**

&#x20;           **FILTER(**

&#x20;               **SeasonSIXES,**

&#x20;               **ball\_by\_ball\_data\[batter] = EARLIER(ball\_by\_ball\_data\[batter])**

&#x20;           **)**

&#x20;       **)**

&#x20;   **)**



**VAR MaxSIXES =**

&#x20;   **MAXX(SIXSummary, \[SIXESCOUNT])**



**var topSIXESplayer = CALCULATETABLE(VALUES(ball\_by\_ball\_data\[batter]),**

&#x20;                            **FILTER(SIXSummary,\[Top SIX COUNT]=MaxSIXES))**





**RETURN** 

**LOOKUPVALUE(**

&#x20;   **'players-data-updated'\[player\_image],**

&#x20;   **'players-data-updated'\[player\_name],MAXX(topSIXESplayer,ball\_by\_ball\_data\[batter]))**



### POINTS TABLE



#### **1)matches won:-**





&#x20;   **matches won =** 



**var selectedseason = SELECTEDVALUE(ipl\_matches\_data\[season])** 



**var currentTeam = SELECTEDVALUE(teams\_data\[team\_name])**



**RETURN** 

**CALCULATE(COUNTROWS(ipl\_matches\_data),**

&#x20;        **ipl\_matches\_data\[season]=selectedseason,**

&#x20;        **ipl\_matches\_data\[match\_winner]=currentTeam,**

&#x20;        **ipl\_matches\_data\[match\_type]="T20")**

&#x20;   



#### **2)Matches Lost:-**



**Matches Lost =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR Team1LostMatches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team1],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**

&#x20;       **NOT ISBLANK(ipl\_matches\_data\[match\_winner]),**

&#x20;       **ipl\_matches\_data\[match\_winner] <> ipl\_matches\_data\[team1]**

&#x20;   **)**



**VAR Team2LostMatches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team2],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**

&#x20;       **NOT ISBLANK(ipl\_matches\_data\[match\_winner]),**

&#x20;       **ipl\_matches\_data\[match\_winner] <> ipl\_matches\_data\[team2]**

&#x20;   **)**



**RETURN**

&#x20;   **Team1LostMatches + Team2LostMatches**



#### **3)Matches Played:-**



**Matches Played =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR Team1Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team1],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20"**

&#x20;   **)**



**VAR Team2Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team2],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20"**

&#x20;   **)**



**RETURN**

&#x20;   **Team1Matches + Team2Matches**



#### **4)NO RESULT:-**



**NO RESULT =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR Team1Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team1],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**

&#x20;       **ipl\_matches\_data\[result]= "NO RESULT"**

&#x20;   **)**



**VAR Team2Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team2],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**       

&#x20;        **ipl\_matches\_data\[result]= "NO RESULT"**



&#x20;   **)**



**RETURN**

&#x20;   **Team1Matches + Team2Matches**



#### **4)Tie matches:-**



**Tie matches =** 



**VAR SelectedSeason =**

&#x20;   **SELECTEDVALUE(ipl\_matches\_data\[season])**



**VAR Team1Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team1],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**

&#x20;       **ipl\_matches\_data\[result]= "Tie"**

&#x20;   **)**



**VAR Team2Matches =**

&#x20;   **CALCULATE(**

&#x20;       **COUNTROWS(ipl\_matches\_data),**

&#x20;       **USERELATIONSHIP(**

&#x20;           **ipl\_matches\_data\[team2],**

&#x20;           **teams\_data\[team\_name]**

&#x20;       **),**

&#x20;       **ipl\_matches\_data\[season] = SelectedSeason,**

&#x20;       **ipl\_matches\_data\[match\_type] = "T20",**       

&#x20;        **ipl\_matches\_data\[result]= "Tie"**



&#x20;   **)**



**RETURN**

&#x20;   **Team1Matches + Team2Matches**



#### **5)Total points:-**



**Total points =** 



**var win = \[matches won]**



**var NR = \[NO RESULT]**



**RETURN (win\*2) + NR**







&#x20;                     

