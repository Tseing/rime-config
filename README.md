自用的 [RIME 输入法](https://rime.im/)配置，搭载[虎码方案](https://tiger-code.com/)，精简了许多不必要而显得繁重的功能。

- `Android` 文件夹下为[同文输入法](https://github.com/osfans/trime)配置，使用了[单静主题](https://github.com/nopdan/danjing)。
- `Windows` 文件夹下为[小狼毫输入法](https://github.com/rime/weasel)配置，使用自改的主题。

更详细的定制指引可以翻阅以下两份文档，需要注意的是同文输入法（trime）是 RIME 的衍生，二者和配置既有交合的部分，也有独特的部分，两个文档需要互相参照着看。例如 `*.trime.yaml` 就是 trime 的特殊配置（适配于手机屏幕），所以在 trime Wiki 中才有相关介绍。

- [trime Wiki](https://github.com/osfans/trime/wiki/trime.yaml%E8%A9%B3%E8%A7%A3)
- [rime Wiki](https://github.com/rime/home/wiki/CustomizationGuide)

## TODO

- README.md
- Android 版 `Shift_L` 锁定时部分键位的 `long_click` 字符（主字符上方）显示错误
- Android 版添加更方便的注音输入
- Windows 版精简功能

## 安装

### Android

- 从应用商店或是 GitHub 仓库下载并安装同文输入法，打开应用，根据指引完成初始设置；
- 应用的默认配置文件夹为 `/storage/emulated/0/rime`，亦可由 `配置管理-用户文件夹` 更改路径；
- 将 `Android` 文件夹下所有内容复制到用户文件夹下；
- 再回到输入法应用，选择部署，等待加载完成即安装成功。

**注意**：完成后还需要在输入法应用中选择 `键盘设置`，打开 `点击候选词（直接上屏候选词）`。否则尽管以触屏方式选词，输入法仍是通过发送数字 `1`、`2`、`3` 的方式选择候选词，在输入时会产生冲突。

### Windows 🚧

## Android 文件清单

### 基本配置

- `default.yaml`
- `default.custom.yaml`

### 主题文件
- `backgrounds`：单静主题的背景文件。
- `danjing.yaml`：单静主题的预设文件。
- `单静.trime.yaml`：单静主题文件，修改主题一般修改此文件，在 [nopdan/danjing](https://github.com/nopdan/danjing) 可以找到另外几款相同风格的主题。

### 基本字符

- `opencc`：简繁及异体字的转化规则，这些功能对于形码无用，暂时把转化功能关闭了，但还是先保留。
- `punctuation.yaml`：全半角符号转换规则。
- `symbols.yaml`：击 `/` + `缩写` 输出的特殊符号，可自定义。

### 脚本文件

- `rime.lua`：Lua 插件开关，写入该文件的插件即开启，注释去即关闭。
- `lua`：自定义的 Lua 插件库，我认为累赘的功能都被关闭了，具体介绍见下文的脚本全功能介绍。
  - `calculator_translator.lua`：简易计算器，关闭。
  - `charset_comment_filter.lua`：Unicode 编码提示，开启。
  - `core2022_filter.lua`：自定义字符集过滤，开启。
  - `dz_ci_filter.lua`：有问题的单字模式，关闭。
  - `exe.lua`：使用外部应用打开 URL，关闭。
  - `number.lua`：击 `/S` + `数字` 输出大写数字，开启。
  - `shijian2.lua`：输出实时时间，关闭。
  - `unicode_display.lua`：Unicode 编码提示，开启。

### 输入方案

- `core2022.dict.yaml`
- `core2022.schema.yaml`
- `easy_english.dict.yaml`
- `easy_english.schema.yaml`
- `PY_c.dict.yaml`
- `PY_c.schema.yaml`
- `tiger.dict.yaml`
- `tiger.schema.yaml`

## 脚本全功能介绍

脚本文件来源于[虎码官方资源站](http://huma.ysepan.com/)，这一部分的功能介绍也来自于官网的介绍文件。因为精简了许多内容，与原始版本并非能一一对应，仅保留可用功能的介绍，方便查阅。

🚧 太乱了还没整理，暂且直接复制上来……

```
/date 或 /frq 或 /orzh，可输出当前日期，有公历 + 农历
    如：2022年12月04日  壬寅年(虎)冬月十一
/time 或 /fsj 或 /okao，可输出当前时间
    如：下午12:37  12点39分48秒
/week 或 /fxq 或 /olzh，可输出当前是 周/星期 几
    如：周日  星期日
/cdate 或 /fnl 或 /wtxs，可输出农历
    如： 壬寅年(虎)冬月廿七
/fjq 或 /lzvq，可输出 节气
    如： 冬至 2022-12-22  立春 2023-02-04
```

```
用 等号= 引导，=“输入内容”，可进行些简易计算
举些基本的例子

基本运算符
+  -  *  /  % 	（加 减 乘 除 取余）
    取余就是求余数 如：10%3  得  1
可以用括号 优先运算
    如：(2+2^3)/12.43  得  0.80450522928399

乘方、开方 ( ^  sqrt)
    2^3 得 8  ； sqrt(9) 得 3

e 直接出自然常数 e=2.718281828459
pi 出  π     pi=3.1415926535898

最大数  max ； 最小数 min
    max{2*3,3*4,7*2.1} 得 14.7
    min{-2,3,-10} 得 -10

支持 tan sin cos log ln exp （正弦 余弦 正切 10为底的对数 e为底的对数 e为底的指数）
    sin(120) 得 0.58061118421231
    exp(2) 得 7.3890560989307
    log(100) 得 2
    ln(2)    得 0.69314718055995
    exp(2) 得 7.3890560989307
反的  atan asin acos


平均数 avg{1,7,8}  得 5.3333333333333
求和   sum{1,2,4} 得 7

fac 阶乘
    fac(3)  得 6
abs 绝对值
    abs(-2) 得 2
random 随机数
    random(1,10) 得 7 （1到10之间的）
floor  向下取整
    floor(2.4)  得2
ceil  向上取整
    ceil(2.4)  得 3
mod 求余函数
    mod(8,3)  得 2 （8除3的余数）
rad 弧度 ，deg 角度，deriv 导数 ……

其他例子：
    floor(9^(8/7)*cos(deg(6))) 得 -3
    =e^pi>pi^e 得 true
    =map({1,2,3},\x.x^2|) 得 {1, 4, 9}
    =map(range(-5,5),\x.x*pi/4|,deriv(sin)) 得 {-0.7071, -1, -0.7071, 0, 0.7071, 1, 0.7071, 0, -0.7071, -1}
    =$(range(-5,5,0.01))(map,\x.-60*x^2-16*x+20|)(max)() 得 21.066
    =test(\x.trunc(sin(x),1e-3)==trunc(deriv(cos)(x),1e-3)|,range(-2,2,0.1)) 得 true
```

```
输入 /huma 或 /zhmn 可打开虎码官网
	仅在PC端小狼毫与鼠须管有效
输入 /baidu 或 /bddu 或 /fuxl 可打开百度搜索
	仅在PC端小狼毫与鼠须管有效
输入 /biying 或 /bing 或 /biyk 或 /htxk 可打开微软必应搜索
	仅在PC端小狼毫与鼠须管有效
输入 /guge 或/google 或 /hgzz 可打开谷歌搜索
	仅在PC端小狼毫与鼠须管有效
输入 /wangpan 或 /whpj 或 /mbia 可打开虎码网盘
	仅在PC端小狼毫与鼠须管有效
输入 /muyi 或/emon 或 /genda 或 /gfda 或 /piua 可打开网页版木易跟打器（由群友 木易某某 开发）
	仅在PC端小狼毫与鼠须管有效
输入 /zitong 或 /zits 或 /whib 可打开字统网 https://zi.tools
	仅在PC端小狼毫与鼠须管有效
输入 /yedian 或 /yedm 或 /dnih 可打开叶典网 http://www.yedict.com
	仅在PC端小狼毫与鼠须管有效


如需自己添加其他网址，打开lua文件夹中的 exe.lua
按以下格式继续追加
  elseif (context.input == "/引导字母" or context.input == "/引导字母") then
    generic_open("所需网址")
    context:clear()

or 代表可以有多个引导方式，例如：全拼简拼，虎码……
```