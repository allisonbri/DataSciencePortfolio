# My Projects  

  
##  **<ins>Transportation and Art Museums in North Carolina Counties</ins>**
  
  In this project I examine whether transportation patterns are related to the types of museums found in North Carolina counties. Using county-level data, I compare how residents commute (for example, by car, public transit or walking) with the percentage of each county's museums that are classified as art museums. The goal is to see whether counties dominated by a particular mode of transportation tend to have a higher or lower share of art museums.  


<details markdown="1">
  <summary>Read more</summary>  
  

[Link to code](PortfolioProject1.ipynb)  

**Overview:**  
This project examines whether transportation patterns are related to the types of museums found in North Carolina counties. Using county-level data, it compares how residents commute (for example, by car, public transit or walking) with the percentage of each county's museums that are classified as art museums. The goal is to see whether counties dominated by a particular mode of transportation tend to have a higher or lower share of art museums.  

**Research Question and dataset:**  

Is there a relationship between the most common mode of transportation used in different North Carolina counties and the percentage of museums in those counties that are classified as art museums?  

https://api.census.gov/data/2024/acs/acs1?get=NAME,B01001_001E&for=county:*&in=state:37&key={api_key}  
Unit of analysis: county  
44 rows and 8 columns used with 26 missing values in columns: Total_Transp_By_Vehicles_Available	Total_Public_Transp	No_Vehicle_Available    and   Walks  

https://museumsdatabase.com/  
Anthropic. (2026). Claude Sonnet 5 [Large language model]. https://claude.ai  
Artificial Intelligence was used to help create a csv dataset from the museum database website.  
Unit of analysis: county  
44 rows and 3 columns: percent_art_museum        museum_count	art_museum_count  

**Context:**  
Museum types may reflect the character of the communities around them. Counties where nearly everyone drives tend to be rural or suburban, while counties with more transit or walking tend to be denser and more urban, where arts institutions are often concentrated. This project asks whether car reliance is associated with the share of a county's museums that are art museums. The analysis is correlational and cannot show causation.  

<ins>Key Variables</ins>  

<mark>Car usage</mark>  

Concept: How much a county's residents rely on private cars rather than other modes of transportation.  
Measure: Number of workers who commute by personal car, truck, or van.  

<mark>Percentage of art museums</mark>  

Concept: How strongly a county's museums lean toward art rather than other types.  
Measure: (art museums ÷ total museums) × 100  
Art museum is defined as the museum database labels the museums, it is not based on the name of the museum.   

<mark>Walks</mark>  

Concept: How much workers in a county walk rather than rely on other modes of transportation.  
Measure: Number of workers who walk to work  

Controls: population density  

**Data Cleaning Process:**  

City base museum data collected from the museum website was grouped by county with the assistance of Claude (Anthropic, 2026) so that it could be merged with the API dataset. To make the two datasets compatible, I split the NAME column in the API data so its values matched the county names in the museum CSV. Then I filtered the museum data to only keep the counties present in the API data, so both datasets contained the same set of counties. Finally, I merged the datasets on county names, which produced a single table ready for plotting.  

**Findings:**  

<img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/345c4419-53c4-4d90-a37e-6360b48547e8" /> <img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/eea22c69-3f2a-46f1-b954-08de4ddffadf" /> <img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/57541c95-ce15-4d72-9353-0077564531d4" /> <img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/ed397797-09f5-4444-9ce3-89c50d8ffca5" />


There is an indirect relationship, however there is not a strong direct correlation. The amount of art museums in a county appears to be more related to population size rather than transportation method. This result is likely due to the size of counties and its relationship with funding and tourism.



**Ethics and Limitations:**  
We are missing some possible confounding variables like tourism and county land area which could skew our results or leave aspects unaccounted for. There is also a large amount of missing values in the data which could be indicative of a possible sampling bias and therefore may be skewing the findings. As well there are some major outliers as seen in the visualizations that the conclusion does not address.  

**Sources:**  
Bingham-Hall, J., & Kaasa, A. (2011). New cultural infrastructure: Can we design the conditions for culture?  
Smith, J. K. (2014). The museum effect: How museums, libraries, and cultural institutions educate and civilize society. Bloomsbury Publishing PLC.  
Teuguia, F. (2025). Navigating the legal landscape of APIs: Innovations, strategies for sustainable, inclusive, and secure digital ecosystems. World Futures, 81(4), 255-290.  
Anthropic. (2026). Claude Sonnet 5 [Large language model]. https://claude.ai  
Artificial Intelligence was used to help create a csv dataset from the museum database website.  


</details>  

***
  
##  **<ins>Predicting User Ratings with Machine Learning</ins>**  
  
  I trained two machine learning models to predict the average user rating of 1,982 top-ranked board games from BoardGameGeek, using only how complex it is, how long it takes, how many people can play, and when it was published. Both the Linear Regression model and the Decision Tree were able to beat a "just guess the average" baseline by a wide margin and explain about 40% of the differences in ratings.  


<details markdown="1">
  <summary>Read more</summary>  



[Link to code](PortfolioProject2.ipynb)  

### **Overview:**  

  I trained two machine learning models to predict the average user rating of 1,982 top-ranked board games from BoardGameGeek, using only basic facts about each game: how complex it is, how long it takes, how many people can play, and when it was published. Both models beat a "just guess the average" baseline by a wide margin and explain about 40% of the differences in ratings. Complexity and release year mattered most. The remaining 60% comes from things this dataset does not contain, such as theme, artwork, and the quality of the rules.  


### **Research Question and dataset:**  

Can a board game's basic characteristics predict how highly its players rate it?  

Target variable: avg_rating; the average score (on a 1 to 10 scale) that BoardGameGeek users give a game.  

The task at hand is regression because we are dealing with continuous numerical values.

**Data Description:**  
Source: [BoardGameGeek data from Kaggle](https://www.kaggle.com/datasets/mattadamhouser/ranked-board-game-data-from-boardgamegeek)  
Unit of analysis: Each row is information on 1 board game  
Size: 2,000 rows and 17 columns. The file contains the *top* 2,000 ranked games, not every game on the site.  
Target: avg_rating.  
Available features: min_players, max_players, avg_time (also min_time and max_time), weight (complexity), year, and age (recommended minimum age). The file also includes identifiers (name, bgg_url, game_id, designer) and ranking columns (rank, geek_rating, num_votes, owned).  
Missing values: Only designer has missing values (3 rows), and I do not use it. There are no duplicate rows.  
Restrictions that affect the data: Because only the top 2,000 games are included, ratings are squeezed into a narrow range. The raters are self-selected BGG members. The dataset has no information on theme, mechanics, artwork, price, or component count.  


**Features included and excluded:**  
*Included:*  
weight, log_time, min_players, max_players_capped, year.  

*Excluded, and why:*  
geek_rating and rank are calculated from the rating itself. Using them would hand the model the answer.  
num_votes and owned measure how popular a game became after release. Address how the game was received, not traits of the game.  
min_time, and max_time: in this file avg_time and max_time are identical, so I use only the log of avg_time.  
name, bgg_url, game_id, and designer are identifiers, not game traits.  
age (recommended minimum age) was left out to keep the model simple and focused on the four traits in my question. Could look into it for further analysis.  



### **Context:**  

**Why it matters:**  
Making a board game takes a lot of time and money, and ratings influence what gets bought or talked about. Knowing which traits go along with high ratings, and how much of a rating they can explain, tells us how far the numbers take us before judgment, taste, and testing have to take over.  

**Who might benefit:**  
Game designers and publishers deciding what kind of game to develop.  
Players and retailers trying to guess whether an unfamiliar game will be well received.  
Students of data science (like me), since a rating model is a good, low-stakes setting for practicing the full machine learning workflow.  

**What to know:**  
BoardGameGeek (BGG) users rate games from 1 to 10 and also rate their weight 1 to 5 for how complex a game is (1 is light, like a family game; 5 is very intricate). A data analysis of BGG by Vatvani (n.d.) found a clear positive relationship between complexity and rating. The author addresses that this does not mean complex games are inherently better, because complex games specifically appeal to the kind of person who uses BGG. My results below show the same pattern, so we should treat it as more of a feature of this community, not as a causational relationship.  

  

### **Data Cleaning:**  
 
- Removed games with avg_time == 0 or max_players == 0  
*A playtime or player count of zero means "unknown," not zero.*  
- Kept only games published in 1950 or later  
*Ancient games such as Go and Chess don't have a meaningful publication year, and a value like -2200 would distort a model looking for straight-line patterns.*  
- Log-transformed playtime (log_time)  
*Playtime is so skewed that a few 10,000-minute games would dominate. The logarithm pulls extremes in and keeps the order of games.*  
- Capped max players at 10 (max_players_capped)  
*A few games list up to 100 players, which would pull the model toward those extreme outliers.*  

In total, 18 of 2,000 games were removed (1,982 remain). No categorical variables needed encoding, and I did not scale features because the model I will be using does not require it.  


### **Data Exploration:**  

*Summary Stats after data cleaning:*  

<img width="550" height="250" alt="CleanSummaryStatsProject2" src="https://github.com/user-attachments/assets/21669753-dafe-4380-9487-40b3ed007387" />  

Ratings cluster around 7.37. Because the file contains only top-ranked games, there are almost no poorly rated games, and the entire spread is about 2.7 rating points. This range does make small differences between games harder to predict, and any relationship I find is probably weaker than it would be across all board games. A standard deviation of only 0.44 also gives me a useful information for judging prediction errors later.  


**Observing Relationships**

<img width="550" height="480" alt="image" src="https://github.com/user-attachments/assets/7570dc4b-948a-412e-bc2f-91dce0a317da" />  

From the graphs we can observe that complexity vs rating and year vs rating appear to have the strongest positive linear relationships. Playtime vs rating has a subtle positive linear relationship and minimum players vs rating appears to have a negative linear relationship.  


I used Spearman correlation because it handles curved relationships and outliers better than the more common Pearson version.  

<img width="590" height="160" alt="image" src="https://github.com/user-attachments/assets/3476fe1f-9289-4f1c-a2c5-65ea07daa723" />  


**What stands out**  
Complex games are rated higher. Newer games are rated higher. Games that need more players at minimum are rated lower, and games that can be played solo or by one person score a little higher. Complexity and playtime overlap heavily (correlation 0.83 between them): long games tend to be heavy games. This multicollinearity may make it hard for the model to say which of the two is affecting the rating score. Year is nearly independent of complexity (about -0.01) and of playtime (about -0.02). So year is not just a stand-in for complexity, it adds separate information.  


### **Training Strategy:**  

**80/20 split.** I trained on 1,585 games and set aside 397 games as a test set. Scoring on the held-out games tells us how the model would do on games it hasn't seen.  
**Shuffled split.** The file is sorted by rank, so an unshuffled split would put mostly top-ranked games in one group.  
**Cross-validation.** To choose the decision tree's depth, I used 5-fold cross-validation on the training set only: the training data is cut into five parts, the model trains on four and is scored on the fifth, and this rotates five times.  
**Preventing data leakage.** The test set was never used to make a modeling decision. Depth was chosen using only training data. While cleaning the data I removed placeholder rows, capped values, and log transformed necessary columns.  

### **Model Development:**  

**Baseline:** The baseline predicts the average training rating (7.37) for every game  

**Model 1:** Linear regression. It fits the best straight-line formula, rating = intercept + (c1 × weight) + (c2 × log_time) + .... I chose it because it is the standard first regression model and its coefficients have plain-language meanings. Its limitation is that it assumes every effect is a straight line.   

**Model 2:** Decision tree. It splits games into groups with yes/no questions (for example "is weight above 2.8?") and predicts the average rating of each final group. I chose it because it works very differently from linear regression, so comparing them answers whether the relationship is mostly straight lines, or if flexibility helps? It can capture curves and interactions automatically. Its limitation is overfitting.  

**Fairness of the comparison:** both models used the same training and test games, the same five features, and the same three metrics.  

**Metrics:**  
R² is the share of the differences in ratings that the model explains. A score of 0 means no better than guessing the average, and 1 means perfect.  
MAE (mean absolute error) is the average size of the miss, in rating points.  
RMSE (root mean squared error) is similar but punishes big misses more heavily, also in rating points.  

These fit a regression problem with a continuous target.  

### **Results:**  


<img width="270" height="110" alt="image" src="https://github.com/user-attachments/assets/42d2ac68-7901-4d58-b318-37857fae1ff5" />  



<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/b05b86d3-24ea-49d4-b5da-8a5e5379f7f8" />  


Both models clearly beat the baseline. R² rises from about 0 to about 0.40, and the average misses falls from 0.36 to 0.28 rating points. The fact that the decision tree barely beats a straight-line model suggests the relationships in this data are mostly linear. Most of what the features can explain, both models find.  


**What the linear model learned:**  
Complexity (weight)	+0.219	Each extra point of complexity goes with a rating about 0.22 points higher  
Year +0.019	Each year later goes with about 0.02 points higher  
Playtime (log_time)	+0.095	Doubling playtime goes with about 0.07 points higher  
Min players	-0.019	Essentially no effect  
Max players (capped)	-0.005	Essentially no effect  


**The tree agrees:**  
Complexity (57%) and year (39%) account for almost all of its predictive power, with playtime at 1%, max players at 2.5%, and min players at 0.2%. Playtime looks important in the correlation table (0.47) but contributes little once complexity is known, because the two overlap so much (0.83).  

### **Where the model struggles:**  

The model plays it safe. Games rated above 8.0 were underestimated by an average of 0.53 points, and games rated below 6.8 were overestimated by an average of 0.37 points. Mid-range games (7.2 to 7.6) were predicted almost perfectly on average (error about 0.02). The model has learned the typical game but cannot recognize the extraordinary ones.  

*The biggest misses:*  

<img width="550" height="290" alt="image" src="https://github.com/user-attachments/assets/e7fde7ef-dff5-4016-8e36-df1e8cce23f2" />  

Several of the high misses are recent, large-scale, campaign-style games, which may attract more fan groups. Several of the low misses are older, mass-market, or licensed games that are well known and widely played, so their ratings may reflect disappointment or a broader audience than the typical BGG rater. The model leaves out theme, fan community, art, price, component count, and rules quality which could explain some outliers in the data and the majorly missed predictions.  

### **Model Conclusion:**  

**Can conclude:**  

Complexity and release year are the two most useful predictors in this dataset, and playtime and player counts add a little once those two are known.
The five basic features together explain roughly 40% of the variation in ratings among top-ranked games.  

**Cannot conclude:**  

- That making a game more complex will cause a higher rating. This is an association. The BGG audience likes complex games, so complexity and rating rise together for this audience.  
- That these patterns hold for all board games, for casual players, or for games outside the top 2,000.  
- That newer games are actually better. They may be rated higher because of who rates them and when, or because older games only stayed in the top 2,000 if they were exceptional.  


So before relying on this model know that it predicts how BoardGameGeek hobbyists rate highly ranked games, using five basic traits. It describes patterns, it does not prove causes, and its errors are largest for the very best and very worst games.  

### **Ethics and limitations:**  

**Biases and gaps in the data:**  
Selected sample. Only the top 2,000 ranked games are included, so poorly rated games are missing. This compresses the range of ratings and likely understates how much these features matter in general.  
Self-selected raters. BGG users are not just the general public. Self-selection can make average ratings a poor approximation for actual quality.
Complexity is itself a rating. weight is a score given by users, not a measurement, so it reflects opinion and experience.  
Missing information. No theme, mechanics, artwork, price, or component count, which probably explain a large amount of the remaining 60% of unexplained variation.  


**Who could be affected by wrong predictions, and how?**  
A publisher or designer who relied on the model could under-invest in a game that would be a hit (like Oathsworn, which the model underestimates by more than a full point) or over-invest in one that would disappoint (like Axis & Allies, which it overestimates).  
A model that rewards complexity could nudge designers toward heavier games, even though the wider public may prefer lighter ones.  
Consumers would be misled if the predicted rating were treated as a quality guarantee.  
Because the model pulls predictions toward the middle, it is the worst for deciding the games people care about most: the major hits and the disappointments.  

**Is it appropriate for real-world decisions?**  
No, not on its own. A typical error of 0.28 points is large compared with the 0.44-point spread of ratings, and the model cannot see most of what makes a game good. It is reasonable as a rough starting point for discussion or as some input but not as a tool for deciding which games to publish or buy.  


**Next steps I would explore:**  
Add game mechanics, categories, and themes and test whether they explain the missing 60%.  
Include games outside the top 2,000 so the full range of ratings is shown.  
Add the recommended minimum age and test interactions like complexity × year.  
Try other models such as random forests or gradient boosting.  

### **References:**  

Matt Adam-Houser. (2023). Ranked Board Game Data from BoardGameGeek. https://www.kaggle.com/datasets/mattadamhouser/ranked-board-game-data-from-boardgamegeek  

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., Blondel, M., Prettenhofer, P., Weiss, R., Dubourg, V., Vanderplas, J., Passos, A., Cournapeau, D., Brucher, M., Perrot, M., & Duchesnay, E. (2011). Scikit-learn: Machine learning in Python. Journal of Machine Learning Research, 12, 2825-2830.  

Vatvani, D. (n.d.). Complexity bias in ratings [Blog post]. https://dvatvani.github.io/BGG-Analysis-Part-2.html  

Wachs, J., & Vedres, B. (2021). Does crowdfunding really foster innovation? Evidence from the board game industry. Technological Forecasting and Social Change, 168, Article 120747. https://ideas.repec.org/a/eee/tefoso/v168y2021ics0040162521001797.html  

Anthropic. (2026). Claude Sonnet 5 [Large language model]. https://claude.ai  
Artificial Intelligence was used to assist in creating and interpreting the model code. All results were thoroughly scanned and adjusted to ensure no robot ignorance is present. So, any discrepancies or mistakes found in this project are human.

</details>

***
