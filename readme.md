# test

[![Build Status](https://travis-ci.org/cwxyz007/test.svg?branch=master)](https://travis-ci.org/cwxyz007/test) [![Coverage Status](https://coveralls.io/repos/github/cwxyz007/test/badge.svg?branch=master)](https://coveralls.io/github/cwxyz007/test?branch=master)

这篇文章的目标就是在 GitHub 上显示如下图标。当然不是简单的显示两张图片，而是显示当前项目的一些状态。

![icons](http://upload-images.jianshu.io/upload_images/1922205-6b6eaf2be71401c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

持续集成官网： [Travis-ci](https://travis-ci.org/)
测试覆盖率官网：[COVERALLS](https://coveralls.io/)

![Build 状态](http://upload-images.jianshu.io/upload_images/1922205-9378467e0e410294.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![测试状态](http://upload-images.jianshu.io/upload_images/1922205-622fccfbc2dc6621.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 持续集成

如果项目中没有测试，那么就不需要包含测试覆盖率这一块。

首先创建一个简单的项目

![项目](http://upload-images.jianshu.io/upload_images/1922205-057c0bc02226c0ef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

那么第一步，当然是选择跟着[官方文档](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/)走啦，先创建 `.travis.yml` 文件，查看 `node` 版本 `node -v`。然后填进去，我的是 8.5.0，所以我的文件是这样的：

```yml
language: node_js
node_js:
  - "8"
```

然后 `git push` 到 GitHub ，然后刷新 Travis CI 的页面：

![Test](http://upload-images.jianshu.io/upload_images/1922205-aff4a86a26f1a2ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

就这样，持续集成就OK了，是不是很简单，然后点击 passing 图标，选择 Markdown 写到 readme 里面就可以在 GitHub 上看到了。

## 测试覆盖率

同样的，跟着[官方文档](https://coveralls.zendesk.com/hc/en-us/articles/201769715-Javascript-Node)上的第一个 [node-coveralls](https://github.com/nickmerwin/node-coveralls) 走。项目还是上面那个测试项目。

测试项目的目录：

![测试项目](http://upload-images.jianshu.io/upload_images/1922205-df74a56b73cac61d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在 [node-coveralls](https://github.com/nickmerwin/node-coveralls) 里面有很多钟方式，我选择 [Istanbul](https://github.com/gotwarlost/istanbul) + [mocha](https://github.com/mochajs/mocha)。

那么，第一步，当然是安装 [Istanbul](https://github.com/gotwarlost/istanbul) + [mocha](https://github.com/mochajs/mocha) 啦，当然还要安装 coveralls[https://coveralls.io/]

```
npm install mocha --save-dev #安装 mohca
npm install istanbul --save-dev #安装 istanbul
npm install coveralls --save-dev #安装 coveralls
```

为了不把 node_module 上传到 GitHub ，所以还需要创建 `.gitignore' ，在里面添加 node_module 文件夹。

然后写测试，测试为：

![测试项目](http://upload-images.jianshu.io/upload_images/1922205-a030cdbbc9ed89fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改 `package.json` 里面的 `test` 脚本为
`istanbul cover ./node_modules/mocha/bin/_mocha --report lcovonly -- -R spec && cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js && rm -rf ./coverage` 

然后运行 `npm test` 命令，会提示一个错误，那个是因为没有在 `package.json' 里面添加 repository 地址，可以忽略。

![测试结果](http://upload-images.jianshu.io/upload_images/1922205-4af38828fc5d8f30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到这一步，就可以把项目 push 到 GitHub 上去了。然后刷新在 [COVERALLS](https://coveralls.io/) 上的项目的网页。

![测试覆盖率](http://upload-images.jianshu.io/upload_images/1922205-9d8683618dc0a27f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

就可以看到成功了！然后点击 EMBED 图标，选择 Markdown 复制到 readme 里面，就可以显示在 GitHub 上了。

关于 [Travis CI](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/) 和 [COVERALLS](https://coveralls.zendesk.com/hc/en-us/articles/201769715-Javascript-Node) 的具体的配置。请参考相应的官网的说明。

本篇文章的项目的 GitHub 地址 ：[Travis Test](https://github.com/cwxyz007/TravisTest)

到这里还不赶紧去 GitHub 上配置一波～。
