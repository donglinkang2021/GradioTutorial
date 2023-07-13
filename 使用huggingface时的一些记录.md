## 挂代理时无法下载huggingface模型的情况

```python
tokenizer = DistilBertTokenizer.from_pretrained("distilbert-base-uncased")
model = DistilBertForSequenceClassification.from_pretrained("distilbert-base-uncased")
```

改成下面即可：

```python
proxies = {
    'http': 'http://127.0.0.1:7890',
    'https': 'http://127.0.0.1:7890'
}

tokenizer = DistilBertTokenizer.from_pretrained("distilbert-base-uncased", proxies=proxies)
model = DistilBertForSequenceClassification.from_pretrained("distilbert-base-uncased", proxies=proxies)
```

### from gpt

如果你正在使用代理服务器进行网络连接，你可以通过为HTTP请求设置代理来解决报错。以下是在使用`requests`库时设置代理的示例代码：

```python
import requests

proxies = {
    'http': 'http://your_proxy_server:your_proxy_port',
    'https': 'http://your_proxy_server:your_proxy_port'
}

tokenizer = DistilBertTokenizer.from_pretrained("distilbert-base-uncased", proxies=proxies)
model = DistilBertForSequenceClassification.from_pretrained("distilbert-base-uncased", proxies=proxies)
```

请将`your_proxy_server`替换为代理服务器的主机名或IP地址，将`your_proxy_port`替换为代理服务器的端口号。在上述代码中，我们使用了相同的代理设置来为`http`和`https`请求设置代理。

通过将代理信息传递给`proxies`参数，你应该能够在使用Hugging Face模型存储库时成功建立连接并下载所需的模型文件。

> 而事实上GPT的方法没有用，真正的解决方法是把梯子关了，直接下载即可。

## 之前的代码运行不了一直显示loading

>  2023.6.19重新回来更新这部分的内容

发现之前的gradio的代码怎么也运行不了，查了网上的问题很少说这个问题，所以此时这个问题就是默认的问题——版本过时了：

> 第一步先关掉代理，现在不用代理也可以访问huggingface了

```shell
pip uninstall gradio
```

删了重装即可：

```
pip install gradio
```

可以正常运行。



