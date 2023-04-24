# ERROR: ptrace(PTRACE_ATTACH, ..) failed for 211581: 不允许的操作



# ERROR: ptrace(PTRACE_ATTACH, ..) failed for 211581: 不允许的操作

在查看JVM参数时，输入如下命令：

```shell
jinfo -flags 212503
```

错误信息如下：

```shell
Attaching to process ID 212503, please wait...
ERROR: ptrace(PTRACE_ATTACH, ..) failed for 212503: 不允许的操作
Error attaching to process: sun.jvm.hotspot.debugger.DebuggerException: Can't attach to the process: ptrace(PTRACE_ATTACH, ..) failed for 212503: 不允许的操作
sun.jvm.hotspot.debugger.DebuggerException: sun.jvm.hotspot.debugger.DebuggerException: Can't attach to the process: ptrace(PTRACE_ATTACH, ..) failed for 212503: 不允许的操作
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal$LinuxDebuggerLocalWorkerThread.execute(LinuxDebuggerLocal.java:163)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal.attach(LinuxDebuggerLocal.java:278)
        at sun.jvm.hotspot.HotSpotAgent.attachDebugger(HotSpotAgent.java:674)
        at sun.jvm.hotspot.HotSpotAgent.setupDebuggerLinux(HotSpotAgent.java:612)
        at sun.jvm.hotspot.HotSpotAgent.setupDebugger(HotSpotAgent.java:338)
        at sun.jvm.hotspot.HotSpotAgent.go(HotSpotAgent.java:305)
        at sun.jvm.hotspot.HotSpotAgent.attach(HotSpotAgent.java:141)
        at sun.jvm.hotspot.tools.Tool.start(Tool.java:185)
        at sun.jvm.hotspot.tools.Tool.execute(Tool.java:118)
        at sun.jvm.hotspot.tools.JInfo.main(JInfo.java:138)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at sun.tools.jinfo.JInfo.runTool(JInfo.java:108)
        at sun.tools.jinfo.JInfo.main(JInfo.java:76)
Caused by: sun.jvm.hotspot.debugger.DebuggerException: Can't attach to the process: ptrace(PTRACE_ATTACH, ..) failed for 212503: 不允许的操作
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal.attach0(Native Method)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal.access$100(LinuxDebuggerLocal.java:62)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal$1AttachTask.doit(LinuxDebuggerLocal.java:269)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal$LinuxDebuggerLocalWorkerThread.run(LinuxDebuggerLocal.java:138)

```

原因：

新版的Linux系统加入了 `ptrace-scope` 机制,该机制的目的是防止用户访问正在执行的进程的内存，但是如jinfo,jmap这些调试类工具本身就是利用`ptrace来获取执行进程的内存等信息。`

解决方案：

关闭ptrace-scope防护

```shell
//临时修改
sudo sysctl -w kernel/yama/ptrace_scope=0

//永久修改
sudo vim /etc/sysctl.d/10-ptrace.conf 
	// 1  修改为 0
kernel.yama.ptrace_scope = 0
```

本次错误记录到此为止。
