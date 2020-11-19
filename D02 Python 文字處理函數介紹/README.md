# Day2 Python 文字處理函數介紹
## Python 基礎文字處理
* 判斷字串中特定字符
* 字串格式化

## 內容
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