# cardviewdemo

**在开发过程中我们的view或布局要使用圆角和阴影的时候**
1. 我们可以使用shape自定义圆角和阴影
2. 系统自带的CardView来封装一层，之后设置圆角和阴影

**但是以上2中方式都有个缺点：**

1. 自定义shape的时候，在对ViewGroup设置背景时，如果里面的子view有背景颜色同时比较靠近边角的时候，子view会伸出圆角范围且会把底层的ViewGroup设置圆角覆盖掉，或者漏出一个角。这样就达不到我们想要的效果了。

2. 使用系统的CardView来设置的话，由于CardView是继承FrameLayout的。如果我们的根布局使用RelativeLayout或者LinearLayout的时候，就需要在外面嵌套一层CardView，这样就会导致我们的界面的view层级增加，影响绘制性能。

写到这里，我们就会想CardView既然是继承自FrameLayout，我们是不是可以将其改成继承RelativeLayout或者LinearLayout，这样我们不就可以既不增加view嵌套层级，也能解决问题了。

按着这个思路，我就实践了一下，把在源码里面吧CardView的代码复制出来，直接改成继承RelativeLayout或者LinearLayout，不就可以了？但是不行。由于其使用的一些其他辅助类我们访问不了。

**好吧，直接出大招**，这次把`CardView`和其`相关的所有类`都复制出来，注意`资源文件`也得复制出来，然后复制一个`CardView`类重命名LinearCardView extends LinearLayout，这下真的就可以了，，，RelativeLayout也可以同样操作，效果图如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201023113312719.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM2MjYyMTU=,size_16,color_FFFFFF,t_70#pic_center =300x)


**提示**

	由于我是直接把CardView源码复制出来了，所以项目就不用在依赖系统的`cardview`库文件了

下面直接提供我修改后的代码分享给大家 [项目下载地址](https://github.com/wangjiandett/cardviewdemo)

项目源码是在androidx中复制出来的，然后做的修改

```
'androidx.cardview:cardview:1.0.0'
```

如果没有使用`androidx`使用`support`库中的代码需要将`cardviews`库中的每个类中导入的包名改成`support`库中对应的就行了，如：复制如下包中的类

```
'com.android.support:cardview-v7:23.2.0'
```

**2020.11.20 修改**

在代码都复制进来后，功能时可以用了，但是在xml布局的时候编写属性无法自动提示要输入的属性
再此修改了`card_views_values.xml`中的属性配置，分别为`RelativeCardView`,`FrameCardView`,`LinearCardView`都自定义了一份属性声明。
方便在android studio的xml中编写属性时自动提示





