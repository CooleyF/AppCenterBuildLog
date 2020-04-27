Build Step: XCode build (signed)
-
Build Step: XCode build (not signed)
-

## ``` ##[error]Error: /usr/bin/xcodebuild failed with return code: 70 ```
---

* xcodebuild [return code 70](https://developer.apple.com/library/archive/documentation/System/Conceptual/ManPages_iPhoneOS/man3/sysexits.3.html) indicates `An internal software error has been detected.  This should be limited to non-operating system related errors as possible `
* In this context, there is not enough information to resolve the issue on the error alone. Further analysis on the log files is needed

#### Recommendations
---

* Review the Build Step logs for XCode build (signed/not signed)
* Looking for errors, warning, and other issues that standout
* If this project built before, make sure to examine the previous successful build for differences which may shed light on the situation

#### If you still need to contact App Center Support
* [Recommendations for Contacting App Center Support](/AppCenterBuildLog/ContactingAppCenterSupport.html)

#### Common Problems
---
1. If the Xcode build step includes line(s) with the following details
    * ` error: exportArchive: IPA processing failed` 
    * ` Error Domain=IDEFoundationErrorDomain Code=1 "IPA processing failed" UserInfo={NSLocalizedDescription=IPA processing failed}`
        * Explanation - This indicates that your app has a dynamic library with i386 or x86_64 architecture.
        
        * Solution - A dynamic library with i386 or x86_64 architecture is not allowed when archive in Xcode 11. Those architectures must be removed from the mentioned library. This can be done by running the following command on the library in terminal:
             * lipo SmartAccessLib.a -remove x86_64 -output SmartAccessLib.a

                (Replace SmartAccessLib.a with your own static library name)
        
            * Commit changes to Repo. In your build configurations via App Center portal click Save and Build. 
    

* Included in [BuildLogAnalyzer.ps1](https://github.com/tdevere/AppCenterBuildLog/blob/master/PowerShellScripts/BuildLogAnalyzer.ps1): NO
