# My Projects
  
  **<ins>Transportation and Art Museums in North Carolina Counties</ins>**
  
  This project examines whether transportation patterns are related to the types of museums found in North Carolina counties. Using county-level data, it compares how residents commute (for example, by car, public transit or walking) with the percentage of each county's museums that are classified as art museums. The goal is to see whether counties dominated by a particular mode of transportation tend to have a higher or lower share of art museums.  


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




  
  **<ins>Predicting User Ratings with Machine Learning</ins>**
  
  I trained two machine learning models to predict the average user rating of 1,982 top-ranked board games from BoardGameGeek, using only basic facts about each game: how complex it is, how long it takes, how many people can play, and when it was published. Both models beat a "just guess the average" baseline by a wide margin and explain about 40% of the differences in ratings. Complexity and release year mattered most. The remaining 60% comes from things this dataset does not contain, such as theme, artwork, and the quality of the rules.  


<details markdown="1">
  <summary>Read more</summary>

[Link to code](PortfolioProject2.ipynb)  

**Overview:**  
I trained two machine learning models to predict the average user rating of 1,982 top-ranked board games from BoardGameGeek, using only basic facts about each game: how complex it is, how long it takes, how many people can play, and when it was published. Both models beat a "just guess the average" baseline by a wide margin and explain about 40% of the differences in ratings. Complexity and release year mattered most. The remaining 60% comes from things this dataset does not contain, such as theme, artwork, and the quality of the rules.  

**Research Question and dataset:**  
Can a board game's basic characteristics predict how highly its players rate it?  

Target variable: avg_rating, the average score (on a 1 to 10 scale) that BoardGameGeek users give a game.  

Task type: Regression, because the target is a continuous number (for example 7.34), not a category.  

Data Description  
Source: BoardGameGeek data from the file basic_data_2023.csv. [Add the exact citation and link for where you downloaded it. See the References section.]
Unit of analysis: One row is one board game.  
Size: 2,000 rows and 17 columns. The file contains the top 2,000 ranked games, not every game on the site.  
Target: avg_rating.  
Available features: min_players, max_players, avg_time (also min_time and max_time), weight (complexity), year, and age (recommended minimum age). The file also includes identifiers (name, bgg_url, game_id, designer) and popularity or ranking columns (rank, geek_rating, num_votes, owned).  
Missing values: Only designer has missing values (3 rows), and I do not use it. There are no duplicate rows.  
Restrictions that affect the data: Because only the top 2,000 games are included, ratings are squeezed into a narrow range (see Section 4). The raters are self-selected BGG members. The dataset has no information on theme, mechanics, artwork, price, or component count.  



Features included and excluded  

Included (5): weight, log_time, min_players, max_players_capped, year.  

Excluded, and why:  

geek_rating and rank are calculated from the rating itself. Using them would hand the model the answer, which is called data leakage.  
num_votes and owned measure how popular a game became after release. They are consequences of how the game was received, not traits of the game.  
avg_time, min_time, and max_time: in this file avg_time and max_time are identical, so I use only the log of avg_time.  
name, bgg_url, game_id, and designer are identifiers, not game traits.  
age (recommended minimum age) was left out to keep the model simple and focused on the four traits in my question. It is a natural candidate for future work.  

**Context:**  
Who might benefit:  

Game designers and publishers deciding what kind of game to develop.  
Players and retailers trying to guess whether an unfamiliar game will be well received.  
Students of data science (like me), since a rating model is a good, low-stakes setting for practicing the full machine learning workflow.  

Why it matters: Making a board game takes a lot of time and money, and ratings strongly influence what gets bought and talked about. Knowing which measurable traits go along with high ratings, and just as importantly how much of a rating they can explain, tells us how far the numbers alone can take us before judgment, taste, and playtesting have to take over.  

Note on the research question: The dataset has no column for the number of physical components, so I study four game traits that are available: complexity, player counts, playtime, and publication year.  

What a reader needs to know: BoardGameGeek (BGG) is the largest online database and community for hobby board games. Users rate games from 1 to 10 and also rate their weight, a 1 to 5 score for how complex a game is (1 is light, like a family game; 5 is very heavy). Wachs and Vedres (2021) describe BGG as the online hub for board game enthusiasts and used its data to study innovation in the industry. Their regression models treat a game's complexity rating, playing time, player counts, and minimum age as basic descriptive features that need to be accounted for. That is the same set of features I use here.  

What earlier work suggests about the variables:  
Complexity and ratings. A data analysis of BGG by Vatvani (n.d.) found a clear positive relationship between complexity and rating. The author cautions that this does not mean complex games are inherently better, because complex games disproportionately appeal to the kind of person who uses BGG. My results below show the same pattern, so I treat it as a feature of this community and not as a law of game design.  

**Data Exploration:**  

Summary statistics (after cleaning, 1,982 games)  
Variable	Mean	Std. dev.	Min	Median	Max  
Average rating	7.37	0.44	6.38	7.33	9.08  
Complexity (weight)	2.52	0.81	1.02	2.45	4.83  
Playtime (minutes)	99.4	318.8	2	60	12,000  
Min players	1.82	0.71	1	2	8  
Max players	5.0	6.2	1	4	100  
Year published	2012.9	8.4	1959	2015	2023  

Ratings are only mildly right-skewed (skewness 0.49) and cluster around 7.3. Because the file contains only top-ranked games, there are almost no poorly rated games, and the entire spread is about 2.7 rating points. This range restriction matters: it makes small differences between games harder to predict, and any relationship I find is probably weaker than it would be across all board games. A standard deviation of only 0.44 also gives me a useful yardstick for judging prediction errors later.  


***Put pictures of graphs and such here***  

I used Spearman correlation because it handles curved relationships and outliers better than the more common Pearson version.  

Feature	Correlation with rating  
Complexity (weight)	+0.53  
Playtime (log_time)	+0.47  
Year published	+0.42  
Min players	-0.28  
Max players (capped at 10)	-0.17  


What stands out:

Complex games are rated higher. Games with a complexity weight of 2 or less average 7.10, games from 3 to 4 average 7.65, and the 86 games above 4 average 7.93.  
Newer games are rated higher. Games published before 1990 average 7.12, while games from 2021 to 2023 average 7.78.  
Games that need more players at minimum are rated lower, and games that can be played solo or by one person score a little higher.  
Complexity and playtime overlap heavily (correlation 0.83 between them): long games tend to be heavy games. This is called multicollinearity, and it makes it hard for a model to say which of the two is "responsible."  
Year is nearly independent of complexity (about -0.01) and of playtime (about -0.02). So year is not just a stand-in for complexity. It adds separate information.  


Outliers and odd values  
Three games have a playtime of 0 minutes and one has a max player count of 0. These are placeholders for "unknown," not real values.  
Playtime is extremely skewed: the median is 60 minutes, but the longest game is listed at 12,000 minutes (skewness about 30).  
Thirty-five games list more than 10 maximum players, up to 100.  
Sixteen games are dated before 1950, including Go (year -2200), Chess (1475), and two games listed with year 0. These dates are not true publication years.  

**Data Cleaning:**  

Cleaning  
Step      Why  
Removed games with avg_time == 0 or max_players == 0    A playtime or player count of zero means "unknown," not zero.  
Kept only games published in 1950 or later      Ancient games such as Go and Chess do not have a meaningful publication year, and a value like -2200 would distort a model that looks for straight-line patterns.  
Log-transformed playtime (log_time)      Playtime is so skewed that a few 10,000-minute games would dominate. The logarithm pulls the extremes in while keeping the order of games.  
Capped max players at 10 (max_players_capped)      A few games list up to 100 players, which would pull a straight-line fit toward those extremes.  

In total, 18 of 2,000 games were removed (1,982 remain). No categorical variables needed encoding, and I did not scale features because the model I will be using does not require it.  

**Training Strategy:**  

80/20 split. I trained on 1,585 games and set aside 397 games as a test set that the models never see during training. Scoring on those held-out games tells me how the model would do on games it has never encountered.  
Shuffled split. The file is sorted by rank, so an unshuffled split would put mostly top-ranked games in one group. The split shuffles the rows first.
Cross-validation for tuning. To choose the decision tree's depth, I used 5-fold cross-validation on the training set only: the training data is cut into five parts, the model trains on four and is scored on the fifth, and this rotates five times.  
Preventing data leakage. (1) Leaky columns are excluded. (2) The test set was never used to make a modeling decision. Depth was chosen using only training data. (3) Cleaning rules (removing placeholder rows, capping, log transform) use fixed rules instead of statistics computed from the test set.  

**Model Development:**  

Baseline: The baseline predicts the average training rating (about 7.37) for every game

Model 1: Linear regression. It fits the best straight-line formula, rating = intercept + (c1 × weight) + (c2 × log_time) + .... I chose it because it is the standard first regression model and its coefficients have plain-language meanings. Its limitation is that it assumes every effect is a straight line and that effects simply add up.  

Model 2: Decision tree. It splits games into groups with yes/no questions (for example "is weight above 2.8?") and predicts the average rating of each final group. I chose it because it works very differently from linear regression, so comparing the two answers a real question: are the relationships mostly straight lines, or does flexibility help? It can capture curves and interactions automatically, and it can be drawn as a flowchart. Its limitation is overfitting, since a deep tree can memorize the training data.  

Fairness of the comparison: both models used the same training and test games, the same five features, and the same three metrics.  

Metrics  
R² is the share of the differences in ratings that the model explains. A score of 0 means no better than guessing the average, and 1 means perfect.  
MAE (mean absolute error) is the average size of the miss, in rating points. It is the easiest to explain to a non-technical reader.  
RMSE (root mean squared error) is similar but punishes big misses more heavily, also in rating points.  

These fit a regression problem with a continuous target.  

**Results:**  

Results on the held-out test set (397 games)  
Model	R²	MAE	RMSE  
Baseline (average)	-0.003	0.362	0.453  
Linear regression	0.399	0.280	0.351  
Decision tree (depth 5)	0.423	0.278	0.344  

Both models clearly beat the baseline. R² rises from about 0 to about 0.40, and the typical miss falls from 0.36 to 0.28 rating points, a reduction of roughly 23%.  The fact that the decision tree barely beats a straight-line model suggests the relationships in this data are mostly linear. Most of what the features can explain, both models find.  


What the linear model learned:  
Feature	Coefficient	Meaning (holding other features fixed)  
Complexity (weight)	+0.219	Each extra point of complexity goes with a rating about 0.22 points higher  
Year	+0.019	Each year later goes with about 0.02 points higher (about 0.19 per decade)  
Playtime (log_time)	+0.095	Doubling playtime goes with about 0.07 points higher  
Min players	-0.019	Essentially no effect  
Max players (capped)	-0.005	Essentially no effect  


The tree agrees: complexity (57%) and year (39%) account for almost all of its predictive power, with playtime at 1%, max players at 2.5%, and min players at 0.2%. Playtime looks important in the correlation table (0.47) but contributes little once complexity is known, because the two overlap so much (0.83).  

**Where the model struggles:**  

It plays it safe. Games rated above 8.0 were underestimated by an average of 0.53 points, and games rated below 6.8 were overestimated by an average of 0.37 points. Mid-range games (7.2 to 7.6) were predicted almost perfectly on average (error about 0.02). The model has learned the typical game but cannot recognize the extraordinary ones.  

The biggest misses:  

Rated much higher than predicted: Strat-O-Matic Baseball (1962; actual 7.83, predicted 6.34), Oathsworn: Into the Deepwood (2022; 9.08 vs. 7.81), Core Space, Clank!: Legacy, ISS Vanguard, and Aeon's End: Outcasts.  
Rated much lower than predicted: Axis & Allies (6.69 vs. 7.46), Rise to Nobility, Fallout, Talisman: Revised 4th Edition, Leonardo da Vinci, and Exit: The Game.  

Several of the high misses are recent, large-scale, campaign-style games, which may attract devoted fan communities. Several of the low misses are older, mass-market, or licensed games that are well known and widely played, so their ratings may reflect disappointment or a broader audience than the typical BGG hobbyist  

The model leaves out theme, fan community, art, maker, and rules quality which could explain some outliers in the data and majorly missed predictions.  

**Model Conclusion:**  

Can conclude:  

Complexity and release year are the two most useful predictors in this dataset, and playtime and player counts add little once those two are known.
The five basic features together explain roughly 40% of the variation in ratings among top-ranked games.  

Cannot conclude:  

That making a game more complex will cause a higher rating. This is an association. The BGG audience likes complex games, so complexity and rating rise together for this audience.  
That these patterns hold for all board games, for casual players, or for games outside the top 2,000.  
That newer games are actually better. They may be rated higher because of who rates them and when (for example, enthusiastic early reviewers), or because older games only stayed in the top 2,000 if they were exceptional.  

**Ethics and limitations:**  

Biases and gaps in the data:  

Selected sample. Only the top 2,000 ranked games are included, so poorly rated games are missing. This compresses the range of ratings and likely understates how much these features matter in general.  
Self-selected raters. BGG users are hobby gamers, not the general public. Research on online reviews (Hu et al., 2009) shows that self-selection can make average ratings a poor proxy for true quality, and that applies here.  
Complexity is itself a rating. weight is a score given by users, not a measurement, so it reflects opinion and experience.  
Missing information. No theme, mechanics, artwork, price, or component count, which probably explain a large share of the remaining 60% of unexplained variation.  

Who could be affected by wrong predictions, and how?  

A publisher or designer who relied on the model could under-invest in a game that would be a hit (like Oathsworn, which the model underestimates by more than a full point) or over-invest in one that would disappoint (like Axis & Allies, which it overestimates).
A model that rewards complexity could nudge designers toward heavier games, even though the wider public may prefer lighter ones. This would reinforce the bias of the BGG audience.
Consumers would be misled if the predicted rating were treated as a quality guarantee.
Because the model pulls predictions toward the middle, it is worst for exactly the games people care about most: the exceptional hits and the disappointments.

Is it appropriate for real-world decisions? No, not on its own. A typical error of 0.28 points is large compared with the 0.44-point spread of ratings, and the model cannot see most of what makes a game good. It is reasonable as a rough starting point for discussion or as one input among many (playtesting, market research, designer judgment), but not as a tool for deciding which games to publish or buy.


Next steps I would explore:  

Add game mechanics, categories, and themes (BGG lists these) and test whether they explain the missing 60%.  
Include games outside the top 2,000 so the full range of ratings is represented.  
Add the recommended minimum age and test interactions such as complexity × year.  
Try other models such as random forests or gradient boosting, and use cross-validation on the full pipeline for more stable comparisons.  

What users should understand before relying on this model It predicts how BoardGameGeek hobbyists rate highly ranked games, using five basic traits. It describes patterns, it does not prove causes, and its errors are largest for the very best and very worst games.  

**References:**
BoardGameGeek. (n.d.). BoardGameGeek. https://boardgamegeek.com
* Fill in the author , year, and the page where I downloaded the file,  
ex: Author/Organization. (Year). basic_data_2023.csv [Data set]. Publisher or site. URL  

Hu, N., Zhang, J., & Pavlou, P. A. (2009). Overcoming the J-shaped distribution of product reviews. Communications of the ACM, 52(10), 144-147. https://doi.org/10.1145/1562764.1562800

James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). An introduction to statistical learning: With applications in R (2nd ed.). Springer. https://doi.org/10.1007/978-1-0716-1418-1

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., Blondel, M., Prettenhofer, P., Weiss, R., Dubourg, V., Vanderplas, J., Passos, A., Cournapeau, D., Brucher, M., Perrot, M., & Duchesnay, E. (2011). Scikit-learn: Machine learning in Python. Journal of Machine Learning Research, 12, 2825-2830.

Vatvani, D. (n.d.). Complexity bias in ratings [Blog post]. https://dvatvani.github.io/BGG-Analysis-Part-2.html

Wachs, J., & Vedres, B. (2021). Does crowdfunding really foster innovation? Evidence from the board game industry. Technological Forecasting and Social Change, 168, Article 120747. https://ideas.repec.org/a/eee/tefoso/v168y2021ics0040162521001797.html

</details>
