# flutter_dynamic
flutter_dynamic 是一个能动态创建Flutter应用的引擎。flutter_dynamic不但支持写UI，还支持写代码逻辑。    
The flutter_dynamic is an engine that create flutter application dynamically. flutter_dynamic not only supports writing UI, but also writing code logic.

* [Github地址](https://github.com/Yingzi-Technology/flutter_dynamic)

## Best practice
> 动态创建类似有UI和交互的页面。  
Dynamically create similar UI and interactive pages.


![yzdynamic.gif](https://upload-images.jianshu.io/upload_images/3868052-24e08253efeff413.gif?imageMogr2/auto-orient/strip/w/320)
<img src="https://upload-images.jianshu.io/upload_images/3868052-24e08253efeff413.gif?imageMogr2/auto-orient/strip" width="320px"/>

## 目录 Table of contents
* [General-info概况](#General-info)
* [Install 安装](#Install)
* [Get-started 使用](#Get-started)
* [Grammar 语法](#Grammar)
* [Contact 联系](#Contact)

## General-info

> 有时候在产品开发的过程中需要远程动态地创建表单或更新某个表单应用，但Flutter框架不像javascript动态语言可以远程下发并动态执行脚本，也不像Android或iOS平台的java或objective c语言支持动态热更新或动态语言特性等，甚至在Flutter中限制了Dart语言的反射特性，所以基于Flutter来做动态页面就显得很有局限性。开发flutter_dynamic引擎一是为了满足产品需要远程动态创建表单应用的需求，二是借此机会探索Flutter更广泛的动态特性实现方案；目前这个引擎还处在不断完善阶段，难免会有缺陷。  
In the process of product development, pages need to be dynamically created remotely. But the Flutter framework is not like the javascript dynamic language that can remotely issue and dynamically execute scripts, nor is it like the Android or iOS platform's java or objective c language that supports dynamic hot updates or dynamic language features, and even limits the reflection of the Dart language in Flutter Features, so dynamic pages based on Flutter are very limited. The flutter_dynamic engine was developed to meet the needs of products that need to dynamically create form applications remotely, and the second is to take this opportunity to explore the implementation of Flutter's broader dynamic characteristics; currently this engine is still in the stage of continuous improvement, and it is inevitable that there will be defects.  

> 本引擎主要包括以下几个方面：  
--提供高度类似Flutter系统的Widget类型，以满足构造UI所需的Widget库；并提供自定义Widget扩展引擎，满足开发者自定义基于本引擎解释的Widget类型；  
--提供variable变量解释引擎，提供类似Dart基本类型语法，满足类似变量定义、类属性定义等；  
--提供action方法解释引擎，提供类似Dart方法语法，满足类似方法调用；  
--提供code代码解释引擎，提供类似Dart关系运算、逻辑运算、控制流程等语法，满足写基本的代码逻辑；  
--提供event事件解释引擎，提供类似Flutter的事件处理；  
This engine mainly includes the following aspects:  
--Provide a Widget type that is highly similar to the Flutter system to meet the Widget library required to construct a UI; and provide a custom Widget extension engine to meet the needs of developers to customize the Widget type based on this engine's interpretation;  
--Provide variable variable interpretation engine, provide basic type syntax similar to Dart, satisfy similar variable definition, class attribute definition, etc.;  
--Provide action method interpretation engine, provide similar Dart method syntax, satisfy similar method calls;  
--Provide code code interpretation engine, provide similar Dart relational operations, logical operations, control flow and other grammars to satisfy basic code logic;  
--Provide event event interpretation engine, provide event processing similar to Flutter;  

## Install
#### step 1. Depend on it
Add this to your package's pubspec.yaml file:
```
dependencies:
  yz_flutter_dynamic:
    git:
      url: https://github.com/fisherjoe/flutter_dynamic.git
      ref: master
```
Or 
Download or clone the code  to the local:
```
dependencies:
  yz_flutter_dynamic:
    path: your/code/path
```
Or
Do as example of code.

#### step 2. Use it

Use as common flutter plugin in  flutter project.

#### step 3. Import it
Now in your Flutter code, you can use:
```dart
import 'package:yz_flutter_dynamic/main.dart';
```

## Get-started
> flutter_dynamic是完全开源的，在代码中的example里也已经具有完整的示例，以下针对核心的流程说明：
flutter_dynamic is completely open source, and there are complete examples in the example in the code. The following is a description of the core process:

#### Hello world

```dart
import 'package:flutter/material.dart';
import 'package:yz_flutter_dynamic/main.dart';

class Helloworld extends StatefulWidget {
  @override
  _HelloworldState createState() => _HelloworldState();
}

class _HelloworldState extends State<Helloworld> {
  @override
  Widget build(BuildContext context) {
    return YZDynamic.buildWidget(
      context, 
      hwDsl, 
    );
  }
}

Map hwDsl =
{
  "xKey": "",
  "widgetName": "Scaffold",
  "props": {
    "appBar": {
      "xKey": "",
      "widgetName": "AppBar",
      "props": {
        "title": {
          "widgetName": "Text",
          "props": {"data": "Navigator"}
        }
      }
    },
    "body": {
      "xKey": "",
      "widgetName": "SafeArea",
      "props": {
        "child": {
          "xKey": "_Text",
          "widgetName": "Text",
          "props": {
            "data": "Hello world"
          }
        }
      }
    }
  }      
};
```
### How to create your dynamic widget
>我们认为Flutter的任何页面或组件都是StatefulWidget，所以当我们无论创建一个新页面或组件时我们都把它当作一个StatefulWidget来看待。页面和StatefulWidget是一样。
We think that any page or component of Flutter is a StatefulWidget, so when we create a new page or component, we treat it as a StatefulWidget. The page is the same as StatefulWidget.

***step1: How to create widget UI***

invoke
```dart
YZDynamic.buildPage(context, json, preConfig: preConfig);
```

json
```dart
{
  "xKey": "globalKeyOfWidget", 
  "widgetName": "Container",      
  "props": { 
  "padding": "[10, 10, 0, 0]",
  "height": "44",
  "child": {
    "widgetName": "Text", 
    "props": {
      "data": "Data of Text widget",
      "color": "0xfff1f1f1"
    }    
  }
  },
  "xEvents": [
  {
    "eventType": "onClick",
    "code": '''
      [code...]      
    '''
  },
  "xVar": {
  
  }
  ]           
}
```
> 上面的代码较完整地呈现了一个构造一个widget的json数据。其中rootWidget的值描述了该widget的根结点Container，返回StatefulWidget包裹的Container。下面将主要对各属性一一说明：  
The above code completely presents a json data for constructing a widget. The value of rootWidget describes the root node Container of the widget, and returns the Container wrapped by the StatefulWidget. The following will mainly explain each attribute one by one:  

- `xKey`：The globalkey of widget to find the widget.

- `widgetName`: The type of widget.

- `xEvents`:  The event of the widget support "onClick" type now. The value support grammar as [Grammar 语法](#Grammar)

- `xVar`: Define the variable of widget.

- `props`: The properties of the widget which property is the same as system of widget's property. There are two types of props value such as : 
	- **string**:  The type of  property value  like "color" "width" should use string type {"widget":"100", "color": "#ff000000"}. Specially the type of EdgeInsets will be "[10, 20, 30, 40]" for "[left, top, right, bottom]". The enum of type will be like "multiline" for TextInputType.multiline
	- **map**: The type of property value like "Size" will be {"color":"", "width":""}.

***step2: How to create page***
> 创建page UI和创建widget UI是一样的，同时它们的json数据也是通用的，widget是page的简单化版。
Creating page UI is the same as creating widget UI. At the same time, their json data is also common. Widget is a simplified version of page.

invoke build page
```dart
YZDynamic.buildPage(context, json, preConfig: preConfig);
```

invoke present page
```dart
YZDynamic.handle(context, json, preConfig: preConfig)
```

json
```dart
{
    "page": {
        "key": "",
        "presentMode": "",
        "state": {
            "initState": [ 
            ], 
            "build": [ 
            ],
            "dispose": [ 
            ]
        },
        "xVar":{},
        "rootWidget": {}
    }
}
```

> 上面的代码较完整地呈现了一个构造一个page的json数据。  page属性里有些和widget不致，下面一一说明：
The above code completely presents a json data that constructs a page. Some of the page attributes are inconsistent with widgets, as explained below:

- `key`：The globalkey of page.

- `presentMode`: The present mode of page. The  value is "dialog / navpage".Use for YZDynamic.handle invocation only.

- `state`: The lifecycle of page which is as good as the system StatefulWidget.

- `xVar`: Define the variable of widget.

- `rootWidget`: The root widget of page. It is similay to the return widget of StatefulWidget's build method.

***step3: How to define variable***

***step4: How to implement event***

***step5: How to write code***


##  Grammar
在源代码的example里有写动态页面的伪代码语法，如图所示：   
In the example of the source code, there is pseudo code syntax for writing dynamic pages, as shown in the figure:  

![Simulator Screen Shot - iPhone 12 - 2020-12-17 at 09.22.41.png](https://upload-images.jianshu.io/upload_images/3868052-917c8c2720d84fe9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/360)


## More Document ... ...
> Feel apologetic that we update the document slowly for the work time reason.

## Contact
Created by [@153768151@qq.com](https://github.com/fisherjoe) - feel free to contact me
