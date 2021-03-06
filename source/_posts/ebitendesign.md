---
title: Ebiten设计
date: 2022-03-20 21:40:31
tags: ebiten
---

# Game 
游戏全局结构体,直接兼容`Ebiten.Game`.

## Global Res
全局资源,建议用来储存字体,常用音频等.

|名称|类型|解释|
:--------------:|:--------------:|:--------------:|
|图片|`ebiten.image`|图片资源|
|文本|`String`|文本资源|
|字体|`font`|字体资源|
|扩展|自定|扩展接口|

## Scene
场景

### Object
对象

#### Res
对象资源

#### Type
对象类型

#### UID
全局唯一定位ID(ID选择器)

#### Class 
定位类型(class选择器)

### Scene Res
场景资源,建议放音频,复用图片

## GameConfig
游戏全局配置


---
以下是详细介绍

# Res
资源类型,使用`interface`  
接受一切内容,但如果没有内置和扩展所适配的类型将会抛出`Warning`错误.


---

# 一些设计规范

1. 游戏发布版本原则上不要抛出`panic`导致游戏跳出.  
因为,在游戏运行时经常会出现不会影响整体游戏的错误,一旦跳出,玩家很有可能会`砸电脑.gif`  
2. 在使用结构体操作时,建议全部使用指针.否则会出现很难调试明白的错误.  
3. 尽可能降低耦合度.
4. 尽可能不要将非绘制操作放进`Draw()`函数.
5. 注意关注`Ebiten API`里线程安全或非安全的提示.
6. 游戏逻辑尽可能单独存`package`,一层层调用用,最好是在`Update()`里只有一个函数掉用(和`Draw()`一个道理).
6. 能归给`Scene`的资源就不要变成全局资源.
7. 能转成`Ebiten`原生类型的资源(如图片`ebiten.image`)就不要用go包里的类型(如`image.image`). 
8. 数学家告诉我们: 写`Ebiten`要先学几何.
9. <del>星一大大是霓虹人,英语很好.</del>
10. <del>我是华夏人,英语一般.</del>
11. `Object`的设计原理参照`Unity`.
12. `MVC`的设计模式可以用于`Ebiten`.  
`MVC` 模式代表 `Model-View-Controller`（模型-视图-控制器）模式。这种模式用于应用程序的分层开发。  
- `Model`（模型）- 模型代表一个存取数据的对象。它也可以带有逻辑，在数据变化时更新控制器。
- `View`（视图）- 视图代表模型包含的数据的可视化。
- `Controller`（控制器）- 控制器作用于模型和视图上。它控制数据流向模型对象，并在数据变化时更新视图。它使视图与模型分离开。

