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
### Step 1:
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/1.png)  
左為用**Kmeans**分成5群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
因為是高維度的資料, 在計算距離上可能會有問題, 所以決定嘗試先降維再分群  
### Step 2:
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/2.png)  
左為**先降維**再用**Kmeans**分成5群的結果, 右為自己根據使用者對各組的平均評分所定義的分群
先降維再分群有分得比較漂亮, 但跟自定義的分群不太像
反覆調整Step1和Step2的參數後都沒有變比較好, 因此決定嘗試改用別的分群方法
### Step 3:
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/3.png)  
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/4.png)  
左上為**沒經降維**就直接用**MiniBatchKMeans**分成5群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
左下為**先經降維**再用**MiniBatchKMeans**分成5群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
原本只是想看看若用MiniBatchKMeans會有什麼變化,   
本來以為會分得更不好, 結果意外發現可以分得跟原先定義的分群更像(左上圖比起Step1的圖, 右上角可以分出了兩群, 右下角可以合為一群)      
MiniBatchKMeans與Kmeans最大的差別是會收斂得更快  
### Step 4:
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/5.png)  
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/6.png)  
左上為**沒經降維**就直接用**KMeans**分成7群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
左下為**先經降維**再用**KMeans**分成7群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
因為使用的對照標準是自己定義的, 有可能定義得不夠好, 所以嘗試調整分群, 把原本設定的群分得更細,   
若一組中有任兩個相關係數低於0.3的種類就將它們拆組, 最後歸出7組, 再根據使用者對各組的平均評分定義分群  
因此使用Kmeans時也改成分7群  
分得更細後Kmeans**未經降維**的分群結果與自定義分群間的相似度有**比Step1**更高,  
而**先經降維再分群**的結果與自定義分群間的相似度也有**比Step2**更高  

### Step 5:
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/7.png)  
![alt text](https://github.com/JCP1014/Travel-Review-Rating-Prediction/blob/master/figure/8.png)  
左上為**沒經降維**就直接用**MiniBatchKMeanss**分成7群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
左下為**先經降維**再用**MiniBatchKMeans**分成7群的結果, 右為自己根據使用者對各組的平均評分所定義的分群  
分成7群後改用MiniBatchKMean的改變比較沒那麼明顯,  
但左上圖比起Step4的左上圖, 下方中間偏右的地方仍有改善一點, 又更接近自定義的分群
