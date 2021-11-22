---
layout: home
---

This is for Windows only

<pre style='color:#000000;background:#ffffff;'><span style='color:#808030; '>[</span>HttpPost<span style='color:#808030; '>]</span>
<span style='color:#800000; font-weight:bold; '>public</span> JsonResult LogIn<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>string</span> userName<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>string</span> password<span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    UserResult userResult <span style='color:#808030; '>=</span> GetLoginResult<span style='color:#808030; '>(</span>userName<span style='color:#808030; '>,</span> password<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>if</span> <span style='color:#808030; '>(</span><span style='color:#808030; '>!</span>userResult<span style='color:#808030; '>.</span>Authenticated<span style='color:#808030; '>)</span>
    <span style='color:#800080; '>{</span>
        <span style='color:#800000; font-weight:bold; '>return</span> Json<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>new</span> <span style='color:#800080; '>{</span> authenticated <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>false</span> <span style='color:#800080; '>}</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>

    <span style='color:#800000; font-weight:bold; '>return</span> Json<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>new</span> <span style='color:#800080; '>{</span> authenticated <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>true</span><span style='color:#808030; '>,</span> userName <span style='color:#800080; '>}</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
<span style='color:#800080; '>}</span>

<span style='color:#800000; font-weight:bold; '>private</span> UserResult GetLoginResult<span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>string</span> userName<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>string</span> password<span style='color:#808030; '>)</span>
<span style='color:#800080; '>{</span>
    <span style='color:#800000; font-weight:bold; '>const</span> <span style='color:#800000; font-weight:bold; '>string</span> DOMAIN_NAME <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>MYDOMAIN</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>

    <span style='color:#800000; font-weight:bold; '>const</span> <span style='color:#800000; font-weight:bold; '>string</span> DisplayNameAttribute <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>DisplayName</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>const</span> <span style='color:#800000; font-weight:bold; '>string</span> SAMAccountNameAttribute <span style='color:#808030; '>=</span> <span style='color:#800000; '>"</span><span style='color:#0000e6; '>SAMAccountName</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>

    <span style='color:#800000; font-weight:bold; '>string</span> fullUserName <span style='color:#808030; '>=</span> $<span style='color:#800000; '>@"</span><span style='color:#0000e6; '>{DOMAIN_NAME}\{userName}</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
    <span style='color:#800000; font-weight:bold; '>try</span>
    <span style='color:#800080; '>{</span>
        DirectoryEntry entry <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>new</span><span style='color:#808030; '>(</span>$<span style='color:#800000; '>"</span><span style='color:#0000e6; '>LDAP://{DOMAIN_NAME}</span><span style='color:#800000; '>"</span><span style='color:#808030; '>,</span> fullUserName<span style='color:#808030; '>,</span> password<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>

        DirectorySearcher searcher <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>new</span><span style='color:#808030; '>(</span>entry<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>

        searcher<span style='color:#808030; '>.</span>Filter <span style='color:#808030; '>=</span> $<span style='color:#800000; '>"</span><span style='color:#0000e6; '>({SAMAccountNameAttribute}={userName})</span><span style='color:#800000; '>"</span><span style='color:#800080; '>;</span>
        searcher<span style='color:#808030; '>.</span>PropertiesToLoad<span style='color:#808030; '>.</span>Add<span style='color:#808030; '>(</span>DisplayNameAttribute<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        searcher<span style='color:#808030; '>.</span>PropertiesToLoad<span style='color:#808030; '>.</span>Add<span style='color:#808030; '>(</span>SAMAccountNameAttribute<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800000; font-weight:bold; '>var</span> result <span style='color:#808030; '>=</span> searcher<span style='color:#808030; '>.</span>FindOne<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800000; font-weight:bold; '>if</span> <span style='color:#808030; '>(</span>result <span style='color:#808030; '>!</span><span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>null</span><span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            <span style='color:#800000; font-weight:bold; '>var</span> displayName <span style='color:#808030; '>=</span> result<span style='color:#808030; '>.</span>Properties<span style='color:#808030; '>[</span>DisplayNameAttribute<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>var</span> samAccountName <span style='color:#808030; '>=</span> result<span style='color:#808030; '>.</span>Properties<span style='color:#808030; '>[</span>SAMAccountNameAttribute<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>

            <span style='color:#800000; font-weight:bold; '>return</span> <span style='color:#800000; font-weight:bold; '>new</span><span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>{</span> Authenticated <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>true</span><span style='color:#808030; '>,</span> UserName <span style='color:#808030; '>=</span> userName <span style='color:#800080; '>}</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>

        <span style='color:#800000; font-weight:bold; '>return</span> <span style='color:#800000; font-weight:bold; '>new</span><span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>{</span> Authenticated <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>false</span> <span style='color:#800080; '>}</span><span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>
    <span style='color:#800000; font-weight:bold; '>catch</span> <span style='color:#808030; '>(</span>Exception ex<span style='color:#808030; '>)</span>
    <span style='color:#800080; '>{</span>
        <span style='color:#800000; font-weight:bold; '>return</span> <span style='color:#800000; font-weight:bold; '>new</span><span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>{</span> Authenticated <span style='color:#808030; '>=</span> <span style='color:#800000; font-weight:bold; '>false</span><span style='color:#808030; '>,</span> Error <span style='color:#808030; '>=</span> ex<span style='color:#808030; '>.</span>ToString<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span> <span style='color:#800080; '>}</span><span style='color:#800080; '>;</span>
    <span style='color:#800080; '>}</span>
<span style='color:#800080; '>}</span>
</pre>
<!--Created using ToHtml.com on 2021-11-22 21:20:53 UTC -->

```
<PackageReference Include="Microsoft.Windows.Compatibility" Version="6.0.0" />
```