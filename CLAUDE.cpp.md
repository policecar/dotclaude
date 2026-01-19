# Development Workflow

## Build

```sh
# macOS (requires GCC 15 via Homebrew for C++23 features)
cmake -S . -G Ninja -B build -DCMAKE_BUILD_TYPE=Debug \
  -DCMAKE_C_COMPILER=$(brew --prefix gcc)/bin/gcc-15 \
  -DCMAKE_CXX_COMPILER=$(brew --prefix gcc)/bin/g++-15

# Linux
cmake -S . -G Ninja -B build -DCMAKE_BUILD_TYPE=Debug

# Build
cmake --build build -j

# Test
ctest --test-dir build -C Debug
```

## CMake Configuration Requirements

The CMakeLists.txt must enforce:
- **Warnings enabled**: `-Wall -Wextra -Wconversion -Wshadow` (GCC/Clang) or `/W4` (MSVC)
- **Warnings as errors**: `-Werror` / `/WX` — this is non-negotiable
- **clang-tidy integrated**: Use `CMAKE_CXX_CLANG_TIDY` with warnings-as-errors
- **Sanitizers in Debug**: UBSan and ASan enabled by default
- **Coverage enabled**: `--coverage` flag for coverage builds
- **Fail-fast on missing tools**: Configuration errors with actionable messages if required tools are absent

## Every Change

```sh
cmake --build build -j
ctest --test-dir build -C Debug
clang-format -i src/**/*.cpp include/**/*.h
clang-tidy src/**/*.cpp --
```

Always run **all** tests after making a change. Always run **all** analysis. Verify code coverage did not decrease.

## Before PR

```sh
cmake -S . -G Ninja -B build-release -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=$(brew --prefix gcc)/bin/gcc-15 \
  -DCMAKE_CXX_COMPILER=$(brew --prefix gcc)/bin/g++-15  # macOS only
cmake --build build-release -j
ctest --test-dir build-release -C Release
uvx codespell
```

Run the coverage report and verify no decrease from baseline.
