# Hmm-NERTagger
## HMM五元组
HMM是一个五元组(O，Q，O0 ，A，B) ：
* O:{o1 ….ot } 是状态集合,  也称为观测序列；
* Q:{q1 …qv } 是一组输出结果，也称隐序列；
* aij =P(qj |qi ):  转移概率分布（隐状态）；
* bij =P(oj |qi ):  发射概率（隐状态表现为显状态的概率）；
* O0 是初始状态（隐状态）；
## HMM模型
应用于命名实体识别中：给定一个词的序列，找出最可能的标签序列（内外符号：[内]表示词属于命名实体，[外]表示不属于）
### 应用到语料例子
标注格式：456人名，789地名，123机构团体，101112其他专业名词，0非实体词

新/0 年/0 前/0 夕/0 ，/0 国/0 家/0 主/0 席/0 习/4 近/5 平/6 通/0 过/0 中/1 国/2 国/2 际/2 广/2 播/2 电/2 台/3 、/0 中/1 央/2 人/2 民/2 广/2 播/2 电/2 台/3 、/0 中/1 央/2 电/2 视/2 台/3 ，/0 发/0 表/0 了/0 2/0 0/0 1/0 4/0 年/0 新/10 年/11 贺/11 词/12 。

## HMM+维特比找最优解
本次实验中五元组是如下：
观察序列是给定的字序列，隐藏状态是每个字对应的词性标注。
初始概率就是直接统计语料的词频
标记间的状态Tj→Ti转移概率可以通过如下公式求出：　　　　　　
　　 ![转移概率](https://github.com/gugug/Hmm-NERTagger/Screenshots/transtition.png)
	例：习/4 近/5 平/6  P（5|4）=C（4，5）/C（4）
而每个状态（标记）随对应的符号（单字）的发射概率可由下式求出：
 ![发射概率](https://github.com/gugug/Hmm-NERTagger/Screenshots/emission.png)
	例：P（习|4）=C（习，4）/C（4）
其中符号C代表的是其括号内因子在语料库中的计数。

维特比算法就是求解HMM上的最短路径，也即是最大概率的算法
 ![维特比](https://github.com/gugug/Hmm-NERTagger/Screenshots/viterbi.png)
