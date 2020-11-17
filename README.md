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