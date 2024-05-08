## &#x20;基础使用

```cmake
find_package(SomeThing
	Names
		SametingOtherName
		SomeThing
)

find_package(Catch 2)
find_package(CTest REQUIRED)
find_package(Boost 1.79 COMPONENTS data_time)
```

## &#x20;Config Mode

 `<PackageName>Config.cmake` 

 `<LowercasePackageName>-config.cmake`

## &#x20;自动查找路径

linux: /usr

Windows: C:\Program Files

如果包配置文件不在标准cmake查找路径下，则可通过设置`CMAKE_PREFIX_PATH` 或 \`PackageName\_DIR\` 变量使得cmake 能查找到配置文件。

例如包配置文件放在以下位置。

opt/somepackage/lib/cmake/somepackage/SomePackageConfig.cmake

CMAKE\_PREFIX\_PATH : opt/somepackage

PackageName\_DIR  opt/somepackage/lib/cmake/somepackage/



## &#x20;Module Mode

Find\<PackageName>.cmake

## 查找路径

`CMAKE_PREFIX_PATH`

如果find\_package() 没有指定查找模式 ， 则优先查找Find\<PackageName>.cmake， 其次再查找包配置文件 `<PackageName>Config.cmake` 



## &#x20;imported Targets

形式： SomePrefix::ThingName
导入目标会传递个各种依赖，比如头文件路径、编译选项等

## FetchContent
1. 包含FetchContent模块
2. 声明要导入的包信息
3. 要求模块可用
```cmake
include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        703bd9caab50b139428cea1aaff9974ebee5742e # release-1.10.0
)
FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        605a34765aa5d5ecbf476b4598a862ada971b0cc # v3.0.1
)
FetchContent_MakeAvailable(googletest Catch2)
```