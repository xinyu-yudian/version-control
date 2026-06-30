## 未提交文件输出格式
每个文件独立展示，显示本地未提交版本，仅展示修改位置上下各5行上下文，支持行号显示、修改行标红、折叠展开，代码超出宽度自动横向滚动。

### 核心规则
1. **三级标题**显示文件仓库相对路径
2. 使用 `<details>` 实现折叠交互，遵循智能折叠规则
3. 每行代码前附带真实行号，行号浅灰色右对齐
4. 修改行字体标红（删除行/新增行），上下文行保持默认颜色
5. 同一文件多处修改按顺序编号排列，每处独立带行号

### 智能折叠规则
- 总修改文件数 = 1：默认展开（加 `open` 属性）
- 总修改文件数 > 1：全部默认折叠，均不加 `open` 属性

### 行号生成规则
1. 从 diff 的 hunk 头 `@@ -old_start +new_start @@` 分别提取修改后的起始行号
2. 每个修改块的行号都是文件实际行号
3. 上下文行、删除行/新增行均正常显示对应行号
4. 行号统一右对齐，宽度自适应，与代码区间隔1em

### 标红规则
- 新增/替换的新代码行使用红色 `#d73a49`
- 未修改的上下文行保持默认字体颜色

### 精确输出模板（必须严格遵循）
```markdown
`relative/path/to/file1.ext`
<details>
<summary>第 1 处修改</summary>
<pre>
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">1</span>代码行内容+行号
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">2</span><span style="color: #d73a49;">新增的代码行+行号</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">3</span>上下文代码行+行号
</code>
</pre>
</details>

<details>
<summary>第 2 处修改</summary>
<pre>
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">1</span>代码行内容+行号
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">2</span><span style="color: #d73a49;">新增的代码行+行号</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">3</span>上下文代码行+行号
</code>
</pre>
</details>
...


 `relative/path/to/file2.ext`
<details>
<summary>第 1 处修改</summary>
<pre>
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">1</span>代码行内容+行号
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">2</span><span style="color: #d73a49;">新增的代码行+行号</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">3</span>上下文代码行+行号
</code>
</pre>
</details>

<details>
<summary>第 2 处修改</summary>
<pre>
<code>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">1</span>代码行内容+行号
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">2</span><span style="color: #d73a49;">新增的代码行+行号</span>
<span style="display:inline-block;width:3em;text-align:right;color:#6a737d;margin-right:1em;">3</span>上下文代码行+行号
</code>
</pre>
</details>
...