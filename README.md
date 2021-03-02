This benchmark is a bunch of self-developed Android apps to verify the native
library analysis tool.
This benchmark cover scenarios listed below:
+ statically exported JNI functions.
+ dynamically exported JNI functions.
+ mixed static and dynamic exportation of functions.
+ using wrapped "RegisterNatives" functions.
+ with/without removed symbols of dynamically exported JNI functions.
+ certain functions (e.g., wrapper function of "RegisterNatives") and/or variables (e.g., "JNINativeMethod" variable for "RegisterNatives" function) stored in "*.h" files.
+ implement various depth of invocation in exported JNI functions and "JNI_OnLoad" functions to test the reachability of the tool.
+ obfuscation of relevant string constants.
+ cases with control of logic statement (e.g., if-else, switch).
+ cover all different kinds of relevent JNI API functions (e.g., "FindClass" and "GetObjectClass" to get Java class).
+ maybe test cases with loops.
+ maybe test cases with class-encapsulation of certain relevant JNI API functions and/or variables by coding in C++ instead of C.
