```shell
conan install . --output-folder=build --build=missing --profile=webassembly.profile
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE="conan_toolchain.cmake" -DCMAKE_BUILD_TYPE=Release
```
