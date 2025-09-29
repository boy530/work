文件结构：
400777\
├── UPDATE_HTML.py                 # * 主入口文件，只需要运行它就好 *
├── main.html                      # 在 Modify_HTML\config.py 修改路径
├── am_kaijian_data.json           # 澳门区开奖记录，按实际开奖修改
├── xg_kaijian_data.json           # 香港区开奖记录，按实际开奖修改
├── bbs1\                          # BBS1页面文件夹
├── bbs\                           # BBS页面文件夹
├── css\
├── img\
├── Logs\                          # 日志文件夹，可以删除也可以保留查看历史日志
└── Modify_HTML\                   # * 除了config.py配置，不要动其它任何文件 *
    └── config.py                  # 配置文件 修改test.html 为 main.html

1. 解压后，把"UPDATE_HTML.py"  "Modify_HTML文件夹"拷贝到网站(main.html bbs/ img/)同一层目录。运行UPDATE_HTML.py即可。
2. Modify_HTML文件夹下任何文件均禁止修改!!
3. Logs文件夹可以删除或保留，每次运行会自动创建。

-----------------------
需要安装 python 3.13来运行脚本 
https://www.python.org/ftp/python/3.13.6/python-3.13.6-amd64.exe

检查已安装版本，星号 * 表示当前默认版本
cmd命令窗口运行： py -0

如果有多个版本，且星号 *不在3.13这一行，需要要 C:\Windows 下创建 py.ini，内容：
[defaults]
python=3.13


以下为代码需要注意的几个地方：
```
UPDATE_HTML_ALL.bat 
REM AM, Comment out with ::
python UPDATE_HTML_AM.py

REM HK, Comment out with :: 
python UPDATE_HTML_HK.py

pause
```

> 在这里修改好对应的版本号，可以只运行这一个文件，就会把香港和澳门的python文件都运行



```
logging.getLogger().handlers[1].setLevel(logging.DEBUG)
```

> 把 logging.DEBUG 改为 logging.INFO 可以减少屏幕日志的输出



```
block_configs = [
    ('essm', '无敌24码', 'number', True),
    #('jcbt', '玄机解特', None, False),
    ('cypt', '创富六肖', 'animal', True),
]
```

> block_configs = [] 这里控制每一个功能块的执行，如果不想让某个功能块运行，可以在前面加 #进行注释



```
if updated:
    f.seek(0)
    f.write(str(soup))
    f.truncate()
    logging.info("HTML文件修改完成！"+"\n"*3)
```

> 这里控制是否最终写入html文件，这里的三个f.前加#的话，可以看日志，是否是想要的结果。主要用于调试



```
modify_html('test.html', result[0], result[1], result[2])
```

> 这里修改 test.html 文件名，为最终要执行修改的的html文件



**删除规则：**
1. 如果仅有一期，且开错，删除
 
对于平特功能块：
2. 如果当期开错，且跟前一期不连续，删除所有期
3. 最新的两期为错，且所有错的期数大于对的期数，删除所有期
4. 最新的两期为错，且所有错的期数小于对的期数，删除所有错的期数

对于非平特功能块：
5. 最新的两期为错，删除所有错的期数
6. 最新期开错，最近两期不连续，删除最新期
7. 最新期开错，且之前的期数中有缺失期数，删除最新期

8. 此外，
   ①肖①码，当七肖未中时，删除
   一肖一码，当九肖未中时，删除
   澳门信封, 当七肖未中时，删除
   两波⑩码这类有"标签页"的，当期未中删除



> kaijian_data.py      数据文件，不要乱修改，以免出错
> kaijian_data.json   需要保留至少三期纪录，以供程序调用**



**关于提需求，可参考如下：**

> 210期: 无敌24码 开:？00准
> 假如特码 开马48
> 一、[注明针对特码还是要包括平码]
> 只针对特码，不考虑平码。
>
> 二、[猜中时，详细写]
> 1。六个生肖中，有中的生肖涂色生肖...
> 如兔03，把兔涂色，并把 开？00准 改为 开马48准
>
> 三、[猜错时]
> 2。当期所有的数字添加删除线，把开？00准 改为 开马48错
>
> 四、[当猜错时的删除规则，及其它特殊规则"像一肖高亮时，玄机也高亮"，"九肖不中删除表" 这样详细写]
> 3。连续两期开错，或是中间期数不连贯，则把本期直接删除
