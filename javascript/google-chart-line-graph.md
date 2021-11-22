---
layout: home
---

<pre style='color:#000000;background:#ffffff;'><span style='color:#800000; font-weight:bold; '>var</span> scr <span style='color:#808030; '>=</span> document<span style='color:#808030; '>.</span>createElement<span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#0000e6; '>script</span><span style='color:#800000; '>"</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
scr<span style='color:#808030; '>.</span>src <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>https://www.gstatic.com/charts/loader.js</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
document<span style='color:#808030; '>.</span>body<span style='color:#808030; '>.</span>appendChild<span style='color:#808030; '>(</span>scr<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
 
<span style='color:#800000; font-weight:bold; '>var</span> div <span style='color:#808030; '>=</span> document<span style='color:#808030; '>.</span>createElement<span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#0000e6; '>div</span><span style='color:#800000; '>"</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
div<span style='color:#808030; '>.</span>id <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>curve_chart</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
div<span style='color:#808030; '>.</span>style<span style='color:#808030; '>.</span>width <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>900px</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
div<span style='color:#808030; '>.</span>style<span style='color:#808030; '>.</span>height <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>500px</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
document<span style='color:#808030; '>.</span>body<span style='color:#808030; '>.</span>appendChild<span style='color:#808030; '>(</span>div<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
 
<span style='color:#800000; font-weight:bold; '>setTimeout</span><span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>function</span><span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>{</span>
 
   google<span style='color:#808030; '>.</span>charts<span style='color:#808030; '>.</span>load<span style='color:#808030; '>(</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>current</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span> <span style='color:#800080; '>{</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>packages</span><span style='color:#800000; '>'</span><span style='color:#800080; '>:</span><span style='color:#808030; '>[</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>corechart</span><span style='color:#800000; '>'</span><span style='color:#808030; '>]</span><span style='color:#800080; '>}</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
      google<span style='color:#808030; '>.</span>charts<span style='color:#808030; '>.</span>setOnLoadCallback<span style='color:#808030; '>(</span>drawChart<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
 
      <span style='color:#800000; font-weight:bold; '>function</span> drawChart<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>{</span>
        <span style='color:#800000; font-weight:bold; '>var</span> data <span style='color:#808030; '>=</span> google<span style='color:#808030; '>.</span>visualization<span style='color:#808030; '>.</span>arrayToDataTable<span style='color:#808030; '>(</span><span style='color:#808030; '>[</span>
          <span style='color:#808030; '>[</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>date</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span> <span style='color:#800000; '>'</span><span style='color:#0000e6; '>mpg</span><span style='color:#800000; '>'</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span>
          <span style='color:#808030; '>[</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>2019-06-17</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span>  <span style='color:#008c00; '>37</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span>
          <span style='color:#808030; '>[</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>2019-06-29</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span>  <span style='color:#008c00; '>57</span><span style='color:#808030; '>]</span><span style='color:#808030; '>,</span>
          <span style='color:#808030; '>[</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>2019-07-11</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span>  <span style='color:#008c00; '>54</span><span style='color:#808030; '>]</span>
        <span style='color:#808030; '>]</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
 
        <span style='color:#800000; font-weight:bold; '>var</span> options <span style='color:#808030; '>=</span> <span style='color:#800080; '>{</span>
          title<span style='color:#800080; '>:</span> <span style='color:#800000; '>'</span><span style='color:#0000e6; '>Prius Gas Mileage</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span>
          curveType<span style='color:#800080; '>:</span> <span style='color:#800000; '>'</span><span style='color:#0000e6; '>function</span><span style='color:#800000; '>'</span><span style='color:#808030; '>,</span>
          legend<span style='color:#800080; '>:</span> <span style='color:#800080; '>{</span> position<span style='color:#800080; '>:</span> <span style='color:#800000; '>'</span><span style='color:#0000e6; '>bottom</span><span style='color:#800000; '>'</span> <span style='color:#800080; '>}</span>
        <span style='color:#800080; '>}</span><span style='color:#800080; '>;</span>
 
        <span style='color:#800000; font-weight:bold; '>var</span> chart <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>new</span> google<span style='color:#808030; '>.</span>visualization<span style='color:#808030; '>.</span>LineChart<span style='color:#808030; '>(</span>document<span style='color:#808030; '>.</span>getElementById<span style='color:#808030; '>(</span><span style='color:#800000; '>'</span><span style='color:#0000e6; '>curve_chart</span><span style='color:#800000; '>'</span><span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
 
        chart<span style='color:#808030; '>.</span>draw<span style='color:#808030; '>(</span>data<span style='color:#808030; '>,</span> options<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
      <span style='color:#800080; '>}</span>
<span style='color:#800080; '>}</span><span style='color:#808030; '>,</span> <span style='color:#008c00; '>1000</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
</pre>
<!--Created using ToHtml.com on 2021-11-22 14:09:11 UTC -->
