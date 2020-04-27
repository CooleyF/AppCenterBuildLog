Build Step: Restore Nuget



## ``` ##[error]The nuget command failed with exit code(1) and error(NU1101: Unable to find package *******. No packages exist with this id in source(s): NuGetOrg ```
---

* Indicates Nuget files cannot be found or restored.

* There is not enough information to resolve the issue on the error alone. Further analysis on the nuget.config file is needed

#### Recommendations
---

* Review the Build Step logs for Restore Nuget
* Looking for errors, warning, and other issues that standout
    - Compare the package in the error to further isolate which file is the source of the issue.
   
    
* If this project built before, make sure to examine the previous successful build for differences which may shed light on the situation

#### If you still need to contact App Center Support
* [Recommendations for Contacting App Center Support](/AppCenterBuildLog/ContactingAppCenterSupport.html)

#### Common Problems
---
1. You are attempting to restore private Nuget feeds.
    * Explanation - When restoring private Nuget feeds the proper credentials and environment variables must be set in the nuget.config file for authentification.

    * Solution-  To restore private NuGet feeds, you include the credentials in the NuGet.config file:




            <?xml version="1.0" encoding="utf-8"?>
            <configuration>
                <packageSources>
                    <add key="nuget" value="https://api.nuget.org/v2/index.json" />
                    <add key="MyGet" value="https://www.myget.org/F/MyUsername/api/v2/index.json" />
                    <add key="MyAuthNuget" value="https://nuget.example.com/v2/index.json" />
                </packageSources>
                <activePackageSource>
                    <add key="All" value="(Aggregate source)" />
                <activePackageSource>
                <packageSourceCredentials>
                    <MyAuthNuget>
                        <add key="Username" value="myusername" />
                        <add key="ClearTextPassword" value="password" />
                    </MyAuthNuget>
                </packageSourceCredentials>
            </configuration>



    * Push changes to repo. In your build configurations via App Center portal click Save and Build. 

2. You are building a UWP Xamarin App and the same nuget feeds are accessible in both iOS and Android projects that share the current repository. 
    * Explanation - In rare occasions App Center detects the nuget.config file for iOS and android on the root level but fails to detect it for UWP projects. 
    
    * Solution - Since the UWP app does not build withe the nuget.config file in the sln project root directory, you will have to move the file into the project folder. 
    * Push changes to repo. In your build configurations via App Center portal click Save and Build.




                 
                   
                   


    

* Included in [BuildLogAnalyzer.ps1](https://github.com/tdevere/AppCenterBuildLog/blob/master/PowerShellScripts/BuildLogAnalyzer.ps1): NO