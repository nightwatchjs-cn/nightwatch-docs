### 例子

#### 1) 点击一个按钮

The example below navigates to google.com, searches for the term "nightwatch.js" and clicks the submit button.
下面的示例访问 google.com，搜索词“nightwatch.js”然后点击提交按钮。


<div class="sample-test">
<pre data-language="javascript" class=" language-javascript"><code class=" language-javascript">
module.exports = {
  before : function(client) {
    // see https://github.com/nightwatchjs/nightwatch/blob/master/examples/globalsModule.js#L12
    client.globals.waitForConditionTimeout = 5000;
  },

  'click example test' : function (client) {

    client
      .url('https://google.com')
      .waitForElementVisible('input[type=text]')
      .setValue('input[type=text]', 'nightwatch.js')
      .click('button[type=submit]', function(result) {
        this.assert.strictEqual(result.status, 0);
      })
      .expect.element('#rcnt').text.to.contain('nightwatchjs.org/');
  },

  after : function(client) {
    client.end();
  }
};
</code></pre>
</div>

#### 输出
<div class="sample-test">
<pre data-language="javascript">
[Click] Test Suite
======================

Running:  clearValue example test
 ✔ Element <input[type=text]> was visible after 67 milliseconds.
 ✔ Passed [strictEqual]: 0 === 0
 ✔ Expected element <#rcnt> text to contain: "nightwatchjs.org/" - condition was met in 768ms

OK. 3 assertions passed. (5.277s)
</pre>
</div>

#### 2) 从列表中选择一个选项

`click` 命令也用于从下拉列表中选择一个选项。以下示例是访问 https://www.w3.org 并从区域下拉列表中选择“全部”选项。

<div class="sample-test">
<pre data-language="javascript" class=" language-javascript"><code class=" language-javascript">
module.exports = {
  before : function(client) {
    // see https://github.com/nightwatchjs/nightwatch/blob/master/examples/globalsModule.js#L12
    client.globals.waitForConditionTimeout = 5000;
  },

  'click option from drop down list' : function (client) {

    client
      .url('https://www.w3.org/')
      .waitForElementVisible('#region_form')
      .click('#region_form select')
      .click('#region_form select option[value="all"]')
      .click('input[type=submit]', function(result) {
        this.assert.strictEqual(result.status, 0);
      });
  },

  after : function(client) {
    client.end();
  }
};
</code></pre>
</div>

#### 输出
<div class="sample-test">
<pre data-language="javascript">
[Click Options] Test Suite
==============================

Running:  click option from drop down list
 ✔ Element <#region_form> was visible after 64 milliseconds.
 ✔ Passed [strictEqual]: 0 === 0

OK. 2 assertions passed. (6.203s)
</pre>
</div>

### 可能的错误

- ```element not visible``` - 如果被引用的元素在页面上不可见（被CSS隐藏，宽度为0，高度为0或者不在视口内）。

运行Nightwatch时使用`--verbose`标志，可以显示完整的错误详细信息。
