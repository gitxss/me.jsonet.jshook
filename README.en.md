<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)

hook artifact in android support java layer and native layer

[中文的README](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.md)
</div>

## About

xposed is a module framework to change the behavior of system and applications without touching any apk. This means that modules can work on different versions or even roms without any changes.

Jshook injects rhino/frida into the app. The development of xposed module requires a certain java grammar foundation, and the technical threshold is high. However, the rhino/frida injected by jshook only needs a short js to quickly implement hooks on mobile phones, and hooks support java layer and native layer.

## Compatibility

1. Xposed api 82
2. Android 5 - 13

## How to use

### How to enable scripts

Before enabling the script, please confirm that the selected application has the hook service option enabled. If the lsposed non-global scope is activated, in addition to checking the system, you need to check the application that the corresponding script takes effect. Every time you change the script content, you need to restart the hooked one. app.

### How to choose an hook framework

If you are familiar with the hook method of xposed, rhino is recommended, and js is used to call the api of the xposed framework, and the compatibility is high; while frida belongs to another hook framework, you need to have a certain understanding of frida, it is difficult to get started, and some parts are not supported model and app.

## Script Description

### Universal

Log Printing：

```js
common.log('...');
console.log('...');
```

Message Tips：

```js
common.toast('...');
```

pop-up prompt：

```js
common.dialog('...');
```

Get Context：

```js
common.getcontext();
```

mod menu：

<table>
<thead>
<tr>
<td colspan="4" align="center">modmenu</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>title</td>
<td>String</td>
<td>Title</td>
<td align="center">N</td>
</tr>
<tr>
<td>item</td>
<td>Array</td>
<td>Menu Item</td>
<td align="center">Y</td>
</tr>
<tr>
<td>title</td>
<td>String</td>
<td>Title</td>
<td align="center">N</td>
</tr>
<tr>
<td>change</td>
<td>Function</td>
<td>callback</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.modmenu('test mod', [
    {
        'id': '1',
        'type': 'category',
        'title': 'category title'
    },
    {
        'id': '2',
        'type': 'switch',
        'title': 'switch1 title',
        'enable': true
    },
    {
        'id': '3',
        'type': 'switch',
        'title': 'switch2 title'
    },
    {
        'id': '4',
        'type': 'webview',
        'data': '<font color="red"><b>text</b></font>',
        //or
        //'url': 'http://xxxxx.com'
    },
    {
        'id': '5',
        'type': 'button',
        'title': 'button title'
    },
    {
        'id': '6',
        'type': 'input',
        'title': 'input title',
        'val': 'default value'
    },
    {
        'type': 'collapse',
        'title': 'collapse title',
        'item': [
            {
                'id': '7',
                'type': 'switch',
                'title': 'switch title'
            }
        ],
        'enable': true
    },
    {
        'id': '8',
        'type': 'slider',
        'title': 'slider title',
        'val': 88,
        'min': 1,
        'max': 100
    },
    {
        'id': '9',
        'type': 'checkbox',
        'title': 'checkbox title',
        'enable': true
    },
    {
        'type': 'checkboxs',
        'item': [
            {
                'id': '10',
                'type': 'checkbox',
                'title': '1 title'
            },
            {
                'id': '11',
                'type': 'checkbox',
                'title': '2 title'
            },
            {
                'id': '12',
                'type': 'checkbox',
                'title': '33333333 title'
            }
        ]
    },
    {
        'id': '13',
        'type': 'radio',
        'title': 'radio title',
        'item': ['test', 'test2', 'test3']
    }
], function (data) {
    common.toast(JSON.stringify(data));
});
```

Example with tabs：

```js
common.modmenu('test mod', [
    {
        'type': 'tab',
        'title': 'tab1 title',
        'item': [
            {
                'id': '1',
                'type': 'switch',
                'title': 'switch1 title'
            }
        ],
        'enable': true
    },
    {
        'type': 'tab',
        'title': 'tab2 title',
        'item': [
            {
                'id': '2',
                'type': 'switch',
                'title': 'switch2 title'
            }
        ]
    }
], function (data) {
    common.toast(JSON.stringify(data));
});
```

Note: To use the mod menu, you need to keep jshook running and authorize the floating window permission. Closing jshook will cause the menu to close, which will not affect the hook service.

### rhino

Get LoadPackageParam

<table>
<thead>
<tr>
<td colspan="4" align="center">getlpparam</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td colspan="4" align="center">None</td>
</tr>
</tbody>
</table>

Example：

```js
common.getlpparam();
```

Get class instances

<table>
<thead>
<tr>
<td colspan="4" align="center">findClass</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>classLoader</td>
<td>ClassLoader</td>
<td>Class Loader</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.findClass('com.test.test',classLoader);
```

hook constructor

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllConstructors</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class instance or class name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookAllConstructors('com.test.test', function (param) {
    //Before the execution of the constructor
    //Print the first argument received by the constructor
    common.log(param.args[0]);
    //Modify the value of this parameter
    param.args[0] = 'fuck';
}, function (param) {
    //After the execution of the constructor
    //...
});
```

hook constructor with specified parameters

<table>
<thead>
<tr>
<td colspan="4" align="center">hookConstructor</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class instance or class name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Type</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution of the constructor</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace the constructor execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookConstructor('com.test.test', ['java.lang.String', 'int'], function (param) {
    //...
}, function (param) {
    //...
});
```

hook class method

<table>
<thead>
<tr>
<td colspan="4" align="center">hookAllMethods</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class instance or class name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookAllMethods('com.test.test', 'methodname', function (param) {
    //...
}, function (param) {
    //...
}, function (param) {
    //The call to the original method returns
    return common.thisMethod(param);
});
```

hook the specified class method

<table>
<thead>
<tr>
<td colspan="4" align="center">hookByMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>method</td>
<td>Method</td>
<td>Method Object</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookByMethod(method, function (param) {
    //...
    //Modify return value
    param.setResult('fuck');
}, function (param) {
    //...
    //Get the return value of the class method and print it
    common.log(param.getResult());
});
```

hook the class method with the specified parameters

<table>
<thead>
<tr>
<td colspan="4" align="center">hookMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>String</td>
<td>Class Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Type</td>
<td align="center">Y</td>
</tr>
<tr>
<td>beforeHookedMethod</td>
<td>Function</td>
<td>Before the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>afterHookedMethod</td>
<td>Function</td>
<td>After the execution</td>
<td align="center">N</td>
</tr>
<tr>
<td>replaceHookedMethod</td>
<td>Function</td>
<td>Replace execution process</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.hookMethod('com.test.test', 'methodname', ['java.lang.String', 'int'], function (param) {
    //...
    //Modify return value
    param.setResult('fuck');
}, function (param) {
    //...
    //Get the return value of the class method and print it
    common.log(param.getResult());
});
```

Modifying static variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">setStaticObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>Variable Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.setStaticObjectField('com.test.test', 'Variable Name', 'Variable Value');
```

Modifying dynamic variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">setObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>fieldValue</td>
<td>Object</td>
<td>Variable Value</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.setObjectField('com.test.test', 'Variable Name', 'Variable Value');
//or
//param.thisObject Get in the hook callback method
common.setObjectField(param.thisObject, 'Variable Name', 'Variable Value');
```

Get static variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">getStaticObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class instance or class name</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.getStaticObjectField('com.test.test', 'Variable Name');
```

Get dynamic variable values

<table>
<thead>
<tr>
<td colspan="4" align="center">getObjectField</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>fieldName</td>
<td>String</td>
<td>Variable Name</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.getObjectField('com.test.test', 'Variable Name');
```

Active invocation of dynamic methods

<table>
<thead>
<tr>
<td colspan="4" align="center">callMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class name or current instance</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>Method name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Value</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.callMethod('com.test.test', 'methodname', ['a', 1]);
```

Active invocation of static methods

<table>
<thead>
<tr>
<td colspan="4" align="center">callStaticMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>className</td>
<td>Object</td>
<td>Class instance or class name</td>
<td align="center">Y</td>
</tr>
<tr>
<tr>
<td>methodMame</td>
<td>String</td>
<td>Method name</td>
<td align="center">Y</td>
</tr>
<tr>
<td>paramTypes</td>
<td>Object[]</td>
<td>Parameter Value</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.callStaticMethod('com.test.test', 'methodname', ['a', 1]);
```

Calling the original method in `replaceHookedMethod`

<table>
<thead>
<tr>
<td colspan="4" align="center">thisMethod</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>param</td>
<td>Object</td>
<td>Parameters</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
//param is retrieved in the replaceHookedMethod
common.thisMethod(param);
```

[View more](https://p-bakker.github.io/rhino/tutorials/scripting_java/)

### frida

[View more](https://frida.re/docs/javascript-api/)

#### fridamod

curl

<table>
<thead>
<tr>
<td colspan="4" align="center">curl</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>url</td>
<td>String</td>
<td>url address</td>
<td align="center">Y</td>
</tr>
<tr>
<td>method</td>
<td>String</td>
<td>request type</td>
<td align="center">N</td>
</tr>
<tr>
<td>header</td>
<td>Array</td>
<td>header info</td>
<td align="center">N</td>
</tr>
<tr>
<td>data</td>
<td>Object</td>
<td>submit data</td>
<td align="center">N</td>
</tr>
<tr>
<td>callback</td>
<td>Function</td>
<td>callback</td>
<td align="center">N</td>
</tr>
</tbody>
</table>

Example：

```js
common.curl('https://xxxxx.com', 'post', ['token: sssss'], {data: '111'}, function (data) {
    common.log(data);
});
```

shell

<table>
<thead>
<tr>
<td colspan="4" align="center">shell</td>
</tr>
<tr>
<td>Parameters</td>
<td>Parameter Type</td>
<td>Parameter Description</td>
<td>Required or not</td>
</tr>
</thead>
<tbody>
<tr>
<td>content</td>
<td>String</td>
<td>content</td>
<td align="center">Y</td>
</tr>
</tbody>
</table>

Example：

```js
common.shell('curl https://xxxxx.com', function (data) {
    common.log(data);
});
```
