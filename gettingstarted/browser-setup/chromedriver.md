### ChromeDriver

#### 概述
[ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/) 是一个独立的服务器，它为Chromium实现了W3C WebDriver有线协议。 ChromeDriver适用于Android版Chrome和桌面版Chrome（Mac，Linux，Windows和ChromeOS）  

#### 下载

可在这个页面里 [ChromeDriver Downloads](https://sites.google.com/a/chromium.org/chromedriver/downloads) 下载各种平台的ChromeDriver。

#### Selenium Server 的用法

如果您通过Selenium Server使用ChromeDriver，只需将cli参数 `webdriver.chrome.driver` 设置为指向driver文件的位置即可。 例如：

<pre><code class="language-javascript">{
  <strong>"selenium"</strong> : {
    "start_process" : true,
    "server_path" : "./bin/selenium-server-standalone-3.{VERSION}.jar",
    "log_path" : "",
    "port" : 4444,
    "cli_args" : {
      "webdriver.chrome.driver" : "./bin/chromedriver"
    }
  }
}</code></pre>




#### Standalone 的用法

If you're only running your tests against Chrome, running ChromeDriver standalone is easier and slightly faster. Also there is no dependency on Java.

如果您只针对Chrome运行测试，则运行ChromeDriver standalone 会更容易，速度更快。 也没有依赖于Java。

这需要一点配置：<br><br>

##### 1) 首先，如果可以的话禁用Selenium Server：

<pre><code class="language-javascript">{
  <strong>"selenium"</strong> : {
    "start_process" : false
  }
}
</code></pre>


##### 2) 配置端口和默认路径前缀

ChromeDriver默认在端口9515上运行。我们还需要清除`default_path_prefix`，因为它默认设置为 `/wd/hub`，这是selenium正在使用的。

<pre><code class="language-javascript">{
  <strong>"test_settings"</strong> : {
    "default" : {
      "selenium_port"  : 9515,
      "selenium_host"  : "localhost",
      "default_path_prefix" : "",

      "desiredCapabilities": {
        "browserName": "chrome",
        "chromeOptions" : {
          "args" : ["--no-sandbox"]
        },
        "acceptSslCerts": true
      }
    }
  }
}
</code></pre>

##### 3) 启动 ChromeDriver server

管理ChromeDriver进程的最简单方法是使用 `chromedriver` [NPM软件包](https://www.npmjs.com/package/chromedriver)，它是对chromedriver文件的第三方包装。 这将抽象出chromedriver文件的下载，并且可以很容易地管理进程的启动和停止。

你可以将它添加到你的 `external globals` 文件中，如下所示：

<pre><code class="language-javascript">
var chromedriver = require('chromedriver');
module.exports = {
  before : function(done) {
    chromedriver.start();

    done();
  },

  after : function(done) {
    chromedriver.stop();

    done();
  }
};  
</code></pre>

#### 使用修正版本的ChromeDriver

在某些情况下，您可能需要使用特定版本的ChromeDriver。 例如，CI服务器运行较旧版本的Chrome。 然后你将需要一个老版本的ChromeDriver。

以下是您的全局文件可能的样子：
<br>
<pre><code class="language-javascript">
var chromedriver = require('chromedriver');
var path = require('path');
var driverInstanceCI;

function isRunningInCI() {
  return this.test_settings.globals.integration;
}

function startChromeDriver() {
  if (isRunningInCI.call(this)) {
    var location = path.join(__dirname, '../bin/chromedriver-linux64-2.17');
    driverInstanceCI = require('child_process').execFile(location, []);
    return;
  }

  chromedriver.start();
}

function stopChromeDriver() {
  if (isRunningInCI.call(this)) {
    driverInstanceCI && driverInstanceCI.kill();
    return;
  }

  chromedriver.stop();
}

module.exports = {
  'ci-server' : {
    integration : true
  },

  before : function(done) {
    startChromeDriver.call(this);

    done();
  },

  after : function(done) {
    stopChromeDriver.call(this);

    done();
  }
};</code></pre>
<br><br>

运行测试（在CI服务器上）：

<pre><code class="language-bash">$ ./node_modules/.bin/nightwatch --env ci-server</code></pre>

#### ChromeOptions
You can specify Chrome options or switches using the `chromeOptions` dictionary, under the `desiredCapabilities`. Refer to the [ChromeDriver website](https://sites.google.com/a/chromium.org/chromedriver/capabilities#TOC-chromeOptions-object) for a fill list of supported capabilities and options.

您可以在 `desiredCapabilities` 下使用 `chromeOptions` 字典指定Chrome选项或开关。请参阅 [ChromeDriver网站](https://sites.google.com/a/chromium.org/chromedriver/capabilities#TOC-chromeOptions-object) 以获取支持的功能和选项的填写列表。

#### 命令行用法

<pre><code>$ ./bin/chromedriver -h
Usage: ./bin/chromedriver [OPTIONS]

Options
  --port=PORT                     监听端口号
  --adb-port=PORT                 adb服务器端口
  --log-path=FILE                 将服务器日志写入文件而不是stderr，将日志级别提高到INFO
  --verbose                       冗长的日志
  --version                       打印版本号并退出
  --silent                        不输出日志
  --url-base                      命令的基本URL路径前缀，例如wd/url
  --port-server                   联系服务器的地址以预留端口
  --whitelisted-ips               逗号分隔的允许连接到ChromeDriver的远程IPv4地址的白名单
</code></pre>
