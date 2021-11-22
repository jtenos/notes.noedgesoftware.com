---
layout: home
---

```
const string LDAP_PATH = "LDAP://";
const string DOMAIN_NAME = "MYDOMAIN";

User user = Login(username, password);
if (user == null) { return Unauthorized(); }
if (!user.Authenticated) 
{ 
    ModelState.AddModelError("", "Invalid credentials"); 
    return View();
}

User Login(string username, string password)
{
    User userResult = new();
    string fullLoginName = $"{DOMAIN_NAME}\{username}";

    try
    {
        DirectoryEntry entry = new(${LDAP_PATH}{DOMAIN_NAME}, 
            fullLoginName, password);

        DirectorySearcher searcher = new(entry);
                
        searcher.Filter = $"({SAMAccountNameAttribute}={username})");
        searcher.PropertiesToLoad.Add("DisplayName");
        searcher.PropertiesToLoad.Add("SAMAccountName");
        var result = searcher.FindOne();
        if (result != null)
        {
            var displayName = result.Properties["DisplayName"];
            var samAccountName = result.Properties["SAMAccountName"];

            userResult.DisplayName = displayName == null || !displayName.Any() ? null : displayName[0].ToString();
            userResult.UserName = samAccountName == null || !samAccountName.Any() ? null : samAccountName[0].ToString();
            userResult.Authenticated = true;
        }
        else
        {
            userResult.Authenticated = false;
        }
    }
    catch (Exception ex)
    {
        userResult.Error = ex.ToString();
        userResult.Authenticated = false;
    }
    return userResult;
}

<PackageReference Include="Microsoft.Windows.Compatibility" Version="3.1.0" />
```