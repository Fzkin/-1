# -1
数据清洗的基本操作

intern -- 为给定的需要适配处理的文件目录  
输入输出 Demo -- 中为不同参数下的生成结果的 Demo  


![Image text](https://github.com/Fzkin/-1/blob/master/img/1.png)
![Image text](https://github.com/Fzkin/-1/blob/master/img/2.png)
![Image text](https://github.com/Fzkin/-1/blob/master/img/3.png)
![Image text](https://github.com/Fzkin/-1/blob/master/img/4.png)

#使用包
from xml.dom.minidom import parse
import xml.dom.minidom

# 使用minidom解析器打开 XML 文档
DOMTree = xml.dom.minidom.parse(xml)
collection = DOMTree.documentElement

#获取选中信息
#一级目录
filename = collection.getElementsByTagName("filename")[0].childNodes[0].data
#二级目录
width = collection.getElementsByTagName("size")[0].getElementsByTagName('width')[0].childNodes[0].data
height = collection.getElementsByTagName("size")[0].getElementsByTagName('height')[0].childNodes[0].data
depth =  collection.getElementsByTagName("size")[0].getElementsByTagName('depth')[0].childNodes[0].data
  

# object 处理
anotations = []
anotation = {}
#获取所有object集合
objs = collection.getElementsByTagName("object")
#逐个获取，填入字典
for obj in objs:
        dif = obj.getElementsByTagName("difficult")[0].childNodes[0].data
        nm =  obj.getElementsByTagName("name")[0].childNodes[0].data
        bdbox =  obj.getElementsByTagName("bndbox")[0]
        x = bdbox.getElementsByTagName('xmin')[0].childNodes[0].data
        y = bdbox.getElementsByTagName("ymin")[0].childNodes[0].data
        w = bdbox.getElementsByTagName("xmax")[0].childNodes[0].data
        h = bdbox.getElementsByTagName("ymax")[0].childNodes[0].data
        anotation["diffcult"] = dif
        anotation["coordinate"] = {"x":x,"y":y}
        anotation["width"] = w
        anotation["height"] = h
        anotation["type"] = nm
        anotations.append(anotation)


#最后循环整合所有信息并存储。
for root,dirs,files in os.walk(int_dir):
    for file in files:
        fi = os.path.join(root,file)
        if fi.endswith("xml"):
            xmls.append(fi)
            try:
                rel = parse_xml(fi)
                result.append(rel)
            except :
                err.append(fi)
                continue
with open("./result.csv" , "w") as f:
    for i in result:
        f.write("{}".format(i))
