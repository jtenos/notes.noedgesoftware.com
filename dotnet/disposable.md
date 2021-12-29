---
layout: home
---

<pre style="color:#000000;background:#ffffff;">public class Something <span style="color:#800080; ">:</span> IDisposable
<span style="color:#800080; ">{</span>
<span style="color:#004a43; ">&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#004a43; ">#</span><span style="color:#004a43; ">region Disposable</span>
    private bool _disposed<span style="color:#800080; ">;</span>
    
    <span style="color:#800000; font-weight:bold; ">void</span> IDisposable<span style="color:#808030; ">.</span>Dispose<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
    	Dispose<span style="color:#808030; ">(</span>true<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    	GC<span style="color:#808030; ">.</span>SuppressFinalize<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800080; ">}</span>
    
    protected <span style="color:#800000; font-weight:bold; ">void</span> Dispose<span style="color:#808030; ">(</span>bool disposing<span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
    	<span style="color:#800000; font-weight:bold; ">if</span> <span style="color:#808030; ">(</span><span style="color:#808030; ">!</span>_disposed<span style="color:#808030; ">)</span>
    	<span style="color:#800080; ">{</span>
    		<span style="color:#800000; font-weight:bold; ">if</span> <span style="color:#808030; ">(</span>disposing<span style="color:#808030; ">)</span>
    		<span style="color:#800080; ">{</span>
    			DisposeManagedResources<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    		<span style="color:#800080; ">}</span>
    
    		DisposeUnmanagedResources<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    		_disposed <span style="color:#808030; ">=</span> true<span style="color:#800080; ">;</span>
    	<span style="color:#800080; ">}</span>
    <span style="color:#800080; ">}</span>
    
    protected virtual <span style="color:#800000; font-weight:bold; ">void</span> DisposeManagedResources<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
    <span style="color:#800080; ">}</span>
    
    protected virtual <span style="color:#800000; font-weight:bold; ">void</span> DisposeUnmanagedResources<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
    <span style="color:#800080; ">}</span>
    
    <span style="color:#808030; ">~</span>Something<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
    	Dispose<span style="color:#808030; ">(</span>false<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800080; ">}</span>
<span style="color:#004a43; ">&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#004a43; ">#</span><span style="color:#004a43; ">endregion</span>
<span style="color:#800080; ">}</span>
</pre>
