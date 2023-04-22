# GUI_RecommendationSystem_streamlit
Use user-based and collaborative filtering to provide recommendations.


# Recommendation_App
Use user-based and collaborative filtering to provide recommendations.

---
## **Develop Environment**
・Colab<br>
・Visual Studio Code 1.73.1<br>
・Python 3.9.13<br>
・Doxygen 1.9.1<br>


## **Techniques**
・Gemsim<br>
・Cosine similarity<br>
・PySpark ALS<br>
・Streamlit<br>


## Reference
- [Underthesea](https://github.com/undertheseanlp/underthesea)<br>
- [Gemsim tutorial](https://www.tutorialspoint.com/gensim/index.htm)<br>
- [Gemsim ML](https://www.machinelearningplus.com/nlp/gensim-tutorial/)<br>
- [Cosine Similarity - Sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html)<br>
- [Cosine Similarity - Wikipedia](https://en.wikipedia.org/wiki/Cosine_similarity)<br>
- [Collaborative Filtering](https://spark.apache.org/docs/2.2.0/ml-collaborative-filtering.html)
- [Streamlit API](https://docs.streamlit.io/library/api-reference)<br>
- [Git large file](https://git-lfs.com/)

---
## Workflow
- Data Collection
- Data Preprocessing
- Building models for recommendations
- Models evaluations
- Build test app using Streamlit


---
## **Data Collection (provided)**
- Dataset is got from [Shopee website](https://shopee.vn/Th%E1%BB%9Di-Trang-Nam-cat.11035567)


## **Data Preprocessing**
 ・ Using Underthesea and other techniques to preprocess and clean the data<br>
 ・ Import vnmese_txt_preprocess_lib library for use<br>
- After processing, we have following data file:<br>
  ・  Products_ThoiTrangNam_raw_final.csv : contains information data of products<br>
  ・  Products_ThoiTrangNam_rating_processed.csv : contain ratings of products by users<br>

Remark:<br>
*Vietnamese-stopwords and wrong-words list should be modified to be suitable with the task*


## **Content-based Filtering**
There are two methods to calculate similarity between products:
1. Using Gensim
2. Using Cosine Similarity


## **Collaborative Filtering**
- ALS (Alternating Least Squares) is a matrix factorization algorithm that is used to predict missing entries in a user-item association matrix.
- Collaborative Filtering is devided into two types: User-based and Item-based. In this project, we will cover both of them.<br>
    ・*User-based Collaborative Filtering:* will look for similar users based on the items users have already liked or positively interacted with.<br>
    ・*Item-based Collaborative Filtering:* recommendation system to use the similarity between items using the ratings by users.<br>
- The general idea of ALS is to repeatedly adjust the user and item feature vectors to minimize the error of observed ratings.
- The target Mean Root Squared Error (MRSE) of this project is less than 1.2
- Run cross-validation on the training set to find the best parameters for the ALS model.
| Parameter | Value     |
| --------- | --------- |
| rank      | 10, 40    |
| maxIter   | 10        |
| regParam  | 0.01, 0.1 |
| alpha     | 1.0       |
| numFolds  | 3         |


---
## **Conclusion**
- **ContentBased filtering**<br>
	・ Gemsim is prefer to use because it is more flexible and can be used with input is text description or product_id.<br>
	・ Saving and storing model is also easier with Gemsim.<br>
- **Collaborative filtering**<br>
	・ ALS Hyperparameters (with RMSE = 1.18)<br>
| rank | maxIter | regParam | alpha |
| ---- | ------- | -------- | ----- |
| 40   | 10      | 0.1      | 1.0   |

	・ <span style="color:blue">***Note:***</span> that increasing value of **rank** will increase the accuracy of the model but will also increase the training time and memory usage. Pay attention to this parameter to not make the model overfitting.<br>
	
***In any case, to achieve good results, it is important that the data preprocessing step must be done properly, filtering useful data, suitable for the given task.***


---
## **GUI**
- GUI is built with Streamlit and deployed on Streamlit cloud. 👉 [GUI's link]:

---
## **Troublesome**

### GitHub large file upload
- For large files, example .csv file
```
git remote add origin https://github.com/nhatminhcdt/Recommendation_App
git lfs track "*.csv"
git add .gitattributes
git lfs migrate import --include="*.csv"
git add "Data/Products_ThoiTrangNam_raw_final.csv"
git add "Data/Products_ThoiTrangNam_rating_processed.csv"
git add "Data/UsrRecMatrix_.csv"
git add "Data/ItemRecMatrix_.csv"
git add .
git commit -m "commit message"
git push --set-upstream origin master
```

### Speech Recognition stuck at 'Listening...'
- Microphone picks up too much ambient noise
```
r = sr.Recognizer()
with sr.Microphone() as source:
	r.adjust_for_ambient_noise(source)
	audio = r.listen(source)
```

---
## **Log**
- 2023/04/18 - Eliminate ambient noises come to Microphone <br>
- 2023/04/17 - First Commit <br>
