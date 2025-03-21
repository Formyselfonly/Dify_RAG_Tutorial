# RAG_Tutorial

本人做过各类Generative AI项目，包含多个大型企业级RAG项目：企业问题回答助手，智能回复机器人。
在这里主要介绍RAG相关项目的经验

## RAG时各种参数是什么意思？怎么设定？（以Dify为例）

不仅介绍主要原理，还介绍一些场景设置参数方案

### Chunk Setting相关

1. General Chunk Type
   ![](/img/General Chunk.png)

   1. Delimiter
      分隔符，比如说\n代表有回车时分割出一个Chunk，\n\n代表有两个回车时分割出一个Chunk
   2. Maximum Chunk Length
      最大的Chunk长度，首先Chunking时会根据Delimiter进行Chunking，
      除此之外，还会根据Chunk的长度分割，比如现在我设置Maximum Chunk Length是500
      那么如果这次一段文本长度是600token的size，那么到500时会Chunking一下
      这个主要是防止分本里面没有进行好的Delimiter时，发生有一段几千Token长度的Chunk出现

   

2. Parent-Child Chunk Type
   根据段落或者整个文档作为一个父Chunk，里面的都是小Chunk
   Chunk的设置与刚才说明的一样
   ![](/img/Parent-Child Chunk.png)

   1. Paragraph Type
      以段落为大Chunk，怎么进行分段由Delimiter决定
      比如说我以\n\n来定段落,小Chunk可以定为\n为分隔符
      (记得这时候把Replace consecutive spaces, newlines and tabs取消，不然就会导致根据没有段落，因为\n\n被取代为\n了)
   2. Full Doc Type
      以整段文本为大Chunk，小Chunk可以定为\n为分隔符

### Index Method相关

![](/img/Index_Method.png)

- 选High Quality
  Economical模式是每个Chunk只有十个关键词来检索，无Token消耗
  公司级别无脑选High Quality，个人开发者也基本无脑选High Quality

### Embedding Model相关

![](/img/Embedding Model.png)

- Embedding会把文本变为向量，向量之间才能进行向量搜索
- 选Embedding模型即可，建议选择OpenAI的Embedding：text-embedding-3-large

### Retrieval Setting相关

- 关键词检索
  根据用户输入的关键词，与Chunk里面的关键词检索
  ![](/img/Full text.png)
  
- 向量检索
  
  ![](/img/Vector.png)
  根据向量检索，用户的输入会被转化为向量
  Chunk也会被转化为向量进行匹配
  
- 混合检索
  ![](/img/Hybrid Search.png)

  - Weighted Score
    自己设定一个比例混合关键词检索和向量检索，比如0.7Semantic，0.3Keyword
  - Rerank
    用model来自动地动态地选择这个比例

- Top K和Score Threshold

  Top K取决于你需要调用的Chunk数量，比如你的各个Chunk都是自成一体的，他们没关系
  那么设置为1都可以。但是如果他们相关，那么就需要多调用几个Chunk给AI回答来提升准确性
  至于Threshold决定这个检索时匹配率有多少会被我们检索过来，这个需要根据情况测试



## 最佳的搭配策略-Dify+RAGFlow怎么实现？



## 联系我z1597006376@gmail.com

暂时写些简单的，有空再更新.

关于具体场景中RAG方案的制订，参数的设定，请联系作者z1597006376@gmail.com

或者有其他Generative AI或者RAG问题，请联系我
