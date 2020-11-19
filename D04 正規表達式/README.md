# Day4 正規表達式 (Regular Expression)
* 使用 Python 操作正規表達式，re 專門處理 Regex

## Python 字串前綴
* 在 Python 中，反斜線 (\) 會被當作是特殊符號得跳脫字元，像是 "\n" 代表換行，加上跳脫字元後 "\\n" 即代表一般 "\n" 符號
* 為了避免字串中出現過多的反斜線，進而導致難以維護正規表達式的配對，因此我們可以使用原始字串前綴 `r"str"`，因此 `r"\n" == "\\n"`
* 為了避免出現特殊符號問題，習慣上會將正規表達式的模式對象加上字串前綴 (ex: `r"\W\.\D"`)

## 建立對象模式 (Pattern Object)
### re.compile(pattern, flags=0)
* 將正規表達式轉為 pattern object，以此方法將其保存下來供後續之用
```python=
import re

# 欲配對文本，期望配對出 SaveTheWorld@hotmail.com
txt = 'SaveTheWorld@hotmail.com \n foobar@gmail.com'

#建立模式對象
pattern_obj = re.compile(pattern=r"(.*)@(?!gmail)\w+\.com")

#進行配對 (使用 pattern.search 配對)
x1 = pattern_obj.search(txt)
print(x1.group())
```

### re.search(pattern, string, flags=0)
* 掃描字符串，查詢匹配正規表達式模式的位置，返回 MatchObject 的物件
* 若沒有可匹配的位置，則返回 None
* 若有多個可配對位置，只有第一個配對成功的會返回

### re.match(pattern, string, flags=0)
* 從字串開始的位置進行配對，只會配對字串開頭，若配對成功則返回 Match 的物件實例，失敗則返回 None
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.match(pattern, txt)
print(type(match)) #顯示為re.Match 物件實例
print(match)

print('\n----分隔線----')
print(f'Match start: {match.start()}; Match end: {match.end()}') #使用.start(), .end()返回配對的起點與終點

print('\n----分隔線----')
print(f'Match text: {match.group()}') #使用.group() or .group(0)返回配對的字串
```
輸出：
```
<class 're.Match'>
<re.Match object; span=(0, 24), match='SaveTheWorld@hotmail.com'>

----分隔線----
Match start: 0; Match end: 24

----分隔線----
Match text: SaveTheWorld@hotmail.com
```

### re.findall(pattern, string, flags=0)
* 掃描字符串，找到正規表達式所配對的所有子串，並組成一個 list 返回
* 若沒有配對成功，則返回空 list
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.findall(pattern, txt)
print(type(match)) #list 物件實力
print(match)
```
輸出：
```
<class 'list'>
['SaveTheWorld@hotmail.com', ' zzzGroup@yahoo.com']
```

### re.finditer(pattern, string, flags=0)
* 和 findall 類似
* 在字符串中找尋正規表達式可以匹配的所有子字串，並返回一個迭代器 (iterator)
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.finditer(pattern, txt)
print(type(match)) #iterator 物件實例
print('\n----分隔線----')
for ma in match:
    print(ma)
    print(f'Match start: {ma.start()}; Match end: {ma.end()}') #使用.start(), .end()返回配對的起點與終點
    print(f'Match text: {ma.group()}') #使用.group() or .group(0)返回配對的字串
    print('\n----分隔線----')
```
輸出：
```
<class 'callable_iterator'>

----分隔線----
<re.Match object; span=(0, 24), match='SaveTheWorld@hotmail.com'>
Match start: 0; Match end: 24
Match text: SaveTheWorld@hotmail.com

----分隔線----
<re.Match object; span=(45, 64), match=' zzzGroup@yahoo.com'>
Match start: 45; Match end: 64
Match text:  zzzGroup@yahoo.com

----分隔線----
```

### re.sub(pattern, repl, string, count=0, flags=0)
* 在字符串中找到正規表達式匹配的子字串，使用另外一個字串 repl 替換匹配的字串
* 若沒有可匹配的字串，即返回未被修改的原始字串
* count 變數可以用來指定要替代的次數，如果 count 是 0(預設值)，所有成功配對的都修改
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.sub(pattern, 'REPLACE', txt, count=0)
match #配對到的email都修改為REPLACE
```
輸出：
```
'REPLACE \n foobar@gmail.com \nREPLACE'
```

* 將 count 設為 1，僅修改第一個找到的
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.sub(pattern, 'REPLACE', txt, count=1) #將count設為1
match #只有一個配對到的修改為REPLACE
```
輸出：
```
'REPLACE \n foobar@gmail.com \n zzzGroup@yahoo.com'
```

### re.subn(pattern, repl, string, count=0, flags=0)
* 功能與 `re.sub()` 基本上相同，但在返回值時會同時返回新的字符串與替換次數
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.subn(pattern, 'REPLACE', txt, count=0)
match #可以發現一共配對替換2次
```
輸出：
```
('REPLACE \n foobar@gmail.com \nREPLACE', 2)
```

* 將 count 設為 1，僅修改第一個找到的
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r".*@(?!gmail)\w+\.com" #這裡使用原始字串作為配對

#進行配對
match = re.subn(pattern, 'REPLACE', txt, count=1) #將count設為1
match #只配對替換1次
```
輸出：
```
('REPLACE \n foobar@gmail.com \n zzzGroup@yahoo.com', 1)
```

### re.split(pattern, string, maxsplit=0, flags=0)
* 利用正規表達式將成功配對的字串部分分割為一個列表，並返回分割後的列表
* maxsplit 是用來指定最多切割多少份，若是 0 (預設值)，則所有配對成功的都會進行切割
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r"\n" #這裡改為配對換行符號

#進行配對
match = re.split(pattern, txt)
match
```
輸出：
```
['SaveTheWorld@hotmail.com ', ' foobar@gmail.com ', ' zzzGroup@yahoo.com']
```
* count 設 1
```python=
#欲配對文本
txt = "SaveTheWorld@hotmail.com \n foobar@gmail.com \n zzzGroup@yahoo.com" 
pattern = r"\n" #這裡改為配對換行符號

#進行配對
match = re.split(pattern, txt, maxsplit=1) #設定最多只配對分割一組
match
```
輸出：
```
['SaveTheWorld@hotmail.com ', ' foobar@gmail.com \n zzzGroup@yahoo.com']
```

## flags 參數
* 此參數可以控制匹配模式，大部分的匹配模式都可以直接使用正規表達式的規則寫出，但此參數提供我們更方便的方法來控制匹配模式。例如:
    * re.I (re.IGNORECASE): 忽略大小寫模式
    * re.M (re.MULTILINE): 多行模式
    * re.S (re.DOTALL): 讓.可以匹配所有的字元 (原本.無法匹配換行字元)
可以使用|來結合多種模式

### flags參數: re.I (re.IGNORECASE)
```python=
#欲配對文本
txt = "Leo123 \nkevin456 \n"
pattern = r"[a-z]+" #配對所有小寫a-z字符 

#進行配對_1
match = re.findall(pattern, txt) #使用預設的一般配對模式
print(type(match)) 
print(match)
#可以發現無法配對大寫的L

print('\n----分隔線----')

#進行配對_2
match2 = re.findall(pattern, txt, flags=re.I)
print(type(match2)) 
print(match2)
#可以發現再加上 re.I後, 可以互略大小寫的配對
```
輸出：
```
<class 'list'>
['eo', 'kevin']

----分隔線----
<class 'list'>
['Leo', 'kevin']
```

### flags參數: re.M (re.MULTILINE)
```python=
#欲配對文本
txt = "Leo123 \nkevin456 \n"
pattern = r"^[a-zA-Z]+" #配對所有開頭是a-z或是A-Z的字元

#進行配對_1
match = re.findall(pattern, txt) #使用預設的一般配對模式
print(type(match)) 
print(match)
#可以發現只配對到Leo (因為在一般配對模式下, 文本被視為一個含有\n的長字串)

print('\n----分隔線----')

#進行配對_2
match2 = re.findall(pattern, txt, flags=re.M) #使用多行配對模式
print(type(match2)) 
print(match2)
#可以發現加上re.M後，可以配對到Leo, Kevin (因為在\n換行符號後會視為新的字串來配對)
```
輸出：
```
<class 'list'>
['Leo']

----分隔線----
<class 'list'>
['Leo', 'kevin']
```

### flags參數: re.S (re.DOTALL)
```python=
#欲配對文本
txt = "Leo123 \nkevin456 \n"
pattern = r".+" #配對所有開頭是a-z或是A-Z的字元

#進行配對_1
match = re.findall(pattern, txt) #使用預設的一般配對模式
print(type(match)) 
print(match)
#配對的內容不包含\n字串

print('\n----分隔線----')

#進行配對_2
match2 = re.findall(pattern, txt, flags=re.S) #使用DOTALL配對模式
print(type(match2)) 
print(match2)
#這樣配對也包含了\n換行符號
```
輸出：
```
<class 'list'>
['Leo123 ', 'kevin456 ']

----分隔線----
<class 'list'>
['Leo123 \nkevin456 \n']
```

### flags參數: 結合多種配對模式 (re.I|re.M)
```python=
#欲配對文本
txt = "Leo123 \nkevin456 \n"
pattern = r"^[a-z]+" #配對所有開頭是a-z

#進行配對_1
match = re.findall(pattern, txt) #使用預設的一般配對模式
print(type(match)) 
print(match)
#一般模式下，找不到可配對字串

print('\n----分隔線----')

#進行配對_2
match2 = re.findall(pattern, txt, flags=re.I|re.M) #使用多行配對模式
print(type(match2)) 
print(match2)
#可以發現加上re.I|re.M後，可以配對到Leo, kevin
```
輸出
```
<class 'list'>
[]

----分隔線----
<class 'list'>
['Leo', 'kevin']
```

## 語法對照表
![](https://github.com/myps6415/NLP-marathon/blob/main/D04%20正規表達式/regex1.png?raw=true)