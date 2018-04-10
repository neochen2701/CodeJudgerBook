# 題目加入流程圖 #

# 使用步驟 #

## 一、加入流程圖標籤 ##

可於**題目說明**或**解題思路**中加入流程圖，在想要加入流程圖的文字範圍內事先加入以下標籤：

```
<div class="mermaid">

</div>
```



## 二、寫入流程圖 ##

在標籤中加入下列內容

```
<div class="mermaid">
graph LR
      A[第一步] --- B[第二步]
      B --- C[第三步]
      C --- D[第四步]
</div>
```
即可顯示：
![](https://i.imgur.com/8wBbBqd.png)

若需調整流程圖顯示方向至**又上至下**，則將```graph LR```更改為```graph TD```

```
<div class="mermaid">
    graph TD
      A[第一步] --- B[第二步]
      B --- C[第三步]
      C --- D[第四步]
</div>
```

![](https://i.imgur.com/hIJAOW9.png)



## 三、加入流程圖標籤 ##

如需在流程圖中加入標籤可使用```|標籤名稱|```：

```
<div class="mermaid">
    graph TD
      A[第一步] --- |這是一個標籤|B[第二步]
      B --- C[第三步]
      C --- D[第四步]
</div>
```

![](https://i.imgur.com/3jjeLxF.png)



## 四、多選項流程 ##

如需在流程圖中新增多個選項項目，可直接針對同一個節點新增不皺至多個選項

```
<div class="mermaid">
    graph TD
      A[第一步] --- |這是一個標籤|B[第二步]
      B --- C[第三步]
      C --- D[第四步選項A]
      C --- E[第四步選項B]
      C --- F[第四步選項C]
</div>
```

![](https://i.imgur.com/2QdVSGw.png)

選項亦可匯流至指定節點

```
<div class="mermaid">
    graph TD
      A[第一步] --- |這是一個標籤|B[第二步]
      B --- C[第三步]
      C --- D[第四步選項A]
      C --- E[第四步選項B]
      C --- F[第四步選項C]
      D --- G[結果A]
      E --- G[結果A]
      F --- H[結果B]
</div>
```

![](https://i.imgur.com/TFCMVM1.png)



## 五、完整範例示範 ##

```
<div class="mermaid">
    graph TD
      A[打開電腦] -->|開啟編輯器| B(打開待編修檔)
      B --> C{閱讀題目說明並思考解法}
      C -->|注意重點1| D[檢查數字是否更動位置]
      C -->|注意重點2| E[檢查文字是否正確對齊]
      C -->|注意重點3| F[檢查是否有語法錯誤]
</div>
```

![](https://i.imgur.com/CR5mBw4.png)