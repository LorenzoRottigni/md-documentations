# 19 - Recommender Systems

For recommender systems is meant a class of algorithms that are used to recommend items to users. The most common example of a recommender system is the recommendation of products to users based on their previous purchases and ratings.
The 2 most common types of recommender systems are:

## Content-based recommender systems
Are based on the attributes of the item, and it recommends items that are similar to those that a user has liked in the past.
Ex. Netflix recommends movies based on the genre of the movie that you liked in the past.

## Collaborative filtering recommender systems
They use the "wisdom of the crowd" to recommend items.
The idea is that if a user A buys the same items as a user B, then A is likely to buy other items that B has bought but has not yet bought.
Ex. Amazon recommends items based on other users shopping experience.
Collaborative filtering is the most common type of recommender system because gives better results and it's relatively easy to understand.
The algorithm has the ability to do feature learning on its own, which means that it can start to learn for itself what features to use.
They can be divided into 2 categories:

### Memory-based collaborative filtering
It uses user rating data to compute the similarity between users or items.

### Model-based collaborative filtering
It uses machine learning algorithms to predict users' rating of unrated items.

## Python implementation
Scikit-learn does not have a built-in function for recommender systems, but we can use some feature extraction functions to create our own recommender system.

### Dataframe
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline

column_names = ['user_id', 'item_id', 'rating', 'timestamp']

df = pd.read_csv('u.data', sep='\t', names=column_names)
# connection between movie_id and movie title
movie_titles = pd.read_csv('Movie_Id_Titles')

# concatenate the two dataframes using item_id as FK
df = pd.merge(df, movie_titles, on='item_id')
```

### Data Analysis
```
Average rating for each movie:
```
df.groupby('title')['rating'].mean().sort_values(ascending=False).head()
# title
# They Made Me a Criminal (1939)                5.0
# Marlene Dietrich: Shadow and Light (1996)     5.0
# Saint of Fort Washington, The (1993)          5.0
# Someone Else's America (1995)                 5.0
# Star Kid (1997)                               5.0
# Name: rating, dtype: float64
```

Number of ratings for each movie:
```
df.groupby('title')['rating'].count().sort_values(ascending=False).head()
# title
# Star Wars (1977)             584
# Contact (1997)               509
# Fargo (1996)                 508
# Return of the Jedi (1983)    507
# Liar Liar (1997)             485
# Name: rating, dtype: int64
```

### Recommender System

Create a dataframe with the average rating and the number of ratings for each movie:
```
ratings = pd.DataFrame(df.groupby('title')['rating'].mean())
ratings.head()
```

Add a column with the number of ratings of each movie belong to the average rating:
```
ratings['num of ratings'] = pd.DataFrame(df.groupby('title')['rating'].count())
ratings.head()
```

#### Plotting
```
ratings['num of ratings'].hist(bins=70)
ratings['rating'].hist(bins=70)
```

Relation between the average rating and the number of ratings:
```
sns.jointplot(x='rating', y='num of ratings', data=ratings, alpha=0.5)
```

#### Recommending similar movies
Create a matrix with the user_id as index and the title as columns:
```
X_movie = df.pivot_table(index='user_id', columns='title', values='rating')
```

```
star_wars_user_ratings = X_movie['Star Wars (1977)']
star_wars_user_ratings.head()

liar_liar_user_ratings = X_movie['Liar Liar (1997)']
liar_liar_user_ratings.head()
```

Compute pairwise correlation between rows or columns of two Series:
```
X_movie.corrwith(star_wars_user_ratings)
similar_to_liar_liar = X_movie.corrwith(liar_liar_user_ratings)
```

Create a dataframe with the correlation between the movies and the number of ratings and drop the NaN values:
```
corr_star_wars = pd.DataFrame(similar_to_star_wars, columns=['Correlation'])
corr_star_wars.dropna(inplace=True)
corr_star_wars.head()
corr_star_wars.sort_values('Correlation', ascending=False).head(30)

# Hollow Reed (1996)	1.000000
# Commandments (1997)	1.000000
# Cosi (1996)	1.000000
# No Escape (1994)	1.000000
# Stripes (1981)	1.000000
# Star Wars (1977)	1.000000
# Man of the Year (1995)	1.000000
# Beans of Egypt, Maine, The (1994)	1.000000
# Old Lady Who Walked in the Sea, The (Vieille qui marchait dans la mer, La) (1991)	1.000000
# Outlaw, The (1943)	1.000000
# Line King: Al Hirschfeld, The (1996)	1.000000
# Hurricane Streets (1998)	1.000000
# Scarlet Letter, The (1926)	1.000000
# Good Man in Africa, A (1994)	1.000000
# Safe Passage (1994)	1.000000
# Golden Earrings (1947)	1.000000
# Full Speed (1996)	1.000000
# Twisted (1996)	1.000000
# Ed's Next Move (1996)	1.000000
# Mondo (1996)	1.000000
# Last Time I Saw Paris, The (1954)	1.000000
# Maya Lin: A Strong Clear Vision (1994)	1.000000
# Designated Mourner, The (1997)	0.970725
# Albino Alligator (1996)	0.968496
# Angel Baby (1995)	0.962250
# Prisoner of the Mountains (Kavkazsky Plennik) (1996)	0.927173
# Love in the Afternoon (1957)	0.923381
# 'Til There Was You (1997)	0.872872
# A Chef in Love (1996)	0.868599
# Guantanamera (1994)	0.866025
```
the result is a list of movies that are similar to Star Wars, but it's not correct because there are movies with only 1 rating that have a 5.0 correlation.
1.0 is the perfect correlation.

```
corr_liar_liar = pd.DataFrame(similar_to_liar_liar, columns=['Correlation'])
corr_liar_liar.dropna(inplace=True)
corr_liar_liar = corr_liar_liar.join(ratings['num of ratings'])
corr_liar_liar.head()
corr_liar_liar[corr_liar_liar['num of ratings'] > 100].sort_values('Correlation', ascending=False).head()

# 	Correlation	num of ratings
# title		
# Liar Liar (1997)	1.000000	485
# Batman Forever (1995)	0.516968	114
# Mask, The (1994)	0.484650	129
# Down Periscope (1996)	0.472681	101
# Con Air (1997)	0.469828	137
```

