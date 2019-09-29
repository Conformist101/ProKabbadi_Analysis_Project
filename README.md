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
Delhi Dabang : 1.008<br>
Bengal warriors: 2.13<br>
UP-Yoddha: 2.999<br>
Bengaluru-bulls: 3.701<br>
U-mumba: 3.701<br>
Telugu-Titans:3.701<br>
patna-pirates: 3.8880<br>
purani-paltan: 4.0226<br>
jaipur-pinkpanthers: 4.98<br>
Gujrat-fortuneGiants: 5.99<br>
Hariyana-steelers: 5.99<br>
Tamil-Thalivas:5.99<br>

Thus as per our analysis <b>Delhi Dabang </b> will win Prokabbadi Season 7

##### b.Predict the the top team in the points table after the completion of league matches.<br>
To Predict the top team in the points table after the completion of league matches we decided to use the Win/Loss% feature to determine the team with highest win. The assumption was that the team having highest Win/loss% in season 7 will have the highest points.The result of our analysis are as follows(team, WinLoss%):<br>
Delhi Dabang : 6.5<br>
Bengal warriors: 2.5<br>
UP-Yoddha: 1.5<br>
Bengaluru-bulls: 1.125<br>
U-mumba: 1.1428<br>
Telugu-Titans:1.1428<br>
patna-pirates: 0.6<br>
purani-paltan: 0.66<br>
jaipur-pinkpanthers: 0.875<br>
Gujrat-fortuneGiants: 0.25<br>
Hariyana-steelers: 0.25<br>
Tamil-Thalivas:0.25<br>

From the Data we can see that Delhi Dabang  are leading the point charts with an amazing win/loss ratio of 6.5 closeley followed by Bengal Warriors. According to the data present we conclude that <b>Dehli Dabang </b>will have highest points in the league matches.


#### c.Predict the team with the highest points for successful raids.<br>
To answer this question we will cosider that team which will have the highest successful_Raid% in season 7. The observations from our analysis are mentioned below(team,SuccessfulRaid%).<br>
Delhi Dabang : 0.42<br>
Bengal warriors: 0.40<br>
UP-Yoddha: 0.29<br>
Bengaluru-bulls: 0.39<br>
U-mumba: 0.32<br>
Telugu-Titans:0.32<br>
patna-pirates: 0.34<br>
purani-paltan: 0.33<br>
jaipur-pinkpanthers: 0.28<br>
Gujrat-fortuneGiants: 0.33<br>
Hariyana-steelers: 0.33<br>
Tamil-Thalivas:0.25<br>

From the data we can see that Delhi Dabang is at the Lead closely followed by Bengal warriors. One also has to consider that DD has Naveen Kumar whose performance in season 7 has been significantly good(holds 3rd pos in raiding table). Moreover his successful raids is significantly better than Bengals Maninder Singh(185> 161) and his average raid pts/ match is also higher than Maninder Singh(12.68>10.1).<br>
Thus by the data analysed and taking into consideration the above mentioned facts we can conclude that Delhi Dabang will have highest points for successful raids.

#### d.Predict the team with the highest points for successful tackles.<br>
To answer this question we would see the Successful_tackle% of each team:<br>
Delhi Dabang : 0.3928<br>
Bengal warriors: 0.3959<br>
UP-Yoddha: 0.4293<br>
Bengaluru-bulls: 0.3824<br>
U-mumba: 0.4341<br>
Telugu-Titans:0.4341<br>
patna-pirates: 0.3964<br>
purani-paltan: 0.39<br>
jaipur-pinkpanthers: 0.4209<br>
Gujrat-fortuneGiants: 0.36<br>
Hariyana-steelers: 0.36<br>
Tamil-Thalivas:0.36<br>

Even though Telugu-Titans and U-mumba have highest successful scores. However considering the fact that Telugu-titans pts might not make them elligible for playoffs so U-mumba might have a shot at the playoffs and as a result their score might improve.
Thus considering this aspect it can be assumed that <b>U-mumba</b> will have hisghest successful Tackle% in season 7.

#### e.Predict the team with the highest super-performance total.<br>

SPT total is calculated as per the following :
S.P.T. = Total number of super-raids in the tournament + total number of super-tackles in the tournament
+ total number of all-outs inflicted in the tournament - total number of all-outs conceded in the tournament.<br>
Using the above formulae following data is collected:<br>
Delhi Dabang : 25<br>
Bengal warriors: 36<br>
UP-Yoddha: 16<br>
Bengaluru-bulls: 26<br>
U-mumba: 25<br>
Telugu-Titans:23<br>
patna-pirates: 36<br>
purani-paltan: 16<br>
jaipur-pinkpanthers: 30<br>
Gujrat-fortuneGiants: 9<br>
Hariyana-steelers: 10<br>
Tamil-Thalivas:1<br>

From the data we can see that both Bengal-Warriors and Patna-Pirates have the same SPT score of 36. However, since Patna-Pirates are not going to qualify for the playoffs and Bengal is definitely going to the playoffs hence there is a good chance that for Bengal this score is going to increase(just by getting a single super raid the point of bengal will increase by 1).<br>
Hence we can conclude that Bengal-Warriors will have the highest super-performance total in season 7.

#### f.Predict the player with the highest SUCCESSFUL RAID percentage.<br>
The successful raid percentage for a player is expressed as (Successful raids/Total raids)x100.<br>
Now this ratio is going to decrease significantly as the player playes more matches. Thus we went with an unorthodox approach were we tried finding the player who had played a minimum no of matches and successfully raided. Upon using the this assumption we fond that the no of players fitting is very less and one such player was :BALRAM playing for Delhi, haing a successful raid % of 100% .

#### g.Predict the player with the highest SUCCESSFUL TACKLE percentage.<br>
FAZEL ATRACHALI will have the highest Tackle percentage(as of now it is around 55%). Since both u-mumba and Telugu-Titans both have very high successful tackle percentages, hence it was worth to look into the players of these teams. Upon consulting the player data in terms of highest succesful tackle FAZEL ATRACHALI occupies the 3rd position. 



