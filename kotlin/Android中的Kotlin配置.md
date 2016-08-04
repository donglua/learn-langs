## 安装Kotlin插件

直接在偏好设置里的 plugins 页面中搜索 Kotlin、安装

![](http://ww2.sinaimg.cn/mw690/5e9a81dbgw1f6hq2ub1d0j213w0mmn05.jpg)

安装完插件后重启 Android Studio，我们可以看到新建里多了 Kotlin 相关的选项。
## 创建 Kotlin Android 项目

* 先创建一个普通 Android 项目 KotlinDemo。
* 然后如下图，选择 Configure Kotlin in Project，让插件为我们配置好 Kotlin

![](http://ww3.sinaimg.cn/mw690/5e9a81dbgw1f6hqrnuayaj212c0lmjxn.jpg)


<img src="http://ww3.sinaimg.cn/mw690/5e9a81dbgw1f6hr41t1v7j20le09qwf7.jpg" width="320px" />

我们选择最新版本点击 OK。
之后，我们的 gradle 配置文件就会变成这样：

KotlinDemo/build.gradle：

```Gradle
buildscript {
  ext.kotlin_version = '1.0.3'
  repositories {
    jcenter()
  }
  dependencies {
    classpath 'com.android.tools.build:gradle:2.1.2'
    classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
  }
}
...
```

KotlinDemo/app/build.gradle：

```Gradle
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'

android {
  ...
  sourceSets {
    main.java.srcDirs += 'src/main/kotlin'
  }
}

dependencies {
  ...
  compile "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
}
repositories {
  mavenCentral()
}
```


## Kotlin 代码转换

![](http://ww3.sinaimg.cn/large/5e9a81dbgw1f6hslfqjyog201e018a9x.gif) 好了，现在我们可以来写 Kotlin 代码了

但是，怎么写... 没关系，Kotlin 的插件提供了把 Java 转换为 Kotlin 代码的功能，就算我们现在还不知道 Kotlin 的语法，也能通过转换现有的 Java 代码来学习。

![](http://ww3.sinaimg.cn/mw690/5e9a81dbgw1f6hsyp1up4j20ly0t4gqb.jpg) 

我们来看一下转换前后的代码：

转换前的 ```MainActivity.java```

```Java
public class MainActivity extends AppCompatActivity {

  @Override protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
    setSupportActionBar(toolbar);

    FloatingActionButton fab = (FloatingActionButton) findViewById(R.id.fab);
    fab.setOnClickListener(new View.OnClickListener() {
      @Override public void onClick(View view) {
        Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
            .setAction("Action", null)
            .show();
      }
    });
  }

  @Override public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
  }

  @Override public boolean onOptionsItemSelected(MenuItem item) {
    int id = item.getItemId();
    if (id == R.id.action_settings) {
      return true;
    }
    return super.onOptionsItemSelected(item);
  }
}
```

转换后变成```MainActivity.kt```

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        val toolbar = findViewById(R.id.toolbar) as Toolbar
        setSupportActionBar(toolbar)

        val fab = findViewById(R.id.fab) as FloatingActionButton
        fab.setOnClickListener { view ->
            Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                    .setAction("Action", null)
                    .show()
        }
    }

    override fun onCreateOptionsMenu(menu: Menu): Boolean {
        menuInflater.inflate(R.menu.menu_main, menu)
        return true
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        val id = item.itemId
        if (id == R.id.action_settings) {
            return true
        }
        return super.onOptionsItemSelected(item)
    }
}

```

是不是很神奇，这样对我们初学者很方便，可以直接跟 Java 进行对比学习。

