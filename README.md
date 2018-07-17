# ios-opencv

This is a precompiled opencv framework for use with Carthage in iOS. This framework is extremely stripped down and only includes the `imgproc` and `imgcodecs` modules and excludes the i386 simulator architecture.

To use, add this to your Cartfile:
```
binary "https://raw.githubusercontent.com/jamezilla/opencv/master/opencv2.json" ~> 3.4.1
```
