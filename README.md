### 原理
类似MultiDex，不过在加载过程中对一些系统函数做了hook加载，这样可以让加载更为安全一点
第一次加载可能略慢，提供了两个方案
* hook 优化函数，每次执行都不进行优化，这样每次启动的速度时间不会相差太大（这种方法兼容性差）
* 第一次启动进行优化加载，并对加载dex进行优化（并对优化后文件进行加密），第一次启动时间可能略慢。
启动时间和MultiDex相差不大。
### 动态加载方案
比如，要求某个dex插件在某个时间点加载，也可以用这个方法加载。这样可以，并且也有一定的安全性（对优化后的文件进行加密）
### 使用方法
* encrypt.x.dex 复制到Assets文件夹内（加密的）


### 参考
MultiDex的实现方法

### 存在问题
* art 模式下在首次启动时间可能会比较长(dvm不存在这种问题)，这是因为首次启动需要dex2oat 优化，但比正常的优化稍微快一点，再次启动app后，几乎没明显影响
以下做了测试：
加载三个dex分别
```
第一个 807kb 首次启动0.8秒左右
第二个 2.6m 首次启动2s 左右
第三个 8.5m 4秒左右
三个一起使用：5.3秒 左右
```
* 另外由于国内 各种os 系统改的七花八门，兼容性可能会差一点，后期慢慢优化
### 写在最后：
c语言比较菜，只能写成这样，后期慢慢优化。