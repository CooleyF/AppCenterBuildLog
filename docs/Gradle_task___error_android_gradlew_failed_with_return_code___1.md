Build Step: Gradle Task



## ``` ##[error]Error: /Users/runner/runners/Some/Path/Here/android/gradlew failed with return code:  1 ```
---


* There is not enough information to resolve the issue on the error alone. Further analysis on the gradle files is needed

#### Recommendations
---

* Review the Build Step logs for Gradle Task
* Looking for errors, warning, and other issues that standout
    - Expiring Daemon because JVM heap space is exhausted
    - Daemon will be stopped at the end of the build after running out of JVM memory
    - > java.lang.OutOfMemoryError (no error message)
    
* If this project built before, make sure to examine the previous successful build for differences which may shed light on the situation

#### If you still need to contact App Center Support
* [Recommendations for Contacting App Center Support](/AppCenterBuildLog/ContactingAppCenterSupport.html)

#### Common Problems
---
1. If the Gradle Task build step includes line(s) with the following details
    * ` Expiring Daemon because JVM heap space is exhausted` 
    * ` Daemon will be stopped at the end of the build after running out of JVM memory`
    * ` > java.lang.OutOfMemoryError (no error message)`

    
    1. Then you are likely in one of these situations        
        * JVM has run out of native memory
        * Java heap is out of memory
            * Explanation - In a very extreme condition, you can run out of free memory while the JVM is running, and at the same time the JVM requires more memory for its internal operation (not the heap space) - then the JVM tells you it needed more memory, but could not get any, and terminates, or it will throw  `> java.lang.OutOfMemoryError (no error message) ` outright.
        
            - Solution -  Add following line to your android/gradle.properties file:



                 
                   
                   
                    // app/build.gradle
                    dexOptions {
                        javaMaxHeapSize "3g"
                        }

                    // gradle.properties
                    org.gradle.jvmargs=-Xmx4g -XX:MaxPermSize=2048m  -XX:+HeapDumpOnOutOfMemoryError-Dfile.encoding=UTF-8
                    
            * Push changes to repo. In your build configurations via App Center portal Click Save and Build.          

                    

    

* Included in [BuildLogAnalyzer.ps1](https://github.com/tdevere/AppCenterBuildLog/blob/master/PowerShellScripts/BuildLogAnalyzer.ps1): NO