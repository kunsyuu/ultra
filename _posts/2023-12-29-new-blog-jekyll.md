---
layout: post
title: 本地调试预览Jekyll网站
---

学习了一下使用Jekyll。

之前一直使用Hexo，但是Hexo的本地文件如果丢失，很可能就不能再复原样式了。

而Jekyll所有的文件都在Github上，不用担心本地文件丢失的问题，而且新增文章时也仅需要提交一个md文件就可以自动部署了。使用Github Desktop依然可以很方便的提交。

网页服务器使用GitHub，再部署到Cloudflare Pages。都是免费的，毕竟写文章水平太烂，没有必要折腾太复杂。

在 Windows 系统上调试和预览 Jekyll 网站的详细步骤：

#### 1. 安装 Ruby 和 DevKit  

- 下载 RubyInstaller  
 访问 RubyInstaller for Windows，选择 Ruby+Devkit 版本（例如 Ruby 3.0.x）。
（DevKit 是编译本地依赖的必要工具，避免后续安装失败）

- 安装 Ruby  
双击下载的安装包，按提示操作：

    - 勾选 Add Ruby executables to your PATH（自动配置环境变量）。

    - 安装完成后，会弹出黑色终端窗口，按提示安装 MSYS2 工具链（按回车键继续，直到完成，这一步需要联网，国内网络可能会失败，需要开启Tun模式）.  

#### 2. 验证 Ruby 安装
打开 命令提示符（CMD） 或 PowerShell，运行：
```bash
ruby -v
gem -v
```
如果返回版本号（如 ruby 3.0.0 和 gem 3.3.0），说明安装成功。

#### 3. 安装 Jekyll 和 Bundler
在命令行中运行：
```bash
gem install jekyll bundler
```
- 如果提示权限问题，可以尝试：
```bash
gem install jekyll bundler --user-install
```
- 安装完成后，验证是否成功：
```bash
jekyll -v
```

#### 4. 创建或进入 Jekyll 项目
- 新建项目（可选）
```bash
jekyll new my-site
cd my-site
```
- 已有项目  
直接进入项目根目录：
```bash
cd C:\path\to\your\jekyll-project
```

#### 5. 安装项目依赖  
在项目目录下运行：
```bash
bundle install
```
（此命令会根据项目中的 Gemfile 安装依赖库）

#### 6. 启动本地服务器
运行以下命令：
```bash
bundle exec jekyll serve --livereload
```
或者
```bash
jekyll s
```
- 参数说明：
    - --livereload：自动刷新浏览器（修改文件后无需手动刷新）。
    - --port 4001：如果默认端口 4000 被占用，可指定其他端口。
    - --host 0.0.0.0：允许同一局域网内的其他设备访问（如手机预览）。
- 成功提示：
```bash
Server address: http://localhost:4000
Server running... press ctrl-c to stop.
```

#### 7. 访问本地预览
打开浏览器，输入 http://localhost:4000（如果修改了端口，替换为实际端口号）。

#### 8. 调试技巧（Windows 专属注意事项）

- 实时修改与刷新  
修改 _posts、_config.yml 或样式文件后，Jekyll 会自动重新生成网站。如果使用 --livereload，浏览器会自动刷新。

- 处理路径问题
    - 避免项目路径包含空格或中文字符（如 C:\My Site 可能引发错误）。
    - 推荐使用简单路径，如 C:\projects\my-site。

- 查看错误日志  
如果页面未更新，观察命令行中的错误提示（如 Markdown 语法错误、YAML 格式问题）。


#### 9. 常见问题与解决

- 报错：cannot load such file -- webrick (LoadError)
运行以下命令安装缺失的库：
```bash
bundle add webrick
```

- 报错：Permission denied
    - 不要使用 sudo，Windows 中应以普通用户权限运行命令。
    - 确保项目目录未被其他程序占用（如编辑器、资源管理器）。

- 端口被占用  
运行以下命令终止占用 4000 端口的进程：
```bash
netstat -ano | findstr :4000
taskkill /PID <进程号> /F
```  

- 实时加载（LiveReload）无效  
检查防火墙是否允许 jekyll serve 访问网络，或在浏览器中手动刷新。

#### 10. 关闭本地服务器  
在命令行窗口按 Ctrl + C 终止进程。