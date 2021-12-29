---
layout: home
---

<pre style="color:#000000;background:#ffffff;"><span style="color:#800000; font-weight:bold; ">var</span> process <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> Process
<span style="color:#800080; ">{</span>
    StartInfo <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> ProcessStartInfo
    <span style="color:#800080; ">{</span>
        CreateNoWindow <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">true</span><span style="color:#808030; ">,</span>
        RedirectStandardOutput <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">true</span><span style="color:#808030; ">,</span>
        RedirectStandardInput <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">true</span><span style="color:#808030; ">,</span>
        UseShellExecute <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">false</span><span style="color:#808030; ">,</span>
        FileName <span style="color:#808030; ">=</span> <span style="color:#800000; ">@"</span><span style="color:#0000e6; ">C:\wkhtmltopdf\bin\wkhtmltopdf.exe</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span>
        Arguments <span style="color:#808030; ">=</span> <span style="color:#800000; ">@"</span><span style="color:#0000e6; ">c:\temp\1.htm c:\temp\1.pdf</span><span style="color:#800000; ">"</span>
    <span style="color:#800080; ">}</span><span style="color:#808030; ">,</span>
    EnableRaisingEvents <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">true</span>
<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
process<span style="color:#808030; ">.</span>OutputDataReceived <span style="color:#808030; ">+</span><span style="color:#808030; ">=</span> <span style="color:#808030; ">(</span>sender<span style="color:#808030; ">,</span> e<span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">&gt;</span>
<span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//Debug.Write(e.Data);</span>
<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
process<span style="color:#808030; ">.</span>Start<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
process<span style="color:#808030; ">.</span>BeginOutputReadLine<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
process<span style="color:#808030; ">.</span>WaitForExit<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
process<span style="color:#808030; ">.</span>CancelOutputRead<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
</pre>
