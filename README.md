# Il2cppXcodeProject

# global-metadata.dat文件的加密

**ios下global-metadata.dat文件的加密**

1. ios下只能将Il2cpp源码编译生成静态库libil2cpp.a文件，然后在Xcode工程替换libil2cpp.a
2. Il2cpp源码编译生成静态库libil2cpp.a文件
    1. 源码位置：/Applications/Unity/Hub/Editor/2019.4.28f1c1/Unity.app/Contents/il2cpp
    2. 源码修改：偏移4个字节il2cpp::vm::MetadataLoader::LoadMetadataFile(const char* fileName) void* fileBuffer = utils::MemoryMappedFile::Map(handle, 0, 4);//解密代码，字节偏移
    3. 编译
        1. ~~将il2cpp整个文件夹copy出来，新建Xcode静态库工程，添加libil2cpp到根目录下，依次添加依赖~~
        2. ~~build setting~~
            1. ~~Search headers~~
            2. **~~C++Language Dialect：gun11~~**
            3. ~~c++ standard libaray:libc++ (LLVM C++ starndad...)~~
            4. ~~c++ language dialect : gun++14~~
            5. ~~Linking->other linker flags~~
            6. ~~宏定义：~~
            7. 额，没成功复现。。。） 直接使用原工程吧
        3. 使用原工程，编译出.a文件（36m，原文件是90多兆）
    4. 加密global-metadata.dat，copy前4个字节，复制插入
3. Xcode工程替换global-metadata.dat 和 libil2cpp.a
4. 打包Xcode工程
