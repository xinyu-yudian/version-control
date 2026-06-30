# SVN 提交推送命令集
## 1. 读取待提交文件
file_list=$(cat .tmp_svn_commit_files)
if [ -z "$file_list" ]; then
  echo "=== ERROR: 无待提交文件 ==="
  exit 1
fi

## 2. 同步新增/删除文件的版本控制状态
while IFS= read -r file; do
  # 处理未纳入版本控制的新增文件
  if [ -f "$file" ] && ! svn info "$file" > /dev/null 2>&1; then
    svn add "$file"
    if [ $? -ne 0 ]; then
      echo "=== ERROR: svn add 执行失败：$file ==="
      exit 1
    fi
  fi
  # 处理已本地删除的版本控制文件
  if [ ! -e "$file" ] && svn info "$file" > /dev/null 2>&1; then
    svn delete "$file"
    if [ $? -ne 0 ]; then
      echo "=== ERROR: svn delete 执行失败：$file ==="
      exit 1
    fi
  fi
done < .tmp_svn_commit_files

## 3. 提交所有变更（兼容含空格的文件名）
commit_output=$(cat .tmp_svn_commit_files | xargs -d '\n' svn commit -m "$commit_msg")
if [ $? -ne 0 ]; then
  echo "$commit_output"
  echo "=== ERROR: svn commit 执行失败 ==="
  exit 1
fi

## 4. 从提交结果中提取修订版本号
revision=$(echo "$commit_output" | grep -oP 'Committed revision \K[0-9]+')

## 5. 输出标准化提交结果标记
echo "==== COMMIT_SUCCESS ===="
echo "COMMIT_MSG: $commit_msg"
echo "COMMIT_REVISION: $revision"
echo "COMMIT_FILES:"
cat .tmp_svn_commit_files
echo "==== SVN_COMMIT_FINISH ===="

## 6. 仅提交成功后清理临时文件
rm .tmp_svn_commit_files