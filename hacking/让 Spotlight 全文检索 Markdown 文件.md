
# 让 Spotlight 全文检索 Markdown 文件

macOS 中的 Spotlight 默认情况下是不对 Markdown 文件（文件名后缀为 .md ）建立全文索引的，因此无法在 Spotlight 中搜索到 Markdown 文件中的内容。
但是我们可以通过手动修改 Spotlight 的配置，让它支持 Markdown 文件的全文检索。

具体步骤如下：

## 进入恢复模式，关闭系统文件保护

* 重启 macOS ，按住 `Command + R` 直到屏幕出现 Apple logo ，进入恢复模式
* 选择中文为界面显示语言
* 选择 工具 > 终端
* 在终端中输入 `csrutil disable` 然后按 `Enter`
* 重启 macOS，正常进入系统

## 修改 Spotlight 配置并重建索引

* 打开终端，输入以下命令

```
cd /System/Library/Spotlight/RichText.mdimporter/Contents
sudo vi Info.plist
```

* 找到 `LSItemContentTypes` 节点，在其 `<array>` 列表的最后一行添加以下内容

```
<string>net.daringfireball.markdown</string>
```

* 输入 `wq` 保存修改
* 输入以下命令，让 Spotlight 重建索引

```
mdimport -r /System/Library/Spotlight/RichText.mdimporter
sudo mdutil -E /
```

* 等待大约10分钟，Spotlight 重建索引完毕后，即可在 Spotlight 中对 Markdown 文件进行全文检索了

## 进入恢复模式，重新开启系统文件保护

* 再次重启 macOS ，按住 `Command + R` 直到屏幕出现 Apple logo ，重新开启系统文件保护
* 选择中文为界面显示语言
* 选择 工具 > 终端
* 在终端中输入 `csrutil enable` 然后按 `Enter`
* 重启 macOS 即可继续正常使用了

## 参考资料

* [How can I make spotlight index markdown files?](http://stackoverflow.com/questions/365669/how-can-i-make-spotlight-index-markdown-files)
* [讓 Spotlight 檢索 Markdown 文件](http://www.itread01.com/articles/1476601557.html)

---

change log: 

	- 创建（2017-01-12）

---



