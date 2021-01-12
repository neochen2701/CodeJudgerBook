FORMAT: 1.0

# Code Judger與校務系統整合服務API

(Code Judger and school system integration web service API, CJ_school_API)

* 此CJ_school_API為Code Judger全校授權學校之加購客制化服務，讓校務系統與Code Judger進行溝通
* 方便學校將資訊、校務等系統的資訊與Code Judger雙向連動
* 共計有3支API，其功能分別為：
  1. 由校務系統新增老師及學生帳號資訊至Code Judger
  2. 由校務系統新增課程及修課學生名單至Code Judger
  3. 取得Code Judger的課程小考成績
* 以下API開頭網址皆使用[https://123.codejudger.com/]，實際網址依全校授權學校需求建置

---

# Group 1. 帳號登入 API

新增老師及學生帳號資訊[https://123.codejudger.com/api/v1/auth/login?user_account={user_account}&user_type={user_type}&user_name={user_name}&access_token={access_token}&time_stamp={time_stamp}&institution={institution}]

## 傳入帳號資訊至Code Judger [POST]

* POST的參數
  * user_account: 老師的帳號或是學生的學號 (required, String)
  * user_type: 使用者身份 `TEACHER/STUDENT`  (required, String)
  * user_name: 使用者姓名  (required, String)
  * access_token: 認證碼  (required, String)
  * time_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)

> 備註：
>
> 1. 身份為老師時，請將user_type改成TEACHER；身份為學生時，請將user_type改成STUDENT
> 2. user_account與access_token在與學校溝通後建置

* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)
  * url: 回傳OK後導到此url就進入系統 (required, String)

### 範例

代號為peter的王小明老師要登入

* user_account : peter@chu.edu.tw
* user_type: TEACHER
* user_name: 王小明
* access_token：shal(chu_tqcpython_1435224116)
* time_stamp: 1435224116
* institution: 13

#### POST

* URL：
  https://123.codejudger.com/api/v1/auth/login
* BODY：
  user_account=peter@chu.edu.tw&user_type=TEACHER&user_name=王小明&access_token=shal(chu_tqcpython_1435224116)&time_stamp=1435224116&institution=13

#### 回傳結果

```json
{
    "status": "OK",
    "url": "https://123.codejudger.com/ewfdskwe;drfjwe;ijfjwewfjlwefjlkwejfljwelfjweljflwjefowejfoiwejfwolefefwojweo"
}
```

---

# Group 2. 新增課程及修課學生名單 API

新增課程及修課學生名單[https://123.codejudger.com/api/v2/course/import?user_account={user_account}user_name={user_name}&access_token={access_token}&time_stamp={time_stamp}&institution={institution}&course_number={course_number}&course_name={course_name}&student_accounts={student_accounts}&student_names={student_names}]

## 傳入課程及修課學生名單至Code Judger [POST]

* POST的參數
  * user_account: 老師的帳號或是學生的學號 (required, String)
  * user_name: 使用者姓名  (required, String)
  * access_token: 認證碼  (required, String)
  * time_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)
  * course_number: 學校指定的課程代碼,必須一個課程只有唯一一個代碼  (required, String)
  * course_name: 課程名稱  (required, String)
  * student_accounts: 學生學號，必須為陣列  (required, Array)
  * student_names: 學生名字，必須為陣列  (required, Array)

* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)

### 範例

代號為peter的王小明老師要加入課號為1091_B10942A的資管大一程式語言(Python)課程，下面要新增學號為B97901022的張曉明同學和學號為B97901023的王陽明同學

* user_account : peter@chu.edu.tw
* user_name: 王小明
* access_token：shal(chu_tqcpython_1435224116)
* time_stamp: 1435224116
* institution: 13
* course_number：1091_B10942A
* course_name：資管大一程式語言(Python)
* student_accounts[0] = B97901022@chu.edu.tw
* student_accounts[1] = B97901023@chu.edu.tw
* student_names[0] = 張曉明
* student_names[1] = 王陽明

#### POST

* URL：
  https://123.codejudger.com/api/v2/course/import
* BODY：
  user_account=peter@chu.edu.tw&user_name=王小明&access_token=shal(chu_tqcpython_1435224116)&time_stamp=1435224116&institution=13&course_number=1091_B10942A&course_name=資管大一程式語言(Python)&student_accounts[0]=B97901022@chu.edu.tw&student_accounts[1]=B97901023@chu.edu.tw&student_names[0]=張曉明&student_names[1]=王陽明

#### 回傳結果

```json
{
    "status": "OK"
}
```

> 備註：
>
> 1. 如果此帳號不存在，開新的帳號為老師帳號，帳號相同不會重複開
> 2. 如果此課程不存在，開新的課程加入老師帳號底下，課程代碼相同不會重複開
> 3. 如王老師要同時新增完 資管大一程式語言(Python)，又想新增 資管大一程式語言(C++)，代碼為1091_B10942A，將上面的course_number和course_name分別改成1091_B10943A和資管大一程式語言(C++)即可
> 4. 可再依學校需求增加「開課日期區間」或是加入「學年」、「學期」

---

# Group 3. 取得課程學生成績 API

提供帳號資訊[https://chu.codejudger.com/api/v2/course/export_exams?user_account={user_account}&user_type={user_type}&user_name={user_name}&access_token={access_token}&time_stamp={time_stamp}&institution={institution}]

## 提供帳號資訊至Code Judger，獲得學生成績 [POST]

* POST的參數
  * user_account: 老師的帳號或是學生的學號 (required, String)
  * access_token: 認證碼  (required, String)
  * time_stamp: 時間戳  (required, String)
  * institution: 單位代號  (required, String)
  * course_number: 學校指定的課程代碼,必須一個課程只有唯一一個代碼  (required, String)

* 回傳參數
  * status: 狀態，沒問題的話為OK (required, String)
  * chapter: 章節陣列
    * exam: 測驗陣列
      * exam_title: 測驗題目
      * scores: 陣列
        * account: 學生帳號
        * points: 成績

### 範例

代號為peter的王小明老師要取得課程代碼為1091_B10942A的小考資料

* user_account : peter@chu.edu.tw
* access_token：shal(chu_tqcpython_1435224116)
* time_stamp: 1435224116
* institution: 13
* course_number：1091_B10942A

#### POST

* URL：
  https://123.codejudger.com/api/v2/course/import
* BODY：
  user_account=peter@chu.edu.tw&access_token=shal(chu_tqcpython_1435224116)&time_stamp=1435224116&institution=13&course_number=1091_B10942A

#### 回傳結果

```json
{
  "status" : "OK",
  "chapter" : [
    {
    "exam" : [
        {
        "exam_title" : "第1次小考",
        "scores" : [
            {
              "account" : "B97901022@chu.edu.tw",
              "points" : "80"
            },
            {
              "account" : "B97901023@chu.edu.tw",
              "points" : "60"
            }
          ]
        },
        {
        "exam_title" : "第2次小考",
        "scores" : [
            {
              "account" : "B97901022@chu.edu.tw",
              "points" : "100"
            },
            {
              "account" : "B97901023@chu.edu.tw",
              "points" : "70"
            }
          ]
        }
      ]
    }
  ]
}
```
