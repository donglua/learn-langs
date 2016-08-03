# AccountManager的使用

> 参考
[开发你自己的Android 授权管理器](http://www.devtf.cn/?p=1121)

## 1. 为什么要使用AccountManager
* 标准的授权流程，简化了开发授权的过程；
* 为你处理拒绝访问的情况；
* 可以处理同一账户的多种 token 类型（如只读，完全控制等）;
* 可以在多个应用间共享 token, 支持 SyncAdapter 等 Background Processes;
* token 等关键内容和一些附加账户信息会直接存放在系统的账户数据库，交由系统管理；
* 既可以在应用内管理，也可以在系统 设置 -> 账户 中管理。

## 2. 使用

* 添加权限

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
<uses-permission android:name="android.permission.MANAGE_ACCOUNTS" />
```