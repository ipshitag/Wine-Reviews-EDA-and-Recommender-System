# WINE REVIEWS EDA AND RECOMMENDER SYSTEM

![Red wine image](https://images.unsplash.com/photo-1535869462434-f92cc30bf40c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=755&q=80)

## Background
Wines have been interwined with the human cultue since a long time. As time went by the wine industry blossomed. Today, revenue in the Wine segment **amounts to US$323,501m in 2020. The market is expected to grow annually by 9.8% (CAGR 2020-2023)**, as stated by [Statista](https://www.statista.com/outlook/10030000/100/wine/worldwide). Thus wine reviews have become equally important, people dont want to invest unknowingly. Hence this analysis is done to see the various trends in the reviewed wines and how can a company benefit from them.

## Questions
The questions that I will try to find answers of, are
1. Which are the most reviewed country and most reviewed
variety?
2. Is there any relationship between the price and points
received?
3. What are some characteristics of wine, country-wise?
4. What are some common terms appearing in the lowest-rated
and highest rated wine?
5. Can we create a recommender system?
6. What should a company keep in mind to get good reviews?
7. Is there any relationship between points and any other
attributes?
8. Which variety of grape will be best to make wine?
9. Referring to which reviewer will be beneficial?
10. Should we go with what is familiar or with something less
standard in terms of variety?

OK, So lets get into it.

## Data
The dataset consists of 129971 rows, in 13 columns. The dataset was scrapped from a famous wine magazine name [Winemag](https://www.winemag.com/). It is a dataset consisting of different wines and their names, province,tasters name, variety, points collected, price, and other variables.

Here are a few examples of descriptions:

*"Fragrant notes of tangerine and yuzu peel abound on this citrusy dry Riesling.
The palate is cutting and fresh, full of juicy white grapefruit and lime flavors.
Light-bodied yet satisfyingly thirst-quenching, it finishes long with invigorating
minerality."*
- Von Schleinitz 2015 Apollo Dry Riesling (Mosel) [See here](https://www.winemag.com/buying-guide/von-schleinitz-2015-apollo-dry-riesling-mosel/)

*"An earthy, nutty aroma and flavor come through the intense sweetness and
full body of this dessert-style wine. It goes for earthy complexity rather than
obvious fruit flavors, and tastes high in sugar and alcohol."*
- Terre Rouge 2013 Vin Doux Naturel Muscat Blanc à Petits Grains (Shenandoah Valley (CA)) [See here](https://www.winemag.com/buying-guide/terre-rouge-2013-vin-doux-naturel-muscat-blanc-a-petit-grain-shenandoah-valley-ca/)

The attributes given,

1. **Title**: Name of wine
2. **Variety**: Type of grape that is used in the wine.
3. **Country**: Country of origin of the wine.
4. **Province**: The region within the state in which the wine was
produced. The specificity of the areas ranged widely.
5. **Region 1 and 2**: A more specific information about the location of
the wine, where the wine was produced.
6. **Price**: The cost of the wine.
7. **Points**: The rating of the wine it ranges from 80 to 100
8. **Taster Name**: Name of the reviewer who reviewed the wine

## Data Cleaning

### Missing Values
The data set had missing values, heavily, in 'region_2'

![Missing values](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___18_1.png)

#### Dealing With Missing Values

1. I dropped the unwanted columns, namely, 
- Unnamed :0
- Designation
- region_1
- region_2
- taster_twitter_handle

2. For the price column, I used the median of the column to fill the null values
3. I dropped the rest of the null, which were in taster_name

### Outliers

For seeing the outliers, I plotted a boxplot for price and points.

#### Price
![Outlier in price](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___24_1.png)

We can see that there are a lot of outliers. But they are not *impossible* values and may help in further. So, I did not drop them.

#### Points
![Outlier in points](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___26_1.png)

Here we can see two outliers, one at ~98 and one at 100. But, they too are not *physically impossible* values. There maybe wines who got 100, that is why I have not dropped them too.

## Exploratory Data Analysis

Let us see brief description about the features
- country: 43 distinct values
- description: 94984 distinct values
- points: 21 distinct values
- price: 381 distinct values
- province: 420 distinct values
- taster_name: 19 distinct values
- title: 94090 distinct values
- variety: 664 distinct values
- winery: 14559 distinct values

### Country Feature

Analyzing the country feature, I found that the **USA has been the most reviewed country**. 
![Highest reviewed country](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___34_0.png)

In terms of price, France has both the most expensive and cheap wines. 
![Country X Price](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___38_0.png)

In terms  of point distribution, we can see England, India, and Austria at the top, but this seemed to be biased because they produce less wine than others. So, I plotted a strip plot, and the results were different. Then, I could see that Italy,France, the US, Portugal, and Spain were the top scorers according to the number of wine produced.
![Country X Point](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___45_0.png)

The most expensive wine of different countries were,
![Most expensive](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___41_1.png)

### Variety Feature
The most common variety was **Pinot Noir**
![Most reviewed variety](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___49_0.png)

The most expensive wine's were made of **Bordeaux style red blend** followed by, **Pinot Noir**
![most expensive variety](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___55_0.png)

The highest rated wine were made of **Port, Prugnolo Gentile, Merlot** etc.
![Highest Rated wine](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..Ro9TEFEZyThqbREfsvNS6A.vuvcfFgtlyjwLfDY2BvpmRLjlk86J4OHOxPXteSiB_X4mvssCCemmaIOjrShxu6xIkjTSAhCw_nzstu1Adi5pZYSx1YutK0HrYCheKPzdHCQ_FJsRfm-V3VTzVP34K8E3M-Wh7Yo6Vd58huIE0NmF5bhxveeqw_yEphjG7lwkTGDpg7ZSEjc4xpZVaZuMGOmD8xNvTZIW58rFu4vH_YzGqxdxvzHB4MsjWyPImEy47Y92uUOiZrVVrinFkLmXTe7SCH7db3DCS3o-vUGTZvv-QJuc25ntXFtIqJNduku3d-jpQvKUSQxoNo11xQXsNMLNTwScmHvQnLmcsU_5_uJeVJnD3TDOjz9v3ZmTEkgXnhAEzslwREF9kANRfFllYdHb9fIoxe6khYdEJYMJprsJpduwnNAOxrsn90tYWxbHxunaMILwfX_in9aFe2lCE6wZKdPEA3GME69hPh_M8L1qJJEbg2CzAkSN9-VP7gmYlas1go-mH0WB0CAAyK1K8X2_uK4jEDlAdgj5QXgDFvxhgQLsU-hI5-KJ5V7c9quT6P2mKd8uvPRvnHq_KNuGf1rx5FBUAsQejncReIZF_wa13tl56tSg6Jbka7hmzO0Ozukw8R3OX57ENVI-N6j02rYbuP23fNcqPKufRe_teafXqz0xbQlTNWiutO1g79Ywas.VxqE7C9VBdF1RHi70CNlxQ/__results___files/__results___58_0.png)

To understand whether there were any variety which got both good points are also were cheap, I did an intersection of both. The result was,

![best and cheap](https://i.ibb.co/XFq5Mrq/2020-09-19-5.png)
Thus we can say that, selecting **Merlot,Cabernet Sauvignon,Chardonnay,Portuguese Red, Syrah and Shiraz** are good choice for wine.

### Taster Feature
![Nice cartoon](http://cdn2.justwineapp.com/assets/article/2015/08/How-To-Taste-Wine-Wide-2.jpg)
The most frequent taster in the dataset was Roger Voss, who was 10000 wines ahead of Michael Schachner, who was at number two. 

![top 20 taster](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..f0v0-QIs_GmglmVmvHhTmA.3zqslN4Iy8Yl1eNBQSsLlxWck_alEC2ADyLRCf6K9CqfLiR_W5k--KDrqR7mu3R1VOrmn3KvYRkP9ZsVBLir2u0Up0d_VNixd-HPyby7y5hC6_MhKtFlwJf8Mpg19ZZWVQs1NXpcYcmbo0m88bQXhzP-dxVv5ffC34kwnTQyIVNfOcPMQr-WE9WDYSiQrl8OQnESsGlvQB4unwBji-bxTIDavctjeALB1vfVDqyYE-0DlT62x79tG9DtKubYzSK3eoeZ6WcxigWwC-_DgfoCsU49rWF-cF_nQ06Djop8XYTDRE-41I8gi-u15tr8U03YbFLEBpp0ug7TGeDFX7S_qs-NbwFt1vF64E9SKjXSfNCbbTwnGz6wSGG8oKosbV_xS8HdB9Qxr_Wro0tADJ6ZbvkQSe-EPT4ELB-X4ZKy1Smn25OkbsugRKDcLQN67nHp4jIQ98YxyO7Ti5vb6nZUAC8lGG_TbD3Hy4uFYlrwR2vS0uexoybFv13x4_epixIRAqvaHjrwLCa7gS5jcCRClr1-ssJpUtdtaWvzPMIeHE_Jl6j54ZVXPoB-QX5_PMUFu59ZPBw7bxstNM2IiVpldr1BEruTuojUdOSkJFjR6HsrhLBlRbdIpnrFV3Ngj7FWu3NqbQM6yq-fLRhIsByJkk8q-CbaFet4A7iQBS424vo.xMK4aDFqzdIR1Am1kd24ZA/__results___files/__results___67_0.png)

The next step was to see if there were any taster who,in general, gave more points or low points. On plotting a box plot and finding the range, I could see that almost everyone was giving points in the same range. A few people did have low values, but that could be because they reviewed less wine than others.
![point distribution](https://www.kaggleusercontent.com/kf/43000787/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..f0v0-QIs_GmglmVmvHhTmA.3zqslN4Iy8Yl1eNBQSsLlxWck_alEC2ADyLRCf6K9CqfLiR_W5k--KDrqR7mu3R1VOrmn3KvYRkP9ZsVBLir2u0Up0d_VNixd-HPyby7y5hC6_MhKtFlwJf8Mpg19ZZWVQs1NXpcYcmbo0m88bQXhzP-dxVv5ffC34kwnTQyIVNfOcPMQr-WE9WDYSiQrl8OQnESsGlvQB4unwBji-bxTIDavctjeALB1vfVDqyYE-0DlT62x79tG9DtKubYzSK3eoeZ6WcxigWwC-_DgfoCsU49rWF-cF_nQ06Djop8XYTDRE-41I8gi-u15tr8U03YbFLEBpp0ug7TGeDFX7S_qs-NbwFt1vF64E9SKjXSfNCbbTwnGz6wSGG8oKosbV_xS8HdB9Qxr_Wro0tADJ6ZbvkQSe-EPT4ELB-X4ZKy1Smn25OkbsugRKDcLQN67nHp4jIQ98YxyO7Ti5vb6nZUAC8lGG_TbD3Hy4uFYlrwR2vS0uexoybFv13x4_epixIRAqvaHjrwLCa7gS5jcCRClr1-ssJpUtdtaWvzPMIeHE_Jl6j54ZVXPoB-QX5_PMUFu59ZPBw7bxstNM2IiVpldr1BEruTuojUdOSkJFjR6HsrhLBlRbdIpnrFV3Ngj7FWu3NqbQM6yq-fLRhIsByJkk8q-CbaFet4A7iQBS424vo.xMK4aDFqzdIR1Am1kd24ZA/__results___files/__results___74_0.png)




