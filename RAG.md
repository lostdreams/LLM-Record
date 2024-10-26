

# Framework & Tool


[写在RAGFlow开源2万星标之际](https://zhuanlan.zhihu.com/p/2308262308)




## PDF Praser

最基础的就是PyPDF，ChtaDoc似乎不开源，此外还有 [PyMuPDF](https://zhuanlan.zhihu.com/p/517737462), 结构化的解析，参考阅读
- [如何利用大模型技术将非结构化的PDF文档转换为结构化的知识图谱？](https://www.zhihu.com/question/2003498355/answer/14244267722),
- [LLM之RAG实战（二十九）| 探索RAG PDF解析](https://zhuanlan.zhihu.com/p/686844517)
- [一文打尽PDF解析的工程实践——Langchain-RAG系列(1)](https://zhuanlan.zhihu.com/p/680175740)
- [ChatPDF | LLM文档对话 | pdf解析关键问题](https://zhuanlan.zhihu.com/p/652975673)
- [Using LlamaParse to Create Knowledge Graphs from ](https://neo4j.com/developer-blog/llamaparse-knowledge-graph-documents/)
- [LangChain on LinkedIn: 🧞PDFs -> Knowledge Graphs ]()


理想中的PDF处理应当具有 1. 抽取目录结构作为统一的标签  2. 对于不同的子标题之间的结构层次关系应当保持  3.最好还具有表格的处理能力




##  Knowledge Storage & Split  &  index

- embedding database
- Elasticsearch 
- 

## Evaluation

- RAGA
- Trulens

## 



#  Information Search

RAG的检索器属于信息检索的领域，不过在于现在的信息检索不会再去额外的训练神经网络来取做，本身RAG就是因为语料庞杂大模型没办法理解训练成本高，所以来信息检索，再去额外的训练神经网络，一旦文本稍微变化，又得重新训练，所以这是不值当的。 现在只考虑向量化检索+传统方法检索结合的方案，对于排序参考推荐算法中的方法。






对于向量化检索的方法，参考这篇Sentence embedding的sota方法[文章](https://www.zhihu.com/question/510987022/answer/3587373048)，和 [文本召回](https://zhuanlan.zhihu.com/p/713319725)作为一个简单的综述。



- 吃透工业界生成式 检索 GIR cs.ir 实战GENRET (https://zhuanlan.zhihu.com/p/721359923) ??? 



## sentence embedding


- [Embedding模型训练技巧的简单回顾](https://zhuanlan.zhihu.com/p/2982612970)
- 


# RAG Method


## Paper

- Hierarchical Retrieval-Augmented Generation Model with Rethink for Multi-hop Question Answering: 分层检索


## BLOG 


-[一文详谈19种RAG架构](https://zhuanlan.zhihu.com/p/1742013004)
- [StructRAG,SelfRAG等](https://www.zhihu.com/question/628651389/answer/12778008349)


## Unstructured RAG

## Paper

- OBSERVATIONS ON BUILDING RAG SYSTEMS FOR TECHNICAL DOCUMENTS：爱立信的RAG实践总结
- 

## BLOG & Practice



# Structured RAG

## RAG & KG

