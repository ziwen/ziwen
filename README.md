#Objective-C Debug 学习
## 子文的博客
![苹果xcode图标](https://devimages.apple.com.edgekey.net/xcode/images/downloads_2x.png)
只会写代码的程序员不是好程序员，程序员是一个从制造bug到解决bug的死循环中不断成长，

	NSLog(@"Founction:%s\n Pretty founction:%s\n Line:%d\n File:%s\n Object:%@",__func__,__PRETTY_FUNCTION__, __LINE__, __FILE__, self );
   
 输出结果
 
	2015-03-11 15:33:20.316 ssss[4080:184167] 
	 Founction:-[AppDelegate application:didFinishLaunchingWithOptions:]
	 Pretty founction:-[AppDelegate application:didFinishLaunchingWithOptions:]
	 Line:19
	 File:/Users/ziwen/Desktop/artical/ssss/ssss/AppDelegate.m
	 Object:<AppDelegate: 0x7f8beb416980>
 
 
上述结果原因是 __func__, __PRETTY_FUNCTION__, __LINE__, __FILE__等都是系统预留的定义词，简单易用。

同时还有一些系统方法可以从CFString 转换为NSString。包括且不限于selector，class，protocol等，参考下面的代码：


	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSLog(@"Current selector: %@", NSStringFromSelector(_cmd));
    NSLog(@"Filename: %@", [[NSString stringWithUTF8String:__FILE__] lastPathComponent]);
    NSLog(@"object class：%@",NSStringFromClass([self class]));
    return YES;
    }

输出结果如下：


	2015-03-11 15:38:10.034 ssss[4104:186832] Current selector: application:didFinishLaunchingWithOptions:
	2015-03-11 15:38:10.034 ssss[4104:186832] Filename: AppDelegate.m
	2015-03-11 15:38:10.034 ssss[4104:186832] object class：AppDelegate
	
通过拿到字符串做一些其他操作，是不是很hi，duang，duang。
