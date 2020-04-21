# webvpn-HFUT 文泉学堂PDF下载
本项目是基于WebVPN-HFUT资源[文泉学堂](https://lib--hfut-wqxuetang-com-443.webvpn.hfut.edu.cn/#/)PDF下载的python脚本

    文泉学堂: “文泉学堂”由清华大学出版社出品，以清华大学出版社近10年出版的电子书为基础，聚合多媒体附件和特色课程内容资源，突出理学、工学、经济学、管理学等专业学科领域知识。是国内高等院校最有针对性的专业知识内容资源，方便师生快速、精准查找专业知识内容，高效率阅读、学习和辅助教学。


## 项目介绍
本项目是在[文泉学堂PDF(带书签)下载原理详细讲解_python脚本实现1秒1页](https://www.52pojie.cn/thread-1108776-1-1.html)的基础上进行了修改，支持了HFUTer。


程序整体思路:

**下载高清图片---->合成PDF---->下载书签---->给PDF添加书签**

### 依赖的库及说明

可以直接执行
`pip install -r requirements.txt`
安装本项目所依赖的模块

```python
from PIL import Image
from reportlab.lib.pagesizes import A4, portrait, landscape, mm
from reportlab.pdfgen import canvas
import os
from io import BytesIO
from selenium import webdriver
from bs4 import BeautifulSoup
from selenium.webdriver.common.keys import Keys
import time
import datetime
import base64
import queue
from Crypto.Util.number import *
from PyPDF2 import PdfFileReader, PdfFileWriter
import requests
```
* 安装模块可以加载国内镜像（这样速度会很快），具体Google
* Crypto模块的安装可能会出错，具体Google，可以参考 [这里](https://www.jb51.net/article/131185.htm)
* Crypto.Util可能会报错，~~其实是安装`pycrypto`，也就是`pip install pycrypto`，这里发现这个模块安装过程中需要依赖VS2008环境。还是不完美~~
    * 所以可以使用`pip install pycryptodome`进行替换。想请看[这里](https://stackoverrun.com/cn/q/12091094)

### 程序使用说明

程序的第30到39行，是需要**替换**的部分
```python
# 请替换url末尾的数字，例如这里的3184535，替换为目标书籍的ID
url = "https://lib--hfut-wqxuetang-com-443.webvpn.hfut.edu.cn/read/pdf/3184535"
# 登陆WebVPN.hfut.edu.cn的账号密码（与信息门户一致）
stu_number='2017214***'
password='poet'
cookie_dict = {}  # cookie字典，这里不用管
# 图片路径
_image_path = "F:\\test\\temp\\img"
# PDF路径(不要与图片路径相同)
_pdf_path = "F:\\test\\temp\\pdf"
```

1. 将url末尾的书籍ID进行替换
2. 输入学号，即 `stu_number`
3. 输入密码，即 `password`
4. 存储图片的路径、PDF的路径

### 最后
合理使用，使用愉快。


### Tips:

下载后可以使用ABBYY对PDF文档进行OCR识别，这样便解决了文档复制问题。