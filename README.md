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

 
> | 事项 | 说明 | 操作 |
> |------|------|------|
> | **UPDATE_HTML_ALL.bat** | 脚本文件 | 📍 双击运行程序 |
> | **Modify_HTML 文件夹** | 核心文件 | 🚫 禁止修改任何文件 |
> | **Logs 文件夹** | 日志文件 | 📁 可删除，运行时会自动创建 |
> | **开奖数据 kaijian_data.json** | 数据文件 | 📊 按实际开奖修改，JSON 标准格式 |

<br/>
### json文件标准格式：
```json
{
  "ABCrecords": [
    {
      "period": "001期",
      "zodiacs": [
        {"name": "n1", "number": "01"},
        {"name": "n2", "number": "02"},
        {"name": "n3", "number": "03"}
      ]
    },
    {
      "period": "002期",
      "zodiacs": [
        {"name": "n1", "number": "01"},
        {"name": "n2", "number": "02"},
        {"name": "n3", "number": "03"}
      ]
    },
    {
      "period": "003期",
      "zodiacs": [
        {"name": "n1", "number": "01"},
        {"name": "n2", "number": "02"},
        {"name": "n3", "number": "03"}
      ]
    }
  ]
}
```

-----------------------

<br/>

**⚠️ 重要注意事项**
> UPDATE_HTML_ALL.bat 双击运行程序 
```
REM AM, Comment out with ::
python UPDATE_HTML_AM.py

REM HK, Comment out with :: 
python UPDATE_HTML_HK.py

pause
```

> **环境要求**  
> 需要安装 Python 3.13 来运行脚本  
> 下载地址：https://www.python.org/ftp/python/3.13.6/python-3.13.6-amd64.exe
> 
> **版本检查**  
> 检查已安装版本，星号 * 表示当前默认版本  
> ```cmd
> py -0
> ```
> 
> **多版本配置**  
> 如果有多个版本，且星号 * 不在 3.13 这一行：
> 1. 在 `C:\Windows` 下创建 `py.ini`
> 2. 添加内容：
>    ```ini
>    [defaults]
>    python=3.13
>    ```
> 
> **或使用完整路径**  
> 用 `set path` 查看 Python 安装路径，然后使用完整路径：  
> ```bash
> "D:\Program Files\Python313\python.exe" UPDATE_HTML_AM.py
> "D:\Program Files\Python313\python.exe" UPDATE_HTML_HK.py
> pause
> ```



<br/>  

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

<br/>

## 关于提问题，可参考如下：
```
明确区块：
如 bbs/016.html

详细问题描述，想要达到什么样的效。如：
只需要特码不用关注平码，生肖或数字在开奖中时，进行高亮。连续两期出错时，需要删除所有出错的记录。

```

