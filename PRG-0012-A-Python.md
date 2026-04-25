# Python

## 2026-04-25 星期六

### Linux 中从源码安装 Python 指定版本

```bash
# 安装编译依赖
sudo yum groupinstall "Development Tools"
sudo yum install openssl-devel bzip2-devel libffi-devel zlib-devel readline-devel sqlite-devel xz-devel tk-devel

# 下载源码
wget https://www.python.org/ftp/python/3.13.7/Python-3.13.7.tgz
tar -xzf Python-3.13.7.tgz
cd Python-3.13.7

# 编译安装
./configure --enable-optimizations
make -j$(nproc)
sudo make altinstall # altinstall 不会覆盖系统默认的 python3
# 安装到最后可能会看到一条警告信息（WARNING: Running pip as the 'root' user...），这是 pip 的常规提示，不影响安装结果，可以忽略

# 验证安装
python3.13 --version # 如果输出 Python 3.13.7，表示安装已完全成功
```

### Linux 中切换系统默认 Python 版本

```bash
# 查看要切换到的 python3.13 的实际安装路径
which python3.13 # 输出 /usr/local/bin/python3.13

# 创建软链接
ln -sf /usr/local/bin/python3.13 /usr/bin/python3
ln -sf /usr/local/bin/python3.13 /usr/bin/python
ln -sf /usr/local/bin/python3.13 /usr/bin/py

# 验证
python3 --version # 预期输出 Python 3.13.x
python --version # 预期输出 Python 3.13.x
py --version # 预期输出 Python 3.13.x
```



## 2026-03-15 星期日

### 异步协程

* [Python asyncio 模块 - 菜鸟教程](https://m.runoob.com/python3/python-asyncio.html)
* [Python 异步协程：从 async/await 到 asyncio 再到 async with - 腾讯云](https://cloud.tencent.com/developer/article/2480588)

## 2026-03-09 星期一

### PostgreSQL

* [PostgreSQL 介绍 - Bilibili](https://www.bilibili.com/video/BV1FUYQz7E4H)

### TimescaleDB

* [TimescaleDB 实战教程 - Bilibili](https://www.bilibili.com/video/BV1g2rKB6EbA)

## 2026-02-28 星期六

### Python  官方文档

* [Python 官网](https://www.python.org/)
* [Python 语言参考手册](https://docs.python.org/zh-cn/3.13/reference/index.html#reference-index)
* [Python 标准库](https://docs.python.org/zh-cn/3.13/library/index.html)

### Python 编码规范

* [Python 风格指南（Google）](https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/index.html)
* [Python 编程规范 + 最佳实践](https://www.cnblogs.com/goldsunshine/p/18080982)

### 资料汇总

* [Python 数据分析资料汇总 - GitHub](https://github.com/hi-weijun/PythonDataScience-Collections)
* [Python 学习资料汇总 - GitHub](https://github.com/Yixiaohan/codeparkshare)
* [Python 入门课程 - YouTube](https://youtu.be/_Cc-dMVD2vs?si=JfyM33bcg2gY00Mt)

### 第三方库

* [十个最常用的第三方库](https://www.51cto.com/article/818238.html)
* [Beautiful Soup - HTML & XML 解析](https://beautiful-soup-4.readthedocs.io/en/latest/)

### 数据分析

* [如何使用 Python 进行实时数据流处理和可视化 - CSDN](https://blog.csdn.net/qq_42120268/article/details/140035371)
* [Python 量化交易](https://www.runoob.com/python-qt/qt-tutorial.html)

### Web 框架

* [FastAPI](https://fastapi.tiangolo.com/zh/)
* [FastAPI 快速入门视频教程 - Bilibili](https://www.bilibili.com/video/BV1KLcTzJETt)

### 可视化

* [Matplotlib 教程](https://www.runoob.com/matplotlib/matplotlib-tutorial.html)
* [seaborn](http://seaborn.pydata.org/)
* [bokeh](bokeh.pydata.org)
* [pyecharts](https://pyecharts.org/)
* [echarts](https://echarts.apache.org/zh/index.html)
