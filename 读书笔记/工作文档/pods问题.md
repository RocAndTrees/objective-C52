问题：


Installing BaiduMapKit (3.3.2)
Using FBSnapshotTestCase (2.1.4)
Installing YBCarBusiness 0.1.0 (was 0.1.0)
[!] The 'Pods-YBCarBusiness_Example' target has transitive dependencies that include static binaries: (/Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/thirdlibs/libcrypto.a, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/thirdlibs/libssl.a, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Base.framework, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Cloud.framework, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Location.framework, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Map.framework, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Radar.framework, /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Search.framework, and /Users/pxl/Documents/sourceTreeCode/yunbo_Module/YBCarBusiness/Example/Pods/BaiduMapKit/BaiduMapKit/BaiduMapAPI_Utils.framework)

答案：
移除 use_frameworks! 就好


