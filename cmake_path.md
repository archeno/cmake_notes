# cmake_path

## 背景

 cmake 传统文件处理命令像`file` 直接处理目标平台的文件，会有以下问题
 * 不能跨平台处理路径(eg: / 和\\  )
 * 只能处理实际存在的路径
 
## 基本用法

### 获取目录部分内容

 ```cmkae
 cmake_path(GET pathVar <COMP> [LAST_ONLY] outVar)
 ```
如下字符串，通过设置不同的COMP得到的结果如下表
    examles_str: C:/one/two/start.middle.end

|Path component| Example|
|--| --|
ROOT_NAME| C:
ROOT_DIRECTORY| /
ROOT_PATH| C:/
FILENAME |start.middle.end
EXTENSION |.middle.end
STEM| start
RELATIVE_PART |one/two/start.middle.end
PARENT_PATH |C:/one/two

LAST_ONLY: 后缀名以最后一个.（默认是/后遇到的第一个.)
>note: # WRONG: Cannot use a string for the path
cmake_path(GET "/some/path/example" FILENAME result)
### 构建目录
```cmake
cmake_path(SET pathVar [NORMALIZE] input)
```

cmake_path(SET path NORMALIZE "/some//path/xxx/../example")
The path variable now holds the value: /some/path/example
## 注意事项
od