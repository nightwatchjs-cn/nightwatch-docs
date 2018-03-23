### 基础设置

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
     <td>src_folders</td>
     <td>string|array</td>
     <td>none</td>
     <td>测试所在的文件夹（不包括子文件夹）</td>
   </tr>
   <tr>
     <td>output_folder <br><span class="optional">可选项</span></td>
     <td>string</td>
     <td>tests_output</td>
     <td>JUnit XML报告文件的保存位置。</td>
   </tr>
   <tr>
     <td>custom_commands_path <span class="optional">可选项</span></td>
     <td>string|array</td>
     <td>none</td>
     <td>加载自定义命令的位置。</td>
   </tr>
   <tr>
     <td>custom_assertions_path <span class="optional">可选项</span></td>
     <td>string|array</td>
     <td>none</td>
     <td>加载自定义断言的位置。</td>
   </tr>
   <tr>
    <td>page_objects_path <br><span class="optional">可选项</span></td>
    <td>string|array</td>
    <td>none</td>
    <td>加载页面对象文件的位置。</td>
  </tr>
   <tr>
     <td>globals_path <br><span class="optional">可选项</span></td>
     <td>string</td>
     <td>none</td>
     <td>外部全局模块的位置，将作为主客户端实例上的属性 <code> globals </code>加载并提供给测试。 <br> <br>全局变量也可以在<code> test_settings </code>环境中定义/覆盖。</td>
   </tr>
   <tr>
     <td>selenium <br><span class="optional">可选项</span></td>
     <td>object</td>
     <td></td>
     <td>包含Selenium Server相关配置选项的对象，详情请参阅下文。</td>
   </tr>
    <tr>
     <td>test_settings</td>
     <td>object</td>
     <td></td>
     <td>该对象包含所有与测试相关的选项，详情请参阅下文。</td>
   </tr>
   <tr>
     <td>live_output <br><span class="optional">可选项</span></td>
     <td>boolean</td>
     <td>false</td>
     <td>并行运行时是否缓冲输出，详情请参阅下文。</td>
   </tr>
   <tr>
     <td>disable_colors <br><span class="optional">可选项</span></td>
     <td>boolean</td>
     <td>false</td>
     <td>控制是否禁用全局cli输出时有颜色。</td>
   </tr>
   <tr>
     <td>parallel_process_delay <br><span class="optional">可选项</span></td>
     <td>integer</td>
     <td>10</td>
     <td>指定以并行模式运行时启动子进程之间的延迟（以毫秒为单位）。</td>
   </tr>
   <tr>
     <td>test_workers <br><span class="optional">可选项</span></td>
     <td>boolean|object</td>
     <td>false</td>
     <td>是否并行运行单个测试文件。 如果设置为“true”，则并行运行测试并自动确定workers数量。 <br>如果设置为一个对象，可以指定workers数量为“auto”或“数字”。
       <br><br>例如：<code>"test_workers" : {"enabled" : true, "workers" : "auto"}</code></td>
   </tr>
   <tr>
    <td>test_runner <br><span class="optional">可选项</span> <span class="optional">自v0.8.0以后</span></td>
    <td>string|object</td>
    <td>"default"</td>
    <td>指定运行测试时使用哪个测试运行器，值可以是`default`（在创建nightwatch运行器）或`mocha`
      <br><br>例如：<code>"test_runner" : {"type" : "mocha", "options" : {"ui" : "tdd"}}</code></td>
    </tr>
  </tbody>
</table>
