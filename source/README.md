### Hexo+githubPage搭建个人博客
>搭建教程：https://www.simon96.online/2018/10/12/hexo-tutorial/

记录自己一点点的进步。

##### 主要搭建步骤：

1. 下载` nodejs `，配置环境变量（默认安装自动配置）。

2. 下载` git `，配置环境变量（默认安装自动配置）。

   

3. 在` cmd `中使用安装hexo：

   ```
   npm install -g hexo-cli //
   ```

   如果下载太慢，先安装淘宝镜像，再进行下载。之后，两者指令相同，作用相同 npm=cnpm;

   

4. 初始化Hexo，新建文件夹作为`  站点根目录  `，在`当前目录`使用cmd（或Git Bash）依次运行以下命令即可：

   ```
   git clone https://github.com/hexojs/hexo-starter.git
   ```

   其实就是，将初始文件克隆到本地，再进行优化。

   

5. 启动服务器。在路径下，命令行（即Git Bash）输入以下命令，运行即可：

   ```
   hexo server
   ```

   

6. 浏览器访问网址： `http://localhost:4000/`

   

至此，您的Hexo博客已经搭建在本地。









