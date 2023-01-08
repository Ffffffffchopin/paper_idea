
任务源于这个寒假做大挑，老师给的项目是做一个水书（水族文字，我也不认识）识别的app，摆在面前的第一个挑战就是收集和整理数据了

源数据的pdf文件我一起放在项目中了，是我在谷歌上找到的2016年官方整理出来用于申请Unicode统一 水书文字的资料（在此吐槽一下知网，民族文化工作呕心沥血整理出来的资料，你说没就没了？），大约有484个中文和水书对照的词条，源文件格式比较混乱，所以我转成了words

## pdf转换docx

一开始我打算直接操作pdf，这不是有我们万能的python嘛。于是我一通CSDN加谷歌，奈何本人实在太菜，不是无法显示图片就是就是显示了之后没法定位，无奈，只能先转换成Words文档再下一步操作



先安装pdf2docx库

```shell
pip install pdf2docx
```

这个库貌似是基于pdfplumber依次定位来实现转换的，具体的原理我还在研究，等有空再写篇文章讲讲，现在就先用着

这个库的使用非常简单
```python
from pdf2docx import Converter
 #pdf文件路径

pdf_file="input.pdf"

    #创建Converter对象
cv=Converter(pdf_file)

    #convert方法全部转换
cv.convert("output.docx")

    #关闭对象
cv.close()
```

先创建Converter对象，参数是我们的pdf文件的路径，然后调用convert方法指定目标文件名，之后只需等待一段较长的时间就会自动转换完成

转换完之后的word文档output.docx还是有很多我们不想要的文字内容比如介绍，附录等，我们手动将它们删除，复制需要的所有表格内容到一个新的文档”table.docx“还是比较容易的

### 数据处理

我们大体的思路是用python-docx一行行地读取表格，在每一行的cell中依次寻找图片和汉字，如果找不到就跳过。然后为每一个中文对应的标签的建立目录放入图片，图片的文件名按照标签名加索引的形式

最后我们的目录结构大概是

data
	-安稳
		-安稳0_.png
		-安稳1_.png
	-肮脏
		-肮脏0_.png

接下来我们 开始正式处理word中的表格数据，首先引入需要的第三方模块

```python
#word文档表格文字处理库
import docx
#进度条
from tqdm import tqdm
#系统模块
import os
#图像提取模块
from PIL import Image
#处理二进制模块
from io import BytesIO
#正则模块
import re
```

其中大部分都是python的内建built-in模块无需手动安装

```python
#数据存储路径
store_path="data"
#待处理word文档路径
word_path="table.docx"
```
然后我们声明好后面会用到的两个路径，一个是要读取的word文档的路径，一个是之后存储数据的根目录路径

```python
#创建数据存储路径
    if not os.path.exists(store_path):
      os.mkdir(store_path)
```
我们创建存储数据的根目录

```python
#提前编译正则表达式用来判断是不是中文
    is_Chinese=re.compile(r'[\u4e00-\u9fff]+')
```

用正则表达式判断文本内容中是否含有中文（这个表达式不能匹配整行，但我认为一个cell里只要有中文基本上应该都是中文了）

```python
#创建Document对象
    docx_doc=docx.Document(word_path)
   ```
创建一个python-docx的Document的实例

```python
 #创建进度条对象
    with tqdm(total=566,desc="处理进度") as pbar:
    #循环表格对象
      for table in docx_doc.tables:
        #循环row对象
        for _ in range(1,len(table.rows)):
          #初始化标签
          label=""
          #初始化图像xpath列表
          images=[]
          #获取cell列表
          cells=table.rows[_].cells
```

我们开始循环，先创建一个tqdm对象打开（566是我运行完以后总的标签数量），循环Documents对象里的每一个table，再循环table对象中的rows（从第二行开始循环是因为第一行是表头）然后初始化我们存每一行的图片所用的字符串label，和列表images，然后提取出row中的cells
```python
for cell in cells:
            #判断cell中有没有中文
            if is_Chinese.match(cell.text):
                label=cell.text.replace("\n","").replace(" ","")
                break
            #判断cell中有没有图片
            img=cell.paragraphs[0]._element.xpath('.//pic:pic')
            if img:
              images.append(img)
          #如果没有标签或者没有图片就跳过
          if label=="":
            continue
          if images==[]:
            continue
```

接着我们开始cell的循环，先判断一下cell.text中有没有中文，有的话就去除换行空格这些特殊字符存在label里，然后用cell里的paragraph对象的xpath判断有没有图片（图片的部分是我从网上查来的暂时还没搞清），如果有的话也存进img变量里。判断label和image都存在才继续。
