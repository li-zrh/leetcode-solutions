# 项目贡献指南

## 代码管理

本项目的唯一代码托管地址为 [https://github.com/li-zrh/leetcode-solutions](https://github.com/li-zrh/leetcode-solutions) ，代码主要贡献者为 [@zhonger](https://github.com/zhonger) 和 [@lukesky0919](https://lukesky0919) 。

### 代码分支情况

本项目暂时共有三个分支：**main**、**zrh** 和 **lsz** 。其中 **zrh** 和 **lsz** 分支为开发者开发使用分支，在经过分支内容评审后合并到 **main** 主分支中。

### 代码拉取到本地

```bash
git pull git@github.com:li-zrh/leetcode-solutions   # 有 ssh 权限时

git pull https://github.com/li-zrh/leetcode-solutions  # 无 ssh 权限时
```

### 代码切换开发分支

```bash
git branch zrh        # 创建 zrh 新分支
git checkout zrh    # 切换到 zrh 新分支上
```

### 提交代码

```bash
git status      # 查询当前工作区情况，注意操作的分支一定要是开发分支，当不确定时，使用 git branch 查看当前所在分支
git add filename    # 如出现未跟踪文件，单文件可以指定文件的名字
git add -A             #  多文件时，使用全部添加跟踪指令

git config --global user.email "xxxx@gmail.com"   # 设置 git 提交时的用户邮箱，与 Github 使用邮箱保持一致
git config --global user.name "lukesky0919"           # 设置 git 提交时的用户名，与 Github 使用用户名保持一致，这两步只需第一次提交前设置

git commit -m "add leetcode0001"           #  添加 commit 信息，一般来说使用有意义的语句，添加 add，修改 modify，修复 fix，删除 delete + 名词
git push origin zrh
```

### 代码评审

符合以下要求即可：

- 以上代码管理操作规范、正确
- 文章内容与文章模板及编辑规范吻合
- 所编写解题思路和代码经过二次验证的确有效
- 代码评审采取交叉评审，即互相检查、验证
- 在线预览效果正常（通过观察 `mkdocs serve` 预览页面来确认）

## 文章编辑规范

本项目所有文章均采用通用 Markdown 语法来进行编辑，支持 MathJax 公式编辑。所有流程图和解题思路描述所需图片均使用自制和 webp 格式，并由 [vgy.me](https://vgy.me) 进行托管。

### Markdown 语法指南

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

普通段落文件（直接输入）

**加粗**
*斜体*
`段落内标签，通常在段落中引用命令时使用`
<u>下划线</u>
~~删除线 ~~
<sub>下标</sub>
<sup>上标</sup>

- 无序列表 
- 无序列表

1. 有序列表
2. 有序列表

| 表头 1 | 表头 2  | 表头 3 |
| :---: | :--- | ---: |
| 表内第一行 | 表内第一行 | 表内第一行  |
| 居中 | 左对齐 | 右对齐  |

> 引用

- [x] 任务一    （已完成状态）
- [ ] 任务二   （未完成状态）

[超链接显示内容](超链接地址)
![图片名](图片所在地址)

​```cpp
# 代码文件名，比如 leetcode0001.cpp

代码内容（文件名与内容之间留一行空白，内容最后不留空行）
# 代码内注释
​```

<!-- 注释内容，以下为公式 -->
$$
y=x^2  
$$
```

### 通用文章规范

- 英文或是数字与中文之间前后各有一个空格，超链接、段内标签等与中文之间也需如此；
- 英文为行首时，前面不留空格；
- 英文与英文标点符号一起时，前面标点符号后空一格开始英文单词；
- 英文与中文标点符号一起时，标点符号在英文或符号之前之后都无须空格；
- 在代码内容中，# 号与文字之间空一格，# 号与代码同行时距离不宜过长，如相邻几行都有注释对齐为佳；当代码注释内容超过一行时最好将注释放在代码的后一行，此时 # 号前不留空格；
- 在使用图片进行解释的时候，在对应段落附近加载图片，并使用“下图”、“上图”这样的字眼进行描述；
- 图片均使用 PPT 自行制作，使用 [Snipaste 截图工具](https://zh.snipaste.com/) 截图保存，并上传至 [vgy.me](https://vgy.me) 后加载使用。
- 编程语言、专用英文词汇使用时，根据其通用的写法来适当调整大小写，比如 Python 3 的第一个字母就需要大写，Java 的第一个字母也需要大写；
- 当括号内是英文字符，使用英文括号（半角），当括号内是中文字符时，使用中文括号（全角）。

### 文章模板

为了更方便使用文章模板，文章模板是在代码根目录下的独立文件 `Template.md`。

## 生成预览

已安装 Python 3、pip 或者 Anaconda。为了加快依赖安装速度，国内用户可参考 [更换（Pypi）pip源到国内镜像](https://developer.aliyun.com/article/652884) 。

```bash
cd leetcode-solutions                   # 进入代码目录
pip install -r requirements.txt      # 根据依赖文件安装所需依赖
mkdocs serve                               # 启动在线预览页面，浏览器访问 http://127.0.0.1:8000

conda install --yes --file requirements.txt     # 或者使用 Anaconda
```

## PDF 生成

与 Sphinx 一起使用生成类似于 Readthedoc 导出文档的 PDF 文件，具体操作步骤后续更新。

## 项目版权

本项目采用 MIT 开源协议，可署名后进行使用、转发。