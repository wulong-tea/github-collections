一个千万量级的APP使用的一些第三方库

.背景
前段时间在调研第三方推送服务的时候，反编译了一部分市面上比较流行的APP。其中一个无论是在设计还是功能上都堪称典型，这款APP总用户数超千万(其官网数据)，在国内某手机助手上支持率超97%。可见其受欢迎程度（APP的名字就不说了）。反编译这个APP后发现其使用的第三方库也很有代表性。这里介绍下他们使用的这些第三方库，给需要的童鞋一些参考。

1.Android Design Support Library
这个并不是一个第三方库，是谷歌官方出的支持库。之所以列出来除了上面说的这个APP有使用到它外，更多的是因为这个库很强大~

这个库和github上的很多开源项目是有很大关系的，material design的很多效果，同一种效果在github上有太多的实现，现在官方把部分效果标准化了。
这里注意不要和兼容库Android Support Library 混淆，虽然都是兼容库，但区别还是很大的。
Android Design Support Library详细介绍点这里
Android Support Library 官方文档翻译
2. butterknife
这个库应该大家都耳熟能详了，大牛JakeWharton的作品，github上star数量超一万，可见其受欢迎程度。

这个开源库可以让我们从大量的findViewById()和setOnclicktListener()解放出来，其对性能的影响微乎其微，其自定义注解的实现都是限定为RetentionPolicy.CLASS，也就是注解到编译出.class文件为止有效，在运行时不额外消耗性能。

Instead of slow reflection, code is generated to perform the view look-ups. Calling bind delegates to this generated code that you can see and debug.
有人觉得使用了这个库之后代码的可读性差一些，这个真心不认同，相反，使用过后反倒代码量少了好多，更清爽简洁了。

关于编译时注解效率的问题可以看下这篇文章关于java编译时注解你需要知道的二三事。解除你的顾虑!

这个库在Android Studio上配合android-butterknife-zelezny使用更酸爽！

3.fastjson，gson
这两个JSON序列化与反序列化库应该都熟悉的了，fastjson是阿里的，gson是Google的，基本功能都差不多，至于为什么两个库都出现在这个APP里面，应该是APP版本的各个开发者使用习惯不一样吧，也有可能是使用的一些第三方库依赖其中一种的原因。

这里要提一下的是fastjson号称是Java语言中最快的JSON库,而且有专门针对Android精简和优化的版本，体积减少了近一半。因为体积更大，为避免出现64K方法数限制而弃用fastjson的理由应该不再成立。fastjson Android版本

不过也许是因为gson是Google官方出的，文档什么的也更详细，gson在APP内出现的频率还是更高的。

4.picasso
A powerful image downloading and caching library for Android
这个是square 开源的一个强大的图片下载和缓存库。很受欢迎，许多项目都有在使用这个库。使用方式也很简单。

关于图片加载库现在比较流行的还有Glide和Fresco。

Glide
Google员工私人项目，Google很多项目在用。picasso能做到的它都能做到，并且还支持gif。我在公司的项目中也使用的是这个库。不过注意在使用这个库给ImageView加载图片的时候，ImageView设置 Tag的Id必须显式指定。

关于Glide和Picasso这篇译文有一个比较详细的对比介绍 Glide VS Picasso(打算使用Glide的话注意看下这篇文章下面的评论)

Fresco
这个是FaceBook的开源项目，上面链接中有中文的详细文档。这个库除了支持的图片格式很广泛外，最大的特性就是在内存优化这块，使用这个库能有效防止OOM情况的出现。

在5.0以下系统，Bitmap缓存位于ashmem，这样Bitmap对象的创建和释放将不会引发GC，更少的GC会使你的APP运行得更加流畅。
5.0及其以上系统，相比之下，内存管理有了很大改进，所以Bitmap缓存直接位于Java的heap上。
当应用在后台运行时，该内存会被清空。
不过这个库非主流强大的功能使得这个库体积有2M之大，使用起来也有点不太方便。

最后，如果你还在用Android-Universal-Image-Loader这个老牌库，建议尽早替换掉它，这个库已经停止更新了。而且无论是使用体验还是性能都没有以上库好。

Really have no time for development... so I stop project maintaining since Nov 27 :(
5.PullZoomView
An Android custom ListView and ScrollView with pull to zoom-in.
这个直接上效果图了


PullZoomView效果图.gif
6.SwipeBackLayout
An Android library that help you to build app with swipe back gesture.
一个能帮我们轻松实现右滑退出当前页面功能的库，这个库也有使用在我们公司的项目中，不过花了不少时间在处理兼容性问题上(有时间的话会把填过的坑分享出来)。

这里有必要再提一下这个库在手势处理方面使用到的ViewDragHelper，非常有用的一个工具类。

ViewDragHelper is a utility class for writing custom ViewGroups. It offers a number
of useful operations and state tracking for allowing a user to drag and reposition
views within their parent ViewGroup.
具体可以看下这篇文章Android ViewDragHelper完全解析 自定义ViewGroup神器


swipeBackLayout.png
7.okhttp okio
这个库也是square开源的一个网络请求库(okhttp内部依赖okio)。据说现在已被Google使用在Android源码上了，可见其强大。

这里有一个大神张鸿洋开源的okhttp封装库okhttp-utils

关于网络请求库，现在应该还有很多人在使用android-async-http。他内部使用的是HttpClient，但是Google貌似在6.0版本里面删除了HttpClient相关API，可见这个库现在有点过时了。

不过我在android-async-http的官方Wiki上发现了这个:


android-async-http_Wiki.png
8.volley
这个库也应该比较熟悉了，Google官方出的一个库，包含网络请求和图片加载缓存功能。在处理小而频繁的网络请求上有优势。

以前使用这个库一般都是添加第三方依赖，比如android-volley 。现在已经有官方Gradle依赖了 。

compile 'com.android.volley:volley:1.0.0'
9.PagerSlidingTagStrip
Interactive paging indicator widget, compatible with the ViewPager from the Android Support Library.
这个库使用比较也比较广泛，实现ViewPage和顶部指示器联动滑动的效果。


pagerSlidingTabStrip.png
10.Android-PickerView
仿iOS的PickerView控件，有时间选择和选项选择并支持一二三级联动效果
这个库的作者还有另外几个开源库也很不错的，有兴趣的可以点上面链接去他的github上看下。


pickerdemo.gif
11.packer-ng-plugin
下一代Android打包工具，1000个渠道包只需要5秒
这个库的作者mcxiaoke在下文还会出现的。

12.NineOldAndroids
Android library for using the Honeycomb animation API on all versions of the platform back to 1.0!

NineOldAndroids is deprecated. No new development will be taking place. Existing versions will (of course) continue to function. New applications should use minSdkVersion="14" or higher which has access to the platform animation APIs.
Thanks for all your support!
View的属性动画在Android API 11及其以后才支持，该库的作用就是让API 11以下的系统也能够正常的使用属性动画。不过该库作者Jake Wharton(是的，又是这位大神)认为现在APP支持的最低版本应该是4.0了，所以不再更新了。

13.Logger
Simple, pretty and powerful logger for android
像作者说的一样，简单，漂亮，强大的一款日志打印工具。


custom-tag.png
14.materialish-progress
A material style progress wheel compatible with 2.3

spinningwheel.gif
15.七牛
七牛云存储,是专为移动时代开发者打造的数据管理平台，为互联网网站和移动App提供数据的在线托管、传输加速以及图片、音视频等富媒体的云处理服务。(来自百度百科)
说到数据管理平台,我就会忍不住想到leancloud,大学那会弄毕设有使用到它，文档对开发者非常友好，一直印象很深刻。

16.shareSDK
ShareSDK是为iOS、Android的App提供社会化功能的一个组件，帮助开发者实现社会化分享、登录、关注、获得用户资料、获取好友列表等主流的社会化功能。
17.友盟+
这里应该是用到了友盟的数据统计分析服务以及自动更新服务，不过要注意的是自动更新服务官方已经发声明表示停止新注册的APP和当前不再使用该功能的APP接入这项服务，已经在使用的在2016年10月15日之后也要停止服务了。

18.ViewPagerIndicator
Paging indicator widgets compatible with the ViewPager from the Android Support Library and ActionBarSherlock.
这个库的作者是Jake Wharton(没看错，还是这位大神)，功能和上面介绍的PagerSlidingTagStrip类似，一般与viewpager组合使用。用法看这里


viewPagerIndicator.png
19.小米推送
小米推送服务支持所有Android平台，在MIUI上属于系统服务框架，共享系统级长连接。
共享系统级连接可以这么理解，理论上不管应用是否在后台运行，只要有网，就能收到推送。这个应该是此APP选择小米推送的重要原因。在MIUI系统上，相比其它第三方推送有先天优势。

20.greenDAO
greenDAO is a light & fast ORM solution for Android that maps objects to SQLite databases. Being highly optimized for Android, greenDAO offers great performance and consumes minimal memory.
在所有将对象映射到 SQLite 数据库中的 ORM 库中，greenDAO 在性能方面占很大优势。而且文档也很详细。

不过最近有一个比较火的跨平台移动数据库引擎realm，支持iOS、OS X（Objective-C和Swift）以及Android。性能比原生的SQLite还要好。目标是要取代SQLite。可以多关注下。

Realm is a mobile database: a replacement for Core Data & SQLite
21.CircleImageView
一个使用很广泛的圆形图片库


CircleImageView.png
22.Crouton
I won't do any active development for Crouton any more. But I still do accept pull requests that fix bugs.
So long, and thanks for all the forks.
这个库功能类似于SnackBar,因为官方已经出了SnackBar，所以作者停止了继续更新这个库。

关于SnackBar的用法 看这里

23.BarcodeScanner
Android library projects that provides easy to use and extensible Barcode Scanner views based on ZXing and ZBar.
一个基于ZXing和ZBar的容易使用和扩展的条形码扫描库

scanner.png
24.Rxjava
从去年开始，RxJava+的文章就一直在国内网站各种刷屏了，最近还看到有公司招聘直接要求熟悉使用RxJava+Retrofit+OkHttp3了，可见其受欢迎程度。虽然这个库的学习成本有点大，好在现在关于它的学习资料也很丰富。

很多RxJava的初学者应该都有看过扔物线的这篇文章 给Android 开发者的 RxJava 详解。
还有上面提到的mcxiaoke组织翻译的文档ReactiveX/RxJava文档中文版。

25.PhotoView
Implementation of ImageView for Android that supports zooming, by various touch gestures.
支持通过各种手势来缩放图片的一个库，现在很多的APP内都有使用到这个库，很受欢迎。

最后
