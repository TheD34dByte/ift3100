# Super Omega Ultra Program!
### S.O.U.P.
<div style="width: 80%;">
<i>Good intentions are not good enough, for they have not put an onion in the soup yet.</i>
<h6 style="display: flex; justify-content: right">- Sonia Levien</h6>
</div>

## Features 
- Simple image analysis
- 3D scene rendering
- Classic and modern illumination
- Etc. (TBD)

## Requirements
- C++ >= 17
- OpenGL >= 3.3
- GLFW >= 3.4-3
- CMake >= 3.31.6
- clangd >= 22.1.6
- NPM >= 9.2.0

## Building
```sh
cmake -S . -B build -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
cmake --build build
```

## Formatting code
```sh
cmake --build build --target format
npm run format:json
```

## Linting code
```sh
cmake --build build --target lint
npm run lint:json
```

## Running tests
TBD

## Authors
- John-William Lebel
- Anne-Sophie Bissonnette
- Loïc Boiteux
- Alexandre Khuong
