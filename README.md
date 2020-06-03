# Report
## Dataset
[Travel Review Ratings](https://archive.ics.uci.edu/ml/datasets/Tarvel+Review+Ratings)
## Analyze the data
根據相關係數觀察到有些種類間有較高正相關,  
將有較高正相關的種類歸為一組,  
則當使用者對某個種類的評分都較高時, 就可以推薦他與該種類歸在同一組的其他種類  
例如:   
'Category 3', 'Category 4', 'Category 5', 'Category 6'間有較高正相關,  
就把'beaches', 'parks', 'theatres', 'museums'歸在同一組,  
若使用者對beaches評分很高, 可能可以推薦parks/theatres/museums給他  
根據相關係數大致歸出了5組：
* [Category 3, Category 4, Category 5, Category 6]
* [Category 7, Category 8, Category 9, Category 10, Category 11]
* [Category 12, Category 13, Category 14]
* [Category 17, Category 18, Category 19]
* [Category 22, Category 23, Category 24]
## Define a reasonable problem
**Clusterring**:   
    根據過去的評分資料將使用者分群, 可用來決定未來要推薦給該使用者的旅遊地點種類
## How to improve results step-by-step
### Original result
  ![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/1.png)
### Reasons

### Approaches

### Improvement
