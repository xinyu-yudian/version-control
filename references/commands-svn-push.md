# SVN 提交推送命令集

file_list=$(cat .tmp_svn_commit_files)
if [ -z "$file_list" ]; then
  echo "=== ERROR: 无待提交文件 ==="
  exit 1
fi

## SVN一次性提交所有变更，同步线上仓库
svn commit -m "$commit_msg" $(cat .tmp_svn_commit_files)

## 输出提交结果标记
echo "==== COMMIT_SUCCESS ===="
echo "COMMIT_MSG: $commit_msg"
echo "COMMIT_FILES:"
cat .tmp_svn_commit_files
echo "==== SVN_COMMIT_FINISH ===="
rm .tmp_svn_commit_files