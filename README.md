# Archi Flatpak

This repository contains the Flatpak manifest for [Archi](https://www.archimatetool.com/), an open source ArchiMate modeling tool.

## Application ID

`com.archimatetool.Archi`

This follows the standard Flatpak naming convention using reverse domain notation based on the official website domain (archimatetool.com).

## Runtime

The Flatpak uses **org.freedesktop.Platform** runtime version 25.08, which is based on Red Hat's freedesktop-sdk. This provides a stable, well-maintained base for the application.

## Building the Flatpak

### Prerequisites

Ensure you have `flatpak` and `flatpak-builder` installed:

```bash
# On Fedora/RHEL
sudo dnf install flatpak flatpak-builder

# On Ubuntu/Debian
sudo apt install flatpak flatpak-builder

# On Arch Linux
sudo pacman -S flatpak flatpak-builder
```

Add the Flathub repository (if not already added):

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Install the required runtime and SDK:

```bash
flatpak install flathub org.freedesktop.Platform//25.08 org.freedesktop.Sdk//25.08
```

### Build

To build the Flatpak:

```bash
flatpak-builder --repo=repo --force-clean build-dir com.archimatetool.Archi.yaml
```

### Install Locally

To install the built Flatpak locally:

```bash
flatpak-builder --user --install --force-clean build-dir com.archimatetool.Archi.yaml
```

### Test

Run the application:

```bash
flatpak run com.archimatetool.Archi
```

## Creating a Bundle

To create a single-file bundle for distribution:

```bash
flatpak build-bundle repo archi.flatpak com.archimatetool.Archi
```

Install the bundle:

```bash
flatpak install archi.flatpak
```

## Application Features

- Full support for ArchiMate 3.2 specification
- Visual modeling with drag and drop interface
- Multiple views and viewpoints
- Model relationship management
- Import/Export capabilities
- HTML report generation
- Cross-platform compatibility

## File Structure

- `com.archimatetool.Archi.yaml` - Main Flatpak manifest
- `com.archimatetool.Archi.desktop` - Desktop entry file
- `com.archimatetool.Archi.metainfo.xml` - AppStream metadata

## Version

Current version: **5.8.0**

Release date: February 18, 2026

## License

Archi is released under the MIT License.

## Links

- [Official Website](https://www.archimatetool.com/)
- [GitHub Repository](https://github.com/archimatetool/archi)
- [User Guide](https://www.archimatetool.com/downloads/archi/Archi%20User%20Guide.pdf)
- [Version History](https://www.archimatetool.com/version-history/)

## Submitting to Flathub

To submit this Flatpak to Flathub:

1. Fork the [Flathub repository](https://github.com/flathub/flathub)
2. Follow the [App submission guide](https://docs.flathub.org/docs/for-app-authors/submission/)
3. Create a new repository named `com.archimatetool.Archi`
4. Submit the manifest files for review

## Permissions

The Flatpak requests the following permissions:

- **X11 and Wayland**: For graphical display
- **IPC**: Required for X11 shared memory
- **OpenGL/DRI**: For hardware acceleration
- **Network**: For collaboration features and updates
- **Home directory access**: To save and open project files
- **XDG Documents**: Access to Documents folder

## Notes

- Archi is built on Eclipse RCP and includes its own Java Runtime Environment (JRE)
- The application bundle is approximately 300MB
- First launch may take a few seconds as Eclipse initializes

## Troubleshooting

If the application doesn't start:

```bash
# Check logs
flatpak run com.archimatetool.Archi --verbose

# Or use journalctl
journalctl --user -xe | grep archi
```

If you encounter permission issues:

```bash
# Grant additional permissions if needed
flatpak override --user --filesystem=/path/to/your/projects com.archimatetool.Archi
```
