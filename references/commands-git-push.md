# Git 提交推送命令集
## 1. 读取待提交文件
file_list=$(cat .tmp_commit_files)
## 无文件直接退出
if [ -z "$file_list" ]; then
  echo "=== ERROR: 无待提交文件 ==="
  exit 1
fi

## 2. 尝试快进拉取远程最新代码，前置规避推送冲突
git pull --ff-only
if [ $? -ne 0 ]; then
  echo "=== ERROR: 本地代码落后于远程，存在合并冲突风险 ==="
  echo "请先手动拉取代码并解决冲突后重试"
  exit 1
fi

## 3. 添加全部变更文件（兼容含空格的文件名）
cat .tmp_commit_files | xargs -d '\n' git add
if [ $? -ne 0 ]; then
  echo "=== ERROR: git add 执行失败 ==="
  exit 1
fi

## 4. 本地提交，传入自定义备注
git commit -m "$commit_msg"
if [ $? -ne 0 ]; then
  echo "=== ERROR: git commit 执行失败 ==="
  exit 1
fi

## 5. 获取提交短哈希，用于结果展示
commit_hash=$(git rev-parse --short HEAD)

## 6. 推送到上游分支（兼容未设置上游分支的场景）
git push origin HEAD
if [ $? -ne 0 ]; then
  echo "=== ERROR: git push 执行失败 ==="
  exit 1
fi

## 7. 输出标准化提交结果标记
echo "==== COMMIT_SUCCESS ===="
echo "COMMIT_MSG: $commit_msg"
echo "COMMIT_HASH: $commit_hash"
echo "COMMIT_FILES:"
cat .tmp_commit_files
echo "==== PUSH_FINISH ===="

## 8. 仅提交推送全部成功后清理临时文件
rm .tmp_commit_files