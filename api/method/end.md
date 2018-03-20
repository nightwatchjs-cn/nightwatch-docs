### 概述

在幕后，`end` 命令向WebDriver服务器发送 `DELETE` 请求，传递当前的 `sessionId` 属性。
`DELETE`完成后， `sessionId` 为空。

如果未设置`sessionId`，则立即调用回调并发送完整事件。

#### 截取失败/错误的截图
如果存在测试失败或错误并且屏幕截图已启用，则在发送 `DELETE` 之前执行截图

在所需的 `test_settings` 环境下 `nightwatch.json` 中设置 `screenshots` 属性，可以开启测试失败/错误启用屏幕截图功能。 例如：

<div class="sample-test">
<pre data-language="javascript" class=" language-javascript"><code class=" language-javascript">
{
  "test_settings" : {
    "default" : {
      "screenshots" : {
        "enabled" : true,
        "on_failure" : true,
        "path" : "./screens"
      }
    }
  }
}
</code></pre>
</div>
