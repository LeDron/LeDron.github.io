---
layout: post
title: "How to use a RecyclerView with loading URL image"
excerpt: "withiut OOM, load URL image in RecyclerView"
tag: [ListView, Android, RecyclerView]
date: 2017-06-01
comments: true
---

# Why RecyclerView?

Android has a limit of heap memory. So when we insert many videos or images in youer app, I'm sure "Out of Memory(OOM)" happens. RecyclerView is similar to ListView, but it is more smart about heap memory.

## Problems
1. if you use a ListView loading Bitmap image items in real time, you have out of memory errors.

---
## Code
Before you write this code, you should add this library in **build.gradle**
~~~ gradle
dependencies{
compile 'com.android.support:recyclerview-v7:25.2.0'
}
~~~

**activity.xml**
~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.nb201612072.myapplication.MainActivity">

<android.support.v7.widget.RecyclerView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/recyclerView">
  </android.support.v7.widget.RecyclerView>

</LinearLayout>

~~~
**listitem.xml**
~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/img"/>
</LinearLayout>
~~~

**MainActivity.java**
</br>
I wrote down urls, but I recommand you programmatically get your urls.
~~~ java

~~~

**Adapter.java**
~~~ java

~~~
