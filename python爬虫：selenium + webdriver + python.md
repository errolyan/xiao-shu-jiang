---
title: python爬虫：selenium + webdriver + python 
tags: 爬虫学习,浏览器驱动,小书匠
grammar_cjkRuby: true
---
# 1.selenium 环境搭建
## 1.1 简介
- 参考教程地址1.https://selenium-python.readthedocs.io/
- 参考教程地址2：http://www.testtao.cn/?p=28
- 参考教程地址3github：https://github.com/SeleniumHQ/selenium
## 1.2 google chrome 浏览器插件下载地址
- ChromeDriver下载地址： http://npm.taobao.org/mirrors/chromedriver/
- ChromeDriver安装方法
- - Windows 将解压后的文件放在python.exe 同级目录下即可
- - Linux：将文件copy到"/usr/bin/"或者"/usr/local/bin/" 目录下
## 1.3 python 模块安装：
```
$ pip install selenium
```
# 2.基本实例教程
## 2.1 example
```
# coding = utf-8
# Date = "18.11.10"
# Author = "Errol Yan"
# Describe = "驱动浏览器自动实现百度搜索"

from selenium import webdriver
import time


browser = webdriver.Chrome()
browser.maximize_window()  #将浏览器最大化显示

browser.get("http://www.baidu.com")
time.sleep(3)

browser.set_window_size(800, 500)  #参数数字为像素点，高500，长800

browser.find_element_by_id("kw").send_keys("selenium")
time.sleep(3)

browser.find_element_by_id("su").click()
time.sleep(3)

browser.back() # 浏览器后退，到百度首页
time.sleep(3)

browser.forward() #浏览器前进至百度搜索结果页
time.sleep(3)

browser.quit()
```
## 2.2 对象的定位
- 对象的定位是自动化测试的核心也是驱动浏览器的关键所在。
- 定位对象的目的有以下几种
- - 操作对象：单击、双击、右键
- - 获取对象的属性，如获取class的属性，name属性等
- - 获取对象的text
- - 获取对象的数量
- 对象定位的方法：
- - id 
- - name
- - class name
- - link text
- - partial link text
- - tag name
- - xpath
- - css selector
### 2.2.1 example 还是百度的例子
```
from selenium import webdriver
import time


browser = webdriver.Chrome()
browser.maximize_window()  #将浏览器最大化显示

browser.get("http://www.baidu.com")
time.sleep(3)

#id = cp 元素的文本信息
data=driver.find_element_by_id("cp").text
print data   #打印信息

browser.set_window_size(800, 500)  #参数数字为像素点，高500，长800
#####################################################################
#通过id方式定位
browser.find_element_by_id("kw").send_keys("selenium")

#通过name方式定位
browser.find_element_by_name("wd").send_keys("selenium")

#通过tag name方式定位
browser.find_element_by_tag_name("input").send_keys("selenium")

#通过class name 方式定位
browser.find_element_by_class_name("s_ipt").send_keys("selenium")

#通过CSS方式定位
browser.find_element_by_css_selector("#kw").send_keys("selenium")

#通过xphan方式定位
browser.find_element_by_xpath("//input[@id='kw']").send_keys("selenium")
time.sleep(3)
#####################################################################
browser.find_element_by_id("su").click()
time.sleep(3)

browser.back() # 浏览器后退，到百度首页
time.sleep(3)

browser.forward() #浏览器前进至百度搜索结果页
time.sleep(3)

browser.quit()
```
### 2.2.2 定位详细讲解
#### 2.2.2.1 id and name
- 最为常用的方式，是 id和name
- tips：在百度首页 ctrl+ shift+c 可以实现查看百度首页的前端代码
```
<input id="kw" class="s_ipt" type="text" maxlength="100" name="wd" autocomplete="off">
```
id=”kw”
通过find_element_by_id(“kw”) 函数就是捕获到百度输入框
name=”wd”
通过find_element_by_name(“wd”)函数同样也可以捕获百度输入框
- CSS定位
- CSS(Cascading Style Sheets)是一种语言，它被用来描述HTML和XML文档的表现。CSS使用选择器来为页面元素绑定属性。这些选择器可以被selenium用作另外的定位策略。CSS的比较灵活可以选择控件的任意属性。
```
find_element_by_css_selector(“#kw”)
```
- xpath
- - 什么是XPath：XPath是一种在XML文档中定位元素的语言。因为HTML可以看做XML的一种实现，所以selenium用户可是使用这种强大语言在web应用中定位元素。
```
xpath:attributer （属性）
driver.find_element_by_xpath("//input[@id='kw']").send_keys("selenium")

#input标签下id =kw的元素
xpath:idRelative （id相关性）
driver.find_element_by_xpath("//div[@id='fm']/form/span/input").send_keys("selenium")

#在/form/span/input 层级标签下有个div标签的id=fm的元素
driver.find_element_by_xpath("//tr[@id='check']/td[2]").click() 

# id为'check' 的tr ，定闪他里面的第2个td
xpath:position （位置）

driver.find_element_by_xpath("//input").send_keys("selenium") 

driver.find_element_by_xpath("//tr[7]/td[2]").click()

#第7个tr 里面的第2个td
xpath: href （水平参考）
driver.find_element_by_xpath("//a[contains(text(),'网页')]").click()

#在a标签下有个文本（text）包含（contains）'网页' 的元素

xpath:link
driver.find_element_by_xpath("//a[@href='http://www.baidu.com/']").click()

#有个叫a的标签，他有个链接href='http://www.baidu.com/ 的元素
```
## 2.3层级定位
场景：
假如两个控件，他们长的一模样，还都叫“张三”，唯一的不同是一个在北京，一个在上海，那我们就可以通过，他们的城市，区，街道，来找到他们。
### 2.3.1 清除功能
```
browser.find_element_by_id("kw").clear() #清除输入框的内容
browser.find_element_by_id("kw").send_keys(“XX内容”)  #输入框输入内容
browser.find_element_by_id("su").click() # 单击按钮搜索

#id = cp 元素的文本信息
data=driver.find_element_by_id("cp").text  #cp的获取

#通过submit() 来操作
driver.find_element_by_id("su").submit() # 通过提交来搜索

```
# 3 中级教程
## 3.1 多层框架或窗口的定位
```
#先找到到ifrome1（id = f1）
browser.switch_to_frame("f1")
#再找到其下面的ifrome2(id =f2)
browser.switch_to_frame("f2")

driver.switch_to_window(“windowName”)
```
隐式地等待一个无素被发现或一个命令完成；这个方法每次会话只需要调用一次
## 3.2 智能等待

```
driver.implicitly_wait(30)
```
## 4.键盘按键用法
```
from selenium.webdriver.common.keys import Keys  #需要引入keys包
driver.find_element_by_id("user_name").send_keys(Keys.TAB)
time.sleep(3)
driver.find_element_by_id("user_pwd").send_keys("123456")
#通过定位密码框，enter（回车）来代替登陆按钮
driver.find_element_by_id("user_pwd").send_keys(Keys.ENTER)
#也可定位登陆按钮，通过enter（回车）代替click()
driver.find_element_by_id("login").send_keys(Keys.ENTER)
```
通过send_keys()调用按键：
send_keys(Keys.TAB)        # TAB
send_keys(Keys.ENTER)    # 回车
```
#ctrl+a 全选输入框内容
driver.find_element_by_id("kw").send_keys(Keys.CONTROL,'a')

#ctrl+x 剪切输入框内容
driver.find_element_by_id("kw").send_keys(Keys.CONTROL,'x')
```
### 4.1 中文输入问题
```
send_keys(u”输入中文”)
```
## 5.鼠标事件
- context_click()  右击
  double_click()   双击
  drag_and_drop()  拖动
```
#定位到要右击的元素
qqq =driver.find_element_by_xpath("/html/body/div/div[2]/div[2]/div/div[3]/table/tbody/tr/td[2]")

#对定位到的元素执行鼠标右键操作
ActionChains(driver).context_click(qqq).perform()


