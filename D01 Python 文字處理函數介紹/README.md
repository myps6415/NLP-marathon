# Day1 Python 文字處理函數介紹
## Python 基礎文字處理
* 計算字串長度 
* 取出字串內特定區間字符
* 合併字串
* 特殊字符運用
* 判斷字符存在與否、打小寫、數字
* 移除、取代字符
* 在字串中尋找指定字符

## 內容
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