---
title: Android Development - Activity
description: 
date: 2024 13:50:00+0000
categories:
    - Android
---

##  Activity 簡介

An activity is a single, focused thing that the user can do. Almost all activities interact with the user, so the Activity class takes care of creating a window for you in which you can place your UI with setContentView(View). 

`setContentView(R.layout.your_layout)`

[Activity 文件](https://developer.android.com/reference/android/app/Activity)

## 用途

在Android開發中，Activity是一個非常核心的概念。一個Activity代表著一個單一的屏幕（UI），用戶可以在這個屏幕上與應用程序交互。每個Activity都提供了一個窗口來繪製其用戶界面。整個應用可以由多個Activity組成，每個Activity都是獨立的。

以下是一些Activity的主要特點和功能：

* 用戶界面的容器：Activity通常包含各種UI元素，如按鈕、文本框和圖片視圖等。

* 生命周期管理：Android系統會根據應用的需要和系統資源的狀態，管理Activity的生命週期。Activity有多個生命週期回調方法，如onCreate(), onStart(), onPause(), onResume(), 和onDestroy()。

* 交互和導航：Activity之間可以透過Intent進行交互。通過Intent，一個Activity可以啟動另一個Activity，並傳遞數據。

* 狀態保存和恢復：當Activity因為系統配置更改（如旋轉屏幕）或者內存不足被系統銷毀時，它可以保存和恢復其狀態。

* 資源管理：Activity可以加載不同的布局和資源，以適應不同的裝置和屏幕尺寸。

* 權限管理：某些Activity可能需要請求特定權限，以訪問系統功能或資料（如攝像頭或聯繫人）。

一個典型的Android應用通常至少包含一個Activity，即主Activity，它是用戶與應用互動的入口點。开发者可以根据应用的需求设计更复杂的Activity架构和导航流程。

當我們新建avtivity時
```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
```