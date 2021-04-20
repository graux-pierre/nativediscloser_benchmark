# Native Bridge Benchmark
This benchmark includes a bunch of Android apps which utilize native code to bridge invocations between Java methods. 

Since, for most of Android analysis tools, native analysis is rarely implemented. Such a bridge scenario will lead to incomplete analysis result. In order to overcome this barrier, the native part of an Android app (i.e., *\*.so* files in each APK) needs to be analyzed.

The apps in this benchmark includes both self-developed apps as well as some open-sourced apps from [*F-Droid*](https://www.f-droid.org/). For self-developed apps, on one hand, we try to make it simple to understand and easy to be verified. On the other hand, they have to cover different scenarios.

So far, there are 16 self-developed apps which are the apps with name started with "native_disclosure_bm". The scenarios they implemented are described below:

+ bm1: it uses both static and dynamic JNI function registration, 1 JNI function invokes an Android Java API, and the Java API method is obtained via a passed in Java object.
+ bm2: based on *bm1*, changed it to use only dynamic JNI function registration.
+ bm3: based on *bm1*, changed it to use only static JNI function registration.
+ bm4: based on *bm1*, the JNI API function `RegisterNatives` for dynamic registration is further wrapped up with a customized C function.
+ bm5: based on *bm4*, the wrapper function is further put into a header file (i.e., *\*.h* file).
+ bm6: based on *bm1*, instead of passing Java object, used Java `this` object to obtain relevant Java APIs.
+ bm7: based on *bm1*, used chained invocation of C functions to realize dynamic registration and Java API invocation.
+ bm8: based on *bm1*, added logic controls (i.e., if-else and switch-case) when invocation Java methods.
+ bm9: based on *bm1*, implemented string constant obfuscation to all strings.
+ bm10: based on *bm1*, passed components to invoke certain Java methods (i.e., objects of `jobject`, `jclass` and `jmethodID`) via a customized C structure.
+ bm11: based on *bm1*, access all strings via C macro.
+ bm12: based on *bm1*, for the one dynamically registered C JNI function, mapped it to 2 different Java native methods.
+ bm13: within 1 C JNI function (i.e., `sinkImei`), there are 3 chained invocations to different Java methods.
+ bm14: based on *bm1*, added more strings of methods and classes but not used to invoke. 
+ bm15: based on *bm1*, using relevant strings from string arrays.
+ bm16: based on *bm1*, get relevant strings by invoking methods of a C++ class with returns of different string representations.

All self-developed apps are executable and tested with a Nexus 5 device with Android version 8.1.0.

The rest apps are open-sourced apps from *F-Droid*. We only investigated the latest version of each app and selected all APKs containing *\*.so* files. Furthermore, we manually checked each selected apps and noticed that most of the apps are developed with FaceBook's [React Native](https://reactnative.dev/docs/getting-started) which is a framework for JavaScript developers to develop apps for different platforms including Android. For such apps, even they commonly contain *\*.so* files, these *\*.so* files are generated by the framework and hard to manually investigate. Therefore, for such apps, they are not presented as benchmark apps.

We finally selected 3 *F-Droid* apps as benchmark and investigated them manually. We describe the investigation result for each app as following:

+ Overchan-Android: Open source application from FDroid. In this app, there is 1 back invocation (i.e., invocation Java methods from native libraries) spotted. However, the relevant java class and object are passed via a customized C structure. Since the structure cannot be parsed, the relevant class cannot be obtained.
