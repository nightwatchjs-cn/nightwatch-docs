### Selenium 设置

以下是selenium服务器进程的诸多选项。Nightwatch可以很方便的自动启动和停止Selenium进程，因为您不必自己管理它，只需要关注测试。

如果你想启用它，把`start_process`设置为`true`，并在`server_path`内指定`jar`文件的位置。

<table class="table table-bordered table-striped">
<thead>
 <tr>
   <th style="width: 100px;">Name</th>
   <th style="width: 100px;">type</th>
   <th style="width: 50px;">default</th>
   <th>description</th>
 </tr>
</thead>
<tbody>
 <tr>
   <td>start_process</td>
   <td>boolean</td>
   <td>false</td>
   <td>是否自动管理selenium进程。</td>
 </tr>
 <tr>
  <td>start_session</td>
  <td>boolean</td>
  <td>true</td>
  <td>是否自动启动Selenium会话，运行与Selenium服务器不交互的单元/集成测试时，通常会将其设置为<code>false</code>。</td>
 </tr>

 <tr>
   <td>server_path</td>
   <td>string</td>
   <td>none</td>
   <td>如果启动<code>start_process</code>，需要指定selenium <code>jar</code> 文件的位置，例如: <code>bin/selenium-server-standalone-2.43.0.jar</code></td>
 </tr>
 <tr>
   <td>log_path</td>
   <td>string|boolean</td>
   <td>none</td>
   <td>selenium <code> output.log </code>文件的放置位置，默认为当前目录。要禁用Selenium日志记录，将其设置为<code> false </code> </td>
 </tr>
 <tr>
   <td>port</td>
   <td>integer</td>
   <td>4444</td>
   <td>Selenium监听端口号</td>
 </tr>
 <tr>
   <td>cli_args</td>
   <td>object</td>
   <td>none</td>
   <td>将传递给Selenium进程的cli参数列表，在这里您可以为浏览器驱动程序设置各种选项，例如：<br><br>
     <ul>
       <li>
         <code>webdriver.firefox.profile</code>:Selenium将默认为每个会话创建一个新的Firefox配置文件。如果你想使用现有的Firefox配置文件，你可以在这里指定它的名字<br>可用的Firefox驱动程序参数完整列表在<a href="https://github.com/SeleniumHQ/selenium/wiki/FirefoxDriver" target="_blank">这里</a>.
       </li>
       <li>
         <code>webdriver.chrome.driver</code>: Nightwatch同样也可以使用 <strong>Chrome</strong> 浏览器. 要启用此功能，你可以在这里 <a href="http://chromedriver.storage.googleapis.com/index.html" target="_blank">下载ChromeDriver</a>。另外不要忘记在<code>desiredCapabilities</code>对象中指定chrome作为浏览器名称。<br>
     更多信息可以在 <a href="https://sites.google.com/a/chromium.org/chromedriver/" target="_blank">ChromeDriver 网站</a> 上找到。<br>
       </li>
       <li>
         <code>webdriver.ie.driver</code>:
         Nightwatch也支持 <strong>Internet Explorer</strong>. 启用此功能在这里下载<a href=
         "https://github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver" target="_blank">IE Driver binary</a>.
     同样不要忘了在<code>desiredCapabilities</code>对象中指定"internet explorer"作为浏览器名称。
       </li>
     </ul>
   </td>
 </tr>
 </tbody>
</table>
