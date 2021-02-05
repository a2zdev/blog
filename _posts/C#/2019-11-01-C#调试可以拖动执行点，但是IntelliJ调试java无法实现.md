---
layout: default
title: C#调试可以拖动执行点，但是IntelliJ调试java无法实现
---

IntelliJ通过标准Java调试界面与正在运行的JVM进行交互，因此可以针对不同的JDK调试程序。这不支持按照您的描述移动执行点。
它允许您将调用堆栈回滚并再次执行方法调用。在IntelliJ中，使用线程窗口选择一个悬挂线程的堆栈框架并回滚到它。然后在程序中继续线程重新调用该方法。

注意：这不会回滚对象的状态，所以可能会发生奇怪的影响。
参考连接：https://codeday.me/bug/20180310/140332.html

但是在rider中调试C#同样是可以实现拖动执行点的功能的，所以这里和调试器有关系

stackoverflow参考：https://stackoverflow.com/questions/1651379/moving-the-instruction-pointer-while-debugging-java-in-eclipse