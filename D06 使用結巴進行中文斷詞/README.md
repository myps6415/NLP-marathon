# Day6 使用結巴進行中文斷詞
## 環境安裝
* 安裝 Jieba
```shell=
pip install jieba
```

* Python code import
```python=
import jieba
```

## 以 jieba 進行斷詞
* 結巴斷詞輸出為 generator，需使用遞迴將值取出
```python=
import jieba
import jieba.posseg as pseg

input_str = '小明碩士畢業於國立臺灣大學，現在在日本東京大學進修深造'
cutted_words = pseg.cut(input_str)
words = [(word, flag) for (word, flag) in cutted_words]
print(words)
```
print:
```
['小明', '碩士', '畢業', '於', '國立', '臺', '灣大學', '，', '現在', '在', '日本', '東京大學', '進修', '深造']
```

## 更改使用字典
* 將結巴使用的字典更改為對繁體中文表現較好的字典
* 可從結巴 [GitHub](https://github.com/fxsjy/jieba/tree/master/extra_dict) 下載
* 設定使用字典
```python=
jieba.set_dictionary('./dict.txt.big')
```

## 辨識新字詞
* 啟用 HMM 已辨識新字詞
* 預設 HMM 功能即為啟用，不用特地設為 True
```python=
input_string = "他来到了网易杭研大厦"
cutted_words = jieba.cut(input_string, HMM=True)
words = [word for word in cutted_words]
print(words)
```
print:
```
['他', '来到', '了', '网易', '杭研', '大厦']
```

## 新增自定義詞庫
* 在既有使用的字典下新增自訂義字詞
```python=
jieba.load_userdict("userdict.txt")
```

userdict.txt 格式：
```
行袂開跤 2 v
袂當 4 d
袂記 4 v
袂有 4 
唱著 
```

## 動態調整字典
* 動態加入字典
```python=
jieba.add_word('國立臺灣大學')
```

* 動態調整詞頻
```python=
jieba.suggest_freq("國立臺灣大學", True)
```

## 詞性標注
* 詞性標注 (PoS Tagging)
```python=
import jieba
import jieba.posseg as pseg

input_str = "小明碩士畢業於國立臺灣大學，現在在日本東京大學進修深造"
cutted_words = pseg.cut(input_str)
words = [(word, flag) for (word, flag) in cutted_words]
print(words)
```
* 詞性完整[對照表](http://blog.pulipuli.info/2017/11/fasttag-identify-part-of-speech-in.html)

## 取出斷詞位置
* 斷詞並標出詞的起始及結束位置
```python=
input_str = u'小明碩士畢業於國立臺灣大學，現在在日本東京大學進修深造' #在此將字串轉為unicode
words = jieba.tokenize(input_str)
for tk in words:
    print(f'word:{tk[0]}, start:{tk[1]}, end:{tk[2]}')
```
print:
```
word:小明, start:0, end:2
word:碩士, start:2, end:4
word:畢業, start:4, end:6
word:於, start:6, end:7
word:國立, start:7, end:9
word:臺灣大學, start:9, end:13
word:，, start:13, end:14
word:現在, start:14, end:16
word:在, start:16, end:17
word:日本東京大學, start:17, end:23
word:進修, start:23, end:25
word:深造, start:25, end:27
```