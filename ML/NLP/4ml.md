# ML
**K-FOld Cross-Validation**: one k subset is test data and k-1 are training data. Repeated k times.

## Evaluation:
Accuracy = # Predict correclty/ total
Precision= # predicted positive that are positive/# predicted positive


## Random Forest
- Ensemeble method that creates multiple simple models and combines them
- Constructs a colleciton of decision tree and then aggregates the predictions of each tree to determine the final prediction.
- Easily handles outliers, missing value, different inputs
- outputs feature important
- Can do classification and regression
```py
#Input is TfidfVectorizer of data
from sklearn.ensemble import RandomForestClassifer
#RandomForestClassifer.feature_importances_ are great for understand the ml
RandomForestClassifier(n_estimators=10, criterion=’gini’, max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features=’auto’, max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, bootstrap=True, oob_score=False, n_jobs=1, random_state=None, verbose=0, warm_start=False, class_weight=None)
```

## CrossValidation
```py
from sklearn.model_selection import KFold, cross_val_score
rf = RandomForestClassifer(n_jobs=-1) #parallelize
k_fold = KFold(n_splits=5)
cross_val_score(rf, X_features, labels, cv=k_fold, scoring='accuracy', n_jobs=-1)
```

## Holdout Test Set
```py
from sklearn.metrics import precision_recall_fscore_support as score
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X_features, labels, test_size=0.2)

from sklearn.ensemble import RandomForestClassifier
RandomForestClassifier(n_estimators=50, max_depth=20, n_jobs=-1)
rf_model = rf.fit(X_train, y_train)
sorted(zip(rf_model.features_importances_, X_train.columns), reverse=True)[0:10]
y_pred = rf_model.predict(X_test)
precision, recall, fscore, support = score(y_test, y_pred, pos_label='spam', average='binary')
```

## Grid Search
Defining grid of hyper parameters and exploring them.
```py
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import precision_recall_fscore_support as score
from sklearn.model_selection import train_test_split
def train_RF(n_est, depth):
  rf = RandomForestClassifer(n_estimatores=n_est, max_depth=depth, n_jobs=-1)
  rf_model = rf.fit(X_train, y_train)
  y_pred = rf_model.predict(X_test)
  precision, recall, fscore, support = score(y_test, y_pred, pos_label='spam', average='binary')
  print(......)

for n_est in [10,50,100]:
  for depth in [10,20,30,None]:
    train_RF(n_est, depth)
```

## Grid Search And Cross Validation
```py
from sklearn.model_selection import GridSearchCV
rf = RandomForestClassifer()
param = {'n_estimators': [10, 150, 300],
          'max_depth': [30,60,90, None]}
gs = GridSearchCV(rf, param, cv=5, n_jobs=-1)
gs.fit(X_tfidf_feat, labels)
pd.DataFrame(gs.cv_results_).sort_values('mean_test_score', ascending=False) [0:5]
