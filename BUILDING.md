## Structure

The project is seperated in multiple modules, all serve single or multiple uses depending on their importance.

| Module               | Description                                                                                                                   |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `apps/plumeimpactor` | GUI interface for the crates shown below, backend using wxWidgets (with a rust ffi wrapper, wxDragon).                        |
| `apps/plumesign`     | Simple CLI interface for signing, using `clap`.                                                                               |
| `crates/core`.       | Handles all api request used for communicating with Apple developer services, along with providing auth for Apple's grandslam |
| `crates/gestalt`     | Wrapper for `libMobileGestalt.dylib`, used for obtaining your Mac's UDID for Apple Silicon sideloading.                       |
| `crates/utils`       | Shared code between GUI and CLI, contains signing and modification logic, and helpers.                                        |
| `crates/shared`      | Shared code between GUI and CLI, contains keychain functionality and shared datapaths.                                        |

## Building

Building is going to be a bit convoluted for each platform, each having their own unique specifications, but the best reference for building should be looking at how [GitHub actions](./.github/workflows/build.yml) does it.

You need:
- [Rust](https://rustup.rs/).
- [CMake](https://cmake.org/download/) (and a c++ compiler).

```sh
# Building / testing GUI
cargo run --bin plumeimpactor
# Building / texting CLI
cargo run --bin plumesign -- <args>
```

Extra requirements are shown below for building if you don't have these already, and trust me, it is convoluted.

#### Linux Requirements

```sh
# Ubuntu/Debian
sudo apt-get install libclang-dev pkg-config libgtk-3-dev libpng-dev libjpeg-dev libgl1-mesa-dev libglu1-mesa-dev libxkbcommon-dev libexpat1-dev libtiff-dev

# Fedora/RHEL
sudo dnf install clang-devel pkg-config gtk3-devel libpng-devel libjpeg-devel mesa-libGL-devel mesa-libGLU-devel libxkbcommon-devel expat-devel libtiff-devel
```

#### macOS Requirements

- [Xcode](https://developer.apple.com/xcode/) or [Command Line Tools](https://developer.apple.com/download/all/).

#### Windows Requirements

- [Visual Studio 2022 Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022).
- Windows 10/11 SDK.