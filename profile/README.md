# 工具介绍
[https://gitee.com/hustai/FourthDimension](https://gitee.com/hustai/FourthDimension)

FourthDimension（第四维度）由华中科技大学人工智能与嵌入式实验室联合言图科技研发，是一款基于大语言模型的智能检索增强生成（RAG）系统，提供私域知识库、文档问答等多种服务。此外，FourthDimension提供便捷的本地部署方法，方便用户在本地环境中搭建属于自己的应用平台。

### 工具特点
支持在线调用和本地部署，可选装不同的Embedding模型和答案生成模型，支持构建私域知识库，实现知识库问答。

### 主要服务
* 私域知识库
* 知识库问答
* 向量存储与检索
* 检索增强生成

# 工具使用

### 前置依赖项
- Anaconda3  

> 使用前请检查Anaconda是否安装，若未安装可参照以下教程进行安装。  
> [Anaconda详细安装过程](https://blog.csdn.net/weixin_43858830/article/details/134310118?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22134310118%22%2C%22source%22%3A%22weixin_43858830%22%7D)

### 快速上手

1. 克隆项目Gitee库
```
mkdir FourthDimension
cd FourthDimension
git clone https://gitee.com/hustai/FourthDimension ./
```
2. 创建Conda虚拟环境
> python版本号要求 >= 3.8.1 ,<4.0
```
conda create -n FourthDimension python==3.8.1
conda activate FourthDimension
```
3. 安装FourthDimension  
3.1 安装前置依赖
```
pip install -r dependencies.txt
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.2 安装FourthDimension 
```
sh FourthDimension.sh install
```

4. 启动FourthDimension
> 如需重启服务请将start参数替换为restart
```
sh FourthDimension.sh start
```

5. 使用FourthDimension  

>config.json为FourthDimension配置文件，在使用FourthDimension时请将config.json置于脚本文件同级目录下

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5.1 导入文档示例代码
```text
import FourthDimension  
# 传入文档路径或文件夹路径，目前支持的文档类型仅为doc、docx
result = FourthDimension.upload('./data/example/')
print(result)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5.2 检索增强生成(问答)示例代码
```text
import FourthDimension
# 传入检索增强生成的问题
answer = FourthDimension.query('什么是活期存款')
print(answer)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5.3 config.json文件说明  
> 使用config.json时请确保文件内无任何注释
```text
{
  //文档文本存储方式，本例中选择elasticsearch
  "word_storage": "elasticsearch",

  //文档向量存储方式，本例中选择faiss
  "embedding_storage": "faiss",

  //检索方式选择，目前提供以下三种方式，本例中选择elasticsearch
  //1.elasticsearch
  //2.faiss
  //3.elasticsearch+faiss
  "search_select": "elasticsearch",

  //embedding模型，本例中选择bge-large-zh-v1.5
  "embedding_model": "bge-large-zh-v1.5",

  //答案生成模型，本例中选择gpt-3.5-turbo-16k
  "answer_generation_model": "gpt-3.5-turbo-16k",

  //openai配置
  "openai": {
    //请在此处配置您的api key
    "api_key": "",
    //默认使用openai官方接口，可根据需求进行修改
    "url": "https://api.openai.com/v1"
  },

  //文档划分设置
  "para_config": {
    //文档划分段落长度，本例中设置为500
    "chunk_size": 500,
    //文档划分重叠度，本例中设置为20
    "overlap": 20
  },

  //召回设置
  "recall_config": {
    //指定使用多少召回结果进行答案生成，本例中设置为10
    "top_k": 10
  },

  //Elasticsearch设置
  "elasticsearch_setting": {
    //默认索引名称，可根据需求进行修改，本例中设置为index
    "index_name": "index",
    //默认为localhost，可根据具体需求修改，本例中设置为localhost
    "host": "localhost",
    "port": 9200,
    //若存在安全认证，则填写用户名和密码
    "username": "",
    "password": "",
    //Elasticsearch分词器，本例中设置为standard
    "analyzer": "standard"
  },

  //Faiss设置
  "faiss_setting": {
    //索引方式
    "retrieval_way": "IndexFlatL2"
  }
}
```
# 论坛交流
微信群二维码

# 相关知识
- [基于检索增强的文本生成](https://hustai.gitee.io/zh/posts/rag/RetrieveTextGeneration.html)

- [如何通过大模型实现外挂知识库优化](https://hustai.gitee.io/zh/posts/rag/LLMretrieval.html)

 [更多相关知识分享————网站链接](https://hustai.tech/zh/)


