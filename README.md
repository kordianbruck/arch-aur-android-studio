# Android Studio for Arch Linux

This is the [Arch User Repository (AUR)](https://aur.archlinux.org/packages/android-studio) package for [Android Studio](https://developer.android.com/studio), the official IDE for Android development. It repackages the stable release tarballs that Google publishes. The IDE installs to `/opt/android-studio`. It bundles its own Java runtime, so you do not need to install Java.

## Installation

Use an AUR helper (a tool that builds and installs AUR packages), such as `paru` or `yay`:

    paru -S android-studio

To build the package by hand:

1. Make sure that the `base-devel` group is installed.
2. Clone the repository: `git clone https://aur.archlinux.org/android-studio.git`.
3. Run `makepkg -si` inside the cloned directory.

## Packaging notes

- Android Studio bundles its own Qt 5, and that build has no Wayland plugin. To prevent a crash on Wayland sessions, the desktop entry sets `QT_QPA_PLATFORM=xcb`.
- The emulator needs `libbsd`, `libxkbfile`, and `libgl`. The package lists them as optional dependencies.
- Android Studio keeps a separate cache directory for each release series, for example `~/.cache/Google/AndroidStudio2026.1`. These caches grow to about 2 GB each. When an upgrade installs a new series, the package deletes the cache of the previous one. Your settings stay in place.

## Contributing

The [GitHub repository](https://github.com/kordianbruck/arch-aur-android-studio) is a mirror of the AUR repository and accepts pull requests. You can also report problems in the comments on the [AUR page](https://aur.archlinux.org/packages/android-studio).
