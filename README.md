# market-qt

```cmd
> cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release -DQT_STATIC=ON
> cmake --build build --config Release
```

Note that your Qt `bin` directory must be in your PATH.

The `QT_STATIC` flag is experimental and should only be used for distribution or if Qt is not installed on your machine.
