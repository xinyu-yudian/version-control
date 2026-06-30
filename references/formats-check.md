## 检查文件输出格式
每个文件独立展示，显示本地未提交版本，仅展示修改位置上下各5行上下文，支持行号显示、修改行标红、折叠展开，代码超出宽度自动横向滚动。

### 核心规则
1. **三级标题**显示文件仓库相对路径
2. 使用 `<details>` 实现折叠交互，遵循智能折叠规则
3. 每行代码前附带真实行号，行号浅灰色右对齐
4. 修改行字体标红（删除行/新增行），上下文行保持默认颜色
5. 同一文件多处修改按顺序编号排列，每处独立带行号

### 智能折叠规则
- 总修改文件数 = 1 且 单文件修改只有1处：默认展开（加 `open` 属性）
- 总修改文件数 > 1 或 单文件修改大于1处：全部默认折叠，均不加 `open` 属性

### 行号生成规则
1. 从 diff 的 hunk 头 `@@ -old_start +new_start @@` 分别提取修改后的起始行号
2. 每个修改块的行号都是文件实际行号
3. 上下文行、删除行/新增行均正常显示对应行号
4. 行号统一右对齐，宽度自适应，与代码区间隔1em

### 代码背景颜色规则
- 所有代码颜色为黑色 `#000000`
- 新增的代码使用绿色背景 `#cef8d8`
- 修改的代码使用黄色背景 `#f0dfba`
- 删除的代码使用红色背景 `#f0939d`
- 未修改的上下文行无背景色

### 精确输出模板（必须严格遵循）
```markdown
`relative/path/to/file1.ext`
<details>
<summary>第 1 处修改</summary>
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

<details>
<summary>第 2 处修改</summary>
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
...


 `relative/path/to/file2.ext`
<details>
<summary>第 1 处修改</summary>
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

<details>
<summary>第 2 处修改</summary>
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
...