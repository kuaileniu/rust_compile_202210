# rust_compile_202210
rust 交叉编译


# 创建项目
cargo new hello

# 准备交叉编译环境（macos）
brew update   

brew install FiloSottile/musl-cross/musl-cross  
brew install mingw-w64 
brew install filosottile/musl-cross/musl-cross
rustup target add x86_64-unknown-linux-musl

mkdir hello/.cargo && cd hello/.cargo && touch config.toml
在 config.toml中添加

[target.x86_64-unknown-linux-musl]
linker = "x86_64-linux-musl-gcc"

# 交叉编译
cd hello
cargo build --target=x86_64-unknown-linux-musl --release
编译后的可执行文件： hello/target/x86_64-unknown-linux-musl/release/hello

# 编译本机环境
cd hello
cargo build --release
编译后的可执行文件： hello/target/release/hello