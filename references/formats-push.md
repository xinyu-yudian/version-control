# 提交结果输出格式

## 代码提交完成结果
> 提交备注：{用户最终填写的提交备注文本}
> 提交时间：{执行提交的时间戳}
> 版本工具：{Git / SVN}

### 本次提交文件清单
{循环遍历所有提交文件，单个文件模板如下}
`relative/path/to/file1.ext`
<details>
<summary>本次提交变更概览</summary>
<pre style="border: 1px solid #000000; padding: 0.5em;">
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #0ede3f;">+</span>行号</span><span style="background: #cef8d8;">新增代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #f5ad14;">~</span>行号</span><span style="background: #f0dfba;">更新代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #ea192d;">-</span>行号</span><span style="background: #f0939d;">删除代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
</code>
</pre>
</details>

{无变更文件时不输出details，仅展示文件路径}