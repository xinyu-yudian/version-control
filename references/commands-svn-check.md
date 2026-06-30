# SVN 未提交文件检测命令集

## 基础状态命令（仅列文件清单）
输出完整状态信息，包含所有变更类别：
```bash
svn status --ignore-externals "$target_path"

## 批量导出前后内容命令
当需要输出「修改前/修改后」代码对比时，使用此命令一次性导出所有变更文件的仓库版本与本地版本。
输出格式包含明确分隔标记，便于解析：
- FILE_PATH: 文件相对路径
- BEFORE_HEAD: 仓库 HEAD 基线版本内容
- AFTER_LOCAL: 本地未提交版本内容
- __NEW_FILE__: 新增文件，无基线版本
- __DELETED_FILE__: 已删除文件，无本地版本

```bash
# 匹配所有内容/属性变更、新增、删除、未跟踪文件，兼容含空格的文件名
svn status --ignore-externals "$target_path" | grep -E '^[MAD? ]' | cut -c 9- | while read file; do
  echo "==== FILE_PATH: $file ====="
  echo "==== BEFORE_REMOTE ====="
  svn cat "$file" 2>/dev/null || echo "__NEW_FILE__"
  echo "==== AFTER_LOCAL ====="
  cat "$file" 2>/dev/null || echo "__DELETED_FILE__"
  echo "==== END ====="
  echo ""
done

## 统一 Diff 格式命令
svn diff --context=5 "$target_path"