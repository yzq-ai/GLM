![glm](/doc/manual/logo-mini.png)


[OpenGL Mathematics](http://glm.g-truc.net/) (*GLM*)是一个C++数学库，专为图形软件而设计，基于[OpenGL Shading Language (GLSL) specifications](https://www.opengl.org/registry/doc/GLSLangSpec.4.50.diff.pdf)规范。*GLM* 提供了类和函数，使用相同的命名约定和功能，因此任何了解*GLSL*的人都可以在C++中使用GLM。

除了*GLSL*的特性外，该项目还提供了一个扩展系统，基于*GLSL*扩展惯例，提供了更多的功能：矩阵变换、四元数、数据打包、随机数、噪声等。

*GLSL*与*[OpenGL](https://www.opengl.org)*完美配合，但也确保与其他第三方库和SDK的互操作性。它是软件渲染（光线追踪/栅格化）、图像处理、物理模拟以及任何需要简单方便的数学库的开发环境的良好选择。

*GLM*使用C++98编写，但在编译器支持时可以利用C++11。它是一个独立于平台的库，没有依赖项，并官方支持以下编译器：

- [Apple Clang 6.0](https://developer.apple.com/library/mac/documentation/CompilerTools/Conceptual/LLVMCompilerOverview/index.html) 及更高版本
- [GCC](http://gcc.gnu.org/) 4.7 及更高版本
- [Intel C++ Composer](https://software.intel.com/en-us/intel-compilers) XE 2013 及更高版本
- [LLVM](http://llvm.org/) 3.4 及更高版本
- [Visual C++](http://www.visualstudio.com/) 2013 及更高版本
- [CUDA](https://developer.nvidia.com/about-cuda) 7.0 及更高版本 (实验版)
- 任何C++11编译器
- 
有关*GLM*的更多信息，请参阅[手册](manual.md)和[API参考文档](http://glm.g-truc.net/0.9.8/api/index.html)。源代码和文档在[Happy Bunny License (Modified MIT) 或MIT License下获得许可](manual.md#section0)

感谢您通过[提交问题](https://github.com/g-truc/glm/issues)（bug报告和功能请求）为项目做出贡献。任何反馈都欢迎发送至[glm@g-truc.net](mailto://glm@g-truc.net)。


```cpp
#include <glm/vec3.hpp> // glm::vec3
#include <glm/vec4.hpp> // glm::vec4
#include <glm/mat4x4.hpp> // glm::mat4
#include <glm/ext/matrix_transform.hpp> // glm::translate, glm::rotate, glm::scale
#include <glm/ext/matrix_clip_space.hpp> // glm::perspective
#include <glm/ext/constants.hpp> // glm::pi

glm::mat4 camera(float Translate, glm::vec2 const& Rotate)
{
	glm::mat4 Projection = glm::perspective(glm::pi<float>() * 0.25f, 4.0f / 3.0f, 0.1f, 100.f);
	glm::mat4 View = glm::translate(glm::mat4(1.0f), glm::vec3(0.0f, 0.0f, -Translate));
	View = glm::rotate(View, Rotate.y, glm::vec3(-1.0f, 0.0f, 0.0f));
	View = glm::rotate(View, Rotate.x, glm::vec3(0.0f, 1.0f, 0.0f));
	glm::mat4 Model = glm::scale(glm::mat4(1.0f), glm::vec3(0.5f));
	return Projection * View * Model;
}
```

## [最新发布](https://github.com/g-truc/glm/releases/latest)

## 项目 安全

| 服务 | 系统 | 编译器 | 状态 |
| ------- | ------ | -------- | ------ |
| [Travis CI](https://travis-ci.org/g-truc/glm)| MacOSX, Linux 64位	| 	Clang 3.6, Clang 5.0, GCC 4.9, GCC 7.3 | [![Travis CI](https://travis-ci.org/g-truc/glm.svg?branch=master)](https://travis-ci.org/g-truc/glm)
| [AppVeyor](https://ci.appveyor.com/project/Groovounet/glm)| Windows 32位和64位 | Visual Studio 2013, Visual Studio 2015, Visual Studio 2017 | [![AppVeyor](https://ci.appveyor.com/api/projects/status/32r7s2skrgm9ubva?svg=true)](https://ci.appveyor.com/project/Groovounet/glm)

## 发布说明

### [GLM 0.9.9.4](https://github.com/g-truc/glm/tree/master) - 2018-1X-XX
#### 改进:
- 添加GLM_FORCE_INTRINSICS以启用SIMD指令代码路径。默认情况下，它是禁用的，允许constexpr支持.

#### 修复:
- 修复mat4x3转换中的错误 #829

### [GLM 0.9.9.3](https://github.com/g-truc/glm/releases/tag/0.9.9.3) - 2018-10-31
#### 特性:
- 为标量数值添加max ULPs参数的equal和notEqual重载 #121
- 添加GLM_FORCE_SILENT_WARNINGS以在使用语言扩展但使用W4或Wpedantic警告时静默GLM警告 #814 #775
- 在GTX_matrix_operation中添加adjugate函数 #151
- 添加GLM_FORCE_ALIGNED_GENTYPES以启用对齐类型和不启用SIMD指令。这将禁用constexpr #816

#### 改进:
- 添加浮点数之间常量时间ULP距离 #121
- 添加GLM_FORCE_SILENT_WARNINGS以抑制GLM警告 #822

#### 修复:
- 修复double类型构建简单噪声 #734
- 根据GLSL规范修复bitfieldInsert #818
- 修复当'k'为负数时的折射情况 #808

### [GLM 0.9.9.2](https://github.com/g-truc/glm/releases/tag/0.9.9.2) - 2018-09-14
#### 修复:
- 修复手册中的GLM_FORCE_CXX**部分
- 修复使用GLM_FORCE_CTOR_INIT来进行向量和四元数类型的默认初始化 #812

### [GLM 0.9.9.1](https://github.com/g-truc/glm/releases/tag/0.9.9.1) - 2018-09-03
#### 特性:
- 在GTC_bitfield中添加bitfieldDeinterleave
- 在GTC_quaternion中为四元数类型添加带有epsilon的equal和notEqual
- 添加EXT_matrix_relational：矩阵类型的equal和notEqual带有epsilon
- 在GTC_type_aligned中添加丢失的对齐矩阵类型
- 添加C++17检测
- 添加Visual C++语言标准版本检测
- 从markdown构建添加PDF手册

#### 改进:
- 添加一个章节手册，以便于贡献代码
- 重构手册，列出了所有配置宏
- 添加了vec1的构造函数
- 改良了constexpr支持，同时排除了SIMD和constexpr #783
- 添加了对Visual C++ 2017工具集的检测
- 添加了identity函数 #765
- 将头文件分离成了EXT扩展，以改善编译时间 #670
- 添加了单独的性能测试
- 澄清了折射率索引的有效范围，为-1至1（包括1）之间 #806


#### 修复:

- 修复了Clang和GCC上的SIMD检测问题
- 由于printf和std::clock_t而解决构建问题 #778
- 修复了int mod
- 匿名联合需要C++语言扩展
- 修复了ortho #790
- 修正了Visual C++ 2013在向量运算代码中的警告 #782
- 修复了constexpr在ICC中的构建错误 #704
- 修复了默认的operator=和构造函数 #791
- 修复了使用SSE指令时从int标量到vec4构造函数的错误转换
- 在使用负半径值时，在随机函数中添加了assert函数，以防止无限循环 #739






### [GLM 0.9.9.0](https://github.com/g-truc/glm/releases/tag/0.9.9.0) - 2018-05-22
此版本的 GLM 增加了许多特性和改进，并修复了一些问题。值得一提的是，GLM 现在需要 Visual Studio 2013、GCC 4.7、Clang 3.4、Cuda 7、ICC 2013 或 C++11 编译器。
#### 特性:

- 在 GTC_packing 中增加了 RGBM 编码。
- 增加了 GTX_color_encoding 扩展。
- 增加了 GTX_vec_swizzle，比 swizzle 运算符更快的编译时间切换。
- 在 GTX_exterior_product 中添加了一个 vec2 叉积实现。
- 添加了 GTX_matrix_factorisation 以分解各种形式的矩阵。 
- 添加了 [GLM_ENABLE_EXPERIMENTAL](manual.md#section7_4) 以启用实验特性。
- 为整数向量添加了打包函数。
- 添加了 conan 打包配置。
- 在 GTX_quaternion 中增加了 quatLookAt。
- 在 GTX_extended_min_max 中增加了 fmin、fmax 和 fclamp。
- 为 EXT_vector_relational 增加了扩展：将 equal 和 notEqual 扩展到带有 epsilon 参数的情况。
- 为 EXT_vector_relational 增加了 openBounded 和 closeBounded。
- 添加了 EXT_vec1：*vec1 类型。
- 添加了 GTX_texture：levels 函数。
- 为使用负一和零附近剪辑平面增加了分离函数。
-  添加了 GLM_FORCE_SINGLE_ONLY 以在不支持 double 的平台上使用 GLM。
- 添加了 GTX_easing 以进行插值函数。

#### 改进:

- 不再默认初始化向量、矩阵和四元数类型。
- 在 GTC_color_space 中添加了低精度变体 convertLinearToSRGB。
- 用 markdown 版本替换了手册。
- 改善了 API 文档。
- 优化了 GTC_packing 实现。
- 优化了 GTC_noise 函数。
- 优化了 GTC_color_space HSV 到 RGB 转换。
- 优化了 GTX_color_space_YCoCg YCoCgR 转换。
- 优化了 GTX_matrix_interpolation axisAngle 函数。
- 添加了 FAQ 12：Windows 头文件导致构建错误...
- 删除了 GCC shadow 警告。
- 添加了包含不同版本的 GLM 的错误。
- 添加了 GLM_FORCE_IGNORE_VERSION 以忽略由包含不同版本的 GLM 导致的错误。
- 在使用非常严格的编译标志时减少警告。
- length() 成员函数是 constexpr。
- 使用 Clang 支持 -Weverything。
- 改善了指数函数测试覆盖率。
- 使用 Clang 单元测试启用了警告作为错误。
- Conan 包是一个外部仓库：https://github.com/bincrafters/conan-glm
- 澄清 quat_cast 的文档，应用于纯旋转矩阵。


#### 修复:

- 删除了对在 0.9.4 中删除的 GTC_half_float 的 Doxygen 引用。
- 修正了 glm::decompose。
- 修正了 intersectRayTriangle。
- 修复了双重四元数 != 操作符。
- 修复了 GTX_spline 中未使用的变量警告。
- 修复了 GLM_FORCE_RADIANS 的引用。
- 修正了 glm::fastInverseSqrt 的快速反平方使用。
- 修复了 axisAngle NaN。
- 修复了带有 null 指数的 GTX_integer 整数 pow。
- 修复了 quat normalize 构建错误。
- 修复了 Visual C++ 2017.2 关于 __has_feature 定义的警告。
- 修复了文档警告。
- 修正了当未启用 OpenMP 时的 GLM_HAS_OPENMP。
- 更好地遵循 GLSL min 和 max 规范。
- 修正了从两个向量构造四元数的特殊情况。
- 修复了 glm::to_string 上四元数错误的组件顺序。
- 修复了 acsch。
- 修复了 CUDA 上 isnan。

#### 废弃:
- 需要Visual Studio 2013、GCC 4.7、Clang 3.4、Cuda 7、ICC 2013或C++11编译器
- 删除了GLM_GTX_simd_vec4扩展
- 删除了GLM_GTX_simd_mat4扩展
- 删除了GLM_GTX_simd_quat扩展
- 删除了GLM_SWIZZLE，使用GLM_FORCE_SWIZZLE代替
- 删除了GLM_MESSAGES，使用GLM_FORCE_MESSAGES代替
- 删除了GLM_DEPTH_ZERO_TO_ONE，使用GLM_FORCE_DEPTH_ZERO_TO_ONE代替
- 删除了GLM_LEFT_HANDED，使用GLM_FORCE_LEFT_HANDED代替
- 删除了GLM_FORCE_NO_CTOR_INIT
- 删除了glm::uninitialize

---
### [GLM 0.9.8.5](https://github.com/g-truc/glm/releases/tag/0.9.8.5) - 2017-08-16
#### 特性:
- 增加Conan包支持 #647

#### 修复:

- 修复源代码中Clang版本检测错误问题 #608
- 修复packF3x9_E1x5指数打包问题 #614
- 修复整数与min、max特化构建错误问题 #616
- 修复simd_mat4构建错误问题 #652
---
### [GLM 0.9.8.4](https://github.com/g-truc/glm/releases/tag/0.9.8.4) - 2017-01-22
#### 修复:
- 修复GTC_packing测试在GCC x86上失败的问题，由于denorms引起 #212 #577
- 修复Clang中POPCNT优化的问题 #512
- 修复intersectRayPlane在平行情况下返回true的问题 #578
- 修复GCC 6.2编译器警告 #580
- 修复GTX_matrix_decompose分解函数 #582 #448
- 修复GCC 4.5及更早版本编译错误 #566
- 修复声明具有swizzle表达式启用的全局vec类型时，Visual C++的内部错误 #594
- 修复在Clang和libstlc++中使用GLM_FORCE_CXX11未使用C++11 STL功能 #604

---
### [GLM 0.9.8.3](https://github.com/g-truc/glm/releases/tag/0.9.8.3) - 2016-11-12
#### 改进:
- 更广泛地支持GLM_FORCE_UNRESTRICTED_GENTYPE #378 

#### 修复:
- 修复使用C++11编译器但C++98 STL的Android编译错误 #284 #564
- 修复GTX_transform2中的shear*函数 #403
- 修复GLM_FORCE_UNRESTRICTED_GENTYPE与ortho函数之间的交互问题 #568
- 修复AVX在32位版本中的bitCount问题 #567
- 修复带有版本规范的CMake find_package #572 #573

---
### [GLM 0.9.8.2](https://github.com/g-truc/glm/releases/tag/0.9.8.2) - 2016-11-01
#### 改进:
- 增加Visual C++ 15检测
- 增加Clang 4.0检测
- 使用GLM_FORCE_CXX**但编译器已知不能完全支持请求的C++版本时，增加警告信息 #555
- 重构GLM_COMPILER_VC值
- 使quat、vec、mat类型的component length() static #565

#### 修复:
- 修复Visual C++ constexpr build错误 #555, #556

---
### [GLM 0.9.8.1](https://github.com/g-truc/glm/releases/tag/0.9.8.1) - 2016-09-25
#### 改进:
- 优化quaternion log函数 #554

#### 修复:
- 替换-pedantic为-Wpedantic，修复GCC警告过滤问题
- 修复SIMD faceforward bug问题 #549
- 修复GCC 4.8使用C++11编译选项的问题 #550
- 修复Visual Studio对齐类型W4警告 #548
- 修复5_6_5和5_5_5_1的packing/unpacking函数 #552


---
### [GLM 0.9.8.0](https://github.com/g-truc/glm/releases/tag/0.9.8.0) - 2016-09-11
#### 特性:
- 增加右手和左手投影和剪辑控制支持 #447 #415 #119
- 在GTX_component_wise中增加compNormalize和compScale函数
- 在GTC_packing中增加packF3x9_E1x5和unpackF3x9_E1x5用于RGB9E5 #416
- 在GTC_packing中添加(un)packHalf
- 在GTC_packing中添加(un)packUnorm和(un)packSnorm
- 在GTC_packing中增加16位pack和unpack
- 在GTC_packing中增加8位pack和unpack
- 添加缺失的bvec*和&&以及||运算符
- 在GTC_integer中添加iround和uround，对正数进行快速round
- 添加原始SIMD API
- 添加'aligned'限定符
- 使用带有对齐vec类型的GTC_type_aligned
- 添加GTC_functions扩展
- 添加isnan和isinf的quaternion版本 #521
- 在GTX_bit中添加lowestBitValue #536
- 添加GLM_FORCE_UNRESTRICTED_GENTYPE可允许非基本genType #543

#### 改进:
- 改进GCC和Clang中的SIMD和swizzle运算符交互 #474
- 改进GTC_random linearRand文档
- 改进GTC_reciprocal文档
- 改进GLM_FORCE_EXPLICIT_CTOR覆盖范围 #481
- 改进Clang、GCC、ICC和VC的OpenMP支持检测
- 改进SIMD友好的GTX_wrap
- 添加vec、mat、quat和dual_quat类型的constexpr #493
- 添加NEON指令集检测
- 添加MIPS CPU检测
- 添加PowerPC CPU检测
- 在Cuda编译器中使用内置函数实现abs函数
- 将GLM_COMPILER_LLVM和GLM_COMPILER_APPLE_CLANG因式分解为GLM_COMPILER_CLANG
- 不再对long long使用警告
- 在构建消息中添加更多信息

#### 修复:
- 修正GTX_extended_min_max文件名拼写错误 #386
- 修正intersectRayTriangle不执行任何意外背面剔除的问题
- 修复GCC和Clang上的C++98长整型警告 #482
- 修复signed integer函数在非x86架构上的问题
- 修复严格别名警告 #473
- 修复缺少vec1重载到length2和distance2函数 #431
- 修复GLM测试'/fp:fast'和'/Za'命令行选项不兼容
- 修正GTC_quaternion的mat3_cast四元数到mat3转换函数 #542
- 修复Cuda的GTX_io问题 #547 #546

#### 废弃:
- 移除GLM_FORCE_SIZE_FUNC定义
- 弃用GLM_GTX_simd_vec4扩展
- 弃用GLM_GTX_simd_mat4扩展
- 弃用GLM_GTX_simd_quat扩展
- 弃用GLM_SWIZZLE，使用GLM_FORCE_SWIZZLE代替
- 弃用GLM_MESSAGES，使用GLM_FORCE_MESSAGES代替

---
### [GLM 0.9.7.6](https://github.com/g-truc/glm/releases/tag/0.9.7.6) - 2016-07-16
#### 改进:
- 增加 pkg-config 文件 #509
- 更新检测到的编译器版本列表
- 改进了 C++ 11 STL 检测 #523

#### 修复:
- 修复 ICC 下 C++11 STL 检测问题 #510
- 修正了 vec1 重载到 length2 和 distance2 函数的问题 #431
- 修复 GCC 和 Clang 下使用 C++98 时 long long 警告的问题 #482
- 修复标量倒数函数 (GTC_reciprocal) #520

---
### [GLM 0.9.7.5](https://github.com/g-truc/glm/releases/tag/0.9.7.5) - 2016-05-24
#### 改进:
- 增加了 Visual C++ Clang 工具集的检测

#### 修复:
- 修正了 uaddCarry 警告 #497
- 修正了 roundPowerOfTwo 和 floorPowerOfTwo 函数 #503
- 修复了在64位中使用时，Visual C++ 自动检测的 SIMD 指令集问题
- 修复了在 GLM_FORCE_INLINE 中使用 to_string 时的问题 #506
- 修正了二进制 vec4 运算符中的 GLM_FORCE_INLINE
- 修正了 GTX_extended_min_max 文件名拼写错误 #386
- 修正了 intersectRayTriangle 未执行任何意外背面剔除的问题


---
### [GLM 0.9.7.4](https://github.com/g-truc/glm/releases/tag/0.9.7.4) - 2016-03-19
#### 修复:
- 修正了 C++98 STL 下 asinh 和 atanh 警告 #484
- 修正了极坐标函数的 latitude #485
- 修正了 mat2x4 和 vec4 的 outerProduct 定义和运算符签名问题 #475
- 修正了 eulerAngles 的精度错误，返回 NaN #451
- 修正了未定义引用错误 #489
- 修正了缺少 GLM_PLATFORM_CYGWIN 声明的问题 #495
- 修正了各种未定义引用错误 #490

---
### [GLM 0.9.7.3](https://github.com/g-truc/glm/releases/tag/0.9.7.3) - 2016-02-21
#### 改进:
- 增加了 AVX512 检测

#### 修复:
- 修正了 CMake 策略警告
- 修正了 GCC 6.0 检测 #477
- 修正了在 Windows 上 Clang 的构建问题 #479
- 修正了在 GCC 中的 64 位常量警告 #463

---
### [GLM 0.9.7.2](https://github.com/g-truc/glm/releases/tag/0.9.7.2) - 2016-01-03
#### 修复:
- 修正了 GTC_round floorMultiple/ceilMultiple 问题 #412
- 修正了 GTC_packing unpackUnorm3x10_1x2 问题 #414
- 修正了 GTC_matrix_inverse affineInverse 问题 #192
- 修正了在 Linux 上使用 ICC 构建出错的问题 #449
- 修正了 ldexp 和 frexp 的编译错误
- 修正了 "Declaration shadows a field" 警告 #468
- 修正了 'GLM_COMPILER_VC2005 is not defined' 警告 #468
- 修正了各种 'X is not defined' 警告 #468
- 修正了缺少一元 + 运算符的问题 #435
- 修正了在使用 C++11 时 Cygwin 的构建问题 #405

---
### [GLM 0.9.7.1](https://github.com/g-truc/glm/releases/tag/0.9.7.1) - 2015-09-07
#### 改进:
- 提高了常量函数 constexpr 的覆盖率 #198
- 在 GTX_string_cast 中增加了 quat 和 dual_quat 的 to_string #375
- 改进了单元测试的总执行时间 #396

#### 修复:
- 修正了对齐警告问题的严格限制 #235 #370
- 修正了不受支持默认函数的编译器的链接错误 #377
- 修正了 vec4 中的编译警告
- 修正了相等向量的非恒等四元数问题 #234
- 修正了 GTX_fast_trigonometry 的执行时间问题 #396
- 修正了 Visual Studio 2015 中的 'hides class member' 警告 #394
- 修正了 builtin bitscan 没有被使用的问题 #392
- 删除了未使用的 func_noise.* 文件 #398

---
### [GLM 0.9.7.0](https://github.com/g-truc/glm/releases/tag/0.9.7.0) - 2015-08-02
#### 特性:
- 添加 GTC_color_space: convertLinearToSRGB 和 convertSRGBToLinear 函数
- 在 GTX_common 中增加了 'fmod' 的 overload 以及测试 #308
- 左手透视和 lookAt 函数 #314
- 添加 eulerAngleXYZ 和 extractEulerAngleXYZ 函数 #311
- 在 <glm/gtx/hash.hpp> 中增加了对 GLM 类型进行 std::hash 的支持 #320 #367
- 添加了用于 texcoord 封装的 <glm/gtx/wrap.hpp>
- 对所有向量和四元数类型添加了静态成分和精度成员 #350
- 添加了 .gitignore #349
- 添加了将 GLM 类型作为联合体默认函数的支持


#### 改进:
- 更改了 __has_include 的使用方式，以支持 Intel 编译器 #307
- YCoCg-R 的整数实现 #310
- 如果设置了 'QUIET' 选项，则不在 'FindGLM' 中显示状态消息 #317
- 在 Linux 64 上添加主分支持续集成服务 #332
- 在 GLM 中关于角度单位的手册进行澄清，并添加 FAQ 11 #326
- 更新检测到的编译器版本列表

#### 修复:
- 修正了 quat 和 dual_quat 类型的默认精度 #312
- 修正了 BE archs 中的 (u)int64 MSB/LSB 处理问题 #306
- 在 g++ 中修正了多行注释警告 #315
- 使用 'std::make_pair<>' 修正了规范符号移除问题 #333
- 修正了 perspective fovy 参数文档 #327
- 移除了在 Linux 32 上导致构建问题的 -m64 #331
- 修正了在 C++98 编译器中的 isfinite 函数 #343
- 修正了在 Linux 上使用 Intel 编译器的问题 #354
- 修正了四元数幂问题 #346
- 修复了分解警告 #373
- 修复了矩阵转换问题 #371

#### 废弃:
- 在 GTC_integer 中删除了 'mod' 的整数声明 #308
- 删除了 GTX_multiple，用 GTC_round 替换

---
### [GLM 0.9.6.3](https://github.com/g-truc/glm/releases/tag/0.9.6.3) - 2015-02-15
- 修复了 Android 无法使用 C++ 11 STL 的问题 #284

---
### [GLM 0.9.6.2](https://github.com/g-truc/glm/releases/tag/0.9.6.2) - 2015-02-15
#### 特性:
- 添加了在 GLM_MESSAGES 中显示 GLM 版本的功能
- 添加了 ARM 指令集检测功能

#### 改进:
- 去除了 zFar < zNear 时透视错误的断言 #298
- 为 vec1、quat 和 dualqual 类型添加了 Visual Studio natvis 支持
- 清理了 C++11 功能检测
- 明确 GLM 许可证
#### 修复:
- 修复了 faceforward 构建问题 #289
- 修复了与 Xlib #define True 1 冲突的问题 #293
- 修复了 VS2010 中 decompose 函数的模板问题 #294
- 修复了 mat4x3 = mat2x3 * mat4x2 运算符 #297
- 修复了 GTC_packing 中 F2x11_1x10 packing 函数中的警告 #295
- 修复了 vec4 的 Visual Studio natvis 支持 #288
- 修复了 GTC_packing packnormx 构建问题，并添加了测试 #292
- 在 GCC 中禁用的 GTX_scalar_multiplication，因为测试无法通过 #242
- 修复了 Visual C++ 2015 constexpr 错误：现在只禁用了部分支持
- 修复了 Clang 中未能内联函数的问题 #302
- 修复了内存损坏（未定义行为）的问题 #303

---
### [GLM 0.9.6.1](https://github.com/g-truc/glm/releases/tag/0.9.6.1) - 2014-12-10
#### 特性:
- 添加了 GLM_LANG_CXX14_FLAG 和 GLM_LANG_CXX1Z_FLAG 语言特性标志
- 添加了 C++14 检测

#### 改进:
- 清理了只报告检测到的功能的 GLM_MESSAGES 编译日志

#### 修复:
- 修复了使用 Cuda 构建时的标量 uaddCarry 错误 #276
- 修复了 C++11 显式转换运算符检测 #282
- 修复了在 *vec1 类型中使用整数 log2 时缺少显式转换的问题
- 修复了 VC 32 位编译器上的 64 位整数 GTX_string_cast to_string 的错误
- 修复了 Android 构建问题，因为 NDK 不支持 STL C++11 #284
- 修复了 VC10 中不支持 _BitScanForward64 和 _BitScanReverse64 的问题
- 修复了 Visual C++ 32 位构建问题 #283
- 修复了 GLM_FORCE_SIZE_FUNC 的 pragma message
- 修复了仅 C++98 构建的问题
- 修复了 GTX_compatibility 和 GTC_quaternion 之间的冲突 #286
- 使用 GLM_FORCE_CXX** 时修复了 C++ 语言限制


---
### [GLM 0.9.6.0](https://github.com/g-truc/glm/releases/tag/0.9.6.0) - 2014-11-30
#### 特性:
- 在 'glm' 命名空间中公开了模板向量和矩阵类型 #239，#244
- 仅限于 C++11 编译器添加了 GTX_scalar_multiplication #242
- 仅限于 C++11 编译器添加了 GTX_range #240
- 为 tvec2 添加了 closestPointOnLine 函数，以便使用 GTX_closest_point #238
- 添加了 GTC_vec1 扩展，为 vec 类型添加了 *vec1 支持
- 更新了带有 vec1 支持的 GTX_associated_min_max
- 为 GTX_packing 添加了对精度和整数类型的支持
- 为 GTX_string_cast 添加了整数类型支持 #249
- 为 vec3 添加了 slerp #237
- 与 isdenomal 一起添加了 GTX_common
- 添加了 GLM_FORCE_SIZE_FUNC 替换 .length() 为 .size() #245
- 添加了 GLM_FORCE_NO_CTOR_INIT
- 添加了“未初始化”以显式不初始化 GLM 类型
- 添加了 GTC_bitfield 扩展，升级了 GTX_bit
- 添加了 GTC_integer 扩展，升级了 GTX_bit 和 GTX_integer
- 添加了 GTC_round 扩展，升级了 GTX_bit
- 添加了 GLM_FORCE_EXPLICIT_CTOR 来要求显式类型转换 #269
- 添加了支持对齐向量、矩阵和四元数类型的 GTX_type_aligned

#### 改进:
- 依赖于 C++11 来实现 isinf 和 isnan
- 移除了 GLM_FORCE_CUDA，Cuda 现在会被隐式检测到
- 分离了 Apple Clang 和 LLVM 编译器的检测
- 使用了 pragma once
- 自动使用 GLM_FORCE_CXX98 和 GLM_FORCE_PURE 编译不支持的 C++ 编译器
- 在 VC12 中添加 not 函数 (来自 GLSL 规范)
- 优化了 bitfieldReverse 和 bitCount 函数
- 优化了 findLSB 和 findMSB 函数性能。
- 通过 Cuda 优化矩阵-向量乘积的性能 #257，#258
- 减少了整数类型的重新定义 #233
- 重写了 GTX_fast_trigonometry #264 #265
- 使类型变得可以平凡复制 #263
- 在 GLM 测试中移除了 <iostream>
- 在 GLM 中使用 std 特性而无需重新声明
- 优化了 cot 函数 #272
- 优化了 sign 函数 #272
- 添加了从 quat 到 mat3 和 mat4 的显式转换 #275
#### 修复:
- 修复了在 Android 上的 C++11 中不支持 std::nextafter 的问题 #217
- 修复了双四元数中缺少 value_type 的问题
- 修复了双四元数长度函数的返回类型问题
- 修复了 GCC 中 isfinite 函数陷入无限循环的问题 #221
- 修复了 Visual Studio 14 编译器警告
- 修复了从另一种 tvec2 类型到另一种 tvec2 的隐式转换问题 #241
- 修复了 quat 和 dualquat 构造函数的不一致性问题
- 修复了 uaddCarray #253
- 修复了浮点比较的警告 #270

#### 废弃:
- 需要 Visual Studio 2010、GCC 4.2、Apple Clang 4.0、LLVM 3.0、Cuda 4、ICC 2013或C++98编译器
- 删除了函数参数中的 degrees
- 默认启用 GLM_FORCE_RADIANS，删除了它的设置
- 删除了 VC 2005/8 和 2008/9 支持
- 删除了 GCC 3.4 到 4.3 支持
- 删除了 LLVM GCC 支持
- 删除了 LLVM 2.6 到 3.1 支持
- 删除了 CUDA 3.0 到 3.2 支持

---
### [GLM 0.9.5.4 - 2014-06-21](https://github.com/g-truc/glm/releases/tag/0.9.5.4)
- 修复了非 UTF8 字符 #196 的问题。
- 增加了 CMake 的 FindGLM 安装 #189。
- 修复了 GTX_color_space - saturation #195 的问题。
- 修复了在 Android NDK 9d 中 glm::isinf 和 glm::isnan 的问题 #191。
- 修复了内置的 GLM_ARCH_SSE4 #204。
- 优化了四元数矢量旋转 #205。
- 修复了缺少 doxygen @endcond 标签的问题 #211。
- 修复了 Clang 中指令集的检测 #158。
- 修复了 orientate3 函数 #207。
- 修复了在四元数球面线性插值中 cosTheta 接近 1 时的 lerp #210。
- 增加了 GTX_io 以支持 <iostream> 的输入输出 #144。
- 修复了 fastDistance 中的歧义性 #215。
- 修复了 tweakedInfinitePerspective #208 中的问题，并增加用户自定义 epsilon。
- 修复了 std::copy 和 std::vector 与 GLM 类型的问题 #214。
- 修复了严格别名问题 #212、#152。
- 修复了在 Android 上不支持 C++11 中的 std::nextafter #213。
- 修复了四元数 exp 和 log 函数中的角落问题 #199。


---
### GLM 0.9.5.3 - 2014-04-02
- 使用 _M_IX86_FP - /arch 编译器参数在 Visual C++ 中自动检测指令集。
- 修复了 GTX_raw_data 的代码依赖性。
- 修复了 GCC 指令集检测的问题。
- 增加了 GLM_GTX_matrix_transform_2d 扩展 (#178，#176)。
- 修复了 CUDA 的问题 (#169，#168，#183，#182)。
- 为除 GTX_string_cast 之外的所有扩展增加了 CUDA 支持。
- 修复了在 GCC 4.8.1 / Android NDK 9c 中的严格别名警告问题 (#152)。
- 修复了缺少 bitfieldInterleave 定义的问题。
- 修复了 usubBorrow (#171)。
- 修复了欧拉角函数 eulerAngle*** 在右手坐标系中不一致的问题 (#173)。
- 为欧拉角函数 eulerAngle*** 增加了完整的测试 #173。
- 为 CUDA 编译器错误增加了解决方法 (#186，#185)。

---
### GLM 0.9.5.2 - 2014-02-08
- 修复了初始化列表的歧义性 (#159，#160)。
- 修复了在 Android NDK 9c 中的警告问题。
- 修复了非二次幂矩阵乘积问题。
- 修复了 mix 函数链接错误。
- 在“纯净”平台上包含 SSE 代码的 GLM 测试中修复了错误。
- 修复了对 fastInverseSqrt (#161) 的未定义引用。
- 通过 <glm/ext.hpp> 修复了 GLM_FORCE_RADIANS 的构建错误 (#165)。
- 修复了向量角函数的点积夹紧范围问题。(#163)
- 在 GCC 4.8.1 / Android NDK 9c 中修复了严格别名警告问题。
- 修复了 GLM_GTC_constants 描述简短的问题 (#162)。

---
### GLM 0.9.5.1 - 2014-01-11
- 修复了 angle 和 orientedAngle 函数有时返回 NaN 值的问题 (#145)。
- 废弃了函数参数的 degrees 并显示消息。
- 增加了 GLM 类型可能的 static_cast 转换 (#72)。
- 修复了在 glm::unProject 中 'inverse' 不是 'glm' 的成员的错误。
- 修复了一些声明和定义之间的不匹配。
- 在使用 namespace glm; 时修复了 inverse 链接错误 (#147)。
- 优化了矩阵求逆和除法的代码 (#149)。
- 增加了 intersectRayPlane 函数 (#153)。
- 修复了 outerProduct 返回类型的问题 (#155)。
---
### GLM 0.9.5.0 - 2013-12-25
- 增加了前向声明 (glm/fwd.hpp) 以加快编译速度。
- 增加了特征头文件。
- 最小化了 GLM 的内部依赖关系。
- 改善了 Intel 编译器的检测。
- 增加了 bitfieldInterleave 和 _mm_bit_interleave_si128 函数。
- 增加了 GTX_scalar_relational。
- 增加了 GTX_dual_quaternion。
- 在 GTX_quaternion 中增加了旋转函数(#22)。
- 增加了每种类型的精度变化。
- 增加了四元数比较函数。
- 修复了负值的 GTX_multiple。
- 移除了 GTX_ocl_type 扩展。
- 修复了后置自增和自减运算符。
- 修复了 zNear == 0 时的 perspective (#71)。
- 移除了左值 swizzle 运算符。
- 清理了不支持的编译器的编译器检测代码。
- 用 C++ 转换替换了 C 强制转换。
- 修复了 .length() 实际返回 int 而非 size_t 的问题。
- 增加了 GLM_FORCE_SIZE_T_LENGTH 和 glm::length_t。
- 移除了不必要的类型转换。
- 优化了打包和拆包函数。
- 移除了 lookAt 函数的 up 参数的归一化(#114)。
- 增加了 inversesqrt 的低精度特化。
- 修复了 ldexp 和 frexp 的实现。
- 增加了 assert 覆盖率。
- 增加了 static_assert 覆盖率。
- 用 STL traits 替换了 GLM traits。
- 允许包含单个核心特征。
- 增加了从两个向量创建四元数的函数。
- 增加了 C++11 初始化列表。
- 为向量类型修复了 umulExtended 和 imulExtended 的实现 (#76)。
- 修复了 GTC 扩展的 CUDA 覆盖范围。
- 增加了 GTX_io 扩展。
- 在定义了 GLM_MESSAGES 后改善了 GLM 消息的启用方式。
- 将矩阵 _inverse 函数实现细节隐藏到私有部分。

---
### [GLM 0.9.4.6](https://github.com/g-truc/glm/releases/tag/0.9.4.6) - 2013-09-20
- 修复了选择最新编译器时的检测问题 #106
- 修复了使用 GCC 和 C++11 时的代码重复问题 #107
- 修复了在 Clang C++11 模式下构建测试套件的问题
- 在 CMake 测试套件中添加了对 c++1y 模式的支持
- 当不使用 Visual C++ 时，将 MS 扩展模式从 CMake 中删除
- 在 Clang 和 GCC 的 CMake 测试套件中添加了 pedantic 模式
- 在 Unix 上为 ICC 添加了 GCC 前端，为 Windows 下的 ICC 添加了 Visual C++ 前端
- 对于不受支持的编译器版本增加了编译错误
- 修复了在定义了 GLM_FORCE_RADIANS 时的 glm::orientation 问题 #112
- 修复了将标量参数作为常量引用的赋值运算符中的 const ref 问题 #116
- 修复了 glm::eulerAngleY 实现的问题 #117


---
### GLM 0.9.4.5 - 2013-08-12
- 修复CUDA支持问题
- 在“纯净”模式下修正内部函数包含问题 #92
- 修复GCC在未启用C++0x模式时的语言检测问题 #95
- 修复问题#97：在C++11中register已被弃用
- 修复问题#96：CUDA问题
- 添加了Windows CE检测 #92
- 为四元数添加了缺失的value_ptr #99

---
### GLM 0.9.4.4 - 2013-05-29
- 修复slerp在costheta接近1时的问题 #65
- 修复mat4x2 value_type构造函数 #70
- 修复Visual C++ 12下的glm.natvis #82
- 在inversesqrt中添加断言，以检测除以零的情况 #61
- 修复缺失的swizzle运算符 #86
- 修正CUDA警告 #86
- 修复VC11下的GLM natvis #82
- 修复GLM_GTX_multiple处理负值的问题 #79
- 修复glm::perspective在zNear为零时的问题 #71

---
### GLM 0.9.4.3 - 2013-03-20
- 增加Clang的限定符检测
- 修复GCC的C++11模式，未启用MS扩展无法启用
- 修正squad、四元函数和exp函数
- 修复GTX_polar_coordinates欧几里得函数，现在接受vec2而非vec3
- 澄清手册的许可证
- 添加手册的docx版本
- 修正GLM_GTX_matrix_interpolation
- 在Android上使用Clang时，修复isnan和isinf问题
- 使用__cplusplus值自动检测C++版本
- 修正bool和bvec*第三个参数的mix函数

---
### GLM 0.9.4.2 - 2013-02-14
- 修复来自GTX_component_wise的compAdd问题
- 修复Windows上英特尔编译器的SIMD支持
- 修复CUDA编译器中的isnan和isinf
- 修复glm::perspective中的GLM_FORCE_RADIANS
- 修正GCC警告
- 修复Xcode上的packDouble2x32
- 修复vec4 SSE实现中的mix函数
- 修复注释中会导致Windows日语模式下出现问题的0x2013短横字符
- 修正文档警告
- 修正CUDA警告
---
### GLM 0.9.4.1 - 2012-12-22
- 改善对half类型的支持：-0.0情况和隐式转换
- 修复Linux上英特尔编译器的交互问题
- 修复四元数和欧拉角之间的交互
- 修复GTC_constants构建
- 修复GTX_multiple
- 当cosTheta接近1时，使用mix函数修复quat slerp
- 改进fvec4SIMD和fmat4x4SIMD实现
- 修正断言消息
- 添加slerp和lerp四元函数及测试

---
### GLM 0.9.4.0 - 2012-11-18
- 添加英特尔编译器支持
- 提升GTC_espilon扩展
- 提升GTC_ulp扩展
- 从源仓库中删除GLM网站
- 添加GLM_FORCE_RADIANS，使所有函数都以弧度为参数
- 修正在MacOS X上检测Clang和LLVM GCC的问题
- 为Visual C++ 2012添加调试器可视化器
- 需要Visual Studio 2005、GCC 4.2、Clang 2.6、Cuda 3、ICC 2013或C++98编译器

---
### [GLM 0.9.3.4](https://github.com/g-truc/glm/releases/tag/0.9.3.4) - 2012-06-30
- 添加SSE4和AVX2检测。
- 删除VIRTREV_xstream和与GCC生成的不兼容性
- 为GCC修复了C++11编译器选项
- 为GCC删除MS语言扩展选项（不可用）
- 为向量类型修复bitfieldExtract
- 修正警告
- 修正SSE包含

---
### GLM 0.9.3.3 - 2012-05-10
- 修复isinf和isnan
- 改进与英特尔编译器的兼容性
- 添加了CMake测试构建选项：SIMD、C++11、快速数学和MS land ext
- 在GCC上修复了SIMD mat4测试
- 修复perspectiveFov实现
- 对于非方阵，修复matrixCompMult
- 在流运算符上修复命名空间问题
- 修正各种警告
- 添加VC11支持

---
### GLM 0.9.3.2 - 2012-03-15
- 修复doxygen文档
- 修复Clang版本检测
- 修正simd mat4 /=运算符
---
### GLM 0.9.3.1 - 2012-01-25
- 修正平台检测
- 修正警告
- 从Doxygen文档中删除详细代码
---
### GLM 0.9.3.0 - 2012-01-09
- 添加CPP Check项目
- 解决与Windows头文件的冲突
- 修正isinf实现
- 解决Boost冲突
- 修正警告
---
### GLM 0.9.3.B - 2011-12-12
- 增加Chrone本地客户端的支持
- 添加epsilon常量
- 从向量类型中删除value_size函数
- 修复GCC上的roundEven
- 改进API文档
- 修正modf实现
- 改善step函数精度
- 修正outerProduct

---
### GLM 0.9.3.A - 2011-11-11
- 改进了Doxygen文档
- 为C++11编译器添加了新的swizzle操作符
- 添加了被声明为函数的新的swizzle操作符
- 为向量和矩阵类型添加了GLSL 4.20长度
- 提升了GLM_GTC_noise扩展：simplex、perlin、周期噪声函数
- 提升了GLM_GTC_random扩展：线性、高斯和各种随机数生成分布
- 添加了GLM_GTX_constants：提供有用的常数
- 添加了扩展版本控制
- 删除了许多未使用的命名空间
- 修复了基于half的类型构造函数
- 添加了GLSL核心噪声函数

---
### [GLM 0.9.2.7](https://github.com/g-truc/glm/releases/tag/0.9.2.7) - 2011-10-24
- 添加更多的 swizzling 构造函数
- 添加缺少的非平方矩阵乘积

---
### [GLM 0.9.2.6](https://github.com/g-truc/glm/releases/tag/0.9.2.6) - 2011-10-01
- 在旧版 GCC 上修复基于 half 的类型构建问题
- 在 Visual C++ 上修复 /W4 警告问题
- 添加缺少的 l-value swizzle 操作符

---
### GLM 0.9.2.5 - 2011-09-20
- 修复 floatBitToXint 函数
- 修复 pack 和 unpack 函数
- 修复 round 函数

---
### GLM 0.9.2.4 - 2011-09-03
- 修复扩展错误
---
### GLM 0.9.2.3 - 2011-06-08
- 修复构建问题

---
### GLM 0.9.2.2 - 2011-06-02
- 扩展矩阵构造函数的灵活性
- 改进四元数实现
- 在各个平台和编译器上修复许多警告

---
### GLM 0.9.2.1 - 2011-05-24
- 自动检测 CUDA 支持
- 改进编译器检测
- 在禁用 C++ 扩展的情况下修复 VC 中的错误和警告
- 修复并测试 GLM_GTX_vector_angle
- 修复并测试 GLM_GTX_rotate_vector

---
### GLM 0.9.2.0 - 2011-05-09
- 添加 CUDA 支持
- 添加 CTest 测试套件
- 添加 GLM_GTX_ulp 扩展
- 添加 GLM_GTX_noise 扩展
- 添加 GLM_GTX_matrix_interpolation 扩展
- 更新四元数 slerp 插值

---
### [GLM 0.9.1.3](https://github.com/g-truc/glm/releases/tag/0.9.1.3) - 2011-05-07
- 修复错误

---
### GLM 0.9.1.2 - 2011-04-15
- 修复错误

---
### GLM 0.9.1.1 - 2011-03-17
-  修复错误

---
### GLM 0.9.1.0 - 2011-03-03
-  修复错误

---
### GLM 0.9.1.B - 2011-02-13
- 更新 API 文档
- 改进 SIMD 实现
- 修复 Linux 构建


---
### [GLM 0.9.0.8](https://github.com/g-truc/glm/releases/tag/0.9.0.8) - 2011-02-13
- 添加四元数乘法操作符
- 澄清 GLM 是一个仅有头文件的库

---
### GLM 0.9.1.A - 2011-01-31
- 添加 SIMD 支持
- 添加新的 swizzle 函数
- 改进 C++0x static_assert 的静态断言错误消息
- 新的设置系统
- 减少分支
- 修复 trunc 实现

---
### [GLM 0.9.0.7](https://github.com/g-truc/glm/releases/tag/0.9.0.7) - 2011-01-30
- 添加 GLSL 4.10 打包函数
- 为每种类型添加 == 和 != 操作符。
---
### GLM 0.9.0.6 - 2010-12-21
- 修复许多矩阵错误

---
### GLM 0.9.0.5 - 2010-11-01
- 改进 Clang 支持
- 修复错误

---
### GLM 0.9.0.4 - 2010-10-04
- 为 GLM 添加自动扩展支持
- 修复错误

---
### GLM 0.9.0.3 - 2010-08-26
- 修复非平方矩阵操作符
---
### GLM 0.9.0.2 - 2010-07-08
- 添加 GLM_GTX_int_10_10_10_2 扩展
- 修复错误

---
### GLM 0.9.0.1 - 2010-06-21
- 修复扩展错误

---
### GLM 0.9.0.0 - 2010-05-25
- 提供 Objective-C 支持
- 修复警告
- 更新文档

---
### GLM 0.9.B.2 - 2010-04-30
- Git 转换
- 从发布版中删除实验性代码
- 修复错误

---
### GLM 0.9.B.1 - 2010-04-03
- 基于 GLSL 4.00 规范
- 添加新的核心函数
- 添加某些隐式转换支持

---
### GLM 0.9.A.2 - 2010-02-20
- 改进某些可能的错误消息
- 改进声明和定义匹配
---
### GLM 0.9.A.1 - 2010-02-09
- 删除已弃用特性
- 内部重新设计
---
### GLM 0.8.4.4 final - 2010-01-25
- 修复警告

---
### GLM 0.8.4.3 final - 2009-11-16
- 修复 half 浮点数算术
- 修复设置定义
---
### GLM 0.8.4.2 final - 2009-10-19
- 修复 half 浮点数加法
---
### GLM 0.8.4.1 final - 2009-10-05
- 更新了文档
- 修复了 MacOS X 构建问题

---
### GLM 0.8.4.0 final - 2009-09-16
- 更新了文档
- 修复了 MacOS X 构建问题

---
### GLM 0.8.3.5 final - 2009-08-11
-  修复bug

---
### GLM 0.8.3.4 final - 2009-08-10
- 根据 GLSL 1.5 规范更新了 GLM
- 修复了 bug
---
### GLM 0.8.3.3 final - 2009-06-25
-  修复了bug

---
### GLM 0.8.3.2 final - 2009-06-04
- 增加了 GLM_GTC_quaternion
- 增加了 GLM_GTC_type_precision

---
### GLM 0.8.3.1 final - 2009-05-21
- 修复了旧的扩展系统
---
### GLM 0.8.3.0 final - 2009-05-06
- 增加了稳定的扩展
- 增加了新的扩展系统
---
### GLM 0.8.2.3 final - 2009-04-01
-  修复了bug

---
### GLM 0.8.2.2 final - 2009-02-24
-  修改了bug

---
### GLM 0.8.2.1 final - 2009-02-13
-  修复了bug

---
### GLM 0.8.2 final - 2009-01-21
-  修复了bug

---
### GLM 0.8.1 final - 2008-10-30
-  修复了bug

---
### GLM 0.8.0 final - 2008-10-23
- 增加了使用扩展的新方法

---
### GLM 0.8.0 beta3 - 2008-10-10
- 为 GLM 测试增加了 CMake 支持

---
### GLM 0.8.0 beta2 - 2008-10-04
- 改进了对半数标量和向量的支持

---
### GLM 0.8.0 beta1 - 2008-09-26
- 改进了 GLSL 符合性
- 增加了 GLSL 1.30 支持
- 改进了 API 文档

---
### GLM 0.7.6 final - 2008-08-08
- 提高了 C++ 标准符合性
- 为类型检查添加了静态断言
---
### GLM 0.7.5 final - 2008-07-05
- 使用 Visual Studio 增加了编译信息系统
- 在 GCC 下进行了严格的构建

---
### GLM 0.7.4 final - 2008-06-01
- 增加了外部依赖项系统

---
### GLM 0.7.3 final - 2008-05-24
- 增加了新的扩展组
---
### GLM 0.7.2 final - 2008-04-27
- 更新了文档
- 增加了预处理器选项

---
### GLM 0.7.1 final - 2008-03-24
- 在 GCC 上禁用了半精度浮点数
- 修复了扩展问题


---
### GLM 0.7.0 final - 2008-03-22
- 改为 MIT 许可证
- 增加了新的文档

---
### GLM 0.6.4 - 2007-12-10
- 修复了赋值运算符

---
### GLM 0.6.3 - 2007-11-05
- 修复了类型数据访问问题
- 修复了 3DSMax SDK 冲突
---
### GLM 0.6.2 - 2007-10-08
- 修复了扩展问题

---
### GLM 0.6.1 - 2007-10-07
- 修复了命名空间错误
- 增加了扩展

---
### GLM 0.6.0 : 2007-09-16
- 增加了新的扩展命名空间 mecanium
- 增加了自动编译器检测

---
### GLM 0.5.1 - 2007-02-19
- 修复了赋值运算符
---
### GLM 0.5.0 - 2007-01-06
- 升级到了 GLSL 1.2
- 增加了 swizzle 运算符
- 增加了设置项

---
### GLM 0.4.1 - 2006-05-22
- 增加了 OpenGL 示例
---
### GLM 0.4.0 - 2006-05-17
- 在 vec* 和 mat* 中增加了缺失的运算符
- 增加了 GLSL 1.2 特性
- 解决了需要 glm.h 之前的 windows.h 问题

---
### GLM 0.3.2 - 2006-04-21
- 修复了纹理坐标问题
- 修复了 mat4 和 imat4 的除法运算符
---
### GLM 0.3.1 - 2006-03-28
- 在 MacOS X 下增加了 GCC 4.0 支持
- 在 Linux 下增加了 GCC 4.0 和 4.1 支持
- 增加了代码优化
---
### GLM 0.3 - 2006-02-19
- 改进了 GLSL 类型转换和构造符合性
- 增加了实验性的扩展
- 增加了 Doxygen 文档
- 增加了代码优化

---
### GLM 0.2 - 2005-05-05
- 改进了从 GLSL 中自适应
- 基于 OpenGL 扩展过程增加了实验性的扩展
- 修复了 bug

---
### GLM 0.1 - 2005-02-21
- 增加了 vec2、vec3、vec4 GLSL 类型
- 增加了 ivec2、ivec3、ivec4 GLSL 类型
- 增加了 bvec2、bvec3、bvec4 GLSL 类型
- 增加了 mat2、mat3、mat4 GLSL 类型
- 增加了几乎所有函数

