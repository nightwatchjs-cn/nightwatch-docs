### 例子

下面的这个例子将打开 google.com, 在搜索框中对“nightwatch.js”进行搜索，然后 _clearValue_ 命令用清除输入，最后验证结果为空：

<div class="sample-test">
<pre data-language="javascript" class=" language-javascript"><code class=" language-javascript">
module.exports = {
  before : function(client) {
    // see https://github.com/nightwatchjs/nightwatch/blob/master/examples/globalsModule.js#L12
    client.globals.waitForConditionTimeout = 5000;
  },

  'clearValue example test' : function (client) {

    client
      .url('https://google.com')
      .waitForElementVisible('input[type=text]')
      .setValue('input[type=text]', 'nightwatch.js')
      .click('button[type=submit]')
      .expect.element('#rcnt').text.to.contain('nightwatchjs.org/');

    client
      .clearValue('input[type=text]')
      .expect.element('#rcnt').text.to.equal('');
  },

  after : function(client) {
    client.end();
  }
};
</code></pre>
</div>

### 输出
<div class="sample-test">
<pre data-language="javascript">
[Clear Value] Test Suite
============================

Running:  clearValue example test
 ✔ Element <input[type=text]> was visible after 68 milliseconds.
 ✔ Expected element <#rcnt> text to contain: "nightwatchjs.org/" - condition was met in 763ms
 ✔ Expected element <#rcnt> text to equal: "" - condition was met in 36ms

OK. 3 assertions passed. (7.593s)
</pre>
</div>

### 可能的错误

Here are the type of errors that you might get when using `clearValue`. Full error details are available when running nightwatch with `--verbose` flag.
当使用`clearValue`你可能会遇到这种类型的错误。在运行nightwatch的时候加上`--verbose`可以查看全部的错误详情。

- ```invalid element state``` - 如果引用的元素不可用或不显示。
- ```element not visible``` - 如果引用的元素在页面不可访问（或者被CSS隐藏，宽度为0或高度为0）。