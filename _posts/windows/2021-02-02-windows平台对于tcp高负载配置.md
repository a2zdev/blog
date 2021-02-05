---
layout: default
title: 【转载】windows平台对于TCP高负载配置
---

Adjusting TCP Settings for Heavy Load on Windows

The underlying Search architecture that directs searches across multiple physical partitions uses TCP/IP ports and non-blocking NIO SocketChannels to connect to the Search engines. These connections remain open in the TIME_WAIT state until the operating system times them out. Consequently, under heavy load conditions, the available ports on the machine running the Routing module can be exhausted.

On Windows platforms, the default timeout is 120 seconds, and the maximum number of ports is approximately 4,000, resulting in a maximum rate of 33 connections per second. If your index has four partitions, each search requires four ports, which provides a maximum query rate of 8.3 queries per second.

(maximum ports/timeout period)/number of partitions = maximum query rate
If this rate is exceeded, you may see failures as the supply of TCP/IP ports is exhausted. Symptoms include drops in throughput and errors indicating failed network connections. You can diagnose this problem by observing the system while it is under load, using the netstat utility provided on most operating systems.

To avoid port exhaustion and support high connection rates, reduce the TIME_WAIT value and increase the port range.

Note: This problem does not usually appear on UNIX systems due to the higher default connection rate in those operating systems.

To set TcpTimedWaitDelay (TIME_WAIT):

1.Use the regedit command to access the HKEY_LOCAL_MACHINESYSTEMCurrentControlSet ServicesTCPIPParameters registry subkey.
2.Create a new REG_DWORD value named TcpTimedWaitDelay.
3.Set the value to 60.
4.Stop and restart the system.

To set MaxUserPort (ephemeral port range):
1.Use the regedit command to access the HKEY_LOCAL_MACHINESYSTEMCurrentControlSet ServicesTCPIPParameters registry subkey.
2.Create a new REG_DWORD value named MaxUserPort.3.Set this value to 32768.
4.Stop and restart the system.

引用：https://docs.oracle.com/cd/E26180_01/Search.94/ATGSearchAdmin/html/s1207adjustingtcpsettingsforheavyload01.html#:~:text=On%20Windows%20platforms%2C%20the%20default,of%2033%20connections%20per%20second.