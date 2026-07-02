## 检查文件输出格式
每个文件独立展示，显示本地未提交版本，仅展示修改位置上下各5行上下文，支持行号显示、修改行标色、折叠展开，代码超出宽度自动横向滚动。
### 核心规则
1. **三级标题**显示文件仓库相对路径
2. 使用 `<details>` 实现折叠交互，遵循智能折叠规则
3. 每行代码前附带真实行号，行号浅灰色右对齐
4. 新增行使用绿色背景，删除行使用红色背景，上下文行保持默认样式
5. 同一文件多处修改按顺序编号排列，每处独立带行号
6. 禁止直接输出原始 diff 纯文本，不得透传 `@@` hunk 头、带 +/- 前缀的原始 diff 行，必须完成行号解析与样式渲染后再输出
7. 每一行代码必须独立生成「行号列 + 代码内容」的完整结构，不得将整段原始 diff 直接包裹进 `<code>` 标签
8. 二进制文件处理规则：
   - 文本文件被误判为二进制时，通过 diff 命令自动强制输出文本 diff，正常渲染行号与样式
   - 确认为真实二进制文件时，在对应修改块内输出统一提示「该文件为二进制类型，无法展示文本 diff」，不得输出乱码内容
   - 二进制文件可补充展示变更类型（新增/删除/修改）、文件大小等元信息，不做强行文本转换

### 智能折叠规则
- 总修改文件数 = 1 且 单文件修改只有1处：默认展开（加 `open` 属性）
- 总修改文件数 > 1 或 单文件修改大于1处：全部默认折叠，均不加 `open` 属性

### 行号生成规则
1. 从 diff 的 hunk 头 `@@ -old_start +new_start @@` 分别提取旧版本起始行号与新版本起始行号
2. 每个修改块的行号都是文件实际行号
3. 上下文行、删除行/新增行均正常显示对应行号
4. 行号统一右对齐，宽度自适应，与代码区间隔1em
5. 行号计数规则：
   - 上下文行：旧行号、新行号各自增1，展示新行号，无前置标记
   - 删除行：仅旧行号自增1，展示旧行号，行号前加红色 `-` 标记
   - 新增行：仅新行号自增1，展示新行号，行号前加绿色 `+` 标记

### 代码背景颜色规则
- 所有代码颜色为黑色 `#000000`
- 新增的代码使用绿色背景 `#cef8d8`
- 删除的代码使用红色背景 `#f0939d`
- 未修改的上下文行无背景色

### 间距统一规则
- 文件与文件之间垂直间距：1em
- 文件标题与首个折叠块之间间距：0.5em
- 单个文件内多个子变更块之间间距：0.3em
- 代码块内部通过 padding 控制内边距，取消默认外边距

### 精确输出模板（必须严格遵循以下模版，不额外增加任何描述）
```markdown
`relative/path/to/file1.ext`
<details style="margin: 0.5em 0 1em 0;">
<summary>第 1 处修改</summary>
<pre style="border: 1px solid #000000; padding: 0.5em;">
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #0ede3f;">+</span>行号</span><span style="background: #cef8d8;">新增代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #ea192d;">-</span>行号</span><span style="background: #f0939d;">删除代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
</code>
</pre>
</details>
<details style="margin: 0.5em 0 1em 0;">
<summary>第 2 处修改</summary>
<pre style="border: 1px solid #000000; padding: 0.5em;">
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #0ede3f;">+</span>行号</span><span style="background: #cef8d8;">新增代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #ea192d;">-</span>行号</span><span style="background: #f0939d;">删除代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
</code>
</pre>
</details>
...
 `relative/path/to/file2.ext`
<details style="margin: 0.5em 0 1em 0;">
<summary>第 1 处修改</summary>
<pre style="border: 1px solid #000000; padding: 0.5em;">
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #0ede3f;">+</span>行号</span><span style="background: #cef8d8;">新增代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #ea192d;">-</span>行号</span><span style="background: #f0939d;">删除代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
</code>
</pre>
</details>
<details style="margin: 0.5em 0 1em 0;">
<summary>第 2 处修改</summary>
<pre style="border: 1px solid #000000; padding: 0.5em;">
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #0ede3f;">+</span>行号</span><span style="background: #cef8d8;">新增代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;"><span style="color: #ea192d;">-</span>行号</span><span style="background: #f0939d;">删除代码行</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">行号</span>未修改代码行内容
</code>
</pre>
</details>
...