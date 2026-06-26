# Repository Guidelines

## Project Structure & Module Organization

Prism Launcher is a Qt/C++ application built with CMake. Main launcher code lives in `launcher/`, grouped by feature areas such as `minecraft/`, `modplatform/`, `ui/`, `net/`, and `tasks/`. Shared third-party or internal support code is under `libraries/`. Unit tests are in `tests/`, with fixtures in `tests/testdata/`. Build configuration is rooted at `CMakeLists.txt`, `CMakePresets.json`, `vcpkg.json`, and `buildconfig/`. Packaging, platform, and developer tooling are in `.github/`, `cmake/`, `nix/`, `scripts/`, and `tools/`. Branding and desktop metadata are in `program_info/`.

## Build, Test, and Development Commands

Use CMake presets where possible:

```sh
cmake --preset windows_msvc
cmake --build --preset windows_msvc
ctest --preset windows_msvc
```

On Windows with MinGW, use `windows_mingw`; on Linux use `linux`; on macOS use `macos` or `macos_universal`. Presets generate into `build/` and install into `install/`. Some presets require `VCPKG_ROOT` and other environment variables; see `CMakePresets.json` and the official build instructions linked from `README.md`.

## Coding Style & Naming Conventions

Follow `.editorconfig`: spaces, 4-space indentation, LF endings, UTF-8, final newline, and trimmed trailing whitespace. YAML and Nix files use 2-space indentation. C++ is formatted with `clang-format` using `.clang-format`; run it on changed C++ files before committing. Naming conventions include `PascalCase` for classes/types, `camelCase` for functions and public fields, `m_` for private/protected members, `s_` for private/protected static members, and `SCREAMING_SNAKE_CASE` for macros and global constants.

## Testing Guidelines

Tests are C++ files in `tests/` named `Feature_test.cpp`, with supporting data under `tests/testdata/`. Add focused tests near related coverage when changing parsing, filesystem, metadata, task, or model behavior. Run the matching CTest preset after building, for example `ctest --preset windows_msvc`; CTest is configured to show output on failure.

## Commit & Pull Request Guidelines

Recent history uses short imperative or conventional-style subjects, often with issue/PR references, such as `fix: recursive mod dependencies` or `Use native APIs for GPU discovery (#5602)`. Keep commits focused. Human contributors must sign off commits with `git commit -s`; AI agents must not add `Signed-off-by` tags. When AI assistance was used, follow `CONTRIBUTING.md` and add an appropriate `Assisted-by:` trailer. Pull requests should describe the change, link related issues, list testing performed, and include screenshots for visible UI changes.
