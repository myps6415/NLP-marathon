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