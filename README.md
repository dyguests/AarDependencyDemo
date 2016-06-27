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

调用 `gradle projects(在窗口的右边)>:lib>Tasks>build>assembleRelease。`

（初次调用可能会下载一堆文件)

会在 `Project目录>lib>build>outputs>aar>`下生成`lib-release.aar`文件。

##3.添加aar依赖

将之前生成的`lib-release.aar`文件，放到`project目录>app>libs`下。(也可以放到别的目录下，统一就行）

修改 项目的`build.gradle`文件

```
allprojects {
    repositories {
        jcenter()
        flatDir {
            dirs project(':app').file('libs')//添加这一块(别的module的aar依赖，就添加对应的代码就行)
        }
    }
}
```

修改 app module的`build.gradle`文件

```
dependencies {
//    compile fileTree(dir: 'libs', include: ['*.jar'])//因为里面的aar文件可能不需要
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:24.0.0'
//    compile project(path: ':lib')//把module依赖，换成aar依赖
    compile name: 'lib-release', ext: 'aar'//把module依赖，换成aar依赖
}
```

完成。

