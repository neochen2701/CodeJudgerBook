# 2.1.3 題目加入流程圖

Gode Judger的編題介面可使用mermaid產生流程圖，以下為各種範例說明。
可從[mermaid](https://mermaidjs.github.io/)手冊，了解更多創建圖形的方式。

## 一、加入流程圖標籤

可於**題目說明**或**解題思路**中加入流程圖，在想要加入流程圖的文字範圍內事先加入以下標籤：

```text
<div class="mermaid">

</div>
```

## 二、編寫流程圖

在標籤中加入下列內容

```text
<div class="mermaid">
graph LR
      A[第一步] --> B[第二步]
      B --> C[第三步]
      C --> D[第四步]
</div>
```

即可顯示：
![流程圖](../../.gitbook/assets/gitbook-Mermaid-0.png)

### 1.流程圖顯示方向

若需調整流程圖顯示方向**由上至下**，則將`graph LR`更改為`graph TD`

```text
<div class="mermaid">
    graph TD
      A[第一步] --> B[第二步]
      B --> C[第三步]
      C --> D[第四步]
</div>
```

即可顯示：

![流程圖由上至下](../../.gitbook/assets/gitbook-Mermaid-1.png)

### 2.流程圖圖形

方形使用\[\]，圓邊使用\(\)，菱形使用{}

```text
<div class="mermaid">
graph TD
    A[方形]
    B(圓邊)
    c{菱形}
</div>
```

即可顯示：

![流程圖圖形](../../.gitbook/assets/gitbook-Mermaid-2.png)

### 3.路徑及箭號

一般路徑為 --- ，加上箭號為 --&gt;   
 虛線為 -.- 加上箭號為 -.-&gt;   
 粗線為 === 加上箭號為 ==&gt;   

```text
<div class="mermaid">
    graph LR
      A --> B
      B -.-> C
      C ==> D
</div>
```

即可顯示：

![路徑及箭號](../../.gitbook/assets/gitbook-Mermaid-3.png)

### 4.路徑標籤

如需在流程圖中加入標籤可使用`|標籤名稱|`：

```text
<div class="mermaid">
    graph TD
      A[第一步] --> |這是一個標籤|B[第二步]
      B --> C[第三步]
      C --> D[第四步]
</div>
```

即可顯示：

![路徑標籤](../../.gitbook/assets/gitbook-Mermaid-4.png)

## 三、多選項流程

如需在流程圖中新增多個選項項目，可直接針對同一個節點新增不皺至多個選項

```text
<div class="mermaid">
    graph TD
      A[第一步] --> B[第二步]
      B --> C[第三步選項1]
      B --> D[第三步選項2]
      B --> E[第三步選項3]
</div>
```

即可顯示：

![多選項流程](../../.gitbook/assets/gitbook-Mermaid-5.png)

選項亦可匯流至指定節點

```text
<div class="mermaid">
    graph TD
      A[第一步] --> B[第二步]
      B --> C[第三步]
      C --> D[第四步選項A]
      C --> E[第四步選項B]
      C --> F[第四步選項C]
      D --> G[結果A]
      E --> G[結果A]
      F --> H[結果B]
</div>
```

即可顯示：

![多選項流程匯流至指定節點](../../.gitbook/assets/gitbook-Mermaid-6.png)

## 四、完整範例示範

```text
<div class="mermaid">
    graph TD
      A[打開電腦] -->|開啟編輯器| B(打開待編修檔)
      B --> C{閱讀題目說明並思考解法}
      C -->|注意重點1| D[檢查數字是否更動位置]
      C -->|注意重點2| E[檢查文字是否正確對齊]
      C -->|注意重點3| F[檢查是否有語法錯誤]
</div>
```

即可顯示：

![完整範例](../../.gitbook/assets/gitbook-Mermaid-7.png)
