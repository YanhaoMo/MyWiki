安装
===
```
# apt install ruby
```

这儿安装了ruby编译器以及包管理器gem.

## 修改包管理器源地址。
```
# gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/

```
## 安装依赖管理器bundler
```
# gem install bundler
```

## 修改依赖管理器源地址
```
bundle config mirror.https://rubygems.org https://gems.ruby-china.org
```

## 安装ror
```
# apt install ruby-dev zlib1g-dev sqlite3 libsqlite3-dev
# gem install rails
```