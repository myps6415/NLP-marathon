# NLP-marathon
Learn NLP knowledge

## Day1 Python 文字處理函數介紹
* Python 基礎文字處理
    * 計算字串長度 
    * 取出字串內特定區間字符
    * 合併字串
    * 特殊字符運用
    * 判斷字符存在與否、打小寫、數字
    * 移除、取代字符
    * 在字串中尋找指定字符
* 內容
    * strip()
    * replace()
    * split()
    * count()
    * startswith()/endswith()
    * capitalize(): 將字串開頭轉為大寫
    * find()/index(): 尋找字串中字元所在位置，index() 當字元不存在時報錯，find() 會輸出 -1
    * upper()/lower()
    * Counter(): 可以快速計算字串中所有字元出現過的次數
    ```python=
    from collections import Counter
    
    Counter('your sentence')
    ```
* 參考 [W3schools](https://www.w3schools.com/python/python_strings.asp)

## Day2 Python 文字處理函數介紹
* Python 基礎文字處理
    * 判斷字串中特定字符
    * 字串格式化
* 內容
    * string.isnumeric(), string.isdigit(), string.isdecimal(): 用來判定字串內是否都屬於數值字元，差別在於 unicode 定義的區間不同
    
    string = '3'
    
    |3 ways|True/False|
    |-|-|
    |isnumeric|True|
    |isdigit|True|
    |isdecimal|True|
    
    string = '½'
    
    |3 ways|True/False|
    |-|-|
    |isnumeric|True|
    |isdigit|False|
    |isdecimal|False|
    
    string = '0.3.8.'
    
    |3 ways|True/False|
    |-|-|
    |isnumeric|True|
    |isdigit|False|
    |isdecimal|True|
    
    string = '2.345' (. 不屬於 numeric 定義字元，所以三個都輸出 False)
    
    |3 ways|True/False|
    |-|-|
    |isnumeric|False|
    |isdigit|False|
    |isdecimal|False|
    
    * isalnum(): string 為字符和數字組成，輸出 True，否則輸出 False
    * isupper()/islower(): 判斷字串內字元是否都是大寫/小寫
    * 常見字串操作整理：
        * [英文整理表格](https://www.w3schools.com/python/python_ref_string.asp)
        * [中文整理表格](https://www.runoob.com/python/python-strings.html)
        
    * String.format()
    ```python=
    '{} {}'.format('python', 'course')
    ```

* 參考資料
    * [Corey Schafer: String Formatting](https://www.youtube.com/watch?v=vTX3IwquFkc)
    {%youtube vTX3IwquFkc%}

## Day3 正規表達式 (Regular Expression)
* 常用於：
    * 模式比對 (Pattern Matching)
    * 文本處理 (Text Manipulation)
    * 解析資料 (Parsing Data)
* 由左到右配對
* 正規表達式語法：
    * Literal Matches: 直接依據輸入的配對文字
    * Character Classes: 有時需要配對多個字元的集合，此時可以利用正規表達式中的 Character Class，例如從文本中找出關鍵字 "gray" 和 "grey"，可以利用 Character Class 來取出 "gray" 或 "grey"
        Test string:
        ```string=
        The color of the wall is gray.
        And, grey happens to be my favorate color.
        ```
        
        Regular Expression
        ```regex=
        gr[ae]y
        ```
        
        * `[a-z]` 取出英文小寫 a ~ z
        * `[a-zA-Z0-9]` 取出英文小寫 a ~ z、大寫 A ~ Z 和數字 0 ~ 9
        * `[^a-zA-Z]` 取出 a ~ z 和 A ~ Z 以外的字元

    * Alternations: 可以理解成 "或 (or)"
        Test string:
        ```string=
        I love cat.
        I love cats.
        I love dog.
        I love dogs.
        ```
        Regular Expression
        ```regex=
        cat|dog
        ```
        所有 cat 和 dog 都會被標示出來

    * Meta Characters: 在正規表達式中有些特殊的符號可以用來代表特別的配對或縮寫，常見的正規表達式 Meta Characters 有：
        * .  ：配對任意字元字串(對！沒看錯,就只有一個點！！)
        * \  ：特殊跳脫字元(用來將有特殊意義的字元轉回一般字元配對）
        * \d：任何數字字元(等同於[0-9]的縮寫）
        * \D：任何非數字字元(等同於[^0-9]的縮寫)
        * \w：任何數字字母底線(等同於[a-zA-Z0-9_]的縮寫
        * \W：任何非數字字母底線(等同於[^a-zA-Z0-9_]的縮寫)
        * \s：任何空白字元(空白, 換行, tab) (等同於[ \f\n\r\t\v]的縮寫)
        * \S : 任何非空白字元(空白, 換行, tab) (等同於[^ \f\n\r\t\v]的縮寫)

    * Quantifiers: 在前面的舉例中，要比對多個字元時，往往需要將正規表達式的配對重複多次，例如 `[\w].-\d\d\d` ，在這裡我們將`\d`重複 3 次以配對 3 個數字字元符號，正規表達式提供了特殊的計數符號，幫助我們不需要重複字元也可以達到配對多次的效果！
        * * : 表該配對為0次或1次以上 (Zero-to-many)
        * ? : 出現 0 次或 1 次 (表該配對可有可無)
        * + : 表該配對為一次或一次以上 (One-to-many)
        * {number} : 表該配對需重複 number 次
        * {min, max} : 表該配對至少 min 次，至多 max 次

    * Group: 可以使用小括號()將配對包起來以整個詞作配對
        Test string:
        ```string=
        I love cat.
        I love cats.
        I love dog.
        I love dogs.
        ```
        Regular Expression
        ```regex=
        I love cat|dog
        ```
        僅會取出：`I love cat`、`I love cat`、`dog`、`dog`
        
        如果 Regular Expression 下
        ```regex=
        I love (cat|dog)
        ```
        會取出：`I love cat`、`I love cat`、`I love dog`、`I love dog`

    * Lookarounds: 利用特殊的語法來讓配對字元看前看後，例如找出命名 "file_xxx" 中後面的檔案名稱 (不包含 file)。我們可以利用 "lookahead (看前)" 與 "lookbehind (看後)" 來達到目的
        * (?=) : 若滿足給定字元，及配對給定字元前面的文字 (positive lookahead)
        * (?!) : 若滿足給定字元，及”不”配對給定字元前面的文字(negative lookahead)
        * (?<=) : 若滿足給定字元，及配對給定字元後面的文字(positive lookbehind)
        * (?<!)：若滿足給定字元，及”不”配對給定字元後面的文字(negative lookbehind)
        Test string:
        ```string=
        silly_cat
        happy_cat
        cool_dog
        cool_cat
        cool_bird
        cool_fish
        fun_cat
        ```
        Regular Expression
        ```regex=
        cool(?=_cat)
        ```
        會取出：`cool`
        
    * Word-boundary: 可以在正規表達式中設定搜尋規則邊界，像是當字詞字元轉為符號字元時即可設定為配對邊界。在正規表達式中這類型的邊界以 "\b" 表示
    * Anchor: 除了上述以字詞當作邊界，也可以將字串開頭或結尾當作配對邊界，可以使用 "^" 作為開頭配對邊界，"$" 作為結尾配對