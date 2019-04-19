# Mappening Backend Architecture

There are two main parts of the backend:

The server that serves the 

## To edit ML

Scikit-learn randomForest machine learning classifiers with TfidfVectorizer use the name and details as the features to automatically categorize events and classify if they have free food. 

The training data was gathered before in the open API days before Cambridge Analytic. We gathered a few thousand events from the previous few years in events_fb. 

In `src/mappening/ml/`, are all the relevant ML files. 

`.ipynb` files

- Used for testing which models work best using grid search
- You can look here to see why the model and model hyperparameters were choosen and experiment with your own

`modelCreation*.py`

- This creates the name and detail vectorizer models and for simplicity saves them locally as pickles
- Running the file retrains the model, note if the model exceeds 100MB it will not save to git and you will need to lower the model complexity

`auto*.py`

- This possesses the function that takes a list of events and calls the model returning the event list with the updated 