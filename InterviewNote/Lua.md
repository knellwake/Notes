# Lua的基本数据结构

# 如何实现lua面向对象编程

# lua里表和元表是什么

# Lua如何调用C#

三种方式
第一种：官方不推荐
第二种：如果Resource文件下的Lua文件，使用Lua的Require函数即可
第三种：如果Lua文件是下载的，使用自定义Loader可满足

[Xlua中通过C#脚本调用lua脚本的三种方式_xlua lua回调-CSDN博客](https://blog.csdn.net/weixin_45556869/article/details/100661523?ops_request_misc=&request_id=&biz_id=102&utm_term=C&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-100661523.first_rank_v2_pc_rank_v29&spm=1018.2226.3001.4187)

# C#如何调用Lua

# lua的垃圾回收机制原理是怎么样的

# 资源如何打包？依赖项列表如何生成？

1.查找指定文件夹ABResource里的资源文件
——Directory.GetFile(资源路径)
——新建AssetBundleBuild对象
——获取资源名称，并赋值对应AB名称
——获取各个资源的依赖项：通过UnityEditor.AssetDataBase类获取各个资源的依赖项
2.使用Unity自带的BuildPipeline进行构建AB包
——BuildPipeLine.BuildAssetBundles(输出AB包路径)
——File.WriteAllLines(将依赖项写入文件里)

# 如何解析版本文件？如何加载AB包资源？具体流程是怎么样的？

1.解析版本文件列表
——File.ReadAllLines(读取文件列表资源路径URL)
——获取资源名称，获取AB包名称，获取依赖项，字典容器存储
——获取Lua文件
2.加载资源
——异步加载资源AB包，AssetBundleRequest请求，AssetBundle.LoadFromFileAsync
——先检查依赖项，再异步加载AB包依赖项
——加载成功后都有对应的回调方法，将资源作为参数传入

![在这里插入图片描述](E:/Typora_MD/Image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxNDA3NTIz,size_16,color_FFFFFF,t_70.png)

# 热更新方案有哪些？以及具体热更流程
1、整包：存放在上SteamingAssets里
——策略：完整更新资源放在包里
——优点：首次更新少
——缺点：安装包下载时间长，首次安装久
2、分包
——策略：少部分资源放在包里，大部分更新资源存放在更新资源器中
——优点：安装包小，安装时间短，下载快
——缺点：首次更新下载解压缩包时间旧
3、适用性
——海外游戏大部分是使用分包策略，平台规定
——国内游戏大部分是使用整包策略
4、文件可读写路径
——Application.streamingAssestsPath 只读目录
——Application.persistentDatapath 可读写目录
——资源服务器地址URL
5、【从资源服务器】下载单个文件或多个文件
——NetWorking.UnityWebRequest获取URL , HTTP GET , 连接资源服务器
——获取到downloadHander的文件数据Data，完成后会回调方法，将文件Data作为参数传出
6、检查是否初次安装

![在这里插入图片描述](E:/Typora_MD/Image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxNDA3NTIz,size_16,color_FFFFFF,t_70-1697618489420-7.png)

![在这里插入图片描述](E:/Typora_MD/Image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxNDA3NTIz,size_16,color_FFFFFF,t_70-1697618495817-10.png)

# 网络客户端C# 和 Lua

# Lua的GC原理是什么？如何避免GC内存泄露？

# 简述Lua实现面向对象的原理???
总结：对象标识、状态、类体系、继承、私有性
1.表table就是一个对象，对象具有了标识self，状态等相关操作

2. 使用参数self表示方法的该接受者是对象本身，是面向对象的核心点,冒号操作符可以隐藏该self参数
3. 类（Class）：每个对象都有一个原型，原型(lua类体系)可以组织多个对象间共享行为
4. setmetatable(A,{__index=B}) 把B设为A的原型
5. 继承（Inheritance）：Lua中类也是对象，可以从其他类（对象）中获取方法和没有的字段
6. 继承特性：可以重新定义（修改实现）在基类继承的任意方法
7. 多重继承：一个函数function用作__Index元方法，实现多重继承，还需要对父类列表进行查找方法，但多继承复杂性，性能不如单继承，优化，将继承的方法赋值到子类当中
8. 私有性（很少用）基本思想：两个表表示一个对象，第一个表保存对象的状态在方法的闭包中，第二个表用来保存对象的操作（或接口），用来访问对象本身。使第一个表完成内容私有性。

# 简述Lua有哪8个类型?简述用途?
nil 空——可以表示无效值，全局变量（默认赋值为nil），赋值nil ，使其被删除
number 整数
table 表 ——
string 字符
userdata 自定义
function 函数
bool 布尔
thread线程

# XLua项目里，lua怎么调用C#的？

# lua可以做哪些优化？







