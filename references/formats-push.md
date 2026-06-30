# 提交结果输出格式
根据实际提交结果，按照对应的提交结果、提交已取消、提交失败三个类型输出提交信息

## 提交完成输出内容模版
### ✅提交完成
> 提交备注：{用户最终填写的提交备注文本}
> 提交时间：{执行提交的时间戳}
> 版本工具：{Git / SVN}
### 使用**公共复用模块**


## 提交已取消输出内容模版
## 🟡提交已取消
## 使用**公共复用模块**
操作说明：用户点击弹窗【取消】按钮，终止全部提交流程，本地变更未同步至线上仓库。


## 提交失败输出内容模版
## ❌提交失败
> 错误类型：{冲突 / 权限不足 / 网络异常 / 无待提交文件 / 其他}
> 操作建议：{对应错误的处理指引}
## 使用**公共复用模块**


## 公共复用模块
### 变更文件清单表格
```html
<table border="1" cellpadding="6" cellspacing="0" width="100%">
  <thead>
    <tr>
      <th>文件路径</th>
      <th>变更类型</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><span style="color:#ea192d;">-</span> relative/path/to/file1.ext</td>
      <td><span style="color:#ea192d;">已删除</span></td>
    </tr>
    <tr>
      <td><span style="color:#0ede3f;">+</span> relative/path/to/file2.ext</td>
      <td><span style="color:#0ede3f;">已添加</span></td>
    </tr>
    <tr>
      <td><span style="color:#f5ad14;">~</span> relative/path/to/file3.ext</td>
      <td><span style="color:#f5ad14;">已修改</span></td>
    </tr>
  </tbody>
</table>