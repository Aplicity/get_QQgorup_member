# get_QQgorup_member
爬取QQ群成员名单数据

## 环境配置
* 操作系统：Mac OS
* 开发语言：python 3.6
* IDE：jupyter notebook（建议使用）
* 浏览器：Chrome（版本75.0.3770.100）
* 需要用到的库：selenium、bs4、time、datetime、pandas、os

## 策略思路
QQ群的主页为：https://qun.qq.com/member.html。

如果想查阅群号为123456的主页，则在主页URL后面加上#gid=123456。即我们想爬取群号为123456的群成员，需要请求的URL为：
https://qun.qq.com/member.html#gid=123456

如果正常登陆页面，第一步需要扫码登陆。如果在电脑端已经登陆过QQ的话，则可以通过选择相应的QQ用户进行登陆。

登陆后，页面的架构可能会有两种：一种是无群成员积分等级的，如下所示：
![image]()

另外，一种有群成员积分等级的：
![image]()

对于两种不同的架构，代码细节上有点出入。不过在本次实验中会识别出是否有群成员积分等级，再获取字段数据。

程序开始会先创建一个文件夹，用于存放数据集。文件夹命令方式：dataset + yyyymmdd（本日日期）；如果文件夹已存在，则放弃创建。

爬虫开始时，先用selenium模拟打开浏览器，现在selenium为3.x版本，需要下载相应的插件才能启动，否则会报错。

对于Chrome浏览器，插件下载地址：http://npm.taobao.org/mirrors/chromedriver/

对于火狐的话：https://github.com/mozilla/geckodriver/releases下载/

下载的时候必须选择与自己浏览器版本相照应的插件版本。

下载完成后解压，并把解压内容添加到python环境变量中去，又或者复制到浏览器安装目录文件中，又或者在代码允许selenium的时候制定插件路径（本次实验中使用的方法）。

代码运行后，会自动弹出新的浏览器，扫码或者点击登陆后，只能展示前面20个左右的群成员名单，需要不停下拉到底部，才能加载到完整的名单信息。在这里通过代码实现。

获取到完整的页面信息后，用BeautifulSoup进行提取数据，并用pandas汇成表格，保存到本地。 

文件命令方式：./dataset_yyyymmdd(当日日期) / + 群号 + .csv
