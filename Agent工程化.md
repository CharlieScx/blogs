
多层架构：
这个区别非常重要。
比如 path 是不是字符串，不是“该不该做”，而是“能不能这么调用”。
但 path 是否允许指向 /etc/passwd，就可能同时涉及两层：
Registry 可以检查 path 类型、是否为空、是否有危险路径格式。
Contract 可以限制本任务只能操作 src/ 目录。
更强的沙箱层可以从系统层禁止访问项目外文件。
所以一个真实 Agent 系统里，安全不是一层管完，而是多层收口。


Agent 执行系统职责边界表：
Contract 管任务边界
Loop 管状态流程
Tool Call 管调用意图
Registry 管工具授权与参数边界
Tool Result 管执行事实
Eval 管行为回归
Permission/Resume 管暂停与恢复