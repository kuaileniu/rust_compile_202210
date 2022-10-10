# rust_compile_202210
rust 交叉编译

https://github.com/tpoechtrager/osxcross
# Rust交叉编译Mac编译Linux/Windows平台
- Rust交叉编译Mac编译Linux/Windows平台 https://blog.51cto.com/u_15057820/4540650
- https://github.com/japaric/rust-cross
# 创建项目
cargo new hello

# 准备交叉编译环境（macos）
brew update   

Windows10下编译Linux的程序 下载安装 https://musl.cc/x86_64-linux-musl-cross.tgz (用的是这个)  ；
 https://musl.cc/x86_64-w64-mingw32-cross.tgz  ; 
 https://musl.cc/x86_64-w64-mingw32-native.zip ; 
 https://wenku.baidu.com/view/571f57cde309581b6bd97f19227916888486b9d1.html
brew install FiloSottile/musl-cross/musl-cross  
brew install mingw-w64 
brew install filosottile/musl-cross/musl-cross
rustup target list                                     // 查看支持的平台
rustup target add x86_64-unknown-linux-musl            // 为编译linux环境的文件作准备
rustup target add target.x86_64-pc-windows-gnu        // 为编译windows环境的文件作准备

mkdir hello/.cargo && cd hello/.cargo && touch config.toml
在 config.toml中添加

[target.x86_64-unknown-linux-musl]
linker = "x86_64-linux-musl-gcc"
‘[target.x86_64-pc-windows-gnu]
linker = "x86_64-w64-mingw32-gcc"

# 交叉编译
cd hello

- 编译linux环境文件
cargo build  --release --target=x86_64-unknown-linux-musl
编译后的可执行文件： hello/target/x86_64-unknown-linux-musl/release/hello

- 编译windows环境文件
cargo build --release --target=x86_64-pc-windows-gnu
编译后的可执行文件： hello/target/x86_64-pc-windows-gnu/release/hello.exe

# 编译本机环境
cd hello
cargo build --release
编译后的可执行文件： hello/target/release/hello