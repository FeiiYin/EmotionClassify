## Note

---

#### BPE 
BPE：在自然语言处理中，序列到序列模型中（机器翻译、对话）需要设置词表，使用较小的词表，有助于提高系统的性能。

BPE在欧洲语系可能表现的更为有效一些，主要由于欧洲语系中存在词缀等概念。

*** BPE的训练和解码范围都是一个词的范围。***

BPE的大概训练过程：首先将词分成一个一个的字符，然后在词的范围内统计字符对出现的次数，每次将次数最多的字符对保存起来，直到循环次数结束。

解码过程，经过训练过程，会得到codec文件，codec文件中保存的就是训练过程的字符对，文件中最开始的是训练时最先保存的字符，即具有较高的优先级。

解码是也是按在词的范围中进行编码的，首先将词拆成一个一个的字符，然后按照训练得到的codec文件中的字符对来合并。

#### jieba 分词

ieba分词算法使用了基于前缀词典实现高效的词图扫描，生成句子中汉字所有可能生成词情况所构成的有向无环图(DAG), 

再采用了动态规划查找最大概率路径，找出基于词频的最大切分组合，对于未登录词，采用了基于汉字成词能力的HMM模型，使用了Viterbi算法

jieba分词支持三种分词模式：

1. 精确模式, 试图将句子最精确地切开，适合文本分析：

2. 全模式，把句子中所有的可以成词的词语都扫描出来，速度非常快，但是不能解决歧义；

3. 搜索引擎模式，在精确模式的基础上，对长词再词切分，提高召回率，适合用于搜索引擎分词。

jiaba分词还支持繁体分词和支持自定义分词。

使用：

```
def jieba_handle_string(line):
    # json.loads 不能读取 单引号分割句子
    # re.sub 替换
    line = re.sub('\'', '\"', line)
    line = json.loads(line)
    str = line["title"]
    seg_list = jieba.cut(str, cut_all=False)
    print(",".join(seg_list))
```

#### 条件随机场（CRF）

条件随机场是逻辑回归的序列化版本。

HMM

参考博客：https://blog.csdn.net/dcx_abc/article/details/78319246




学长提供：https://github.com/NLP1502/NLP/tree/master/learningResources/Case

学长提供：https://github.com/NLP1502/NLP/tree/master/textTag/enhance3/models
