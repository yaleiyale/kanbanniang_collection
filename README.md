# live2d看板娘

资源收集自网络  

修改后的版本并不通用，应配合 [Dreamer-Paul/Pio](https://github.com/Dreamer-Paul/Pio) 使用

在移动端不显示需加入如下样式：
```css
@media only print {
    .pio-container {
        display: none;
    }
}
```
可使用如下布局查看效果：
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Dreamer-Paul/Pio@2.4/static/pio.min.css" />
<link rel="stylesheet" href="/css/live2d.css" />
<div class="pio-container right">
    <div class="pio-action"></div>
    <!-- magic params，没事不建议动 -->
    <canvas id="pio" width="272" height="272"></canvas>
</div>
<script>
    async function getSentence() {
        let res;
        await fetch('https://v1.hitokoto.cn')
            .then(response => response.json())
            .then(data => res = data.hitokoto)
            .catch(console.error)
        return res
    }
    async function initPio() {
        let sentence = await getSentence()
        let pio = new Paul_Pio({
            "mode": "fixed",
            "hidden": true,
            "content": {
                "link": ["https://github.com/yaleiyale/obsidian-jekyll-blog"],
                "skin": ["要换成我的朋友吗？", "让她放个假吧~"],
                "hidden": true,
                "welcome": sentence,
                "touch": sentence,
                "referer": "你通过 %t 来到了这里",
                "custom": [
                    { "selector": "a", "type": "link" },
                    { "selector": "#cola", "text": "打赏要理性哦😻~" },
                    { "selector": "img", "text": "点下看看吧🔍~" },
                    { "selector": ".wl-reaction", "text": "我来要赞咯🌟" },
                    { "selector": ".wl-comment", "text": "文明发言，不然会被🚫哦~" },
                    { "selector": ".highlight", "text": "代码可以一键复制呢🔖~" },
                    { "selector": ".sidebar-toggle", "text": "打开侧边栏叭🗂️~" },
                    { "selector": ".effect-info", "text": "哇，你发现了什么❗" },
                    { "selector": "#sidebar-search-input", "text": "想搜索什么呢❓" },
                    { "selector": ".note-title", "text": "这是标题~" }]
            },
            "model": [
                "https://cdn.jsdelivr.net/gh/yaleiyale/web_kanbanniang_collection@2.0/umaru/model.json",
                "https://cdn.jsdelivr.net/gh/yaleiyale/web_kanbanniang_collection@2.0/rem/model.json",
                "https://cdn.jsdelivr.net/gh/yaleiyale/web_kanbanniang_collection@2.0/koharu/model.json",
                "https://cdn.jsdelivr.net/gh/yaleiyale/web_kanbanniang_collection@2.0/kurumi/model.json",
            ]
        })
    }
</script>
<script async="async"
    src="https://cdn.jsdelivr.net/combine/gh/Dreamer-Paul/Pio@2.4/static/l2d.min.js,gh/Dreamer-Paul/Pio@2.4/static/pio.min.js"
    onload="initPio()"></script>
```