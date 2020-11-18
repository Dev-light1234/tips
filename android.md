[Build Tools] flex is too old for newer distributions
-

### Error code

```
FAILED: out/host/linux-x86/obj/EXECUTABLES/checkpolicy_intermediates/policy_scan.c 
/bin/bash -c "prebuilts/misc/linux-x86/flex/flex-2.5.39 -oout/host/linux-x86/obj/EXECUTABLES/checkpolicy_intermediates/policy_scan.c external/selinux/checkpolicy/policy_scan.l"
flex-2.5.39: loadlocale.c:130: _nl_intern_locale_data: Assertion `cnt < (sizeof (_nl_value_type_LC_TIME) / sizeof (_nl_value_type_LC_TIME[0]))' failed.
```

### Description
This problem is well-known and can be fixed by replacing the prebuilt flex tool with a newer version

### Solution 1

Set the locale to C before executing make:

    LC_ALL=C make
This solution is simple and most people use it. **But** in many situations it doesn't work and I recommend the soccend solution.

### Solution 2

Just rebuild it manually.
```
cd prebuilts/misc/linux-x86/flex
rm flex-2.5.39
tar zxf flex-2.5.39.tar.gz
cd flex-2.5.39
./configure
make
mv flex ../
cd ../
rm -rf flex-2.5.39
mv flex flex-2.5.39
```
***
<https://groups.google.com/forum/#!topic/android-building/0kzPnw3akxg>   
<https://github.com/sonyxperiadev/bug_tracker/issues/136>
