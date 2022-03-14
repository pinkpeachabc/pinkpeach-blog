---
title: Android数据储存
date: 2019-12-31 22:40:26
tags:
- Android
categories:
- Android学习
---

大部分应用程序都会涉及数据储存方式，Android程序也不例外。Android中的数据储存方式有五种。分别为文件储存、SharedPreferences、SQLite数据库、ContentProvider以及网络储存。根据程序适配的Android SDK版本不同，申请权限分为两种，分别为静态申请和动态申请权限，这次主要讲怎么申请和遇到过的坑。

<!--more-->

## 文件储存遇到的坑

>由于Android版本的更新，和现在的手机几乎不再使用SD卡。导致初学者在用这个方法的时候就会出现问题。

在文件存储中分为内部储存和外部储存，出坑的主要是外部储存。在eclipse中可以正常写入可到了Android stuido中却写入不进去。

首先，若使用外部存储需要先设置外部存储的**读写权限**，若是不添加将无法写入。

## 静态申请权限

```java
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

>此方式只适应于Android SDK6.0以下的版本，当大于这个版本的时候就需要添加动态申请权限了。

## 动态申请权限

这时候需要新建PermisionUtils类内容如下，最后在需要的地方调用这个类。

```java
public static class PermisionUtils {

        // Storage Permissions
        private static final int REQUEST_EXTERNAL_STORAGE = 1;
        private static String[] PERMISSIONS_STORAGE = {
                Manifest.permission.READ_EXTERNAL_STORAGE,
                Manifest.permission.WRITE_EXTERNAL_STORAGE};


        public static void verifyStoragePermissions(Activity activity) {
            // Check if we have write permission
            int permission = ActivityCompat.checkSelfPermission(activity,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE);

            if (permission != PackageManager.PERMISSION_GRANTED) {
                // We don't have permission so prompt the user
                ActivityCompat.requestPermissions(activity, PERMISSIONS_STORAGE,
                        REQUEST_EXTERNAL_STORAGE);
            }
        }
    }
```

```java
PermisionUtils.verifyStoragePermissions(this);
```

> 这个时候在这个时候在点击写入便会出现以下界面：

![屏幕快照 2019-12-31 下午11.14.51](https://tva1.sinaimg.cn/large/006tNbRwly1gagbsv7y8dj30dy0o0ju8.jpg)

> 这时候我本以为可以直接读出来我写入的内容了，但我还是太年轻了。我还是读取不出来。这个点困扰我很长时间知道我发现了手机里有一个应用访问授权。**一定要把它打开！！！**

![屏幕快照 2019-12-31 下午11.16.01](https://tva1.sinaimg.cn/large/006tNbRwly1gagc0hdlymj30dy0o00ur.jpg)

> 最后完美读出

![屏幕快照 2019-12-31 下午11.16.01](https://tva1.sinaimg.cn/large/006tNbRwly1gagc1el2e0j30dy0o0q5x.jpg)