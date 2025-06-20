# Python 文件与目录操作入门教程（基于 `os` 模块）

> 🐍 本文基于 [廖雪峰的 Python 教程](https://www.liaoxuefeng.com/wiki/1016959663602400) 的学习内容整理，并加入适合初学者理解的详细讲解，仅供自己学习使用。

---

## 🧰 为什么要学会操作文件与目录？

在日常开发中，我们经常需要操作文件系统，比如：

- 自动创建文件夹或清理日志；
- 扫描某个目录下所有 `.txt` 或 `.py` 文件；
- 获取文件路径、扩展名、移动文件等；

Python 提供了强大的内置模块 `os` 和 `os.path` 来帮助我们完成这些任务。你可以把它们理解为 Python 与操作系统沟通的桥梁。

---

## 1️⃣ 导入 `os` 模块

在使用前我们需要导入：

```python
import os
2️⃣ 判断当前操作系统类型
了解操作系统类型有时很重要，特别是写跨平台程序时：
print(os.name)  # 输出 'posix' 表示类Unix系统，'nt' 表示Windows
# 更详细的系统信息（Windows不支持）
print(os.uname())
3️⃣ 访问环境变量
环境变量存储了很多系统配置：
print(os.environ)  # 查看所有环境变量
print(os.environ.get('PATH'))  # 获取 PATH 环境变量
⚠️ 推荐使用 get()，这样即使环境变量不存在也不会报错。
4️⃣ 常用路径操作（重点）
✅ 拼接路径（推荐）
path = os.path.join('folder', 'file.txt')
print(path)
# Windows: folder\file.txt，Linux/macOS: folder/file.txt
✅ 获取绝对路径
abs_path = os.path.abspath('.')
print(abs_path)
✅ 拆分路径
print(os.path.split('/home/user/test.txt'))
# 输出：('/home/user', 'test.txt')
✅ 获取文件扩展名
print(os.path.splitext('hello.py'))
# 输出：('hello', '.py')
✅ 以上函数只是对路径字符串进行处理，不关心文件是否真实存在！
5️⃣ 创建、删除、重命名
📁 创建目录
os.mkdir('new_folder')
❌ 删除空目录
os.rmdir('new_folder')
✏️ 重命名文件
os.rename('old.txt', 'new.txt')
🗑️ 删除文件
os.remove('new.txt')
6️⃣ 文件复制操作（使用 shutil）
因为 os 不支持复制文件，我们使用 shutil：
import shutil
shutil.copyfile('source.txt', 'target.txt')
7️⃣ 使用列表生成式筛选文件（高效！）
📂 列出所有子目录：
dirs = [x for x in os.listdir('.') if os.path.isdir(x)]
print(dirs)
📄 列出所有 .py 文件：
py_files = [x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1] == '.py']
print(py_files)
✅ 这就是 Python 强大的「列表推导式」，推荐掌握！
✅ 总结速查表
<html>
<body>
<!--StartFragment--><html><head></head><body>
操作 | 函数
-- | --
导入模块 | import os
系统类型 | os.name / os.uname()
环境变量 | os.environ.get()
拼接路径 | os.path.join()
当前路径 | os.path.abspath('.')
拆分路径 | os.path.split()
文件扩展名 | os.path.splitext()
创建目录 | os.mkdir()
删除目录/文件 | os.rmdir() / os.remove()
重命名 | os.rename()
文件复制 | shutil.copyfile()
文件筛选 | 列表生成式

</body></html><!--EndFragment-->
</body>
</html>
📚 推荐阅读
📘 [Python官方文档 - os 模块](https://docs.python.org/3/library/os.html)

📘 廖雪峰 Python 教程
