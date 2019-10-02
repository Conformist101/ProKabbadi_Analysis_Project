# ProKabbadi_Analysis_Project:

## Objective:
The Project is undertaken to analyse various aspects of the ProKabbadi Tournament and using various data like Team Statistics predict several outcomes. The Broad category of Questions are mentioned below:

a.Predict the winner of the tournament.<br>
b.Predict the the top team in the points table after the completion of league matches.<br>
c.Predict the team with the highest points for successful raids.<br>
d.Predict the team with the highest points for successful tackles.<br>
e.Predict the team with the highest super-performance total.<br>
f.Predict the player with the highest SUCCESSFUL RAID percentage.<br>
g.Predict the player with the highest SUCCESSFUL TACKLE percentage.<br>

## Code-file :
<b>Team-data: team-wise-data</b><br>
Team analysis data mapping:<br>
Delhi Dabang : Team_data_analysis_DD<br>
Bengal warriors: Team_data_analysis<br>
UP-Yoddha: Team_data_analysis_UP<br>
Bengaluru-bulls: Team_data_analysis_BB<br>
U-mumba: Team_data_analysis_2<br>
Telugu-Titans:Team_data_analysisTelT<br>
patna-pirates: Team_data_analysis_PP<br>
purani-paltan: Team_data_analysis_PurP<br>
jaipur-pinkpanthers: Team_data_analysis_JPP<br>
Gujrat-fortuneGiants: Team_data_analysis_GF<br>
Hariyana-steelers: Team_data_analysis_HS<br>
Tamil-Thalivas:Team_data_analysis_TamT<br>
<b>Player-data:</b> <br>
Successful-raid: player-wise-data/successful-raid <br>
Successful-tackle: player-wise-data/successful-tackle<br>

 
### 1. Data Extraction: Sources and means of data extraction
The main sources from where the data was procured was the Prokabbadi sites.
WebScraping techniques were employed to extract the data. Since the website was dynamic in nature hence techniques like BeautifulSoup and using a crawler( Scrapy) failed to fetch any data. Hence we decided to use Selenium plugin to create a automated solution of capturing data. The implemetation is present in the WebScraping folder of this project.

### 2. Startegy followed in cleaning the data
The data collected by using Selenium implementation was already cleaned and had no missing attributes.However while importing the data in the Jupyter notebook for analysis a basic transformation was applied to reverse the rows and columns. This was done because in the original data the columns represented the seasons and rows represented the features.

### 3. Model Building and analysis steps
The approach followed in model building are as follows:
Step 1: Understanding the business problem and preparing gathering more knowledge about the Kabbadi sport,specifically how the scoring works and what are the important aspects of the game.<br>
Step 2: Understanding the Data collected from scraping and making sense of the various features and how they are related to the predictor variables. <br>
Step 3: Using the domain knowledge used gained in the research phase we started creating our own features set as most of the basic features were highly correlated. The newly designed features were a combination of existing featuresa and upon constructing a heatmap we could see that corelation matrix had chaged significantly. Pandas profiling tool was also used in this context to do preliminary EDA.<br>
Step 4: To choose the most important features for the set we used sklearns.feature_selection : (SelectKBest and Chi2 test) .We also used sklearn.ensemble import ExtraTreesClassifier to get a list of all the important features(feature_importances_). Finally the features were chosen by using a RecursiveFeatureElimination process.<br>
Step 5: Initially we went for an ANN implementation for the problem at hand. We defined an ANN model in Keras using theano backend. Activator function used = RELU and with 12 input points. However the accuracy that we could achieve was at max 24% and at an average the accuracy was 14%. We assumed since there was not a huge amount of data to train the model hence an ANN implementation mignt not be feasible. We then decided to use XGBoost as it shows great promise even if the data is less.<br>

### 4. Analysis of the questions:

#### a.Predict the winner of the tournament.<br>
To predict the winner an XGBoost model was created. We used a XGBRegressor to find the poition of the team in season 7 basis the performance in the previous seasons and overall performance. The observations from our analysis are mentioed below(teams,positional_score).<br>
<table>
  <tr>
    <th>TeamName</th>
    <th>Position-scores</th>
  </tr>
	<tr><td>Delhi Dabang </td><td>1.008</td></tr>
	<tr><td>Bengal warriors</td><td>2.13</td></tr>
	<tr><td>UP-Yoddha</td><td>2.999</td></tr>
	<tr><td>Bengaluru-bulls</td><td>3.701</td></tr>
	<tr><td>U-mumba</td><td>3.701</td></tr>
	<tr><td>Telugu-Titans</td><td>3.701</td></tr>
	<tr><td>patna-pirates</td><td>3.888</td></tr>
	<tr><td>purani-paltan</td><td>4.0226</td></tr>
	<tr><td>jaipur-pinkpanthers</td><td>4.98</td></tr>
	<tr><td>Gujrat-fortuneGiants</td><td>5.99</td></tr>
	<tr><td>Hariyana-steelers</td><td>5.99</td></tr>
	<tr><td>Tamil-Thalivas</td><td>5.99</td></tr>
</table>

Thus as per our analysis <b>Delhi Dabang </b> will win Prokabbadi Season 7

##### b.Predict the the top team in the points table after the completion of league matches.<br>
To Predict the top team in the points table after the completion of league matches we decided to use the Win/Loss% feature to determine the team with highest win. The assumption was that the team having highest Win/loss% in season 7 will have the highest points.The result of our analysis are as follows(team, WinLoss%):<br>

<table>
  <tr>
    <th>TeamName</th>
    <th>WinLoss%</th>
  </tr>
	<tr><td>Delhi Dabang </td><td>6.5</td></tr>
	<tr><td>Bengal warriors</td><td>2.5</td></tr>
	<tr><td>UP-Yoddha</td><td>1.5</td></tr>
	<tr><td>Bengaluru-bulls</td><td>1.125</td></tr>
	<tr><td>U-mumba</td><td>1.1428</td></tr>
	<tr><td>Telugu-Titans</td><td>1.1428</td></tr>
	<tr><td>patna-pirates</td><td>0.6</td></tr>
	<tr><td>purani-paltan</td><td>0.66</td></tr>
	<tr><td>jaipur-pinkpanthers</td><td>0.875</td></tr>
	<tr><td>Gujrat-fortuneGiants</td><td>0.25</td></tr>
	<tr><td>Hariyana-steelers</td><td>0.25</td></tr>
	<tr><td>Tamil-Thalivas</td><td>0.25</td></tr>
</table>

From the Data we can see that Delhi Dabang  are leading the point charts with an amazing win/loss ratio of 6.5 closeley followed by Bengal Warriors. According to the data present we conclude that <b>Dehli Dabang </b>will have highest points in the league matches.


#### c.Predict the team with the highest points for successful raids.<br>
To answer this question we will cosider that team which will have the highest successful_Raid% in season 7. The observations from our analysis are mentioned below(team,SuccessfulRaid%).<br>
<table>
  <tr>
    <th>TeamName</th>
    <th>SuccessfulRaid%</th>
  </tr>
	<tr><td>Delhi Dabang </td><td>0.42</td></tr>
	<tr><td>Bengal warriors</td><td>0.4</td></tr>
	<tr><td>UP-Yoddha</td><td>0.29</td></tr>
	<tr><td>Bengaluru-bulls</td><td>0.39</td></tr>
	<tr><td>U-mumba</td><td>0.32</td></tr>
	<tr><td>Telugu-Titans</td><td>0.32</td></tr>
	<tr><td>patna-pirates</td><td>0.34</td></tr>
	<tr><td>purani-paltan</td><td>0.33</td></tr>
	<tr><td>jaipur-pinkpanthers</td><td>0.28</td></tr>
	<tr><td>Gujrat-fortuneGiants</td><td>0.33</td></tr>
	<tr><td>Hariyana-steelers</td><td>0.33</td></tr>
	<tr><td>Tamil-Thalivas</td><td>0.25</td></tr>
</table>

From the data we can see that Delhi Dabang is at the Lead closely followed by Bengal warriors. One also has to consider that DD has Naveen Kumar whose performance in season 7 has been significantly good(holds 3rd pos in raiding table). Moreover his successful raids is significantly better than Bengals Maninder Singh(185> 161) and his average raid pts/ match is also higher than Maninder Singh(12.68>10.1).<br>
Thus by the data analysed and taking into consideration the above mentioned facts we can conclude that Delhi Dabang will have highest points for successful raids.

#### d.Predict the team with the highest points for successful tackles.<br>
To answer this question we would see the Successful_tackle% of each team:<br>
<table>
  <tr>
    <th>TeamName</th>
    <th>Successful_tackle%</th>
  </tr>
	<tr><td>Delhi Dabang </td><td>0.3928</td></tr>
	<tr><td>Bengal warriors</td><td>0.3959</td></tr>
	<tr><td>UP-Yoddha</td><td>0.4293</td></tr>
	<tr><td>Bengaluru-bulls</td><td>0.3824</td></tr>
	<tr><td>U-mumba</td><td>0.4341</td></tr>
	<tr><td>Telugu-Titans</td><td>0.4341</td></tr>
	<tr><td>patna-pirates</td><td>0.3964</td></tr>
	<tr><td>purani-paltan</td><td>0.39</td></tr>
	<tr><td>jaipur-pinkpanthers</td><td>0.4209</td></tr>
	<tr><td>Gujrat-fortuneGiants</td><td>0.36</td></tr>
	<tr><td>Hariyana-steelers</td><td>0.36</td></tr>
	<tr><td>Tamil-Thalivas</td><td>0.36</td></tr>
</table>

Even though Telugu-Titans and U-mumba have highest successful scores. However considering the fact that Telugu-titans pts might not make them elligible for playoffs so U-mumba might have a shot at the playoffs and as a result their score might improve.
Thus considering this aspect it can be assumed that <b>U-mumba</b> will have hisghest successful Tackle% in season 7.

#### e.Predict the team with the highest super-performance total.<br>

SPT total is calculated as per the following :<br>
S.P.T. = (Total number of super-raids in the tournament + total number of super-tackles in the tournament + total number of allouts inflicted in the tournament - total number of all-outs conceded in the tournament).<br>
Using the above formulae following data is collected:<br>
<table>
  <tr>
    <th>TeamName</th>
    <th>SPT-SCORE</th>
  </tr>
	<tr><td>Delhi Dabang </td><td>25</td></tr>
	<tr><td>Bengal warriors</td><td>36</td></tr>
	<tr><td>UP-Yoddha</td><td>16</td></tr>
	<tr><td>Bengaluru-bulls</td><td>26</td></tr>
	<tr><td>U-mumba</td><td>25</td></tr>
	<tr><td>Telugu-Titans</td><td>23</td></tr>
	<tr><td>patna-pirates</td><td>36</td></tr>
	<tr><td>purani-paltan</td><td>16</td></tr>
	<tr><td>jaipur-pinkpanthers</td><td>30</td></tr>
	<tr><td>Gujrat-fortuneGiants</td><td>9</td></tr>
	<tr><td>Hariyana-steelers</td><td>10</td></tr>
	<tr><td>Tamil-Thalivas</td><td>1</td></tr>
</table>

From the data we can see that both Bengal-Warriors and Patna-Pirates have the same SPT score of 36. However, since Patna-Pirates are not going to qualify for the playoffs and Bengal is definitely going to the playoffs hence there is a good chance that for Bengal this score is going to increase(just by getting a single super raid the point of bengal will increase by 1).<br>
Hence we can conclude that Bengal-Warriors will have the highest super-performance total in season 7.

#### f.Predict the player with the highest SUCCESSFUL RAID percentage.<br>
The successful raid percentage for a player is expressed as (Successful raids/Total raids)x100.<br>
As per our analysis we extracted the players having Successful riad % > 0.5. Now as per the data we can see that there are some players having successful raid% = 1. However these players are not regular raiders and considering the average averageSuccessfulraid% is less than 1. So the reason they have such high raid% is because they have played very less games. So basis the averageSuccessfulraid% we can assume that as the game progresses their SuccessfulRaid% will decrease.<br>
Thus we can focus on the players who are actual raiders and have scores >0.5. In this context if we consider the Top 4 players we can see that there is no significant difference between the scores and Pawan kumar Sherawat has higher successful raid% over Naveen Kumar, but has a liitle bit lower averagesuccesfulRaid% in comparison to Naveen Kumar. But considering the fact that Pawan kumar Sherawat has more experience than Naveen Kumar hence we have concluded that <b>Pawan kumar Sherawat </b> will have the <b>Highest SUCCESSFUL RAID percentage</b> in Season 7.
<table>
  <tr>
    <th>Name</th>
    <th>Successful Raid%</th>
    <th>Average Successful raid%</th>
  </tr>
  <tr><td>Naveen Kumar</td><td>0.522059</td><td>10.65</td></tr>
<tr><td>Pawan Kumar Sehrawat</td><td>0.54519</td><td>9.842105</td></tr>
<tr><td>Maninder Singh</td><td>0.537736</td><td>8.55</td></tr>
<tr><td>Siddharth Sirish Desai</td><td>0.525735</td><td>7.944444</td></tr>
<tr><td>Ankush</td><td>0.666667</td><td>1.333333</td></tr>
<tr><td>Victor Onyango Obiero</td><td>0.5</td><td>1.333333</td></tr>
<tr><td>Rakesh Narwal</td><td>0.5</td><td>1.5</td></tr>
<tr><td>Chand Singh</td><td>1</td><td>0.111111</td></tr>
<tr><td>Vikas Chhillar</td><td>0.5</td><td>1</td></tr>
<tr><td>Saurabh Nandal</td><td>1</td><td>0.055556</td></tr>
  
</table>


#### g.Predict the player with the highest SUCCESSFUL TACKLE percentage.<br>
The successful tackle percentage for a player is expressed as (Successful tackle/Total tackles)x100.<br>
FAZEL ATRACHALI will have the highest Tackle percentage(as of now it is around 55%) moreover his averagesuccessfultackle% is also 3 and significantly higher than the rest(PFB the data below).we are aslo not considering players who have Succesful tackle % as 1 as they are not regular defenders and their averageSuccessfultackle% is less than 1. <br>
So we conclude that <b>FAZEL ATRACHALI</b> will have the<b>highest SUCCESSFUL TACKLE percentage</b> in Season 7.


<table>
  <tr>
    <th>Name</th>
    <th>Successful Tackle%</th>
    <th>Average Successful Tackle%</th>
  </tr>
  <tr><td>Fazel Atrachali</td><td>0.548077</td><td>3</td></tr>
<tr><td>Baldev Singh</td><td>0.514286</td><td>2.7</td></tr>
<tr><td>Parvesh Bhainswal</td><td>0.522727</td><td>2.3</td></tr>
<tr><td>Nitesh Kumar</td><td>0.517647</td><td>2.444444</td></tr>
<tr><td>More GB</td><td>0.588235</td><td>1.176471</td></tr>
<tr><td>Surender Gill</td><td>0.5</td><td>0.466667</td></tr>
<tr><td>Siddharth Sirish Desai</td><td>0.5</td><td>0.166667</td></tr>
<tr><td>Sonu Jaglan</td><td>0.75</td><td>0.2</td></tr>
<tr><td>Gurdeep</td><td>0.666667</td><td>1</td></tr>
<tr><td>Lalit Chaudhary</td><td>1</td><td>0.5</td></tr>
<tr><td>Selvamani K</td><td>0.5</td><td>0.285714</td></tr>
<tr><td>Ravindra Ramesh Kumawat</td><td>0.5</td><td>0.333333</td></tr>
<tr><td>Meraj Sheykh</td><td>0.5</td><td>0.076923</td></tr>
<tr><td>Mohit Balyan</td><td>1</td><td>1</td></tr>
<tr><td>Ankush</td><td>1</td><td>0.333333</td></tr>
<tr><td>Ankit Beniwal</td><td>0.5</td><td>0.166667</td></tr>
<tr><td>Sumit</td><td>0.5</td><td>0.5</td></tr>
<tr><td>Amit Kumar</td><td>0.5</td><td>0.166667</td></tr>
<tr><td>Aman Kadian</td><td>0.5</td><td>0.333333</td></tr>
<tr><td>Satywan</td><td>0.5</td><td>1</td></tr>
</table>



