---
name: unsubmitted-files
description: Use when the user asks for 未提交文件, 未提交到线上库, SVN/Git 未提交, not pushed, uncommitted files, or uses format like "未提交：目录名/路径". Lists files not yet submitted to the online repository under the specified path (default to project root if no path given), including uncommitted/untracked/staged changes, Git local commits not pushed to upstream, or SVN local changes not committed, and outputs each result file in top-bottom diff format.
---

# Unsubmitted Files

List project files that have not been submitted to the remote/online repository.

## Output Format Rules
- Strictly follow the template defined in `references/output-formats.md`
- **Default format**: 未提交文件输出格式-上下对比版
- Use repository-relative paths. Do not include unchanged files.
- When using side-by-side diff format, you must first generate the batch export command (from `references/git-commands.md` or `references/svn-commands.md`), wait for the user to paste the output, and then parse and render it.

Use repository-relative paths. Do not include unchanged files.

## Workflow

1. Detect the VCS from the current workspace.
2. Collect candidate files that are not present in the online repository yet.
3. Read current file contents for files that still exist.
4. Output only the requested file list and code blocks, unless there is an error or ambiguity that must be explained.

## Git

Use the instructions in `references/git-commands.md` as required


## SVN

Use the instructions in `references/svn-commands.md`  as required


## Reading And Formatting Code

Read each existing file before output. Use the file extension to choose a Markdown fence language when obvious, such as `ts`, `tsx`, `js`, `json`, `md`, `py`, `java`, `cs`, `css`, `html`, `xml`, `yaml`, `sql`, `sh`, or `text`.

For binary files or files that cannot be read as text, output:

```text
(binary or unreadable file; code omitted)
```

If there are no unsubmitted files, answer exactly:

```text
没有发现未提交到线上库的文件。
```

Do not summarize the code. Do not add extra commentary after the list.