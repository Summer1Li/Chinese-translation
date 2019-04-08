参考链接:https://mp.weixin.qq.com/s/GLnhqub7dQsYSCTO-Kutsw

最近在Github发现一个基于google浏览器的爬虫项目，此项目是由美国大神2018年开源的。这个开源项目不需要使用者再去手写核心爬虫，只需要下载安装，然后传入一些配置参数即可。重要的能做到google图片的无限量爬取，只有不想爬的图片，没有爬不到的。下来就介绍一下这个牛逼的开源项目。

前沿：

这是一个命令行python程序，用于搜索Google Images上的关键字/关键短语，并可选择将图像下载到您的计算机。还可以从另一个python文件调用此脚本。

如果只想为每个关键字下载最多100个图像，则无需安装依赖项。如果您想要每个关键字超过100个图像，需要同时安装Selenium库chromedriver。故障排除部分中的详细说明。

Github地址：https://github.com/hardikvasa/google-images-download


项目介绍: google-images-download

此项目开源到现在一年的时间，就已经收割了3900+star,真的不得不跪拜大神的能力，能将一个简单的爬虫做到如此牛逼的地步。



当然，这么热门的项目，也不是一个人短时间完成的。Github上显示，此项目的贡献者就高达26人，代码总共提交了133次。此项目能收到这么多star，还是在于更多的贡献者和后期的不断维护升级。

这个项目在github也做了具体的使用说明和介绍，大家可以根据自身的项目情况进行配置即可（为了方便阅读，通过google翻译为中文)。

用于‘搜索’和‘下载’数百个google图像到本地硬盘的python脚本
内容
* 摘要
* 兼容性
* 安装
* 用法-使用命令行界面
* 用法-来自另一个python文件
* 参数
* 配置文件格式
* 例子
* 判处错误/问题
* 结构体
* 有助于
* 放弃

关于此项目使用这里多逼逼几点：

版本要求：
该项目作者GitHub上说python2x与Python3x都可以，推荐Python3。

项目使用：有2种使用方式

       方式一：使用pip安装报的方式(推荐)
pip install  google_images_download
   
        方式二：手动下载
git clone https://github.com/hardikvasa/google-images-download.git 
cd google-images-download && sudo python setup.py install

图片数量：
google搜索关键字首页默认100张图片，要抓取更多的图片，就得增加翻页功能。此项目已经实现了翻页功能，只需要使用者同时安装Selenium库chromedriver，代码里面配置即可。

参数方式：
原作者对参数的传递形式和每一个参数都做了详细的说明，大家可以github详细了解。


使用案例

这里给大家分享一下如何将此项目用来爬取去自己需要的图片。原作者介绍了几种关键字输入的方式。这里以文件读取的形式将关键字传入。这里爬取图片的数量选为500张，需要下载、安装Selenium库chromedriver。

1、搭建爬虫环境
pip install selenuium
pip install requests
pip install google_images_download

2、下载chromedriver驱动
因为下载的图片数量大于100，所以还需要在安装chromedriver，在代码配置chromedriver位置即可。

首先要查看自己电脑上安装的google浏览器版本号


▲谷歌浏览器版本号▲
github给的下载路径国内是无法下载的，不过小编已经将大多数驱动下载下来，需要的可以后台私信获取。当然也可以通过别的渠道获取。


▲github给的下载地址▲

在chrome官网找到与本机的google浏览器版本号一致的chromedriver


▲chrome官网对应的驱动版本号▲

下载完后，安装的路径根据操作系统自己指定。我使用的时win系统，安装在了D盘，具体路径如下：
"D:\download\chromedriver.exe"

3、编辑爬取的关键字文件：
如图所示，只需要在keywords.csv文件里面按图所示填写对应老师的名称即可。



4、代码展示：

import csv
import os
import sys

from google_images_download import google_images_download

# 实例化一个下载器
downloader = google_images_download.googleimagesdownload()

BASE_DIR = os.path.dirname(os.path.abspath(__file__))
sys.path.insert(0, BASE_DIR)

# 读取关键字文件
csv_file = csv.reader(open(BASE_DIR + "\google_images\keywords.csv", "r"))

def download_images(csv_file):
   """
   传入关键字等参数，下载对应的图片文件
   files: 读取的关键字文件
   limit: 爬取的图片数量
   print_urls: 是否显示爬取的图片url
   chromedriver: chromedriver安装的路径。不填此参数，默认爬取前100张图片
   output_directory：自定义保存图片的位置
   """
   for key_word in csv_file:
       arguments = {"keywords": key_word, "limit": 500, "print_urls": True,
                    "chromedriver": "D:\download\chromedriver.exe",
                    "output_directory": BASE_DIR + "\\files\\"}

       downloader.download(arguments)

if __name__ == '__main__':
   download_images(csv_file)

运行：python google_download.py，你就会发现有源源不断的老师图片进入你的硬盘，接下来就是坐等爬完所有你要的图片了。

此文章主要还是给大家分享这个开源项目，至于使用，本文只是做了一个简单的使用，想要了解更多的，可以直接在github查看。在实际中，我们可以利用这个python脚本去爬取基于google的任何图片了。
