# 1683、无效的推文

统计字符数是`CHAR_LENGTH（）`这个函数

<pre class="language-sql"><code class="lang-sql"><strong>SELECT 
</strong>    tweet_id
FROM 
    tweets
WHERE 
    CHAR_LENGTH(content) > 15
</code></pre>
