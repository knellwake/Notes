# Unity基础 API 组件

常用API与组件

SDK导入

## Unity脚本从唤醒到销毁有着一套比较完整的生命周期，列出系统自带的几个重要的方法。

Awake —> OnEnable —> Start —> FixedUpdate —>Update —> LateUpdate—> OnGUl —> OnDisable —> OnDestroy

主要执行顺序

编辑器->初始化->物理系统->输入事件->游戏逻辑->场景渲染->GUI渲染->物体激活或禁用->销毁物体->应用结束

主要函数介绍

![image-20231018132948982](E:/Typora_MD/Image/image-20231018132948982.png)

## OnEnable、Awake、Start运行时的发生顺序？哪些可能在同一个对象周期中反复的发生？

Awake–>OnEnable->Start

OnEnable在同一周期中可以反复地发生!

## Unity3d中Awake和Start 谁先执行，update和fixedUpdate 有什么区别？

awake先执行，一般用来初始化成员变量
start设置物体属性和渲染
fixedUpdate固定帧渲染，用于更新渲染物理引擎
update帧渲染，用于更新操作

## 物理更新一般放在哪个系统函数里？

FixedUpdate，每固定帧绘制时执行一次，和Update不同的是FixedUpdate是渲染帧执行，如果你的渲染效率低下的时候FixedUpdate调用次数就会跟着下降。

FixedUpdate比较适用于物理引擎的计算，因为是跟每帧渲染有关。 Update就比较适合做控制。

## 移动相机动作在哪个函数里，为什么在这个函数里？

**LateUpdate**，是在所有的Update结束后才调用，比较适合用于命令脚本的执行。
官网上例子是摄像机的跟随，都是所有的Update操作完才进行摄像机的跟进，不然就有可能出现摄像机已经推进了，但是视角里还未有角色的空帧出现。
## Unity中销毁GameObject的方式，简述Destroy和DestroyImmediate的区别

Destroy销毁消息对象，内存中还是存在，只有内存不够才被清除释放内存
DestroyImmediate立即销毁对象，并释放内存

## 如何销毁一个UnityEngine.Object及其子类？

使用Destroy()方法;

## 如何让已经存在的GameObject在LoadLevel后不被卸载掉？

DontDestroyOnLoad(transform.gameObject);

## Unity3D中的碰撞器和触发器的区别？

碰撞器是触发器的载体，而触发器只是碰撞器身上的一个属性。

当Is Trigger=false时，碰撞器根据物理引擎引发碰撞，产生碰撞的效果，可以调用OnCollisionEnter/Stay/Exit函数；

当Is Trigger=true时，碰撞器被物理引擎所忽略，没有碰撞效果，可以调用OnTriggerEnter/Stay/Exit函数。

如果既要检测到物体的接触又不想让碰撞检测影响物体移动或要检测一个物件是否经过空间中的某个区域这时就可以用到触发器。

## 物体发生碰撞的必要条件？
两个物体都必须带有碰撞器Collider，其中一个物体还必须带有Rigidbody刚体。

## CharacterController和Rigidbody的区别？
Rigidbody具有完全真实物理的特性，而CharacterController可以说是受限的的Rigidbody，具有一定的物理效果但不是完全真实的。

## 在物体发生碰撞的整个过程中，有几个阶段，分别列出对应的函数 三个阶段

OnCollisionEnter、 OnCollisionStay、 OnCollisionExit

## Unity3d的物理引擎中，有几种施加力的方式，分别描述出来

- rigidbody.AddForce
- rigidbody.AddForceAtPosition

## localPosition 与 Position 的使用区别？
localPosition :自身坐标系，相对于父级的位置
Position ：世界坐标系中的位置

## 物体自身旋转使用的函数？物体绕某点旋转使用函数叫什么？
自身旋转：transform.Rotate()
绕某点旋转：transform.RotateAround

## 简述四元数Quaternion的作用，四元数对欧拉角的优点？
四元数⽤于表示旋转，对旋转⻆度进⾏计算时⽤到四元数
相对欧拉⻆的优点：
1）能进⾏增量旋转
2）避免万向锁
3）给定⽅位的表达⽅式有两种，互为负（欧拉⻆有⽆数种表达⽅式）

## U3D中用于记录节点空间几何信息的组件名称，及其父类名称
Transform 父类是 Component

## 获取、增加、删除组件的命令分别是什么？
- 获取：GetComponent
- 增加：AddComponent
- 删除：Destroy

## Addcomponent后哪个生命周期函数会被调用
对于AddComponent添加的脚本，其Awake，Start，OnEnable是在Add的当前帧被调用的
其中Awake，OnEnable与AddComponent处于同一调用链上

Start会在当前帧稍晚一些的时候被调用，Update则是根据Add调用时机决定何时调用：如果Add是在当前帧的Update前调用，那么新脚本的Update也会在当前帧被调用，否则会被延迟到下一帧调用。

## 简述prefab的用处

在游戏运行时实例化，prefab相当于一个模板，对你已经有的素材、脚本、参数做一个默认的配置，主要用于经常会用到的物体做成一个集合方便反复使用，以便于以后的修改，同时prefab打包的内容简化了导出的操作，便于团队的交流。

##  Image和RawImage的区别

- Imgae比RawImage更消耗性能
- Image只能使用Sprite属性的图片，但是RawImage什么样的都可以使用
- Image适合放一些有操作的图片，裁剪平铺旋转什么的，针对Image Type属性
- RawImage就放单独展示的图片就可以，性能会比Image好很多

## 简述Invoke与InvokeRepeating

**Invoke**
Invoke() 方法是 Unity3D 的一种委托机制
如： Invoke(“Test”, 3); 它的意思是：3 秒之后调用 Test() 方法；

使用 Invoke() 方法需要注意 以下3点：
1 ：它应该在 脚本的生命周期里的（Start、Update、OnGUI、FixedUpdate、LateUpdate）中被调用；
2：Invoke(); 不能接受含有参数的方法；
3：在 Time.ScaleTime = 0; 时， Invoke() 无效，因为它不会被调用。

**InvokeRepeating**
InvokeRepeating(“Test”, 3 , 5);
这个方法的意思是指：3 秒后调用 Test() 方法，并且之后每隔 5 秒调用一次 Test() 方法。

## 正在运行的脚本，隐藏物体与禁止脚本导致触发OnDisable时，Invoke与coroutine是否正常运行？

只将脚本禁止：都会正常运行。

如果把物体直接隐藏：Invoke正常运行，coroutine不会正常运行。

原因：因为游戏物体隐藏了，一切与游戏物体相关的脚本生命周期都会停止，协程自然也会停止 ；
如果游戏对象没有隐藏，只是将脚本隐藏，游戏对象照样可以通过反射获取协程迭代器对象继续协程的执行。

## 采用Input.mousePosition来获取鼠标在屏幕上的位置
左下角为原点（0,0），右上角为（Screen.Height,Screen.Width）

## 如何检测物体是否被其他对象遮挡
射线检测
EventSystem.IsPointerOverGameObject
是否具有给定 ID 的指针是否位于 EventSystem 对象上

## 请简述OnBecameVisible及OnBecameInvisible的发生时机，以及这一对回调函数的意义？
当物体是否可见切换之时。可以用于只需要在物体可见时才进行的计算。

## Application.LoadLevel 命令作用是什么？
加载关卡，已弃用
现在使用SceneManager.LoadScene

## 调式记录到控制台的命令是什么？
Debug.Log();
## 请描述为什么Unity3d中会发生在组件上出现数据丢失的情况
一般是组件上绑定的对象被删除了，导致组件找不到该对象了而出现数据丢失现象。或者对象在Editor外部被删除和移动位置。

## 什么是导航网格（ NavMesh）？

用于自动寻路的网格
比如A*寻路

[Unity3D新版NavMesh系统功能初步探索_unity2022没有navmesh-CSDN博客](https://blog.csdn.net/chqj_163/article/details/109479439?ops_request_misc=%7B%22request%5Fid%22%3A%22160664353119726891123423%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=160664353119726891123423&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-109479439.first_rank_v2_rank_v28p4&utm_term=NavmESH)

## Unity 摄像机有几种工作方式，分别是什么？

正交模式和透视模式

## 如何使Camera只观察指定对象？





# UGUI

##  Text 和 TMPText的区别 优缺点
Text是像素渲染放大之后就会模糊，使用Text父物体的放大缩小会影响子物体Text的清晰度， TMPText不会，它是网格渲染TMPText会把字体生成一个类似于贴图的东西然后读取贴图的坐标来获取对应的文字，更换文字的消耗会比Text大。
TMPText更适用于不会变动的文字，特别是在量大的情况下，性能比Text高一些，需要经常变动的问题用Text好点，TMPText在字体库很大的情况下查找更换会比较慢。

## 画布的三种模式.缩放模式

- 屏幕空间-覆盖模式(Screen Space-Overlay)，Canvas创建出来后，默认就是该模式，该模式和摄像机无关，即使场景内没有摄像机，UI游戏物体照样渲染

  - 屏幕空间：电脑或者手机显示屏的2D空间，只有x轴和y轴
  - 覆盖模式：UI元素永远在3D元素的前面

- 屏幕空间-摄像机模式(Screen Space-Camera)，设置成该模式后需要指定一个摄像机游戏物体，指定后UGUI就会自动出现在该摄像机的“投射范围”内，和NGUI的默认UI Root效果一致，如果隐藏掉摄像机，UGUI当然就无法渲染

- 世界空间模式(WorldSpace)，设置成该模式后UGUI就相当于是场景内的一个普通的“Cube 游戏模型”，可以在场景内任意的移动UGUI元素的位置，通常用于怪物血条显示和VR开发

  ![image-20231018144631893](E:/Typora_MD/Image/image-20231018144631893.png)

## 如何使子控件居中,如果使用UGUI怎么实现
锚点设置为中心
## 请简述如何在不同分辨率下保持UI的一致性

多屏幕分辨率下的UI布局一般考虑两个问题：

1. 布局元素的位置，即屏幕分辨率变化的情况下，布局元素的位置可能固定不动，导致布局元素可能超出边界
2. 布局元素的尺寸，即在屏幕分辨率变化的情况下，布局元素的大小尺寸可能会固定不变，导致布局元素之间出现重叠等功能。

​	为了解决这两个问题，在Unity UGUI体系中有两个组件可以来解决问题，分别是布局元素的Rect Transform和Canvas的Canvas Scaler组件。

​	CanvasScaler中UI Scale Mode有三种模式，Constant Pixel Size、Scale With Screen Size、Constant Physical Size，其中第二个就是根据屏幕分辨率来进行缩放适配。在这个模式下，有两个参数，一个是我们在开发过程中的标准分辨率，一个是屏幕的匹配模式，通过这里面的设置，就可以完成多分辨率下的适配问题。

## 将图片的TextureType选项分别选为Texture和Sprite有什么区别

Sprite作为UI精灵使用，Texture作用模型贴图使用。

## 为什么dynamic font在unicode环境下优于static font

使用动态字体时，Unity将不会预先生成一个与所有字体的字符纹理， 静态字体体积会很大。

# 数据持久化 相关

## Unity3d提供了一个用于保存和读取数据的类(PlayerPrefs)，请列出保存和读取整形数据的函数

PlayerPrefs类是一个本地持久化保存与读取数据的类
PlayerPrefs类支持3中数据类型的保存和读取，浮点型，整形，和字符串型。
分别对应的函数为：

SetInt();保存整型数据；GetInt();读取整形数据；
SetFloat();保存浮点型数据； GetFlost();读取浮点型数据；
SetString();保存字符串型数据； GetString();读取字符串型数据；

## 动态加载资源的方式?

- instantiate：最简单的一种方式，以实例化的方式动态生成一个物体。

- Assetsbundle：即将资源打成 asset bundle 放在服务器或本地磁盘，然后使用WWW模块get 下来，然后从这个bundle中load某个object，unity官方推荐也是绝大多数商业化项目使用的一种方式。

- Resource.Load:可以直接load并返回某个类型的Object，前提是要把这个资源放在Resource命名的文件夹下， Unity不管有没有场景引用，都会将其全部打入到安装包中

- AssetDatabase.loadasset ：这种方式只在editor范围内有效，游戏运行时没有这个函数，它通常是在开发中调试用的。

## unity常用资源路径有哪些

```C#
//获取的目录路径最后不包含  /
//获得的文件路径开头包含 /
Application.dataPath; //Asset文件夹的绝对路径
//只读
Application.streamingAssetsPath;  //StreamingAssets文件夹的绝对路径（要先判断是否存在这个文件夹路径）
Application.persistentData ; //可读写

//资源数据库 (AssetDatabase) 是允许您访问工程中的资源的 API
AssetDatabase.GetAllAssetPaths; //获取所有的资源文件（不包含meta文件）
AssetDatabase.GetAssetPath(object) //获取object对象的相对路径
AssetDatabase.Refresh(); //刷新
AssetDatabase.GetDependencies(string); //获取依赖项文件


Directory.Delete(p, true); //删除P路径目录
Directory.Exists(p);  //是否存在P路径目录
Directory.CreateDirectory(p); //创建P路径目录

AssetDatabase //类库，对Asset文件夹下的文件进行操作，获取相对路径，获取所有文件，获取相对依赖项
Directory //类库，相关文件夹路径目录进行操作，是否存在，创建目录，删除等操作
```

## 编辑器类存放路径是什么？
Asset/Editor
##  如何安全的在不同工程间安全地迁移asset数据？三种方法

1. 将Assets和Library一起迁移
2. 导出包package
3. 用unity自带的assets Server功能

# 优化
##  什么是DrawCall？DrawCall高了又什么影响？如何降低DrawCall？
Unity中，每次引擎准备数据并通知GPU的过程称为一次Draw Call。DrawCall越高对显卡的消耗就越大。
降低DrawCall的方法：

- Dynamic Batching
- Static Batching
- 高级特性Shader降级为统一的低级特性的Shader。

## 如何在Unity3D中查看场景的面数，顶点数和Draw Call数？
在Game视图右上角点击Stats。降低Draw Call 的技术是Draw Call Batching

## 简述一下对象池，你觉得在FPS里哪些东西适合使用对象池？

对象池就存放需要被反复调用资源的一个空间。

比如游戏中要常被大量复制的对象，子弹，敌人，以及任何重复出现的对象。

**特点**：用内存换取cpu的优化

## 当游戏中需要频繁创建一个物体时，我们需要怎样做能够节省内存？

1.使用预制体对象
2.使用对象池技术

## 如何优化内存？

1. 压缩自带类库；
2. 将暂时不用的以后还需要使用的物体隐藏起来而不是直接Destroy掉；
3. 释放AssetBundle占用的资源；
4. 降低模型的片面数，降低模型的骨骼数量，降低贴图的大小；
5. 使用光照贴图，使用多层次细节(LOD)，使用着色器(Shader)，使用预设(Prefab)
6. 代码中少产生临时变量

## 你认为unity在开发过程中哪些地方比较容易造成内存泄漏和内存泄漏问题？如何避免？

## 如何解决过多创建和删除对象带来的卡顿问题

## 背包系统中只有20个格子，现在有总共有100个物体，除了显示在视野中的20个外，对其他的处理方法？（注：将其他隐藏起来不可行，对象池得有具体的说明）

##  LOD是什么，优缺点是什么？

**LOD(Level of detail)多层次细节**，是最常用的游戏优化技术。
它按照模型的位置和重要程度决定物体渲染的资源分配，降低非重要物体的面数和细节度，从而获得高效率的渲染运算。

缺点：增加了内存

[【100个 Unity实用技能】 | Unity 的 LOD技术（多细节层次）_unity lod_呆呆敲代码的小Y的博客-CSDN博客](https://xiaoy.blog.csdn.net/article/details/122425837)

## MipMap是什么，作用？

**MipMapping**：在三维计算机图形的贴图渲染中有常用的技术，为加快渲染进度和减少图像锯齿，贴图被处理成由一系列被预先计算和优化过的图片组成的文件，这样的贴图被称为MipMap。

## 启用MipMaps对内存的影响是？MipMap的作用？如何操作？

增加约33%的内存，1/4 +1/16
Lod相关知识


# 动画
##  什么叫做链条关节？
Hinge Joint，可以模拟两个物体间用一根链条连接在一起的情况，能保持两个物体在一个固定距离内部相互移动而不产生作用力，但是达到固定距离后就会产生拉力。

## 简述SkinnedMesh的实现原理
根据骨骼，动态整体实现表层Mesh，相对普通mesh由不同面片堆砌，根据骨骼结构，对顶点的变换计算出不同的蒙皮，最终进行模型的渲染

SkinnedMesh蒙皮网格动画
分为骨骼和蒙皮两部分
骨骼是一个层次结构，存储了骨骼的Transform数据
蒙皮是mesh顶点附着在骨骼之上，顶点可以被多个骨骼影响，决定了其权重等，
还有将顶点从Mesh空间变换到骨骼空间~

##  Animation和Animator的区别
Animation和Animator 虽然都是控制动画的播放，但是它们的用法和相关语法都是大有不同的。Animation控制一个动画的播放，而Animator是多个动画之间相互切换，并且Animator有一个动画控制器，俗称动画状态机。

Animator利用它做动画的切换是很方便的，但是它有一个缺点就是占用内存比Animation大。

## 请描述游戏动画有哪几种，以及其原理？
主要有关节动画、骨骼动画、单一网格模型动画(关键帧动画)。

关节动画：把角色分成若干独立部分，一个部分对应一个网格模型，部分的动画连接成一个整体的动画，角色比较灵活，Quake2中使用这种动画；

骨骼动画，广泛应用的动画方式，集成了以上两个方式的优点，骨骼按角色特点组成一定的层次结构，有关节相连，可做相对运动，皮肤作为单一网格蒙在骨骼之外，决定角色的外观；

单一网格模型动画由一个完整的网格模型构成，在动画序列的关键帧里记录各个顶点的原位置及其改变量，然后插值运算实现动画效果，角色动画较真实。

## 请描述游戏动画有几种，以及其原理。

关键帧动画：每一帧动画序列当中包含了顶点的空间位置信息以及改变量，然后通过插值运算，得出动画效果。选中某一游戏对象，创建animation，添加属性Transform，MeshRender、collider。还可以添加关键帧，在关键帧上Add Animation Event事件。

骨骼动画：模型当中有一个骨骼结构层次的对象，存储了各个骨骼在空间内的位置信息。皮肤蒙皮附着在骨骼上，决定了角色的外观，每一个顶点数据都会随着多个骨骼影响而改变，从而实现动画效果。创建animator将各个动画拖入到动画状态机当中，设置参数，连接各个动画状态，在通过脚本控制来实现动画控制

关节动画：了解不多，是骨骼动画的前身，模型分成N个部分网格，分成部分动画，组成一个整体动画

## Animation.CrossFade 是什么？

动画淡入淡出

## 反向旋转动画的方法是什么？
1.将动画速度调成-1
2.改代码animation.speed=-1

## 写出 Animation 的五个方法
AddClip 将 clip 添加到名称为 newName 的动画中。
Blend 在后续 time 秒中将名称为 animation 的动画向 targetWeight 混合。
CrossFade 在后续 time 秒的时间段内，使名称为 animation 的动画淡入，使其他动画淡出。
CrossFadeQueued 使动画在上一个动画播放完成后交叉淡入淡出。
IsPlaying 名称为 name 的动画是否正在播放？
PlayQueued 在先前的动画播放完毕后再播放动画。
RemoveClip 从动画列表中移除剪辑。
Sample 对当前状态的动画进行采样。
Stop 停止所有使用该动画启动的正在播放的动画。

## Avator的作用

用户提供的模型骨架和Unity的骨架结构进行适配，是一种骨架映射关系。
方便动画的重定向
AnimationType有三种类型
Humanoid人型：可以动画重定向，游戏对象挂载animator，子类原始模型+重定向模型，设置原始模型和使用模型的AnimationType为Humanoid类型
Generic非人型
Legacy旧版
Avator Mask身体遮罩，身体某一部分是否受到动画影响
反向动力学 IK，通过手或脚来控制身体其他部分











# 数学

## 向量的运算有哪些？Unity有哪些API可以计算

加法减法：物理上计算两个力的合力或者几个速度分量的叠加Vertor3（a1+b1,a2+b2,a3+b3）
数乘：向量与一个标量相乘，变量的正负，表示方向的正反方向变化，对向量的长度进行缩放
点乘：a点乘b得到一个标量，集合意义是a和b长度相乘再乘以两者夹角的余弦
叉乘：a叉乘b得到一个新向量，满足unity的左手坐标系

Vector3类
单位化normalized
向量长度magnitude
叉乘cross
点乘 dot
两向量夹角 angle
距离 distance
投影 project

## 向量的点乘、叉乘以及归一化的意义？
叉乘 几何意义：得到一个与这两个向量都垂直的向量，这个向量的模是以两个向量为边的平行四边形的面积
点乘 几何意义：可以用来表征或计算两个向量之间的夹角，以及在b向量在a向量方向上的投影

点乘描述了两个向量的相似程度，结果越大两向量越相似，还可表示投影
叉乘得到的向量垂直于原来的两个向量
标准化向量：用在只关系方向，不关心大小的时候

## 矩阵相乘的意义及注意点？
用于表示线性变换：旋转、缩放、投影、平移、仿射
注意矩阵的蠕变：误差的积累


# Unity Editor 相关 渲染 3D
## 简述Unity3D支持的作为脚本的语言的名称？
Unity支持的语言：C#

Unity的脚本语言基于Mono的.Net平台上运行，可以使用.NET库，这也为XML、数据库、正则表达式等问题提供了很好的解决方案。
## Unity和cocos2d的区别
Unity3D支持C#、javascript等，cocos2d-x 支持c++、Html5、Lua等。

cocos2d 开源 并且免费

Unity3D支持iOS、Android、Flash、Windows、Mac、Wii等平台的游戏开发，cocos2d-x支持iOS、Android、WP等。
## 使用Unity3d实现2d游戏，有几种方式？

1. 使用本身的GUI、UGUI
2. 把摄像机的Projection(投影)值调为Orthographic(正交投影)，不考虑z轴；
3. 使用2d插件，如：2DToolKit、NGUI

## Unity3D是否支持写成多线程程序？如果支持的话需要注意什么？
支持：如果同时你要处理很多事情或者与Unity的对象互动小可以用thread,否则使用coroutine。

Unity3d没有多线程的概念，不过unity也给我们提供了StartCoroutine（协同程序）和LoadLevelAsync（异步加载关卡）后台加载场景的方法。

注意：仅能从主线程中访问Unity3D的组件，对象和Unity3D系统调用。C#中有lock这个关键字,以确保只有一个线程可以在特定时间内访问特定的对象

## 在编辑场景时将GameObject设置为Static有何作用？
设置游戏对象为Static将会剔除（或禁用）网格对象当这些部分被静态物体挡住而不可见时。因此，在你的场景中的所有不会动的物体都应该标记为Static。

## 有A和B两组物体，有什么办法能够保证A组物体永远比B组物体先渲染？

把A组物体的渲染对列大于B物体的渲染队列
## Unity中，照相机的Clipping Planes的作用是什么?调整 Near、Far两个值时，应该注意什么?

剪裁平面 。从相机到开始渲染和停止渲染之间的 距离。

## 将Camera组件的ClearFlags选项选成Depth only是什么意思？有何用处？
仅深度，该模式用于对象不被裁剪。

## 问一个Terrain，分别贴3张，4张，5张地表贴图，渲染速度有什么区别？为什么？

没有区别，因为不管几张贴图只渲染一次。

## 层剔除
用layermask ，通过位运算的方式去设置
在代码中使用时如何开启某个Layers？

**LayerMask mask = 1 << 你需要开启的Layers层。**

**LayerMask mask = 0 << 你需要关闭的Layers层。**

举几个例子：

```c#
LayerMask mask = 1 << 2; 表示开启Layer2。

LayerMask mask = 0 << 5;表示关闭Layer5。

LayerMask mask = 1<<2|1<<8;表示开启Layer2和Layer8。

LayerMask mask = 0<<3|0<<7;表示关闭Layer3和Layer7。
```

##  MeshRender中material和sharedmaterial的区别？
修改sharedMaterial将改变所有物体使用这个材质的外观，并且也改变储存在工程里的材质设置。 不推荐修改由sharedMaterial返回的材质。如果你想修改渲染器的材质，使用material替代。

## 实时点光源的优缺点是什么？
可以有cookies – 带有 alpha通道的立方图(Cubemap )纹理。点光源是最耗费资源的。

## Unity提供了几种光源，分别是什么？
四种。

- 平行光：Directional Light
- 点光源：Point Light
- 聚光灯：Spot Light
- 区域光源：Area Light

## 当一个细小的高速物体撞向另一个较大的物体时，会出现什么情况？如何避免？
穿透（碰撞检测失败）（例如CS射击游戏，可以使用开枪时发射射线，射线碰撞到则掉血击中）

##　在场景中放置多个Camera并同时处于活动状态会发生什么？
受Camera覆盖各场景物件均同时实时绘制，主Camera视场里有多个Camera的渲染合集。可以用depth（深度），Layer（层）+ Culling Mask,enable = false/true来控制，或者调整Viewport Rect可以调整不同摄像机的显示内容。

## 什么是渲染管道？
是指在显示器上为了显示出图像而经过的一系列必要操作。 渲染管道中的很多步骤，都要将几何物体从一个坐标系中变换到另一个坐标系中去。

主要步骤有： 本地坐标->视图坐标->背面裁剪->光照->裁剪->投影->视图变换->光栅化。
##  GPU的工作原理？
简而言之，GPU的图形（处理）流水线完成如下的工作：（并不一定是按照如下顺序）。

顶点处理：这阶段GPU读取描述3D图形外观的顶点数据并根据顶点数据确定3D图形的形状及位置关系，建立起3D图形的骨架。在支持DX8和DX9规格的GPU中，这些工作由硬件实现的Vertex Shader（定点着色器）完成。

光栅化计算：显示器实际显示的图像是由像素组成的，我们需要将上面生成的图形上的点和线通过一定的算法转换到相应的像素点。把一个矢量图形转换为一系列像素点的过程就称为光栅化。例如，一条数学表示的斜线段，最终被转化成阶梯状的连续像素点。

纹理帖图：顶点单元生成的多边形只构成了3D物体的轮廓，而纹理映射（texture mapping）工作完成对多变形表面的帖图，通俗的说，就是将多边形的表面贴上相应的图片，从而生成“真实”的图形。TMU（Texture mapping unit）即是用来完成此项工作。

像素处理：这阶段（在对每个像素进行光栅化处理期间）GPU完成对像素的计算和处理，从而确定每个像素的最终属性。在支持DX8和DX9规格的GPU中，这些工作由硬件实现的Pixel Shader（像素着色器）完成。

最终输出：由ROP（光栅化引擎）最终完成像素的输出，1帧渲染完毕后，被送到显存帧缓冲区。

总结：GPU的工作通俗的来说就是完成3D图形的生成，将图形映射到相应的像素点上，对每个像素进行计算确定最终颜色并完成输出。

## 请问alpha test在何时使用？能达到什么效果？
Alpha Test,中文就是透明度测试。
简而言之就是V&F shader中最后fragment函数输出的该点颜色值（即上一讲frag的输出half4）的alpha值与固定值进行比较。Alpha Test语句通常于Pass{}中的起始位置。Alpha Test产生的效果也很极端，要么完全透明，即看不到，要么完全不透明。

## 什么叫动态合批？跟静态合批有什么区别？
如果动态物体共用着相同的材质，那么Unity会自动对这些物体进行批处理。
动态批处理操作是自动完成的，并不需要你进行额外的操作。

**区别：**动态批处理一切都是自动的，不需要做任何操作，而且物体是可以移动的，但是限制很多。静态批处理：自由度很高，限制很少，缺点可能会占用更多的内存，而且经过静态批处理后的所有物体都不可以再移动了。

##  两种阴影判断的方法、工作原理？

本影和半影：

本影：景物表面上那些没有被光源直接照射的区域（全黑的轮廓分明的区域）。
半影：景物表面上那些被某些特定光源直接照射但并非被所有特定光源直接照射的区域（半明半暗区域） 工作原理：从光源处向物体的所有可见面投射光线，将这些面投影到场景中得到投影面，再将这些投影面与场景中的其他平面求交得出阴影多边形，保存这些阴影多边形信息，然后再按视点位置对场景进行相应处理得到所要求的视图（利用空间换时间，每次只需依据视点位置进行一次阴影计算即可，省去了一次消隐过程）

## alpha blend工作原理?

Alpha Blend 实现透明效果，不过只能针对某块区域进行alpha操作，透明度可设。

## 什么是LightMap？

LightMap：就是指在三维软件里实现打好光，然后渲染把场景各表面的光照输出到贴图上，最后又通过引擎贴到场景上，这样就使物体有了光照的感觉。

## 写出光照计算中的diffuse的计算公式？

diffuse = Kd x colorLight x max(N*L,0)；Kd 漫反射系数、colorLight 光的颜色、N 单位法线向量、L 由点指向光源的单位向量、其中N与L点乘，如果结果小于等于0，则漫反射为0。



## UnityAction和UnityFunc的区别
unity中需要带上修饰event，事件与委托密切相关，两行代码变一行代码
public event Action myEvent;

UnityAction本质上就是委托，带泛型参数最多4个，且没有返回值的方法
Action<T1,T2,T3>
UnityFunc本质上也是委托，带泛型参数最多4个，可以有返回值的方法
Func<T1,T2,T3,Return>

Action和Func的重要区别：
Action只用于没有返回值的方法，Func只用于有返回值的方法
它们泛型里的区别：
Action的泛型里要和方法参数的类型相同，且只有一种泛型
Func的泛型里前者和方法参数类型相同，最后一个与返回值类型相同

一般用于回调方法，注册事件，类直接数据交互松耦合
[Unity学习 - C#委托的介绍(delegate、Action、Func、predicate)-CSDN博客](https://blog.csdn.net/sinat_23383269/article/details/46723103?ops_request_misc=%7B%22request%5Fid%22%3A%22160671212219724847140734%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=160671212219724847140734&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-3-46723103.first_rank_v2_rank_v28p4&utm_term=Unity action func&spm=1018.2118.3001.4449)

# 进程、线程、协程



## 简述进程、线程、协程的概念

### 进程

保存在硬盘上的程序运行以后，会在内存空间里形成一个独立的内存体，这个内存体有自己独立的地址空间，有自己的堆，不同进程间可以进行进程间通信，上级挂靠单位是操作系统。一个应用程序相当于一个进程，操作系统会以进程为单位，分配系统资源（CPU 时间片、内存等资源），进程是资源分配的最小单位。

### 线程

线程从属于进程，也被称为轻量级进程，是程序的实际执行者。线程是操作系统能够进行运算调度的最小单位。它被包含在进程之中，是进程中的实际运作单位。一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程，每条- 线程并行执行不同的任务。一个线程只有一个进程。
每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口，但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
线程拥有自己独立的栈和共享的堆，共享堆，不共享栈，线程亦由操作系统调度(标准线程是的)。

### 协程

协程是伴随着主线程一起运行的一段程序。
协程与协程之间是并行执行，与主线程也是并行执行，同一时间只能执行一个协程提起协程，自然是要想到线程，因为协程的定义就是伴随主线程来运行的。
一个线程可以拥有多个协程，协程不是被操作系统内核所管理，而完全是由程序所控制。
协程和线程一样共享堆，不共享栈，协程由程序员在协程的代码里显示调度。
协成是单线程下由应用程序级别实现的并发。

## 简述协程的作用

在Unity中只有主线程才能访问Unity3D的对象、方法、组件。当主线程在执行一个对资源消耗很大的操作时，在这一帧我们的程序就会出现帧率下降，画面卡顿的现象!

那这个时候我们就可以利用协程来做这件事，因为协程是伴随着主线程运行的，主线程依旧可以丝滑轻松的工作，把脏活累活交给协程处理就好了！简单来说：协程是辅助主线程的操作，避免游戏卡顿。


## 简述协程的底层原理

- 协程是通过迭代器来实现功能的，通过关键字IEnumerator来定义一个迭代方法。

- StartCoroutine 接受到的是一个 IEnumerator ，这是个接口，并且是枚举器或迭代器的意思。

- yield 是 C#的一个关键字，也是一个语法糖，背后的原理会生成一个类，并且也是一个枚举器，而且不同于 return，yield 可以出现多次。

- yield 实际上就是返回一次结果，因为我们要一次一次枚举一个值出来，所以多个 yield 其实是个状态模式，第一个 yield 是状态 1，第二个 yield 是状态 2，每次访问时会基于状态知道当前应该执行哪一个 yield，取得哪一个值。

> 从程序的角度讲，协程的核心就是**迭代器**。
> 想要定义一个协程方法有两个因素，第一：方法的返回值为 IEnumerator 。第二，方法中有 yield关键字。
> 当代码满足以上两个条件时，此方法的执行就具有了迭代器的特质，其核心就是 MoveNext方法。
> 方法内的内容将会被分成两部分：yield 之前的代码和 yield 之后的代码。yield之前的代码会在第一次执行MoveNext时执行， yield之后的代码会在第二次执行MoveNext方法时执行。
> 而在Unity中，MoveNext的执行时机是以帧为单位的，无论你是设置了延迟时间，还是通过按钮调用MoveNext，亦或是根本没有设置执行条件，Unity都会在每一帧的生命周期中判断当前帧是否满足当前协程所定义的条件，一旦满足，当前帧就会抽出CPU时间执行你所定义的协程迭代器的MoveNext。
> 注意，只要方法中有yield语句，那么方法的返回值就必须是 IEnumerator ，不然无法通过编译。

## 线程与协程的区别

协程：即协作式程序，其思想是，一系列互相依赖的协程间依次使用CPU，每次只有一个协程工作，而其他协程处于休眠状态。协程实际上是在一个线程中，只不过每个协程对CPU进行分时，协程可以访问和使用unity的所有方法和component。同一时间只能执行某个协程。开辟多个协程开销不大。协程适合对某任务进行分时处理。

线程：多线程是阻塞式的，每个IO都必须开启一个新的线程，但是对于多CPU的系统应该使用thread，尤其是有大量数据运算的时刻，但是IO密集型就不适合；而且thread中不能操作unity的很多方法和component。同一时间可以同时执行多个线程。开辟多条线程开销很大。线程适合多任务同时处理。

##  简述Invoke与协程的区别

- Invoke方法：执行没有被挂起，相当于设置完被调用函数的执行时间后即时向下执行。应用到每隔一段时间执行某个函数很方便。
- Coroutine方法：新开一条执行序列（跟新建线程差不多）并挂起，等待中断指令结束。开销不大。当需要挂起当前执行时使用。
- 协程的效率比Invoke高。



#  ScriptableObejct

ScriptableObject是一个数据容器，它可以用来保存大量数据。

- 主要的用处就是在项目中通过将数据存储在ScriptableObject对象，避免值拷贝来减少游戏运行中的内存占用。

- 当你有一个预制体，上面挂了一个存有不变数据的MonoBehaviour 脚本时，每次我们实例化预制体时都将产生一次数据拷贝，这时我们可以使用ScriptableObject对象来存储数据，然后通过引用来访问预制体中的数据。这样可以避免在内存中产生一份拷贝数据。与MonoBehaviour 一样，ScriptableObject也继承自Unity基类object，但是与MonoBehaviour不同的是，ScriptableObject不能和GameObject对相关联，相反，通常我们会将它保存为Assets资源。

- 在编辑器模式下，我们可以在编辑和运行时将数据保存到ScriptableObject，因为保存ScriptableObject需要用到编辑器空间个脚本，但是在开发模式下不能使用ScriptableObject来保存数据，但是你可以使用ScriptableObject资源中已保存的数据。

  [Unity零基础到进阶 | Unity中Scriptable Object介绍学习_呆呆敲代码的小Y的博客-CSDN博客](https://xiaoy.blog.csdn.net/article/details/124165347)

#  FSM有限状态机

FSM是一种数据结构，它由以下几个部分组成：

内在的所有状态（必须是有限个）
输入条件
状态之间起到连接性作用的转换函数
为什么要用FSM？

因为它编程快速简单，易于调试，性能高，与人类思维相似从而便于梳理，灵活且容易修改

FSM的描述性定义：
一个有限状态机是一个设备，或是一个模型，具有有限数量的状态。它可以在任何给定时间根据输入进行操作，使得系统从一个状态转换到另一个状态，或者是使一个输出或者一种行为的发生，一个有限状态机在任何瞬间只能处于一种状态。

State 状态基类，定义了基本的Enter，Update，Exit三种状态行为，通常在这三种状态行为的方法里会写一些逻辑。每个State都会有StateID（状态id，可以是枚举等），FSMControl（控制该状态的状态控制器的引用），Check方法（用来进行状态判断，并返回StateID，通过FSMControl驱动）

FSMControl，包含了一下FSMMachine，封装层。

FSMMachine，驱动它的State列表，Update方法调用当前State的Check方法来获得StateID，当currentState的Check方法返回的StateID和当前StateID不同，则切换状态。

这是一个简单的FSM状态机系统，根据需要自己写个Control继承FSMControl来驱动状态。因为Check是State的职责，所以每一个不同对象的行为如Human的Idle和Dog的Idel区分肯定也不同。因此需要分别去写HumanIdleState和DogIdleState。如果还有Cat，Fish，可想而知代码量会有多么庞大。

因此我将FSMControl抽象为一个公共基类，把State的Check具体实现作为FSMControl的Virtual方法。这样在IdleState里的Check方法就不用写具体的状态切换判断逻辑，而是调用它FSMControl子类（自己写的继承自FSMControl的Control类）的重写方法

这样每次添加的新对象只要有Idle这个状态，就可以用一个公用的StateIdle，状态切换的逻辑差异放在Control层


# 行为树与有限状态机

**有限状态机系统：**是指在不同阶段会呈现出不同的运行状态的系统，这些状态是有限的、不重叠的。这样的系统在某一时刻一定会处于其所有状态中的一个状态，此时它接收一部分允许的输入，产生一部分可能的响应，并且迁移到一部分可能的状态。

1. 基本节点是状态：他包含了一系列运行在该状态的行为以及离开这个状态的条件。
2. 状态可以任意跳转,实现简单,但是对于大的状态机很难维护，状态逻辑的重用性低。
3. 每一个状态的逻辑会随着一些新状态的增加而越来越复杂。维持状态的数量和状态逻辑复杂性是一个很大的难点。需要合理的分割以及重用状态。
4. 状态机状态的复用性很差，一旦一些因素变化导致这个环境发生变化。你只能新增一个状态，并且给这个新状态添加连接他以及其他状态的跳转逻辑。
5. 状态机的跳转条件一旦不满足，就会一直卡在某一个状态。

**行为树：**一个流行的AI技术，涵盖了层次状态机，事件调度，事件计划，行为等一系列技术。实现AI的过程更加得有技巧，框架设计者较为全面考虑了我们可能会遇到的种种情况，把每种情况都抽象成了一个类型的节点，而我们要做的就是按照规范去写节点，然后把节点连接成一颗行为树。更加得具有面向对象的味道，行为模块间的藕合度相对较低。

1. 高度模块化状态，去掉状态中的跳转逻辑，使得状态变成一个“行为”。
2. "行为"和"行为"之间的跳转是通过父节点的类型来决定的。比如并行处理两个行为，在状态机里面无法同时处理两个状态。
3. 通过增加控制节点的类型，可以达到复用行为的目的。
4. 可视化编辑。

#  简述行为树的概念及优缺点

概念：

1. 对于有限状态机而言，必须明确状态的转换方式；对于行为树，必须明确状态前提：前提条件。
2. 每一个行为必须有“前提条件” ，这决定了该行为是否被选择。
3. 行为树的运算也是通过帧循环的update来驱动，不一定是每帧都update，但是要周期性update。
4. 每一次run从根节点(root)开始，每一运行都会选择一个可行的子节点运行，这种选择可以是随机方式，也可以是预设好优先条件。
5. 行为树由叶子节点和中间节点组成，叶子节点是最基本的行为(如跑动，攻击)，中间节点代表逻辑单元(巡逻，逃跑)。
6. 当一个叶子节点被选择后，就会激活其对应的基本的行为。
7. 最基本的行为可能执行成功也可能失败。
8. 高等级的行为（中间节点）是否执行成功依赖于他们的孩子节点是否执行成功。
9. 一个子节点失败可能导致父母节点选择另外一个孩子。
10. 除了选择(selector)一个单独的子节点行为，一个节点还可能顺序(sequence)or并行(concurrent)得运行他的所有子节点。
11. 一个行为除了有前提条件，可能还有上下文条件(父节点or孩子节点可能存储一定的状态变量)。
    高优先级的行为可能抢占低优先级的行为。

优点：

1. 行为逻辑和状态数据分离，任何节点写好以后可以反复利用。
2. 重用性高，可用通过重组不同的节点来实现不同的行为树。
3. 呈线性的方式扩展，易于扩展。
4. 可配置，把工作交给designer。
5. 能够胜任"AI" “掉宝”等等场景。

缺点：

1. 每一帧都从root开始，有可能会访问到所以的节点，相对State Machine消耗更多的cpu。
2. 任何一个简单的操作都必须要使用节点。


# 使用过哪些Unity插件

|  插件名   |     作用     |
| :-------: | :----------: |
|  DoTween  |   动画插件   |
| easytouch | 手游触摸控制 |
|           |              |
|           |              |
|           |              |
|           |              |
|           |              |
|           |              |
|           |              |

shader graph	制作shader光影效果
cinemachine+timeline+postprocessingstack	制作过场动画
nodecanvas	制作怪物ai	
Fungus	对话插件
3D WebView	浏览器插件
Vectrosity	划线插件
AVPro Video	视频播放插件
Feel	受击插件
Device Simulator	移动设备模拟器
StateMachine	状态机插件
# 设计模式
## 用过哪些设计模式？ 谈谈自己比较熟悉的设计模式
[常用设计模式有哪些？ (refactoringguru.cn)](https://refactoringguru.cn/design-patterns)
创建型：工厂方法、抽象工厂、单例、原型、生成器
结构型：代理、外观、组合、适配器、装饰、桥接、享元
行为：迭代器、中介者、观察者、策略、状态、命令、访问者、模板方法、备忘录、责任链

1）工厂方法模式 面试题 [设计模式--工厂方法模式在unity3d里面的使用_unity工厂模式和多态-CSDN博客](https://blog.csdn.net/zhaoguanghui2012/article/details/43758907?ops_request_misc=%7B%22request%5Fid%22%3A%22160604747319724836743005%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=160604747319724836743005&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-43758907.first_rank_ecpm_v3_pc_rank_v2&utm_term=unity+工厂方法&spm=1018.2118.3001.4449)
在父类中提供一个创建对象的方法，在其子类中决定实例化对象的类型。
优点：单一职责，开闭，里氏替换LSP，依赖抽象DIP，迪米特法则DP
缺点：每一次增加一个具体产品，都需要增加一个具体类和对应的具体工厂，代码复杂度就成倍增加，增加了系统具体类的依赖。

2）抽象工厂模式：创建一系列相关的对象，而无需指定具体类。简记超级工厂创建其它工厂。
优点：单一职责、开闭、LSP、DIP、DP
缺点：引入众多接口和类，代码复杂度增加
抽象工厂通常基于一组工厂方法

3）单例模式 【面试题】
保证一个类只有一个实例，并提供一个访问实例的全局节点。
单例 （Singleton） 类声明了一个名为 get­Instance获取实例的静态方法来返回其所属类的一个相同实例。
单例的构造函数必须对客户端 （Client） 代码隐藏。 调用获取实例方法必须是获取单例对象的唯一方式。
优点：解决了2个问题
缺点：违反单一职责原则，开闭原则。
Unity中的单例模式和不继承MonoBehaviord的普通单例模式。
应用例子：游戏中各种各样的管理器Manager
隐藏游戏体：obj.hideFlags = HideFlags.HideAndDontSave
[[Unity基础\] 单例类MonoSingleton 和普通单例Singleton-CSDN博客](https://blog.csdn.net/qq_21407523/article/details/104374457)

4）状态模式 面试题
是一种行为设计模式，在对象的内部发生状态改变时改变其行为
解决大量if else 或者switch 多状态的情形
代码结构
客户端：新建具体状态，并且调用具体行为
状态控制器：状态属性，转换状态方法，调用状态的具体行为
状态父类或接口：控制器属性，设置控制器方法（保存控制器），抽象行为
具体状态：继承状态，重写为具体行为
[C# 状态模式讲解和代码示例 (refactoringguru.cn)](https://refactoringguru.cn/design-patterns/state/csharp/example)
优点：单一、开闭、控制器和父类状态封装，只需要注重具体状态类行为修改。易于维护和扩展、减少因新增状态对原因脚本进行大量修改，每个状态只需要维护自己，多项目开发、易于维护
缺点：状态较少的情况下就小题大做
举个例子：场景状态，主场景状态，加载场景状态，战斗场景状态，3个场景的切换

5）观察者模式 【面试题】
是一种行为设计模式，允许你定义一种订阅通知机制
代码结构
发布者：当新事件发生后，向其他对象发送自己所订阅的事件，发送通知方法。
订阅者接口：声明了通知方法Update更新
具体订阅者：可以执行一些操作来响应发布者的消息。
客户端：分别创建发布者和订阅者对象，然后为订阅者注册发布者更新
优点：开闭，迪米特法则，建立对象之间联系，数据松耦合
缺点：通知顺序是随机的
中介者和观察者相似

6)中介者模式
是一种行为设计模式，减少对象之间混乱无序的依赖关系，对象之间通过中介者对象进行合作。现实世界：飞机塔台调度
代码结构
N个组件：各种包含业务逻辑的类
中介者接口：接口申明了与组件的交流方式，通知
具体中介者：封装了多种组件间的关系。
组件并不知道其它组件的情况，组件如果发生变化，通知中介者，然后判断并发送给相应的其它组件。接受者和发送者不知道谁来处理请求和谁发出的请求
优点：单一、开闭、减少个组件的依赖关系，复用各个组件
缺点：

## 请说出 4 种面向对象的设计原则，并分别简述它们的含义
0、单一职责原则
一个类实现一个功能

1、开闭原则OCP（Open Close Principle）
对扩展开放，对修改关闭。

2、里氏代换原则LSP（Liskov Substitution Principle）
任何基类可以出现的地方，子类一定可以出现，即子类一定可以替换其基类。

3、依赖倒转原则DIP（Dependence Inversion Principle）
针对接口编程，依赖于抽象而不依赖于具体。

4、接口隔离原则ISP（Interface Segregation Principle）
使用多个隔离的接口，比使用单个接口要好。
它还有另外一个意思是：降低类之间的耦合度。

5、迪米特法则，又称最少知道原则DP（Demeter Principle）
一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。

6、合成复用原则CRP（Composite Reuse Principle）
合成复用原则是指：尽量使用合成/聚合的方式，而不是使用继承。

## 设计一个状态机类型，状态值为int类型，要求：
拥有接口，获取当前状态，切换状态
外部可以监听状态切换事件，参数为切换前状态和切换后状态（使用delete和event）

## 如何处理unity中界面资源，界面逻辑以及功能模块三者之间的耦合关系

## 什么是MVC模式

# Shader
## Unity3D Shader分哪几种，有什么区别？

表面着色器的抽象层次比较高，它可以轻松地以简洁方式实现复杂着色。表面着色器可同时在前向渲染及延迟渲染模式下正常工作。

顶点片段着色器可以非常灵活地实现需要的效果，但是需要编写更多的代码，并且很难与Unity的渲染管线完美集成。

固定功能管线着色器可以作为前两种着色器的备用选择，当硬件无法运行那些酷炫Shader的时，还可以通过固定功能管线着色器来绘制出一些基本的内容。

## Vertex Shader是什么，怎么计算？

**顶点着色器** 是一段执行在GPU上的程序，用来取代fixed pipeline中的transformation和lighting，Vertex Shader主要操作顶点。

> Vertex Shader对输入顶点完成了从local space到homogeneous space（齐次空间）的变换过程，homogeneous space即projection space的下一个space。在这其间共有world transformation, view transformation和projection transformation及lighting几个过程。

## 分别解释顶点着色器和像素着色器是什么

顶点着⾊器是⼀段执⾏在GPU上的程序，⽤来取代 fixed pipeline中的transformation和lighting，Vertex Shader主要操作顶点。‘’

像素着色器实际上就是对每一个像素进行光栅化的处理期间，在GPU上运算的一段程序。

不同与顶点着色器，像素着色器不会以软件的形式来模拟像素着色器。

像素着色器实质上是取代了固定功能流水线中多重纹理的环节，而且赋予了我们访问单个像素以及访问每一个像素纹理坐标的能力



# 实现 某 系统 功能...

## 去掉敏感字的程序（手写程序）

字符串replace

## 用代码实现第三人称角色控制器？第一人称角色控制器

大致思路：
摄像机与角色的距离范围
摄像机旋转、平移
鼠标控制摄像机

## 红点系统的实现

思路：
红点系统基于MVC的思想，将分为三层：数据层，驱动层，显示层。

数据层中的数据结构，考虑到需要层级的联系，所以以结点为核心,每个结点会持有其父结点和子结点,有点像双向链表的前驱后继,但是它构成的不是链表而是树。
当一个结点状态发生变化,它会通知到其父结点,父节点会自行处理变化去通知它自己的父结点,有点递归的意思，如果是数量通知，子节点的消息会以此累计到自己的父节点中，以此类推，具体看需求。
整个系统数据层驱动层与展示层是剥离的,展示层需要显示什么结点的内容,以该结点的key去注册,数据层与显示层实现了观察者模式，即可收到每次该结点状态变化的通知，并实时更新界面。
[Unity之红点树系统多层级高效能_彩色墨水的博客-CSDN博客](https://blog.csdn.net/weixin_44186849/article/details/122471049)

[Unity手游实战：从0开始SLG——独立功能扩展（三）用树实现客户端红点系统 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/85978429)

## 写一个计时器工具，从整点开始，格式为00：00：00

分小时、分、秒

## 用鼠标实现在场景中拖动物体，用鼠标滚轮实现缩放(用一个 Cube 即可）

在场景中添加一个Plan，Camera，Directional Light，Cube。添加两个脚本一个挂在Camera上，另一个挂在Cube上。
1.鼠标滚轮实现缩放：将摄像机的镜头拉近或者拉远，调整摄像机的视角就可以实现2.鼠标实现在场景中拖动物体：解决思路就是将世界坐标转换成屏幕坐标，然后计算物体与鼠标之间移动量，循环鼠标被按下操作，得到鼠标的当前位置，加上计算好的移动量，将新的坐标赋值给物理就行了。 具体代码实现：http://www.cnblogs.com/hewencong/p/4299722.html

##　<愤怒的小鸟>给予初速度以后,怎么让小鸟受到重力和空气阻力的影响而绘制抛物线轨迹,说出具体的计算方法

Vector3 v 代表初速度 v’代表现在的速度， 假设小鸟是沿的 z 轴也就是transform.forward 方向，运动的质量为 m，那么 v‘=v-new Vector3(0,mgt,ft)，transform.Translate(v’)做的就是抛物线运动（g 为重力加速度不要用现实中的需要自己调试，f 为阻力也要自己调试
设置，t 为时间）

## MMO项目

### 背包系统是如何实现的？

### 道具系统的道具是如何实现的？

###  资源管理是如何实现的？












# TCP/IP协议栈各个层次及分别的功能？

网络接口层：这是协议栈的最低层，对应OSI的物理层和数据链路层，主要完成数据帧的实际发送和接收。
网络层：处理分组在网络中的活动，例如路由选择和转发等，这一层主要包括IP协议、ARP、ICMP协议等。
传输层：主要功能是提供应用程序之间的通信，这一层主要是TCP/UDP协议。
应用层：用来处理特定的应用，针对不同的应用提供了不同的协议，例如进行文件传输时用到的FTP协议，发送email用到的SMTP等。

# 使用原生 GUI 创建一个可以拖动的窗口命令是什么？
GUI.DragWindow

# 写出WWW的几个方法
WWW.LoadFromCacheOrDownload：可被用于将Assets Bundles自动缓存到本地磁盘
WWW.Dispose ：释放现有的 WWW 对象。
WWW.isDone：是否完成下载？（只读）
WWW.progress：下载进度（只读）。



1 、同步的细节处理
2 、BUFF影响，数值回滚
3、 复杂动画转换过渡，融合底层逻辑
4 、曲线运动碰撞检测不到
5、 帧同步，如何侦测不同步，为啥就不同步了
6、 发射子弹的状态同步
7 、状态同步的缺点优点
8、组件系统，组件设计游戏的方式，以游戏驱动的设计模式，ECS架构
9 、技能系统架构

























