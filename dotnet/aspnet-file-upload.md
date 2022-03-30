---
layout: home
---

<pre style='color:#d1d1d1;background:#000000;'><span style='color:#9999a9; '>/*</span>
<span style='color:#9999a9; '>&#xa0;STANDARD FORM POST:</span>
<span style='color:#9999a9; '></span>
<span style='color:#9999a9; '>&lt;form method="post" action="/upload" enctype="multipart/form-data"></span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&lt;input type="file" name="file" /></span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&lt;input type="submit" value="submit" /></span>
<span style='color:#9999a9; '>&lt;/form></span>
<span style='color:#9999a9; '></span>
<span style='color:#9999a9; '>FETCH API:</span>
<span style='color:#9999a9; '>&lt;input type="file" name="file" /></span>
<span style='color:#9999a9; '>&lt;input type="button" value="submit" onclick="uploadFile();" /></span>
<span style='color:#9999a9; '>&lt;script></span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;function uploadFile() {</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;const data = new FormData();</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;data.append("file", document.querySelector("[name=file]").files[0]);</span>
<span style='color:#9999a9; '></span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;fetch("/upload", {</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;method: "POST",</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;body: data</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;}).then(response => {</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;response.text().then(console.log);</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;&#xa0;});</span>
<span style='color:#9999a9; '>&#xa0;&#xa0;&#xa0;&#xa0;}</span>
<span style='color:#9999a9; '>&lt;/script></span>
<span style='color:#9999a9; '></span>
<span style='color:#9999a9; '>&#xa0;*/</span>
app<span style='color:#d2cd86; '>.</span>MapPost<span style='color:#d2cd86; '>(</span><span style='color:#02d045; '>"</span><span style='color:#00c4c4; '>/upload</span><span style='color:#02d045; '>"</span><span style='color:#d2cd86; '>,</span>
    async Task<span style='color:#d2cd86; '>&lt;</span>IResult<span style='color:#d2cd86; '>></span> <span style='color:#d2cd86; '>(</span>HttpRequest request<span style='color:#d2cd86; '>)</span> <span style='color:#d2cd86; '>=</span><span style='color:#d2cd86; '>></span>
    <span style='color:#b060b0; '>{</span>
        <span style='color:#e66170; font-weight:bold; '>if</span> <span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>!</span>request<span style='color:#d2cd86; '>.</span>HasFormContentType<span style='color:#d2cd86; '>)</span>
            <span style='color:#e66170; font-weight:bold; '>return</span> Results<span style='color:#d2cd86; '>.</span>BadRequest<span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>

        <span style='color:#e66170; font-weight:bold; '>var</span> form <span style='color:#d2cd86; '>=</span> await request<span style='color:#d2cd86; '>.</span>ReadFormAsync<span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>
        <span style='color:#e66170; font-weight:bold; '>var</span> formFile <span style='color:#d2cd86; '>=</span> form<span style='color:#d2cd86; '>.</span>Files<span style='color:#d2cd86; '>[</span><span style='color:#02d045; '>"</span><span style='color:#00c4c4; '>file</span><span style='color:#02d045; '>"</span><span style='color:#d2cd86; '>]</span><span style='color:#b060b0; '>;</span>

        <span style='color:#e66170; font-weight:bold; '>if</span> <span style='color:#d2cd86; '>(</span>formFile <span style='color:#e66170; font-weight:bold; '>is</span> <span style='color:#e66170; font-weight:bold; '>null</span> || formFile<span style='color:#d2cd86; '>.</span>Length <span style='color:#d2cd86; '>=</span><span style='color:#d2cd86; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#d2cd86; '>)</span>
            <span style='color:#e66170; font-weight:bold; '>return</span> Results<span style='color:#d2cd86; '>.</span>BadRequest<span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>

        await <span style='color:#e66170; font-weight:bold; '>using</span> <span style='color:#e66170; font-weight:bold; '>var</span> stream <span style='color:#d2cd86; '>=</span> formFile<span style='color:#d2cd86; '>.</span>OpenReadStream<span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>

        <span style='color:#e66170; font-weight:bold; '>var</span> reader <span style='color:#d2cd86; '>=</span> <span style='color:#e66170; font-weight:bold; '>new</span> StreamReader<span style='color:#d2cd86; '>(</span>stream<span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>
        <span style='color:#e66170; font-weight:bold; '>var</span> text <span style='color:#d2cd86; '>=</span> await reader<span style='color:#d2cd86; '>.</span>ReadToEndAsync<span style='color:#d2cd86; '>(</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>

        <span style='color:#e66170; font-weight:bold; '>return</span> Results<span style='color:#d2cd86; '>.</span>Text<span style='color:#d2cd86; '>(</span>text<span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>
    <span style='color:#b060b0; '>}</span><span style='color:#d2cd86; '>)</span><span style='color:#b060b0; '>;</span>
</pre>
<!--Created using ToHtml.com on 2022-03-30 20:51:56 UTC -->
