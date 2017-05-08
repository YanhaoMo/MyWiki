# 安装解释器和包管理器
```
# apt install python3 python3-pip
```

## 更新pip到官方最新（可选）
```
# pip install --upgrade pip
```

＃ 使用国内源
#＃临时使用
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```

## 永久使用
修改文件`~/.pip/pip.conf`，内容为：

```text
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```