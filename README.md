# data_preprocessing
template code for datapreprocessing
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
df=pd.read_csv("data.csv")
X=df.iloc[:, :-1].values
y=df.iloc[:,-1].values
df.head()
from sklearn.impute import SimpleImputer
imputer=SimpleImputer(missing_values=np.nan ,strategy='mean')
imputer.fit(X[:,1:3])
X[:,1:3]=imputer.transform(X[:,1:3])
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
ct=ColumnTransformer(transformers=[('encoder',OneHotEncoder(),[0])],remainder='passthrough')
X=np.array(ct.fit_transform(X))
from sklearn.preprocessing import LabelEncoder
le=LabelEncoder()
y=le.fit_transform(y)
from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test=train_test_split(X,y,test_size=0.2,random_state=0)
