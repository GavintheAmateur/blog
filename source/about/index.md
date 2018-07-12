---
layout: page
title: "About"
description: "Hey, this is Gavin."
header-img: "img/about-bg.jpg"
---

<!-- Language Selector -->
<select onchange= "onLanChange(this.options[this.options.selectedIndex].value)">
    <option value="0" selected> 中文 Chinese </option>
    <option value="1"> 英语 English </option>
</select>

<!-- Chinese Version -->
<div class="zh post-container" >
        我，爱马拉松，学游泳，准备玩铁三。
        我，不会唱歌，学钢琴，想会写手歌。
        我，是文科生，学编程，想做个网站。
        一万年太短，白驹过隙间。
        世界那么大，我想去看看。
</div>
<div class="en post-container" >
I'm a runner. I learnt swimming to race triathlon.
I can't carry a tune. I want to learn music to be a songwriter.
I major in arts. I'm learning coding to build a website.
I'm Gavin. I'm a learner.
</div>
<!-- Handle Language Change -->
<script type="text/javascript">
    var $zh = document.querySelector(".zh");
    var $en = document.querySelector(".en");
    function onLanChange(index){
        if(index == 0){
            $zh.style.display = "block";
            $en.style.display = "none";
        }else{
            $en.style.display = "block";
            $zh.style.display = "none";
        }
    }
    onLanChange(0);
</script>



{% if site.duoshuo_username %}
<!-- 多说评论框 start -->
<div class="comment">
    <div class="ds-thread"
    {% if site.duoshuo_username == "huxblog" %}
        data-thread-id="1187623191091085319"
    {% else %}
        data-thread-key="{{site.duoshuo_username}}/about"
    {% endif %}

    data-title="{{page.title}}"
    data-url="{{site.url}}/about/"></div>
</div>
<!-- 多说评论框 end -->

<!-- Duoshuo hacking -->
<!-- <input id="dsUser" type="hidden" value="{{site.duoshuo_username}}"  />-->

<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
    // dynamic User hacking by Hux
    var _user = document.getElementById('dsUser').value;
    // duoshuo comment query.
    var duoshuoQuery = {short_name: _user };
    (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();
</script>
<!-- 多说公共JS代码 end -->
{% endif %}


{% if site.disqus_username %}
<!-- disqus 评论框 start -->
<div class="comment">
    <div id="disqus_thread" class="disqus-thread">

    </div>
</div>
<!-- disqus 评论框 end -->

<!-- disqus 公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES * * */
    var disqus_shortname = "{{site.disqus_username}}";
    var disqus_identifier = "{{site.disqus_username}}/{{page.url}}";
    var disqus_url = "{{site.url}}{{page.url}}";
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<!-- disqus 公共JS代码 end -->
{% endif %}
