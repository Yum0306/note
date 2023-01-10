想想当初看上python不就是觊觎爬虫爬来的妹子图又好看（大）又漂亮吗（白），呸，我想学的是技术

![](/imgs/2023-01-10/4yzlvxrHoMegkqfk.jpeg)

```python
import requests
import os
#这个模块可能需要自己安装 pip install bs4
import bs4
from bs4 import BeautifulSoup
import sys
import importlib
import random
import time
importlib.reload(sys)

#定义好初始化的爬去路径和文件保存位置
Mzitu_Url = "https://www.mzitu.com/mm/pages/1"
save_path = "/home/qin0306/workspace/pyworkspace/spider/spider_mzitu/images/"

#创建一个空的请求头字典
header={}

#这里先写好一些User-Agent 用于规避网站对爬虫程序的鉴别
headers = [
    "Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.153 Safari/537.36",
    "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:30.0) Gecko/20100101 Firefox/30.0",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.75.14 (KHTML, like Gecko) Version/7.0.3 Safari/537.75.14",
    "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0)",
    'Mozilla/5.0 (Windows; U; Windows NT 5.1; it; rv:1.8.1.11) Gecko/20071127 Firefox/2.0.0.11',
    'Opera/9.25 (Windows NT 5.1; U; en)',
    'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)',
    'Mozilla/5.0 (compatible; Konqueror/3.5; Linux) KHTML/3.5.5 (like Gecko) (Kubuntu)',
    'Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.8.0.12) Gecko/20070731 Ubuntu/dapper-security Firefox/1.5.0.12',
    'Lynx/2.8.5rel.1 libwww-FM/2.14 SSL-MM/1.4.1 GNUTLS/1.2.9',
    "Mozilla/5.0 (X11; Linux i686) AppleWebKit/535.7 (KHTML, like Gecko) Ubuntu/11.04 Chromium/16.0.912.77 Chrome/16.0.912.77 Safari/535.7",
    "Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:10.0) Gecko/20100101 Firefox/10.0",
    'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36'
]
#随机一个User-Agent到请求头字典里面
header["User-Agent"] = random.choice(headers)


#创建文件函数
def create_file(file_path):
    #首先判断该路径是否村存在
    if os.path.exists(file_path) is False:
        #不存在创建
        os.makedirs(file_path)
    #切换当前目录到刚刚创建的文件地址
    os.chdir(file_path)


#主要下载方法
def download_file():
    global header
    #这里先请求初始页面，也就是获取有多少组图片
    first_rep = requests.get(Mzitu_Url,headers=header)
    #创建一个BeautifulSoup对象用于解析html页面 返回值是一个字符串
    first_soup = BeautifulSoup(first_rep.text,"html.parser")
    #在下载的html页面中搜索所有的在class=“postlist”的div下的所有的带新窗口跳转的a标签 返回是一个包含a标签的数组
    tab_a_list = first_soup.find("div",class_="postlist").find_all("a",target='_blank')
    #打印列表的长度也就是该页下有多少详情页
    print(len(tab_a_list))
    #循环每一个a标签
    for a in tab_a_list:
        #获取a标签的名称 用于创建文件夹或者文件保存路径
        folder = a.text;
        #判断是不是一个空的a标签，没有标签体内容的a标签
        if len(folder):
            #生成文件保存的上一级文件夹路径
            folder_path = save_path + folder
            #创建文件夹
            create_file(folder_path)
            print("创建文件夹:"+str(folder_path))
            #获取a标签的href属性值
            img_url = a.attrs['href']
            #获取随机的User-Agent属性 网站会通过这个判断你是不是一个网络爬虫
            header["User-Agent"] = random.choice(headers)
            #发起一个请求，添加请求地址、请求头、以及超时限制（这里就已经到达了每个图片组的详情）
            second_rep = requests.get(img_url,headers=header,timeout=30)
            #把返回的就已经是详情页面就是图片列表的文本了
            second_soup = BeautifulSoup(second_rep.text, 'html.parser')
            #这里开启异常捕获，主要是在进行文件保存写出的时候可能会出现异常，所以需要捕获异常
            try:
                #这里是获取在class=“pagenavi”的div下的第六个span元素的文本内容，为什么是第六个，这个是因为他的图片是分页展示的，总张数的数字是在第六个span元素里面的
                max_img_seq = second_soup.find("div",class_="pagenavi").find_all("span")[6].text
                print("张数:"+str(max_img_seq))
                #获取这组图片有多少张之后就可以知道我需要请求多少次了
                for seq in range(1,int(max_img_seq)+1):
                    #重新随机一个User-Agent
                    header["User-Agent"]=random.choice(headers)
                    #让当前线程阻挂起 1-3秒 请求太频繁的话也会被认定你是爬虫，毕竟手速摆在那，你一个ip没变过，一直快速请求，肯定不合理
                    time.sleep(random.randint(1, 3))
                    #以图片的张数号码，决定图片的保存位置，网站上是这么做的，我们这里也这么做
                    path = img_url + "/"+str(seq)
                    print("图片地址:"+str(path))
                    #发起第三波请求，获取具体的图片的src
                    three_rep = requests.get(path,headers=header,timeout=30)
                    three_soup = BeautifulSoup(three_rep.text,"html.parser")
                    #获取class="main-image"下的img标签
                    img_note_type = three_soup.find("div",class_="main-image").find('img')
                    #如果获取到这这个img是一个bs4.element.Tag类型（元素标签类型类型）
                    if isinstance(img_note_type,bs4.element.Tag):
                        #然后读取img标签的src属性就可以拿到这张图片的下载路径
                        url_img = img_note_type.attrs['src']
                        print("文件下载路径:"+str(url_img))
                        #获取文件名称 这里通过使用“/”截取可以吧文件路径（网络路径）截取成一个数组，然后数组下标-1就是最后一项，也就是文件的名称（xxx.jpg）
                        file_name = url_img.split("/")[-1]
                        #发起第四次请求
                        header["User-Agent"] = random.choice(headers)
                        header["Referer"]=url_img
                        img = requests.get(url_img,headers=header,timeout=30)
                        print("图片下载完毕，开始保存")
                        #将请求下来的图片保存在文件夹的基础上文件名称（原网站你的名称名称）
                        file = open(folder_path+"\\"+file_name,"ab")
                        #写出图片
                        file.write(img.content)
                        print("图片保存成功")
                        #文件操作完毕，关闭文件
                        file.close()
            except Exception as e:
                #如果出现文件操作异常，这里打印异常信息
                print("异常信息:"+str(e))
				
#程序主入口  主函数
if __name__ == '__main__':
    #主方法调用
    download_file()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyOTQ5NzcxXX0=
-->