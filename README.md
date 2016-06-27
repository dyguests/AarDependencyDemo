#AarDependencyDemo

AarDependencyDemo,aar文件依赖

通过把module依赖改成aar依赖，可以有效减少编译时间。

#HandsOn

##1.初始化项目

项目中有两个Module，一个app module，一个lib module。

app < lib

app/.../MainActivity.java

```
 Toast.makeText(this, LibUtil.test(this), Toast.LENGTH_LONG).show();
```

现在要打module依赖改成aar依赖.

##2.生成aar文件

调用 gradle projects(在窗口的右边)>:lib>Tasks>build>assembleRelease。

（初次调用可能会下载一堆文件)

会在 Project目录>lib>build>outputs>aar>下生成lib-release.aar文件。

##3.添加aar依赖



