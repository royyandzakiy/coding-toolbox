## Install
```bash
# clang
conan install . -of build-clang --build=missing -s compiler=clang -s compiler.version=20 -s compiler.runtime_type=Release

# msvc
conan install . -of build-msvc --build=missing -s compiler=msvc -s compiler.version=193 -s compiler.runtime=dynamic -s compiler.cppstd=23
```

## Error
```bash
# The error indicates that Conan is trying to install msys2/cci.latest package but the package folder is missing or corrupted. This is a common issue with Conan cache
> ERROR: Pkg 'msys2/cci.latest:956a88975bda9dfcc485e2861d71e74bd7e2b9a5' folder must exist: C:\Users\royya\.conan2\p\msys208d4cdbd2b6d8\p

conan remove msys2/cci.latest -c # Remove the problematic msys2 package
conan remove "*" -c # Or remove all cache if you want to be thorough
```