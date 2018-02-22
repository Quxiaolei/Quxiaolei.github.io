# 在OC项目中使用cocos2d-x框架时的注意事项

1. 引用c++代码时,文件名改为.mm

2. 遇到未识别的String文件类型等时,将.c/.cpp文件名改为.m或者.mm,或者在预编译文件中添加

```objectivec
#   ifdef __OBJC__
#   endif
```

3. 解决onExit宏定义冲突的问题:

```objectivec
#pragma push_macro("onExit")
#undef onExit
#include "cocos2d.h"
#pragma pop_macro("onExit")
```

4. s_sharedApplication单例名为AppDelgate,会和系统的重复,所以需要新建一个文件,将单例放入

5. 在使用项目时,需要先更新本地cocos2d-x相关代码

```
cd ***/lib3rd/cocos2d-x.git
python download-deps.py
git submodule update --init
```
