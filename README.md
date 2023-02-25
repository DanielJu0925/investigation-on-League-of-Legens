# "Title of project"

by Bofu Zou and Zhuoxuan Ju

## Introduction


## Cleaning and EDA

### Data Cleaning

As we download our dataset from the website, we saved and loaded it in our notebook as csv form. After the loading process, we discovered that this dataframe had about 140000 rows and 123 columns. Inside the dataframe, we first discovered that the date column is still in a string type, and thus we convert it into datetime format. Also, we noticed that the playername column had a unusual name called unknown player. Since it is a game match data report, the name should be recorded for every player. So we consider it as missing value. In addition, we converted the columns contain 0 and 1 to boolean columns which are better for us to have a clear view for our later investigation. After that, we droped the some not related columns in order to make the dataframe clean to use. Looking into the tier 1 leagues' team data in the League of Legends matchs is what our focuing are. So we filter out the other leagues and the players information, only keeping the tier 1 league's information in our dataset. 

The head of the cleaned dataframe is from the code below:
    `print(tier1_team.head().to_markdown(index=False))`

| gameid           | datacompleteness   | url                                         | league   |   year | split   |   playoffs | date                |   game |   patch |   participantid | side   | position   |   playername |   playerid | teamname           | teamid                                  |   champion | ban1     | ban2         | ban3      | ban4     | ban5    |   gamelength | result   |   kills |   deaths |   assists |   teamkills |   teamdeaths |   doublekills |   triplekills |   quadrakills |   pentakills |   firstblood |   firstbloodkill |   firstbloodassist |   firstbloodvictim |   team kpm |   ckpm |   firstdragon |   dragons |   opp_dragons |   elementaldrakes |   opp_elementaldrakes |   infernals |   mountains |   clouds |   oceans |   chemtechs |   hextechs |   dragons (type unknown) |   elders |   opp_elders |   firstherald |   heralds |   opp_heralds |   firstbaron |   barons |   opp_barons |   firsttower |   towers |   opp_towers |   firstmidtower |   firsttothreetowers |   turretplates |   opp_turretplates |   inhibitors |   opp_inhibitors |   damagetochampions |     dpm |   damageshare |   damagetakenperminute |   damagemitigatedperminute |   wardsplaced |    wpm |   wardskilled |   wcpm |   controlwardsbought |   visionscore |   vspm |   totalgold |   earnedgold |   earned gpm |   earnedgoldshare |   goldspent |        gspd |   total cs |   minionkills |   monsterkills |   monsterkillsownjungle |   monsterkillsenemyjungle | result_str   |
|:-----------------|:-------------------|:--------------------------------------------|:---------|-------:|:--------|-----------:|:--------------------|-------:|--------:|----------------:|:-------|:-----------|-------------:|-----------:|:-------------------|:----------------------------------------|-----------:|:---------|:-------------|:----------|:---------|:--------|-------------:|:---------|--------:|---------:|----------:|------------:|-------------:|--------------:|--------------:|--------------:|-------------:|-------------:|-----------------:|-------------------:|-------------------:|-----------:|-------:|--------------:|----------:|--------------:|------------------:|----------------------:|------------:|------------:|---------:|---------:|------------:|-----------:|-------------------------:|---------:|-------------:|--------------:|----------:|--------------:|-------------:|---------:|-------------:|-------------:|---------:|-------------:|----------------:|---------------------:|---------------:|-------------------:|-------------:|-----------------:|--------------------:|--------:|--------------:|-----------------------:|---------------------------:|--------------:|-------:|--------------:|-------:|---------------------:|--------------:|-------:|------------:|-------------:|-------------:|------------------:|------------:|------------:|-----------:|--------------:|---------------:|------------------------:|--------------------------:|:-------------|
| 8401-8401_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 09:24:26 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | Oh My God          | oe:team:f4c4528c6981e104a11ea7548630c23 |        nan | Renekton | Lee Sin      | Caitlyn   | Jayce    | Camille |         1365 | True     |      13 |        6 |        35 |          13 |            6 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.5714 | 0.8352 |           nan |         2 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        2 |      nan |          nan |           nan |       nan |           nan |          nan |        1 |            0 |          nan |        8 |            3 |             nan |                  nan |            nan |                nan |            1 |                0 |               40086 | 1762.02 |           nan |                2263.25 |                        nan |            79 | 3.4725 |            33 | 1.4505 |                   32 |           162 | 7.1209 |       45468 |        30167 |      1326.02 |               nan |       36908 | -0.00586225 |        nan |           nan |            172 |                      98 |                        18 | win          |
| 8401-8401_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 09:24:26 |      1 |   12.01 |             200 | Red    | team       |          nan |        nan | ThunderTalk Gaming | oe:team:df80f468a3f9a722df056fe9104f052 |        nan | Samira   | Diana        | Akali     | LeBlanc  | Rumble  |         1365 | False    |       6 |       13 |        11 |           6 |           13 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.2637 | 0.8352 |           nan |         1 |             2 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        1 |      nan |          nan |           nan |       nan |           nan |          nan |        0 |            1 |          nan |        3 |            8 |             nan |                  nan |            nan |                nan |            0 |                1 |               30417 | 1337.01 |           nan |                2541.89 |                        nan |            64 | 2.8132 |            34 | 1.4945 |                   26 |           155 | 6.8132 |       38538 |        23237 |      1021.41 |               nan |       37125 |  0.00586225 |        nan |           nan |            116 |                      94 |                         2 | lose         |
| 8401-8401_game_2 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 10:09:22 |      2 |   12.01 |             100 | Blue   | team       |          nan |        nan | Oh My God          | oe:team:f4c4528c6981e104a11ea7548630c23 |        nan | Renekton | Caitlyn      | Thresh    | Jayce    | Camille |         1444 | True     |      22 |        9 |        40 |          22 |            9 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.9141 | 1.2465 |           nan |         2 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        2 |      nan |          nan |           nan |       nan |           nan |          nan |        1 |            0 |          nan |        9 |            2 |             nan |                  nan |            nan |                nan |            1 |                0 |               59746 | 2482.52 |           nan |                3026.05 |                        nan |            67 | 2.7839 |            32 | 1.3296 |                   38 |           180 | 7.4792 |       54283 |        38176 |      1586.26 |               nan |       50858 |  0.298771   |        nan |           nan |            178 |                      88 |                        41 | win          |
| 8401-8401_game_2 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 10:09:22 |      2 |   12.01 |             200 | Red    | team       |          nan |        nan | ThunderTalk Gaming | oe:team:df80f468a3f9a722df056fe9104f052 |        nan | Samira   | Diana        | Jarvan IV | LeBlanc  | Akali   |         1444 | False    |       8 |       22 |        16 |           8 |           22 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.3324 | 1.2465 |           nan |         1 |             2 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        1 |      nan |          nan |           nan |       nan |           nan |          nan |        0 |            1 |          nan |        2 |            9 |             nan |                  nan |            nan |                nan |            0 |                1 |               35129 | 1459.65 |           nan |                3107.16 |                        nan |            82 | 3.4072 |            21 | 0.8726 |                   29 |           159 | 6.6066 |       41155 |        25048 |      1040.78 |               nan |       37638 | -0.298771   |        nan |           nan |            115 |                      88 |                         0 | lose         |
| 8402-8402_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8402 | LPL      |   2022 | Spring  |          0 | 2022-01-10 11:26:11 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | FunPlus Phoenix    | oe:team:33d17f3717f58e12a3da80b377221fb |        nan | LeBlanc  | Twisted Fate | Aphelios  | Nautilus | Leona   |         1893 | True     |      12 |        8 |        25 |          12 |            8 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.3803 | 0.6339 |           nan |         4 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        4 |      nan |          nan |           nan |       nan |           nan |          nan |        2 |            0 |          nan |       10 |            3 |             nan |                  nan |            nan |                nan |            3 |                0 |               54264 | 1719.94 |           nan |                2528.49 |                        nan |           100 | 3.1696 |            59 | 1.87   |                   41 |           274 | 8.6846 |       64011 |        43324 |      1373.19 |               nan |       58619 |  0.149322   |        nan |           nan |            264 |                     162 |                        34 | win          |


### Univariate Analysis
<iframe src="assets/league_distribution.html" width=800 height=600 frameBorder=0></iframe>

In this pie chart, we are looking for which the tier 1 league has the most number of match played. It seems like LPL has the most game of matches played in 2022, and LCK has the second most game played in 2022. We can analysis further on the popularity of League of Legends in differet countries.


### Bivariate Analysis
<iframe src="assets/tkpm_league.html" width=800 height=600 frameBorder=0></iframe>

This bar chart is looking at the team kill per minute in different tier 1 leagues. We can have a clear view of the differences in team kill per minute in different leagues. Specifically, LPL has the highest team kill per minute, and we can know their matches contain more fights comparing to other leagues.

## Assessment of Missingness


## Hypothesis Testing