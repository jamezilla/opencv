# ios-opencv

This is a precompiled opencv framework for use with Carthage in iOS. This framework is extremely stripped down and only includes the `imgproc` and `imgcodecs` modules and excludes the i386 simulator architecture.

To use, add this to your Cartfile:
```
binary "https://raw.githubusercontent.com/jamezilla/opencv/master/opencv2.json" ~> 3.4.1
```

The iOS platform build script has the following patch to configure this build:

```
diff --git a/platforms/ios/build_framework.py b/platforms/ios/build_framework.py
index 32305f9a0..251933ba6 100644
--- a/platforms/ios/build_framework.py
+++ b/platforms/ios/build_framework.py
@@ -128,6 +128,9 @@ class Builder:
             "-DAPPLE_FRAMEWORK=ON",
             "-DCMAKE_INSTALL_PREFIX=install",
             "-DCMAKE_BUILD_TYPE=Release",
+            "-DBUILD_LIST=imgproc,imgcodecs",
+            "-DBUILD_opencv_highgui=OFF",
+            "-DBUILD_opencv_videoio=OFF",
         ] + ([
             "-DBUILD_SHARED_LIBS=ON",
             "-DCMAKE_MACOSX_BUNDLE=ON",
@@ -285,6 +288,6 @@ if __name__ == "__main__":
         ] if os.environ.get('BUILD_PRECOMMIT', None) else
         [
             (["armv7", "armv7s", "arm64"], "iPhoneOS"),
-            (["i386", "x86_64"], "iPhoneSimulator"),
+            (["x86_64"], "iPhoneSimulator"),
         ])
     b.build(args.out)
```
