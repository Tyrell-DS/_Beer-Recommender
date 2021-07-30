# Beer Recommender 

## Business Understanding

Beer recommendations happen largely through word of mouth. There are no online beer recoommeder systems, however there is large amounts of data that exist from people liking 
and rating beers. BeerAdvocate.com,which has been in existence and has reviews from 1996, has an excellent source of data regarding this issuse. For comparison Amazon has been in existence since 1994 and revoloutionized recommender systems as well as the online shopping platform. This project's focus in on a smaller scope. This project aims to build a recommender system for the at home beer aficianado who wants to try something different than the usual 6 pack they grab. 

## Repo File structure

![Untitled Workspace](https://user-images.githubusercontent.com/19891506/127584979-5926fa82-4d4a-4678-842e-dd9a252e1445.png)



## Cleaning and EDA:
The dataset was originally downloaded from Kaggle. The link is provided below. The columns in the dataset are 'brewery_id',	'brewery_name',	'review_time',	'review_overall',	'review_aroma',	'review_appearance',	'review_profilename',	'beer_style',	'review_palate',	'review_taste',	'beer_name',	'beer_abv', and	'beer_beerid' During the cleaning process I discovered that the data was remarkably clean. There is 1586614 rows in the dataset each representing a review of a single beer by one individual. There are 33387 users in the data set with the most reviews by one person being 5817, and the least was several users with 1 review. The average number of reviews between all users being 47. I cleaned the users by removing all users with more than 1000 reviews, and all users with less than 10 reviews. This got my total number of users down to 9936. 100 was used as the upper limit so that I could get rid of all the people with a lotof reviews. It would be hard to recommend anything for these users because their libaries are so vast that anything could be a good review for them. I also removed all people with less than 10 reviews because it would be hard to properly recommend anything for them. 

There were 56857 unique beers in the dataset. I removed all beers with less than 200 reviews from the dataset. This was done so that the model runs efficiently and my metrics are accurate. This reduced the number of unique beers in the dataset to 1236. After filtering the dataset I was left with 634964 total reviews that represented 40% of the original dataset. I believed this dataset fully captured the signal of the ratings. The reviewers all left in the set had at least more than 10 reviews, and all beers had a minimum of 200 reviews. The beers left in the data set are popular beers that are more readily available to consumers, rather than rare obscure beers that are hard to find.

Finally to create a dataset that would be used in the modeling process I renamed the columns 'review_profilename', 'beer_name', and  'review_overall, to 'user', 'item', and
'rating' while also dropping all other columns. This was done in order to get a data frame that is usable in the surprise module. Finally during the cleaning process I used Pandas, Numpy, and Suprise modules. 

## Modeling:
Now moving on to the modeling folder I created two models from the cleaned dataset. The first model I created was an SVD model. I had been studying recommenders through Flatiron, as well as Udemy and found that the SVD model was the gold standard for recommenders focusing on RMSE metric. First in the modeling process I loaded the cleaned dataset, and instantiated a reader. Next I created a Dataset from the pandas dataframe and performed a train test split. I created a SVD model whose RMSE was 0.586. I performed a grid search on this model that that increased the RMSE to 0.5844. Using the previous parameters as a starting point I ran an additional grid search which brought the RMSE down even lower to 0.5838.  

For the KNN modeling process I started off similarly to the SVD model. Once it got time to start modeling I created 4 models each representing one of the KNN models in the suprise library. The four models are KNNBasic, KNNWithMeans, KNNWithZScore, and KNNBaseline. The RMSE scores of the models were 0.6076, 0.6061, 0.6113, and 0.5887 respectively. I chose to go with the baseline model and ran two grid searches on it. I was able to get the RMSE down to 0.5843. I chose the KNN model due to knowing what's happening within the model. The cosine similarity matrix determines how closely related two vectors are by their orientation. So if thinking about this as two users in my beer dataset the cosine similarity between two people who liked the same beers would be close to 1. This similarity will decrease all the way to -1 by how much these two people tastes differ. Additionally I found that the KNN model ran faster than SVD model. For the modeling process I used Pandas, Surpise, Pickle, collections, operator, heapq,and random modules. 

## FInal Notebook 
The final notebook is a clean version of my KNN model. I pickled the model and its params as well as some addiional lists. Additionally there are two functions in the notebook. The first function is rater. This function was written and apart of the flatiron recommendation system lab. I modified the code so that it references beers as well as replacing associated variables so that they point to my data. This data takes in an integer that represent how many beers a person wish to rate. This creates a dictionary that is then turned into a pandas dataframe which is then appended to our original clean_data. This allowes us to insert a new user into my dataset and allows me to create some recoomendations for them. The second function is a rec function created by Frank Kane and included in the materials for his course Building Recommender Systems with Machine Learning and AI which I purchased on udemy. This function takes in a user and an integer then returns an amount of reviews equal to the integer provided. The function also eliminates beers that have been reviewed by the user. Running the two function as well as an addiotnal 7 lines of code I created will return recommendations.  

## Reproduction
In order to recreate the model first the dataset must be downloaded from kaggle at the link below then three notebooks must be run. The first is Clean_EDA ran in the Data Cleaning and EDA folder. The save to CSV have been commented out, and the files should already exist in the data folder located within Data Cleaning and EDA folder. Everything should be ran until In [47]. Everything past that was used to test surprise.  The second notebook that should be ran is the KKN_model_gs located within the modeling folder. This model has a lot of the exploratory modeling commeneted out. Everything not commented should be ran. There was some pickling and loading. If you load the pickled final model at the end of the book; that model has been fitted already and will run.  Finally beer recommender in Final project notebook should be ran to get recommendations. Conversly Beer recommender could be opened and ran on its own to get recommendations. 

## Resources
Presentation Link: https://docs.google.com/presentation/d/1JigDRQRSiw8AjhYgtjU_rmN3tgTtbuEAeIIrOq-UCig/edit#slide=id.p

Frank Kane's Udemy course: https://www.udemy.com/course/building-recommender-systems-with-machine-learning-and-ai/

Flatiron github: https://github.com/learn-co-curriculum/dsc-implementing-recommender-systems-lab/tree/solution

Dataset: https://www.kaggle.com/rdoume/beerreviews


## Contact info

LinkedIn: https://www.linkedin.com/in/tyrell-jackson-7b723295/

E - Mail: Tyrell.Jackson2009@gmail.com

Slack: @Tyrell 


