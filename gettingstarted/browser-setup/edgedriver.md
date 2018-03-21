### Microsoft WebDriver

#### 概述
[Microsoft WebDriver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/) 是一个独立的服务器，它为Edge浏览器实现了W3C WebDriver有线协议。它支持Windows10及以上版本。

#### 下载

Microsoft WebDriver 可以在这里 [下载](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/).

#### Selenium Server 用法

如果您通过Selenium Server使用Microsoft WebDriver，只需将cli参数 `webdriver.edge.driver` 设置为指向driver文件的位置即可。 例如：

<pre><code class="language-javascript">{
  <strong>"selenium"</strong> : {
    "start_process" : true,
    "server_path" : "bin/selenium-server-standalone-3.{VERSION}.jar",
    "log_path" : "",
    "port" : 4444,
    "cli_args" : {
      "webdriver.edge.driver" : "bin/MicrosoftWebDriver.exe"
    }
  },
  <strong>"test_settings"</strong> : {
    "default" : {
      "selenium_port"  : 4444,
      "selenium_host"  : "localhost",

      "desiredCapabilities": {
        "browserName": "MicrosoftEdge",
        "acceptSslCerts": true
      }
    }
  }
}</code></pre>


#### Standalone 用法

如果您只针对Edge运行测试，那么运行EdgeDriver standalone可能会稍微快一点，也没有依赖于Java。
您需要启动/停止EdgeDriver，这需要一点配置:<br><br>

##### 1) 首先，（如果可以）禁用Selenium服务器：

<pre><code class="language-javascript">{
  <strong>"selenium"</strong> : {
    "start_process" : false
  }
}
</code></pre>


##### 2) 配置端口和默认路径前缀
Microsoft WebDriver默认在端口9515上运行。我们还需要清除`default_path_prefix`，因为它默认设置为`/wd/hub`，这是selenium正在使用的。

<pre><code class="language-javascript">{
  <strong>"test_settings"</strong> : {
    "default" : {
      "selenium_port"  : 17556,
      "selenium_host"  : "localhost",
      "default_path_prefix" : "",

      "desiredCapabilities": {
        "browserName": "MicrosoftEdge",
        "acceptSslCerts": true
      }
    }
  }
}
</code></pre>

##### 3) 启动 MicrosoftWebDriver 服务
Windows CMD命令行下，CD 到 `MicrosoftWebDriver.exe` 文件所在的文件夹，然后运行：

<pre><code>C:\nightwatch\bin>MicrosoftWebDriver.exe
[13:44:49.515] - Listening on http://localhost:17556/
</code></pre>


完整的命令行用法：

<pre><code>C:\nightwatch\bin>MicrosoftWebDriver.exe -h
Usage:
 MicrosoftWebDriver.exe --host=<HostName> --port=<PortNumber> --package=<Package> --verbose</code></pre>

#### 实施状态
EdgeDriver尚未完成全部功能，这意味着它尚未完全符合WebDriver标准或与Selenium完全兼容。 实施状态可以在 [Microsoft WebDriver主页](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/webdriver-commands/) 上进行追踪。
