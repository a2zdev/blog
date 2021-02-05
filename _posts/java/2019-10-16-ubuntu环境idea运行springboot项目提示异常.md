---
layout: default
title: ubuntu环境idea运行springboot项目提示异常
---

## ubuntu环境idea运行springboot项目提示异常

错误描述如下：
Description:
The Tomcat connector configured to listen on port 80 failed to start. The port may already be in use or the connector may be misconfigured.

Action:
Verify the connector's configuration, identify and stop any process that's listening on port 80, or configure this application to listen on another port.

原因在于在linux下，如果使用1024以下的端口则需要root权限。
我启动项目的时候配置的是80端口，所以出现异常。
修改端口大于1024即可。