# Compiling GCC 16.1 on WSL2 Ubuntu 24.04

> [!WARNING]
> **Time & Resource Warning:** Compiling GCC is a heavy task. On a standard laptop, it can take **1 to 3 hours**. Make sure your WSL2 has at least 8GB of RAM (or enough swap) to avoid "internal compiler error" crashes.

### 1. Install Build Dependencies
You’ll need your current GCC and some math libraries to build the new one.
```bash
sudo apt update
sudo apt install build-essential libmpfr-dev libgmp3-dev libmpc-dev flex bison -y
```

### 2. Download the GCC 16.1 Source
```bash
cd ~
wget https://ftp.gnu.org/gnu/gcc/gcc-16.1.0/gcc-16.1.0.tar.gz
tar -xf gcc-16.1.0.tar.gz
cd gcc-16.1.0
```

### 3. Download Prerequisites & Configure
GCC has a script to fetch a few extra internal libraries (`gmp`, `mpfr`, `mpc`) automatically if they aren't already perfect.
```bash
# Download support libraries
./contrib/download_prerequisites

# Create a separate build directory (GCC docs recommend this)
mkdir build && cd build

# Configure the build
# --disable-multilib: Speeds things up by only building for 64-bit
# --enable-languages: We only need C and C++
../configure -v \
    --build=x86_64-linux-gnu \
    --host=x86_64-linux-gnu \
    --target=x86_64-linux-gnu \
    --prefix=$HOME/gcc-16.1.0 \
    --enable-checking=release \
    --enable-languages=c,c++ \
    --disable-multilib
```

### 4. The Big Build
Use the `-j` flag to use all your CPU cores. Since you're on a "tuff" laptop, you likely have 8+ threads.
```bash
# Replace '8' with the number of CPU cores you want to use
make -j$(nproc)
```
*Go grab a coffee (or lunch). This will take a while.*

### 5. Install and Test
Once it finishes, install it to the prefix folder we defined earlier (`~/gcc-16.1.0`).
```bash
sudo make install
```

To run your C++26 project using this specific build:
```bash
# Verify the version
~/gcc-16.1.0/bin/g++ --version

# Compile your project
~/gcc-16.1.0/bin/g++ -std=c++26 -freflection main.cpp -o cpp26_test
```

### Why do this instead of just using GCC 14?
By building **GCC 16.1**, you get the first "stable" implementation of **C++26 Reflection**. 


Since you mentioned you're an **Embedded Software Engineer**, being able to use reflection to automatically generate serialization code for your ESP32 or Zephyr projects (without macros!) is a total game changer.

Would you like a sample C++26 reflection snippet to test once the build finishes?