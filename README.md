# movie_recomendation_system
this is my new git repository
anish lama

import numpy as np
import pandas as pd
import ast
movies= pd.read_csv('tmdb_5000_movies.csv')
credits= pd.read_csv('tmdb_5000_credits.csv')
Movies=movies.merge(credits, on="title")
Movies
Credits=credits.merge(movies, on="title")
Credits.head(1).shape
Movies=Movies[['movie_id','genres',"vote_average","title","overview","cast","keywords","crew"]]
# Movies.isnull().sum()
# Movies.dropna(inplace=True)
# Movies.duplicated().sum()
# for the genres of the each movies
# creating a function and append the data in the list
def new_genres(obj):
    l=[]
    for i in ast.literal_eval(obj):
        l.append(i["name"])
    return l

Movies['genres']=Movies['genres'].apply(new_genres)
Movies.genres
 # for i in range(len(Movies)+1):
 #    list=[]
 #    for li in Movies.genres:
 #     list.append(li)
 #     print(list)

Movies.keywords[0]
# for i in range(len(Movies)+1):
#     lis=[]
#     for li in Movies.keywords:
#         lis.append(li['name'])
#         print(lis)
# for the keywords of the each movies
def new_keywords(obj):
    l=[]
    for i in ast.literal_eval(obj):
        l.append(i["name"])
    return l
Movies["keywords"]=Movies["keywords"].apply(new_keywords)
Movies.keywords

Movies.cast[0]
# for the cast of the each movies
# creating a function and append the data in the list
def cast(obj):
    lis=[]
    for i in ast.literal_eval(obj):
        lis.append(i["name"])
    return lis  
Movies["cast"]=Movies["cast"].apply(cast)
Movies.cast[0]
# def converts1(obj):
#     lis=[]
#     counter = 0
#     for i in ast.literal_eval(obj):
#         if counter !=3:
#             lis.append(i["name"])
#             counter+=1
#         else:
#             break
#     return lis  
Movies.crew[0]
# for the crew of the each movie
# creating a function and append the data in the list
def extracting_director(obj):
    dire=[]
    for i in ast.literal_eval(obj):
        if i['job'] == 'Director':
            dire.append(i['name'])
            break
    return dire    

Movies['crew']=Movies['crew'].apply(extracting_director)
Movies
Movies.crew
Movies.overview[0]
Movies.head()
# for the crew of the movies
# creating a function with the function_name of convertsql and the name of the cast is append in a list 
def converted(obj):
    L=[]
    counter=0
    for i in ast.literal_eval(obj): 
        if counter!=3:
            L.append(i['name'])
            counter+=1
        else:
            break
    return L        
Movies['cast']=Movies['cast'].apply(converted)
Movies.cast[0]
Movies.head()
Movies.overview[0]

Movies['tags']=Movies['genres']+Movies['keywords']+Movies['cast']+Movies['crew']+Movies['vote_average']
Movies.head()
new_df=Movies[['movie_id','title','tags']]
new_df.head()
new_df['tags']=new_df['tags'].apply(lambda x:" ".join(x))
new_df.head()

new_df.tags[0]
new_df=new_df['tags'].apply(lambda x:x.Lower())
new_df.head()

