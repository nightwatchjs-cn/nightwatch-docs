### GeckoDriver

#### 概述
[GeckoDriver](https://github.com/mozilla/geckodriver) 是一个独立的应用程序，用于与基于Gecko的浏览器（如Firefox）进行交互。 它由Rust编写并由Mozilla维护。

从Firefox 48开始，GeckoDriver是自动化Firefox的唯一方式，传统的FirefoxDriver曾经是Selenium的一部分，将不再支持，它在内部将HTTP调用转换为 [Marionette](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette), Mozilla内置于Firefox的自动化协议。

#### 下载

在这个GitHub页面可下载适合不同平台的[GeckoDriver Releases](https://github.com/mozilla/geckodriver/releases).

建议Selenium 2.x用户使用版本__v0.9__，而Selenium 3用户应该使用最新版本。

#### 用法

If you're using GeckoDriver through Selenium Server, simply set the cli argument `"webdriver.gecko.driver"` to point to the location of the binary file. E.g.:

如果您通过Selenium Server使用GeckoDriver，只需将cli参数 `webdriver.gecko.driver` 设置为指向Driver文件的位置即可，例如：

<pre><code class="language-javascript">{
  <strong>"selenium"</strong> : {
    "start_process" : true,
    "server_path" : "./bin/selenium-server-standalone-3.{VERSION}.jar",
    "log_path" : "",
    "port" : 4444,
    "cli_args" : {
      "webdriver.gecko.driver" : "./bin/geckodriver"
    }
  }
}
</code></pre>

GeckoDriver也可以用作独立应用程序，使用步骤文档在GitHub：https://github.com/mozilla/geckodriver#usage.
<br><br>
##### 命令行用法

<pre><code>$ ./bin/geckodriver-0.10 -help
geckodriver 0.10.0

USAGES:
    geckodriver-0.10 [FLAGS] [OPTIONS]

FLAGS:
        --connect-existing    连接到现有的Firefox实例
    -h, --help                打印帮助信息
        --no-e10s             在未启用多进程支持（e10s）的情况下启动Firefox
    -V, --version             打印版本信息
    -v                        设置详细程度，传递一次调试级别日志记录和两次跟踪级别日志记录

OPTIONS:
    -b, --binary <BINARY>           Path to the Firefox binary, if no binary capability provided
        --log <LEVEL>               Set Gecko log level [values: fatal, error, warn, info, config, debug, trace]
        --marionette-port <PORT>    Port to use to connect to gecko (default: random free port)
        --host <HOST>               Host ip to use for WebDriver server (default: 127.0.0.1)
    -p, --port <PORT>               Port to use for WebDriver server (default: 4444)
</code></pre>

#### Firefox Capabilities
GeckoDriver supports a capability named `firefoxOptions` which takes Firefox-specific preference values. Details are available on the GeckoDriver GitHub page: https://github.com/mozilla/geckodriver#firefox-capabilities.

#### Firefox Profile
Specifying the firefox profile can be done by setting the `profile` property in the `firefoxOptions` dictionary, as detailed above. This can be the base64-encoded zip of a profile directory and it may be used to install extensions or custom certificates.

#### Implementation Status
GeckoDriver is not yet feature complete, which means it does not yet offer full conformance with the WebDriver standard or complete compatibility with Selenium. Implementation status can be tracked on the [Marionette MDN page](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette/WebDriver/status).
