# littleCode
一个自己的代码小仓库


# tsscript 学习的技巧
快速执行的技巧： vscode 中安装 code-runner 插件，并在 code-首选项-键盘快捷键 中设置快捷键 code-runner.run 为 cmd + q 并回车，即可。
code-runner报错： /bin/sh: node: command not found 
在settings.json配置文件中增加：   "code-runner.runInTerminal": true, 或者 code-runner.executorMap 下的 javascript 的路径
