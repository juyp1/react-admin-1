# 代码生成工具
为了方便开发，系统配套提供了基于配置+模版的代码生成工具，可以快速生成增删改查相关代码。

## 特性
1. 基于文本配置文件，简单直接；
1. 可以基于swagger文档、数据库、配置文件，多种方式生成代码；
1. 基于模版，生成代码质量高，而且很容易扩展我们所需要的模版；

## 使用说明
基于默认配置文件 /script/gen/config.conf 进行代码生成
```bash
$ yarn gen
```

指定配置文件
```bash
$ yarn gen ./my-confog.conf
```

忽略文件覆盖提示
```bash
$ yarn gen -y
```

## 配置文件编写说明
配置文件通过自定义脚本读取，需要遵循一些简单的编写规则

1. 脚本读取文件文本内容，配置文件可以是任何类型；
1. 脚本通过空格拆分各个配置项，空格个数不限制；
1. \#\#\#\#\#\# （六个#号）所包裹的内容是用来区分配置模块的，不要随意改动， 配置块的顺序可以随意调整；
1. 配置获取优先级为：接口 > 数据库表 > 当前配置文件；
1. 接口配置中的url行注释掉，将不基于接口进行生成；
1. 数据库配置中，tableName行注释掉，将不基于数据库表生成；
1. 三种注释方式 # ; //，可以基于需求，使用任意一种方式进行代码注释；

### form表单元素关键字说明： 
1. q: 作为查询条件(query) ；
1. f: 作为表单(form)；
1. r: 是否必填（required）；
1. 5: 单独数字，最大可输入长度；
1. form表单可用类型：
    1. input hidden number textarea password mobile email
    1. select select-tree checkbox checkbox-group radio radio-group switch
    1. date time date-time date-range cascader json icon-picker

### 数据库链接各式
```
mysql://user:password@host:port/database?querystring
```
### ajax请求地址说明
1. 请求关键字：查询、修改、添加、删除、详情、批量删除；
1. 各式：请求类型 method url dataPath（获取接口数据的key 比如: data.list）；
1. 基于接口生成页面时：
    1. 具体的地址在《基础配置》中填写；
    1. 通过「查询」接口获取查询条件、表头信息；
    1. 通过「修改」接口获取表单信息；
    1.没有填写的请求将基于「查询」或者「目录」RestFul风格生成；

### 页面类型配置
1. 列表页、弹框编辑、页面编辑 系统默认模板和文件名，可以不指定模板和文件名；
1. 自定义页面：
    1. 需要同时指定模板和目标文件名比如：自定义页面 ./src/template.js->customer.jsx；
    1. 模板路径相对项目根目录开始写起；

