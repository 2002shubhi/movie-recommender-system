# NextFlix
NextFlix is a movie-recommendation web application made as part of Microsoft Engage 2022. Through this project, I demonstrated two algorithms commonly used in web-streaming as well as audio-processing apps, namely collaborative and content based filtering. In the next section, I discuss the algorithms and implementation in detail.

NOTE The following steps can be followed to run the web app locally:

Clone the master branch of this repo onto your pycharm39 terminal. Run streamlit app.py in the terminal.


You can also access the app on heroku:
https://mrsshubhi.herokuapp.com/

# Dataset
https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata
This dataset was generated from The Movie Database API. This product uses the TMDb API but is not endorsed or certified by TMDb.
Their API also provides access to data on many additional movies, actors and actresses, crew members, and TV shows.

# Recommendation Engine

“A lot of times, people don’t know what they want until you show it to them.” Steve Jobs

A recommender system is an application of machine learning that produces individualized recommendations as output or has the effect of guiding the user in a personalized way to interesting objects in a larger space of possible options.

# Content based recommender: 

This does not include any personalization and has no user data. This method is good for linking movies by underlying thematic elements. See analysis in the notebook for more information.

We use the pandas library to import our dataset and after pre-processing this data, we create tags for each movie. We compare these tags using the sklearn and create a similarity matrix using cosine similarity on bag of words. This matrix is accessed from streamlit using pickle.

# Collaborative filtering based recommender: 
This project is a first pass at using knn (k nearest neighbours) algorithm to predict user ratings of movies they haven't watched yet. Since my project doesnot have a login-register system yet, this user was assumed to be a default user and given a fixed id. Filtering was done using knn on basis of the IMDb scores of movies. The results were stored as json files to be accessed through streamlit.

# app.py

This is the streamlit application.  Here we have defined 3 functions:
a] fetch_poster(id), which fetches the movie posters from the tmdb api when their respective ID's are given to the function.
b] recommend(movie), which recommends movies based on cosine content filtering. This is called when the movie option is selected from the drop-down menu.
c] knn function, imported from classifier.py, which filters the movie based on the genre and IMDb score appended to the testpoint.

# Implementation

On our homepage, the user is able to choose between select, movie and genre based filtering using the drop-down menu. If the user selects movie, they are prompted to choose any movie from the drop-down menu. Upon doing so and clicking the 'Recommend' button, the user is given 5 similar movies based on content based filtering using cosine similarity along with their posters.

![image](https://user-images.githubusercontent.com/84243901/171042107-6815ee06-3a7d-4112-afbd-a74e0a85ac05.png)
![image](https://user-images.githubusercontent.com/84243901/171043309-2cec97a5-a012-4299-a83a-8810198db1c9.png)

If the user chooses genre, the user is allowed to select however many genre they would want, using the multi-select drop-down menu of genres. Upon choosing these, the user can pick an IMDb score between 1-10 of the movies they would like to be recommended. Doing so, they are recommended n number of movies, by selecting n from a streamlit function , based on knn algorithm along with the link to their IMDb pages.
![image](https://user-images.githubusercontent.com/84243901/171043411-384b1d26-1470-41e7-a56a-5b8bd478ea3e.png)


# Future Scope
a) A login-register functionality could be provided so the system is able to retain user ID. The user can be prompted to rate around 5 movies based on which we can recommend them movies users similar to them also liked. This would be a much truer implementation of collaborative filtering.
b) We could recommend users movies based on popularity filtering, such as trending movies and top-rated movies. We could also deploy a hybrid recommendation system giving appropriate weight to content based and collaborative filtering respectively.
c)We could evaluate algorithms using RMSE and deploy more precise and accurate algorithms going forward.

# References

1]https://www.youtube.com/watch?v=i06byQMdAzo&ab_channel=DPhi
A wonderful session on recommender systems and their extensive types and implementations by Mr. Sumit Jain, ex data-scientist at Microsoft.
2]https://github.com/ecbenezra/recommender-system
Amazingly detailed models with extensive explanation on popularity, content, collaborative and hybrid recommendation engines.
3]https://scikit-learn.org/stable/
Simple and efficient tools for predictive data analysis.
4]https://streamlit.io/
A faster way to build and share data apps.
5]https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world
While I ended up using Streamlit instead of Flask, I would highly recommend this blog to all of my peers, simply put because of the complex concepts explained away using a simple, witty approach.

Special Thanks to:
CampusX, Krish Naik, Springlearn India for their incredible YouTube videos on the topic of recommendation systems.
