# Super_Hero_Clustering
## Introduction
This project is to distribute comic super heroes into different clusters based on their abilities using machine learning. It can be divided into two parts.  
* Part 1: Using cosine similarity to find out the most similar hero for the input one based on the abilities.  
* Part 2: Clustering heroes into different groups by KMeans method.  

## Data  
**Data Source:**  
https://www.kaggle.com/claudiodavi/superhero-set#super_hero_powers.csv  
This data was scraped from <a href='https://www.superherodb.com/'>SuperHeroDb</a> and was collected in June/2017 from superherodb which  had not been updated since, so it may not be up to date.  

Data example:  
<img src='Data_example.png' alt='screenshot for data example' title='data example' width=600px height=400px>  

Data summary:  
668 x 168  (668 heroes and 168 types of abilities)  

**Although the columns are already in one-hot style, the values are 'True/False' in String, which need to be converted into 1 or 0 for the convenience of future analysis.**  

## Methodology  
**I.  Data preprocessing**  
1. Load data from CSV file and convert column's value from 'False/True' <String> to appropriate 0/1 <Int> for the convenience of following analysis.  
2. The converted column data is useful for:
  * A python dictionary pairing with hero's name as key for the similarity search.
  * A numpy vector for KMeans clustering.
  * A pandas dataframe with header for ggplot visualization.  
All three data sets were created as described above.  
  
**II. Data Analysis**  

**PART 1. Similarity Search**  
By comparing cosine similarity of the one-hot data for hero's ability among the data set, we can find out the hero with the highest similarity to the input one. For example:  
<img src='similarity_sample.png' alt='screenshot for similarity search' title='similarity example'>  
**PART 2. Clustering heroes**  
1. Since the proper clustering number k is required for the modeling, a plot was created with the Sum of Squared Error (SSE) against a range of k (2 to 30) to find out the elbow value of k. In this project, it took k=10 (Fig.1).  
Fig.1: <img src='elbow_result.png' alt='screenshot for elbow plot' title='elbow plot result'>  
2. Cluster the data set with the proper k (k=10) and add the predicted label to the data frame (Fig.2).  
Fig.2: <img src='hero_df.png' alt='screenshot for clustered hero dataframe' title='hero dataframe'>  
3. Visualize the clustering by two differnet methods:  
* Principal Component Analysis (PCA);  
* t-Distributed Stochastic Neighbouring Entities (t-SNE).  

## Results  
1. 

## Discussion  


## Conclusion  

