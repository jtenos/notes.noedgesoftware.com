---
layout: home
---

```
Protected Function GetScriptDirectoryAbsolutePath() As String
  Dim appPath As String = Request.ApplicationPath
  If (appPath = "/") Then
    appPath = String.Empty
  End If
  Return String.Format("{0}://{1}{2}/scripts/",
    Request.Url.Scheme, Request.Url.Authority, appPath)
End Function
```