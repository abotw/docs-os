
# pbcopy & pbpaste

`pbpaste` 是 macOS 系统中用于与剪贴板（Clipboard）交互的命令行工具，它可以让你在终端中**读取剪贴板中的内容**。

---

##  `pbpaste` 简介

### 功能

- 从系统剪贴板读取文本并输出到标准输出（通常是终端）。
    
- 常用于脚本中提取剪贴板内容以进一步处理。
    

### 基本用法

```bash
pbpaste
```

这将把当前剪贴板中的文本内容输出到终端。

---

## 示例用法

### 1. 将剪贴板内容保存到文件

```bash
pbpaste > output.txt
```

### 2. 把剪贴板内容传给其他命令处理（例如统计行数）

```bash
pbpaste | wc -l
```

### 3. 使用剪贴板内容作为命令参数

```bash
grep "$(pbpaste)" somefile.txt
```

---

## 配套命令：`pbcopy`

### 简介

- `pbcopy` 是与 `pbpaste` 相对的命令，用于**将标准输入的文本写入剪贴板**。
    

### 示例用法

```bash
echo "Hello, clipboard!" | pbcopy
```

然后你可以通过粘贴操作（`Cmd + V`）或者用 `pbpaste` 检查：

```bash
pbpaste
# 输出：Hello, clipboard!
```

---

## 实用组合示例

### 剪贴板内容去重并排序

```bash
pbpaste | sort | uniq | pbcopy
```

### 将某个文件内容复制到剪贴板

```bash
cat somefile.txt | pbcopy
```

---

## 注意事项

- `pbpaste` 和 `pbcopy` 只能处理 **纯文本** 内容（不能处理图像、富文本等）。
    
- 它们主要用于 **交互式用户剪贴板**（GUI 环境），**不能在 SSH 会话下使用**，除非通过 GUI 共享剪贴板。
    

---

## 总结

|命令|作用|
|---|---|
|`pbpaste`|从剪贴板读取文本内容|
|`pbcopy`|将文本写入剪贴板|
