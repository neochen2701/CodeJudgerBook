# 6.1 Code Judger與校務系統整合服務API

FORMAT: 1.0

## Code Judger與校務系統整合服務API

(Code Judger and school system integration web service API, CJ\_school\_API)

* 此CJ\_school\_API為Code Judger全校授權學校之加購客制化服務，讓校務系統與Code Judger進行溝通
* 方便學校將資訊、校務等系統的資訊與Code Judger雙向連動
* 共計有3支API，其功能分別為：
  1. 由校務系統新增老師及學生帳號資訊至Code Judger
  2. 由校務系統新增課程及修課學生名單至Code Judger
  3. 取得Code Judger的課程小考成績
* 以下API開頭網址皆使用\[[https://123.codejudger.com/\]，實際網址依全校授權學校需求建置](https://123.codejudger.com/]%EF%BC%8C%E5%AF%A6%E9%9A%9B%E7%B6%B2%E5%9D%80%E4%BE%9D%E5%85%A8%E6%A0%A1%E6%8E%88%E6%AC%8A%E5%AD%B8%E6%A0%A1%E9%9C%80%E6%B1%82%E5%BB%BA%E7%BD%AE)

## Group 1. 帳號登入 API

新增老師及學生帳號資訊\[[https://123.codejudger.com/api/v1/auth/login?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution}](https://123.codejudger.com/api/v1/auth/login?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution})]

### 傳入帳號資訊至Code Judger \[POST]

* POST的參數
  * user\_account: 老師的帳號或是學生的學號 (required, String)
  * user\_type: 使用者身份 `TEACHER/STUDENT`  (required, String)
  * user\_name: 使用者姓名  (required, String)
  * access\_token: 認證碼  (required, String)
  * time\_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)

> 備註：
>
> 1. 身份為老師時，請將user\_type改成TEACHER；身份為學生時，請將user\_type改成STUDENT
> 2. user\_account與access\_token在與學校溝通後建置

* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)
  * url: 回傳OK後導到此url就進入系統 (required, String)

#### 範例

代號為peter的王小明老師要登入

* user\_account : peter@tqc.mail.edu.tw
* user\_type: TEACHER
* user\_name: 王小明
* access\_token：sha1(xxxxxxxx\_1234567890)
* time\_stamp: 1234567890
* institution: 13

**POST**

*   URL：

    [https://123.codejudger.com/api/v1/auth/login](https://123.codejudger.com/api/v1/auth/login)
*   BODY：

    user\_account=peter@tqc.mail.edu.tw\&user\_type=TEACHER\&user\_name=王小明\&access\_token=sha1(xxxxxxxx\_1234567890)\&time\_stamp=1234567890\&institution=13

**回傳結果**

```javascript
{
    "status": "OK",
    "url": "https://123.codejudger.com/ewfdskwe;drfjwe;ijfjwewfjlwefjlkwejfljwelfjweljflwjefowejfoiwejfwolefefwojweo"
}
```

## Group 2. 新增課程及修課學生名單 API

新增課程及修課學生名單\[[https://123.codejudger.com/api/v2/course/import?user\_account={user\_account}user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution}\&course\_number={course\_number}\&course\_name={course\_name}\&student\_accounts={student\_accounts}\&student\_names={student\_names}](https://123.codejudger.com/api/v2/course/import?user\_account={user\_account}user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution}\&course\_number={course\_number}\&course\_name={course\_name}\&student\_accounts={student\_accounts}\&student\_names={student\_names})]

### 傳入課程及修課學生名單至Code Judger \[POST]

* POST的參數
  * user\_account: 老師的帳號或是學生的學號 (required, String)
  * user\_name: 使用者姓名  (required, String)
  * access\_token: 認證碼  (required, String)
  * time\_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)
  * course\_number: 學校指定的課程代碼,必須一個課程只有唯一一個代碼  (required, String)
  * course\_name: 課程名稱  (required, String)
  * student\_accounts: 學生學號，必須為陣列  (required, Array)
  * student\_names: 學生名字，必須為陣列  (required, Array)
* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)

#### 範例

代號為peter的王小明老師要加入課號為1091\_B10942A的資管大一程式語言(Python)課程，下面要新增學號為B97901022的張曉明同學和學號為B97901023的王陽明同學

* user\_account : peter@tqc.mail.edu.tw
* user\_name: 王小明
* access\_token：sha1(xxxxxxxx\_1234567890)
* time\_stamp: 1234567890
* institution: 13
* course\_number：1091\_B10942A
* course\_name：資管大一程式語言(Python)
* student\_accounts\[0] = B97901022@tqc.mail.edu.tw
* student\_accounts\[1] = B97901023@tqc.mail.edu.tw
* student\_names\[0] = 張曉明
* student\_names\[1] = 王陽明

**POST**

*   URL：

    [https://123.codejudger.com/api/v2/course/import](https://123.codejudger.com/api/v2/course/import)
*   BODY：

    user\_account=peter@tqc.mail.edu.tw\&user\_name=王小明\&access\_token=sha1(xxxxxxxx\_1234567890)\&time\_stamp=1234567890\&institution=13\&course\_number=1091\_B10942A\&course\_name=資管大一程式語言(Python)\&student\_accounts\[0]=B97901022@tqc.mail.edu.tw\&student\_accounts\[1]=B97901023@tqc.mail.edu.tw\&student\_names\[0]=張曉明\&student\_names\[1]=王陽明

**回傳結果**

```javascript
{
    "status": "OK"
}
```

> 備註：
>
> 1. 如果此帳號不存在，開新的帳號為老師帳號，帳號相同不會重複開
> 2. 如果此課程不存在，開新的課程加入老師帳號底下，課程代碼相同不會重複開
> 3. 如王老師要同時新增完 資管大一程式語言(Python)，又想新增 資管大一程式語言(C++)，代碼為1091\_B10942A，將上面的course\_number和course\_name分別改成1091\_B10943A和資管大一程式語言(C++)即可
> 4. 可再依學校需求增加「開課日期區間」或是加入「學年」、「學期」

## Group 3. 取得課程學生考試成績 API

提供帳號資訊\[[https://chu.codejudger.com/api/v2/course/export\_exams?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution}](https://chu.codejudger.com/api/v2/course/export\_exams?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution})]

### 提供帳號資訊至Code Judger，獲得學生成績 \[POST]

* POST的參數
  * user\_account: 老師的帳號或是學生的學號 (required, String)
  * access\_token: 認證碼  (required, String)
  * time\_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)
  * course\_number: 學校指定的課程代碼,必須一個課程只有唯一一個代碼  (required, String)
* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)
  * chapter: 章節陣列
    * exam: 測驗陣列
      * exam\_title: 測驗題目
      * scores: 陣列
        * account: 學生帳號
        * points: 成績

#### 範例

代號為peter的王小明老師要取得課程代碼為1091\_B10942A的小考資料

* user\_account : peter@tqc.mail.edu.tw
* access\_token：sha1(xxxxxxxx\_1234567890)
* time\_stamp: 1234567890
* institution: 13
* course\_number：1091\_B10942A

**POST**

*   URL：

    [https://123.codejudger.com/api/v2/course/import](https://123.codejudger.com/api/v2/course/import)
*   BODY：

    user\_account=peter@tqc.mail.edu.tw\&access\_token=sha1(xxxxxxxx\_1234567890)\&time\_stamp=1234567890\&institution=13\&course\_number=1091\_B10942A

**回傳結果**

```javascript
{
  "status" : "OK",
  "chapter" : [
    {
    "exam" : [
        {
        "exam_title" : "第1次小考",
        "scores" : [
            {
              "account" : "B97901022@tqc.mail.edu.tw",
              "points" : "80"
            },
            {
              "account" : "B97901023@tqc.mail.edu.tw",
              "points" : "60"
            }
          ]
        },
        {
        "exam_title" : "第2次小考",
        "scores" : [
            {
              "account" : "B97901022@tqc.mail.edu.tw",
              "points" : "100"
            },
            {
              "account" : "B97901023@tqc.mail.edu.tw",
              "points" : "70"
            }
          ]
        }
      ]
    }
  ]
}
```

## Group 4. 取得課程學生作業成績 API

提供帳號資訊\[[https://123.codejudger.com/api/v2/course/export\_assignments?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution}](https://123.codejudger.com/api/v2/course/export\_assignments?user\_account={user\_account}\&user\_type={user\_type}\&user\_name={user\_name}\&access\_token={access\_token}\&time\_stamp={time\_stamp}\&institution={institution})]

### 提供帳號資訊至Code Judger，獲得學生成績 \[POST]

* POST的參數
  * user\_account: 老師的帳號或是學生的學號 (required, String)
  * access\_token: 認證碼  (required, String)
  * time\_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)
  * course\_number: 學校指定的課程代碼,必須一個課程只有唯一一個代碼  (required, String)
* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)
  * chapter: 章節陣列
    * exam: 測驗陣列
      * exam\_title: 測驗題目
      * scores: 陣列
        * account: 學生帳號
        * points: 成績

#### 範例

代號為peter的王小明老師要取得課程代碼為1091\_B10942A的作業資料

* user\_account : peter@tqc.mail.edu.tw
* access\_token：sha1(xxxxxxxx\_1234567890)
* time\_stamp: 1234567890
* institution: 13
* course\_number：1091\_B10942A

**POST**

*   URL：

    [https://123.codejudger.com/api/v2/course/export\_assignments](https://123.codejudger.com/api/v2/course/export\_assignments)
*   BODY：

    user\_account=peter@tqc.mail.edu.tw\&access\_token=sha1(xxxxxxxx\_1234567890)\&time\_stamp=1234567890\&institution=13\&course\_number=1091\_B10942A

```json
{
    "status": "OK",
    "chapter": [
        {
            "assignment": [
                {
                    "assignment_title": "第1次作業",
                    "scores": [
                        {
                            "account": "B97901022@tqc.mail.edu.tw",
                            "points": "80"
                        },
                        {
                            "account": "B97901023@tqc.mail.edu.tw",
                            "points": "60"
                        }
                    ]
                },
                {
                    "assignment_title": "第2次作業",
                    "scores": [
                        {
                            "account": "B97901022@tqc.mail.edu.tw",
                            "points": "100"
                        },
                        {
                            "account": "B97901023@tqc.mail.edu.tw",
                            "points": "70"
                        }
                    ]
                }
            ]
        }
    ]
}
```

