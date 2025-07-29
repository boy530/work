以下为代码需要注意的几个地方：

```
Modify_HTML_vAll.py 
subprocess.run(["python", "Modify_HTML_HK_v5_1ok.py"]) #香港
subprocess.run(["python", "Modify_HTML_v5_9ok.py"])    #澳门
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

1. 最新期开错，并且<li>跟上一期的<li>不连贯时删除
2. 最新期开错，且最新期为最小期数时删除
3. 最新期开错，且存在的<li>中有缺失时，删除
4. 此外，
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
