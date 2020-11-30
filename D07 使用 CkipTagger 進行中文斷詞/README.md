# Day7 使用 CkipTagger 進行中文斷詞
## 繁體中文斷詞：CkipTagger
* CkipTagger 為中研院詞庫小組所開發的斷詞套件，是以深度學習模型為基礎而成的斷詞應用。其訓練的文本資料來源為中央社、wiki (用舊版套件先進行斷詞) 及 ASBC(Academia Sinica Balanced Corpus)。

* CkipTagger 模型主要的功能有：
    1. WS：斷詞
    2. POS：詞性標注
    3. NER：實體辨識
    
## 系統環境安裝
* 標準安裝 (同時安裝 tensorflow, gdown)
    * gdown 是與 Google Drive 之間的 API，可以從 Google Drive 上下載資料
```shell=
pip install -U ckiptagger[tf, gdown]
```

* 最小安裝 (不安裝 tensorflow, gdown)
    * 若環境已有安裝 tensorflow, gdown，可使用此種方法
```shell=
pip install -U ckiptagger
```

* 完整安裝 (安裝 gpu 版 tensorflow)
```shell=
pip install -U ckiptagger[tfgpu,gdown]
```

## CkipTagger 優勢
* 在繁體中文斷詞與詞性標記表現優於結巴
* 能辨識 11 類一般領域專有名詞及 7 類數量詞
* 支援使用者自訂 參考/強制 詞典
* 支援不限長度的句子
* 不會自動 增/刪/改 輸入的文字

## CkipTagger 斷詞技巧
* Word-level approach
    * Maximum length (長詞優先)
    * 動態規劃查找最大概率路徑 (Jieba)

* Character-level approach
    * character Sequence Labeling

* CkipTagger 則是綜合上面兩種方法，針對 word 及 character 同時進行分析

## 以 CkipTagger 進行斷詞
* 下載預訓練權重
* 此模型需 2 GB 的儲存空間
```python=
from ckiptagger import data_utils, WS
data_utils.download_data_gdown('./')
```

* 建構斷詞器
* 使用 Ckiptagger 進行斷詞
```python=
#建構斷詞
ws = WS("./data")

input_string = '小明碩士畢業於國立臺灣大學，現在在日本東京大學進修深造'
word_sentence_list = ws(
    input_string,
    sentence_segmentation = True, # To consider delimiters
    segment_delimiter_set = {",", "。", ":", "?", "!", ";"}) # This is the defualt set of delimiters
print(word_sentence_list)
```
print:
```
[['小'], ['明'], ['碩'], ['士'], ['畢'], ['業'], ['於'], ['國'], ['立'], ['臺'], ['灣'], ['大'], ['學'], ['，'], ['現'], ['在'], ['在'], ['日'], ['本'], ['東'], ['京'], ['大'], ['學'], ['進'], ['修'], ['深'], ['造']]
```

## 以 CkipTagger 詞性標注
* 使用 Ckiptagger 詞性標注
```python=
from ckiptagger import POS

pos = POS("./data")
pos_sentence_list = pos(word_sentence_list)
print(pos_sentence_list)
```

## 以 CkipTagger 命名實體辨識
* 使用 CkipTagger 命名實體識別
```python=
ner = NER("./data")

entity_sentence_list = ner(word_sentence_list, pos_sentence_list)
print(entity_sentence_list)
```

## 帶入自定義字典
* 將自定義字典加入斷詞器中
```python=
from ckiptagger import construct_dictionary

word_to_weight = {"日本東京大學": 1}
dictionary = construct_dictionary(word_to_weight)
```

* 建構斷詞器
```python=
ws = WS("./data")
input_traditional_str = ['小明碩士畢業於國立臺灣大學，現在在日本東京大學進修深造']
word_sentence_list = ws(input_traditional_str, recommend_dictionary=dictionary)
print(word_sentence_list)
```
print:
```
[['小明', '碩士', '畢業', '於', '國立', '臺灣', '大學', '，', '現在', '在', '日本東京大學', '進修', '深造']]
```

## 延伸閱讀
* [CkipTagger 官方 GitHub](https://github.com/ckiplab/ckiptagger)
* [中研院詞庫小組馬偉雲主持人演講](https://linguistics.ntu.edu.tw/static/media/Ma_CkipTagger_1129.2f82ba88.pdf)
* [CkipTagger命名實體類別](https://github.com/ckiplab/ckiptagger/wiki/Entity-Types)
* [CkipTagger詞性標注類別](https://github.com/ckiplab/ckiptagger/wiki/POS-Tags)
* [中研院詞庫小組馬偉雲主持人演講筆記](https://allen108108.github.io/blog/2019/11/01/中文自然語言處理%20(NLP)%20的進展與挑戰/)