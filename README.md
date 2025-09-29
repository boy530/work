## 📁 文件结构
```
web/
├── UPDATE_HTML_ALL.bat           # 双击运行程序 
├── UPDATE_HTML.py                # 主入口
├── main.html                     # 主页
├── am_kaijian_data.json          # 澳门开奖记录
├── xg_kaijian_data.json          # 香港开奖记录
├── bbs1/                         # BBS1页面文件夹
├── bbs/                          # BBS页面文件夹
├── Logs/                         # 日志文件夹
└── Modify_HTML/                  # 核心文件夹（禁止修改）
    └── config.py                 # 配置文件
```

## 🚀 快速开始

### 步骤
解压后，把 `UPDATE_HTML.py` 和 `Modify_HTML` 文件夹拷贝到网站（`main.html`、`bbs` 文件夹）同一层目录。
双击 `UPDATE_HTML_ALL.bat` 即可运行。

### 注意事项

- *Modify_HTML 文件夹*：任何文件均禁止修改！
- *Logs 文件夹*：可以删除或保留，每次运行会自动创建
- *开奖数据*：请按实际开奖修改对应的 JSON 文件

-----------------------


以下为需要注意的几个地方：
> UPDATE_HTML_ALL.bat 双击运行程序 
```
REM AM, Comment out with ::
python UPDATE_HTML_AM.py

REM HK, Comment out with :: 
python UPDATE_HTML_HK.py

pause
```

> 需要安装 python 3.13来运行脚本 
> https://www.python.org/ftp/python/3.13.6/python-3.13.6-amd64.exe
> 
> 检查已安装版本，星号 * 表示当前默认版本
> cmd命令窗口运行： py -0
> 
> 如果有多个版本，且星号 *不在3.13这一行，需要在 C:\Windows 下创建 py.ini，内容：
> [defaults]
> python=3.13
> 
> 或者，用 set path 查看 ptyhon安装路径。然后写上完整路径如：
> "D:\Program Files\Python313\python.exe" UPDATE_HTML_AM.py    #来指定python的版本



<br>  

## 删除规则：
```
【仅有一期时】：
1. 如果仅有一期，且开错，删除

【对于平特功能块】：
1. 如果当期开错，且跟前一期不连续，删除所有期
2. 最新的两期为错，且所有错的期数大于对的期数，删除所有期
3. 最新的两期为错，且所有错的期数小于对的期数，删除所有错的期数

【对于非平特功能块】：
1. 最新的两期为错，删除所有错的期数
2. 最新期开错，最近两期不连续，删除最新期
3. 最新期开错，且之前的期数中有缺失期数，删除最新期

【其它】：
1. ①肖①码，当七肖未中时，删除
2. 一肖一码，当九肖未中时，删除
3. 澳门信封, 当七肖未中时，删除
4. 两波⑩码这类有"标签页"的，当期未中删除
```

<br>

## 关于提问题，可参考如下：
```
明确区块：
如 bbs/016.html

详细问题描述，想要达到什么样的效。如：
只需要特码不用关注平码，生肖或数字在开奖中时，进行高亮。连续两期出错时，需要删除所有出错的记录。

```

