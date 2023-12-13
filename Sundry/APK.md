# 安卓逆向 Apktool

[Install Guide | Apktool](https://apktool.org/docs/install/)

1. 下载 apktool.bat 
2.  下载 apktool.jar
3. 将 `apktool.jar` 和 `apktool.bat` 移动到您的 Windows 目录。 （通常是 `C://Windows` ）
4. 命令提示符cmd 输入运行 `apktool` 

##　反编译

- cd 到 apk 的目录下
- 输入

```shell
$ apktool d test.apk
```

**注意：**
此时 dex 文件直接反编译成了 **[smali](https://www.zhihu.com/search?q=smali&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A590981557})** 文件，而我们需要的是 .dex 文件。

此时再运行：

```text
$ apktool d -s -f test.apk
```

-d 反编译 apk 文件
-s 不反编译 dex 文件，而是将其保留
-f 如果目标文件夹存在，则删除后重新反编译

[怎样反编译 Android APK？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/29370382)