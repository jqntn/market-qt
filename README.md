# market-qt

```cmd
> cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH="C:\Qt\6.7.2\msvc2019_64"
> cmake --build build --config Release
```

Note that `CMAKE_PREFIX_PATH` is only necessary if you manage your Qt installation yourself. Your Qt `bin` directory should also be in your PATH.
