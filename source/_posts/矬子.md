---
title: Delphi异常处理机制
date: 2012-03-21 15:06:02
tags:
- Delphi
categories:
- 技术文章
- Delphi
---
Delphi的异常处理方式有两种：`try...except...end`和`try...finally...end`。
`try...except`主要用于捕获异常，只有出现异常的时候才会执行except部分。
`try...finally`主要用于资源释放，无论try语句块是否有异常都会执行finally语句块。

如下面的代码：
```
 try
   raise exception.create('发现异常');  //在try语句块中抛出一个异常
 except
   on e:Exception do    //捕获异常
   begin
     showMessage(e.message);   
   end;
 end;
```

用`try..except`是不会出现异常提示信息的对话框，需要自己主动去show出异常信息。而`try..finally`则会出现异常提示信息。`try..except`和`try..finally`可以相互嵌套。

          
使用`on e:Exception do`可以精确处理特定的异常。Exception是所有异常类的基类，Delphi内部就定义了处理常见异常的异常类（在SysUtils单元中），也可以从Exception继承定义自己的异常类。

使用raise语句可以抛出一个异常：
```
 EMyException=class(Exception)
 end;
 try
   try
     raise EMyException.Create('我自己的异常');
   except
   on e:EMyException do
     showMessage(e.message);
   end; 
 finally
   showMessage('我始终被执行');
 end
```
