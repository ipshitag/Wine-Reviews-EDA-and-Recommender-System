# Wine-Reviews-EDA-and-Recommender-System

K NEAREST WINES
Abstract
In this project, exploratory data analysis is done on the wine dataset[1] and tried to fit a model to it. While doing the study, I will try to find how the variables are connected. In the model building, I have used sentiment analysis and k nearest algorithm with brute and taken a similarity metric as cosine. I have also tried to hard code a recommender system and have analyzed the problem in doing so.

##	Introduction
For a long time, wine has been a part of human culture. Wines have always been a topic of discussion, and thus the wine industry has also flourished. With an increase in demand for wine, the production has also increased. Furthermore, from such a large variety of collections, people like to choose the reviewed wine because no one wants to invest their money in something they will not like. Some interesting cases portray how critical wine reviewing has become. One of those is a man insuring his nose for $8mm in 2008[2].
Here, in this project, I will try to understand whether the description of a wine, as given by an expert, can be used to understand the points received by it. Moreover, I will try to plot a sentiment analysis plot of those descriptions. Along with that, I will try to make a recommender system using the K Nearest Algorithm, taking points, variety, and the province as attributes.

We will try to find answers to some critical questions, like 
1.	Which are the most reviewed country and most reviewed variety?
2.	Is there any relationship between the price and points received?
3.	What are some characteristics of wine, country-wise?
4.	What are some common terms appearing in the lowest-rated and highest rated wine?
5.	Can we create a recommender system?
6.	What should a company keep in mind to get good reviews?
7.	Is there any relationship between points and any other attributes?
8.	Which variety of grape will be best to make wine?
9.	Referring to which reviewer will be beneficial?
10.	Should we go with what is familiar or with something less standard in terms of variety?


##	Data
The dataset consists of 129971 rows, in 13 columns. The dataset was scrapped from a famous wine magazine name Winemag[3]. It is a dataset consisting of different wines, along with their names, province, tasters name, variety, points collected, price, and other variables.
Here are a few examples of descriptions: 
"Fragrant notes of tangerine and yuzu peel abound on this citrusy dry Riesling. The palate is cutting and fresh, full of juicy white grapefruit and lime flavors. Light-bodied yet satisfyingly thirst-quenching, it finishes long with invigorating minerality." [4]
-	Von Schleinitz 2015 Apollo Dry Riesling (Mosel)
"An earthy, nutty aroma and flavor come through the intense sweetness and full body of this dessert-style wine. It goes for earthy complexity rather than obvious fruit flavors, and tastes high in sugar and alcohol." [5]
-	Terre Rouge 2013 Vin Doux Naturel Muscat Blanc à Petits Grains (Shenandoah Valley (CA))

Further, we get different pieces of information
1. Title: Name of wine
2. Variety: Type of grape that is used in the wine.
3. Country: Country of origin of the wine.
4. Province: The region within the state in which the wine was produced. The specificity of the areas ranged widely.
5. Region 1 and 2: A more specific information about the location of the wine, where the wine was produced.
6. Price: The cost of the wine.
7. Points: The rating of the wine it ranges from 80 to 100
8. Taster Name: Name of the reviewer who reviewed the wine

##	Exploratory Data Analysis
In my EDA, I have first cleaned my data and then tried to explore different features of the dataset.

3.1. Data Cleaning
At first, I dropped all the duplicates in the data. Next, I checked whether I had null values or not. Most of my null values were in price,taster_name,taster_twitter_handle, and designation. To deal with this, I filled the price with the median value of the price column and dropped the unwanted columns, including designation and taster_twitter_handle. Then I dropped the remaining null columns.

3.2 Feature-wise analysis
In the dataset we have, <br>
•	country: 		 43 distinct values<br>
•	description:       	 94984 distinct values<br>
•	points:		 21 distinct values<br>
•	price: 		381 distinct values<br>
•	province: 		420 distinct values<br>
•	taster_name:      19 distinct values<br>
•	title: 			94090 distinct values<br>
•	variety: 		664 distinct values<br>
•	winery: 		14559 distinct values<br>


	 3.2.1 Country Feature
		Analyzing the country feature, I found that the USA has been the most reviewed country. In terms of price, France has both the most expensive and cheap wines. In terms of point distribution, we can see England, India, and Austria at the top[6], but this seemed to be biased because they produce less wine than others. So, I plotted a strip plot, and the results were different.[7] Then, I could see that Italy, France, the US, Portugal, and Spain were the top scorers.


	3.2.2 Variety Feature
		A variety of wine means the grape used to make it. Typically, 75% of the wine should be made of that grape. On analyzing, Pinot Noir was the most reviewed variety[8]. While Bordeaux-style[9] red blend was the most expensive[10].My next interest was to see which combination of grapes was mostly the highest rated. I could see Port, Muscat, Chardonnay, and a few others, which got full points[11].


	 3.2.3 Taster Feature
		The most frequent taster in the dataset was Roger Voss, who was 10000 wines ahead of Michael Schachner, who was at number two[12]. The next step was to see if there were any taster who, in general, gave more points or low points. On plotting a box plot and finding the range, I could see that almost everyone was giving points in the same range. A few people did have low values, but that could be because they reviewed less wine than others.[13][14]


	 3.2.4 Description Feature
              I created word clouds of description according to their points. The description of lowest rated wines [15] had the words bitter, burnt, acidity in their description. The most expensive wine[16] had the comments show, smooth, aged in the description. For the highest rated wines[17], most of the words were years, vintage, aged, wood age, and other words related to aging, which shows that aging is an essential aspect. Not only aging but some good technique of aging is required. I could also find that description length had nothing to do with the price of the wine[18] but had a linear relationship with points[19].


	 3.2.5 Point Feature
		The first thing that came to my mind was that the lowest point was 80 and the highest was 100, which means that the magazine generally gives good points. Most of the wines had points between 82 to 95 and were normally distributed[20]. Further on plotting a heatmap[21] and seeing the scatter plot[21] between price and point, we see that there is a very weak relationship between both, and the most expensive wine is not the highest-rated.
The fragile relationship between price and point is the motivation for the recommender system.

##	Model
The goal of this model is to build a recommender system based on various attributes, preferably price or points.

4.1 Hard coding (Naïve Try)<br>
	    	My first try was to build a recommender system that took the preferred budget and points and returned a wine with the same point and less price. For this, I traversed through the whole data frame and filtered as needed. This hardcoded recommender was wrong because, even though the points a be the same, the characteristic of wine differs. A better way to recommend will be using description as the similarity factor.

4.2 Sentiment Analysis<br>
			For sentiment analysis, I have used the 'Sentiment Intensity Analyzer' from Vader, which is very useful for reviews and texts. I have used the compound score to measure how neutral, positive, or negative the tweet was. Based on sentiment analysis,[23] I could see that there was a relationship between sentiment and point, but no relationship between price and description. This finding further assured us that we could build a recommender using point and description.

4.3 K Nearest Neighbour<br>
			For KNN modeling, the distance metric is chosen as cosine similarity with brute algorithm. The pivot matrix built has an index as variety, the column value is province, and the value is given points. Using this pivot matrix, I have instantiated the knn model with seven neighbors, as I could see a elbow forming at around seven. In the final output, it selects a random row from the dataset, computes the neighbors, and returns the top 5 other rows with the lowest distance. The loop runs five times.
Here is an example:- 

	Recmmendation for ## Monastrell-Petit Verdot ##:
1: Monastrell-Petit Verdot with distance: 0.0
2: Verdil with distance: 0.0
3: Garnacha Tintorera with distance: 0.29681061814200493
4: Syrah-Tempranillo with distance: 0.3089577204131023
          5: Chardonnay-Sauvignon Blanc with distance: 0.4270485104506998

## 5.	Future Work
The future work of the project include: 
•	Build the recommender based on points, price, variety, or title as given by the user.
•	Deploy the recommender on flask or Django
•	Try to predict points using the description
•	Using a better language model

All the codes are present in my Kaggle notebook.[24]

## 6.	References
[1] https://github.com/RoaldSchuring/wine_recommender<br>
[1.1] https://www.kaggle.com/zynicide/wine-reviews<br>
[2] https://www.forbes.com/2008/03/22/gort-winemaker-nose-face-cx_vr_0319autofacescan02.html#27e5d7f152f4<br> 
[3] https://www.winemag.com/<br>
[4] https://www.winemag.com/buying-guide/von-schleinitz-2015-apollo-dry-riesling-mosel/<br>
[5] https://www.winemag.com/buying-guide/terre-rouge-2013-vin-doux-naturel-muscat-blanc-a-petit-grain-shenandoah-valley-ca/<br>
[6] https://ibb.co/StCk1JQ<br>
[7] https://ibb.co/RDFBGgk<br>
[8] https://ibb.co/bKqYTFB<br>
[9] https://www.winemag.com/varietals/bordeaux-style-red-blend/<br>
[10] https://ibb.co/3Nm2Br0<br>
[11] https://ibb.co/ySDwyxm<br>
[12] https://ibb.co/QMN9PwF<br>
[13] https://ibb.co/0284j2v<br>
[14] https://ibb.co/99wvSBG<br>
[15] https://ibb.co/Mgbp8C0<br>
[16] https://ibb.co/sHwg8MF<br>
[17] https://ibb.co/KwzhnCF<br>
[18] https://ibb.co/KyrDgGQ<br>
[19] https://ibb.co/cNt8VYH<br>
[20] https://ibb.co/RHQrMkt<br>
[21] https://ibb.co/XJyPTj5<br>
[22] https://ibb.co/JsG9zjd<br>
[23] https://ibb.co/LCqLQxG<br>
[24] 















