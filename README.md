用命令行交叉编译Android Arm so包

1 先使用/home/hm/android_ndk_r15c/build/tools下的 make-standalone-toolchain.sh 脚本生成独立的交叉编译工具链
  具体用法可用 --help 参数查看帮助，主要是输入几个参数。
  其中 --toolchain 参数用于设置要使用的编译链, 在 $NDK/toolchains 目录下可以看到所有支持的编译链工具，根据需要选择
  参考：https://my.oschina.net/gotax/blog/516861?fromerr

2 然后在CMakeLists.txt文件中配置与android相关的参数
3 最后执行 cmake, 再执行 make，so包应该就出来了。
