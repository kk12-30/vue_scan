# Vue未授权接口扫描工具

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.6%2B-blue" alt="Python Version">
  <img src="https://img.shields.io/badge/Platform-Windows-lightgrey" alt="Platform">
</p>

## 功能介绍

这是一个用于扫描Vue框架前台泄露的未授权目录接口的图形化工具。该工具可以帮助安全测试人员快速发现Vue应用中可能存在的未授权访问漏洞，提高渗透测试效率。

### 主要功能

1. **JS文件爬取**：支持爬取指定网站的前端JS文件URL，自动处理相对路径和绝对路径
2. **路由路径提取**：支持从JS文件中提取Vue路由接口路径，识别多种路由定义格式
3. **接口测试**：支持对提取的接口进行逐一测试访问，检测未授权访问漏洞
4. **响应分析**：显示接口访问的响应包大小和内容，便于判断是否存在未授权访问
5. **自定义验证**：支持自定义URL验证，灵活应对不同场景
6. **高级渲染**：支持使用Playwright进行页面渲染，更准确地检测SPA应用

## 使用方法

### 环境要求

- Python 3.6+
- PyQt5 及相关依赖
- requests
- BeautifulSoup4
- Playwright
- 需存在路径“C:\Program Files\Google\Chrome\Application\chrome.exe”

### 安装依赖

```bash
# 安装基本依赖
pip install -r requirements.txt
```

### 运行程序

```bash
vue_scan.exe
```

### 使用步骤

1. **爬取JS文件**：
   - 在"初始URL"输入框中输入目标网站URL（例如：http://example.com/）
   - 点击"Get-JS"按钮爬取该网站的所有JS文件URL

2. **提取路径**：
   - JS文件爬取完成后，点击"getPath"按钮从JS文件中提取Vue路由路径

3. **测试路径**：
   - 在"自定义URL"输入框中输入要测试的基础URL（建议在URL后面加上#号，例如：https://www.example.com/#/）
   - 点击"测试路径"按钮对所有提取的路径进行测试

4. **查看结果**：
   - 在"测试结果"标签页中查看每个路径的测试结果，包括响应大小和内容
   - 通过比较响应大小和内容，判断是否存在未授权访问

5. **单独验证URL**：
   - 在"自定义URL"输入框中输入完整的URL
   - 点击"verify"按钮进行验证

## 注意事项

- Vue应用的URL通常包含#号（例如：https://example.com/#/）
- 响应包大小相似可能表示接口访问返回的是原来的前台登录界面，即不存在未授权访问
- 通过响应内容可以更直观地判断页面是否成功跳转

## 原理说明

Vue框架的路由信息通常在JS文件中以`path: '/xxx'`的格式存在。本工具通过正则表达式提取这些路径，然后拼接到基础URL后进行访问测试，通过分析响应内容和大小来判断是否存在未授权访问。
