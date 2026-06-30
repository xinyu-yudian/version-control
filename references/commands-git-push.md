# Git 提交推送命令集

## 1. 读取待提交文件
file_list=$(cat .tmp_commit_files)

## 无文件直接退出
if [ -z "$file_list" ]; then
  echo "=== ERROR: 无待提交文件 ==="
  exit 1
fi

## 2. 添加全部变更文件
git add $(cat .tmp_commit_files)

## 3. 本地提交，传入自定义备注
git commit -m "$commit_msg"

## 4. 推送到上游分支
git push

## 5. 输出提交结果标记
echo "==== COMMIT_SUCCESS ===="
echo "COMMIT_MSG: $commit_msg"
echo "COMMIT_FILES:"
cat .tmp_commit_files
echo "==== PUSH_FINISH ===="

## 清理临时文件
rm .tmp_commit_files