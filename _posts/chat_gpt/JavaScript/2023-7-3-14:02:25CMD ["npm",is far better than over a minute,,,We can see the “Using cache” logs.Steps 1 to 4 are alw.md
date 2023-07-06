Question:

Reply in Chinese (Simplified).
The following is the text content of a web page,analyze the core content and summarize:
Speed up your builds with Docker CacheSteve GrosboisPublié le 29 février 2016 - 2 min de lectureWhen you start with Docker,it seems normal to get inspired by some samples and examples you grabed around the web.First steps with DockerLet’s start,for example,with a simple nodejs project. You grab this nice Dockerfile,and,yes,it works great.FROM mhart/alpine-node
WORKDIR /src
# Copy your code in the docker image
COPY . /src
# Install your project dependencies
RUN npm install
# Expose the port 3000
EXPOSE 3000
# Set the default command to run when a container starts
CMD ["npm","start"]
Building again and again but no gainNow,you are working on your source code. And each time you want to build your image to test your code,the npm install.Know dockerHere comes three things to know :Docker build your image step by step.
Each step is dependent to the previous one.
Each step is cached by DockerBecause my code have changed,Docker use his cache before the step 3. After this,docker rebuild intermediates images from step 3 to step 6.We can see the “Removing intermediate container” logs : docker don’t use his cache for this steps because it depends on the step 3.Optimize your Dockerfile to get the best of cacheTo get the best of Docker cache :Think your Dockerfile like layers of images storted by specialization.First,i need a node ready image :
Second,i need a node image which working dir is /src
Then,i need a node ready image which working dir is /src and listening on port 3000 and running npm start as default command.
I need this previous image but with the node dependencies i specified in my package.json
Last step is the most specified step of this image,An optimized Dockerfile of my project :FROM mhart/alpine-node:5.6.0
WORKDIR /src
# Expose the port 3000
EXPOSE 3000
# Set the default command to run when a container starts
CMD ["npm",is far better than over a minute,,,We can see the “Using cache” logs.Steps 1 to 4 are always the same in our project,so cache is always used.The long npm install task at step 6 is only ran if there is a change on copied package.json file on step 5.The step 7 is the only step where an image is rebuilt based on previous steps when we make a change on our source code.We hope this post will help you gain time on your future Docker ready projects.Checkout our website and twitterDockerNodejsDevelopment,

Answer:

用中文（简体）回复。
以下是一个网页的文本内容，分析核心内容并总结：
加速你的 Docker 构建利用缓存
Steve Grosbois
发布于 2016 年 2 月 29 日 - 阅读时间 2 分钟
当你开始使用 Docker 时，你可能会参考一些你在网上找到的样例和示例。
使用 Docker 的第一步
比如说，你有一个简单的 nodejs 项目。你找到了这个不错的 Dockerfile，是的，它运行得很好。
FROM mhart/alpine-node
WORKDIR /src
# 把你的代码复制到 docker 镜像中
COPY . /src
# 安装你的项目依赖
RUN npm install
# 暴露端口 3000
EXPOSE 3000
# 设置容器启动时运行的默认命令
CMD ["npm","start"]
反复构建但没有收益
现在，你正在修改你的源代码。每次你想要构建你的镜像来测试你的代码，都要执行 npm install。
了解 docker
这里有三件事要知道：
Docker 一步一步地构建你的镜像。
每一步都依赖于前一步。
每一步都被 Docker 缓存了
因为我的代码发生了变化，Docker 在第三步之前使用了它的缓存。在这之后，docker 从第三步到第六步重新构建了中间镜像。
我们可以看到“Removing intermediate container”这样的日志：docker 不使用它的缓存来执行这些步骤，因为它们依赖于第三步。
优化你的 Dockerfile 来充分利用缓存
要充分利用 Docker 缓存：
把你的 Dockerfile 想象成按专业化程度排序的镜像层。
首先，我需要一个准备好 node 的镜像：
其次，我需要一个工作目录是 /src 的 node 镜像
然后，我需要一个工作目录是 /src、监听端口 3000、并且以 npm start 作为默认命令运行的 node 镜像。
我需要这个前面的镜像，但是加上我在 package.json 中指定的 node 依赖项
最后一步是这个镜像最具体化的一步，我的项目的优化后的 Dockerfile：
FROM mhart/alpine-node:5.6.0
WORKDIR /src
# 暴露端口 3000
EXPOSE 3000
# 设置容器启动时运行的默认命令
CMD ["npm","start"]
# 只有当 package.json 发生变化时才复制它并安装依赖项
COPY package.json /src/package.json
RUN npm install --production

# 复制源代码到镜像中（除了 .dockerignore 中排除的文件）
COPY . /src

我们希望这篇文章能帮助你在未来的 Docker 项目中节省时间。
访问我们的网站和推特
DockerNodejsDevelopment

总结：

这篇文章介绍了如何利用 Docker 的缓存机制来加速构建 nodejs 镜像的过程。文章给出了一个简单的示例，并解释了 Docker 是如何一步一步地构建镜像，并且如何根据前面的步骤来缓存中间结果。文章还给出了一些优化 Dockerfile 的技巧，让缓存更有效地发挥作用。文章最后提供了作者的网站和推特链接。

<hr/>

