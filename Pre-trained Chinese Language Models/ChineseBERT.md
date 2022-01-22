# ChineseBERT: Chinese Pretraining Enhanced by Glyph and Pinyin Information
>Shannon.AI    
ACL2021
### 结构
![overview of chinesebert](https://github.com/Owen1u/NLP_Review/blob/main/images/overview_of_chinesebert.png)<br>
![glyph embedding](https://github.com/Owen1u/NLP_Review/blob/main/images/glyph_embedding.png)<br>
字形嵌入使用不同字体的汉字图像得到。每个图像都是24*24的大小，将仿宋、行楷和隶书这三种字体的图像向量化，拼接之后再经过一个全连接，就得到了汉字的字形嵌入。<br>
![pinyin embedding](https://github.com/Owen1u/NLP_Review/blob/main/images/pinyin_embedding.png)<br>
拼音嵌入首先使用pypinyin将每个汉字的拼音转化为罗马化字的字符序列，其中也包含了音调。比如对汉字“猫”，其拼音字符序列就是“mao1”。对于多音字如“乐”，pypinyin能够非常准确地识别当前上下文中正确的拼音，因此ChineseBERT直接使用pypinyin给出的结果。在获取汉字的拼音序列后，再对该序列使用宽度为2的CNN与最大池化，得到最终的拼音序列。<br>

### 掩码策略
- Char Masking(CM):最简洁最直观的掩码方法，以单个汉字为单位进行掩码。
- Whole Word Masking(WWM):以词为单位，将词中的所有字掩码。注意基本的输入单元依然是字，只是一个词包含的所有汉字都被掩码。比如，“我喜欢上海”在掩码词“上海”之后就是“我喜欢[M][M]”，而非“我喜欢[M]”。