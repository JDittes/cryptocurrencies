# Cryptocurrencies

This project was created to use Machine Learning to classify cryptocurrencies from a list that originally numbered more than 1,250 different cryptocurrencies.

In the data-cleaning proces I eliminated all crptocurrencies that were no longer being traded, and I dropped all those that didn't identify a working algorithm. Next, I dropped those rows that had null values, leaving me with one final step: dropping the final 153 currencies that had yet to mine any coins. This left me with a dataset of 532 rows.

From this set, I pullt the column that included the cryptocurrency name. I didn't want this around, as I was about to do some major work on the factors affecting each currency. I also saved the 'Algorithm' column in a separate DataFrame so I could use it later. As a string, it wouldn't be much use in the scaling that I needed to do. I dropped both columns from the *cryp_df* that I had created and cleaned.

Next I used the scaler, *get_dummies* to turn the "Algorithm" and "ProofType" columns into binary format. In order for Machine Learning to be effective, I needed to eliminate strings and convert all values to numbers. There were so many algorithms and prooftypes that I added 96 rows to my dataframe in this process. But the data was numerical. Now it was in a position where I could classify...then learn.

I used *StandardScaler()* to scale the values in each column. This was important because the values in "TotalCoinsMined" and "TotalCoinSupply" were actually very high, but the scaler brought them down to manageable Levels. The max value of mined coins was 989,988,713,439. The currency with the maximum supply of coins had almost 10,000,000. That's a lot to scale when the minimum number mined was 42, and the smallest supply was 75,000,000.

Finall, I trained the data, coupling *fit_trasform* to the *StandardScaler* algorithm.

## Recuding Data Dimensions Using PCA
I was now ready to reduce the vast number of factors (algorithmic, ProofType) to the three principal components, using Principal Component Analysis. First, I used the *PCA algorithm* I had downloaded from sklearn and, with the help of *fit_transform*, narrowed down the three principal components

Given how many columns there were, PCA didn't show me a lot. The top three components explained 2.8%, 2.1%, and 2.05% of the data combined. That's not a lot to go on, but they were still the principal components.

## Clustering Cryptocurrencies using K-Means
It was time to figure out how many clusters would be optimal for classifying this huge set. I graphed an *elbow curve* using MatPlotLib. I found that the elbow curved sharply at 4, so I determined to graph four clusters.

Next I concatenated the two dataframes: the original and the scaled. This gave me a datafram with my 3 principal components as well as the numberical information for the algorithms and prooftypes I had transformed above.

To this dataframe I added four columns that contained strings: 'CoinName', 'Algorithm', 'ProofType', and 'Class.'

## Visualizing Cryptocurrency Results
It was now time to 'see' all the data-crunching I had done. I created a 3D scatterplot using Plotly Express. This was pretty cool, but it pointed out a problem in my data. Of the four classes I had identified, one, Class 2, had only one value, which was well outside the range of the other factors. Still, it was cool to see how the algorithm had classified all those values.

Next, I created a table with the tradable cryptocurrencies I had worked with. For this I used *hvplot.table*. 

My last graphical interface was a 2D table using *hvplot.scastter*. The result here was disappointing. There is such a huge range, too many of the values were clustered too close to the y or x axes to really differentiate them. When I zoomed in, I could see them, but it would have taken some explanation to an outside party.

## Conclusion
If I had more time with this dataset, I would find a way to remove Class 2 and graph with only 3 datasets instead of the 4 identified using the Elbow Method. I would also go more carefully through my calculations to see if I might have made an error here.

This was a fun session, letting me develop my python skills while adding important analytical algorithms and graphs to my analytical tool bag.
