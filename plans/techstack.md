# Tech Stack

## Core Framework

- **Python 3.10+** - Main programming language (cross-platform)
- **CustomTkinter** - Modern, customizable GUI framework (cross-platform: Windows, macOS, Linux)
  - Alternative: **PyQt6/PySide6** (more powerful but heavier, cross-platform)
  - Alternative: **wxPython** (native look, cross-platform)

## Platform Support

- **Windows 11** - Full support
- **Windows 10** - Full support
- **macOS** - Full support (10.14+)
- **Linux** - Full support (Ubuntu, Debian, Fedora, Arch, etc.)

## GUI & UI Components

- **CustomTkinter** - Main GUI framework
- **tkinter.ttk** - Additional widgets if needed
- **Pillow (PIL)** - Image processing, optimization, cropping, resizing
- **tkinter.scrolledtext** - Text editing areas

## Web Rendering & Preview

- **webview** (pywebview) - Embedded browser for live preview
  - Alternative: **cefpython3** - Chromium Embedded Framework
  - Alternative: **PyQt6.QtWebEngineWidgets** - If using PyQt6

## File Management

- **pathlib** - Modern file path handling
- **json** - Configuration and project data storage
- **os/sys** - System operations

## HTML/CSS/JS Generation

- **jinja2** - Template engine for HTML generation and framework code templates
- **beautifulsoup4** - HTML parsing and manipulation
- **cssutils** - CSS parsing and manipulation (optional)

## Framework Export & Code Generation

- **jinja2** - Template engine for React, Vue, and other framework templates
- **jsbeautifier** - Format generated JavaScript/JSX code (optional)
- **cssbeautifier** - Format generated CSS code (optional)
- **zipfile** - Create zip archives of exported projects

## Drag & Drop

- **Custom Implementation** - Primary approach using mouse events (more reliable with CustomTkinter)
  - Track Button-1 press → Motion → Button-1 release
  - Visual feedback with overlay widgets
  - Platform-independent
- **tkinterdnd2** - Alternative/fallback (may have compatibility issues with CustomTkinter)

## Project Management

- **json** - Project file format (.coweb)
- **zipfile** - Project export/import
- **shutil** - File operations

## Additional Libraries

- **requests** - Fetching external resources, API calls for deployment, GitHub Releases API
- **packaging** - Version comparison for update checking
- **watchdog** - File system monitoring for auto-save
- **pygments** - Syntax highlighting for code editor
- **tinycss2** or **cssutils** - CSS parsing for import functionality
- **html5lib** - HTML parsing (alternative to BeautifulSoup4)
- **paramiko** - SFTP/FTP for deployment
- **python-dotenv** - Environment variable management for deployment
- **webcolors** - Color name to hex conversion, contrast checking
- **Pillow-SIMD** - Faster image processing (optional)
- **fonttools** - Font file manipulation and analysis
- **keyring** - Secure credential storage (API keys, passwords)
- **logging** (stdlib) - Application logging
- **threading** (stdlib) - Background operations (auto-save, file I/O, update checking)
- **queue** (stdlib) - Thread-safe communication

## Development Tools

- **pytest** - Testing framework
- **black** - Code formatting
- **pylint/flake8** - Linting

## Packaging & Distribution (Cross-Platform)

- **Windows**:
  - **PyInstaller** - Create Windows executable (.exe)
  - **cx_Freeze** - Alternative packaging tool
  - **Inno Setup** - Windows installer creation (.exe installer)
  - **NSIS** - Nullsoft Scriptable Install System (alternative)
- **macOS**:
  - **PyInstaller** - Create macOS application (.app bundle)
  - **py2app** - macOS-specific packaging
  - **create-dmg** - Create macOS disk image (.dmg)
- **Linux**:
  - **PyInstaller** - Create Linux executable
  - **cx_Freeze** - Alternative packaging tool
  - **AppImage** - Create AppImage (portable Linux app)
  - **Snap** - Create Snap package (Ubuntu/Snap Store)
  - **Flatpak** - Create Flatpak package (alternative)
  - **deb/rpm** - Create distribution packages

## Setup Wizard (Cross-Platform)

- **CustomTkinter** - Build custom setup wizard UI (matches main app style, cross-platform)
- **Platform Detection**:
  - **platform** (stdlib) - Detect operating system
  - **sys.platform** - Platform identification
- **Windows-Specific**:
  - **winreg** (Windows Registry) - Register file associations (.coweb files)
  - **win32api/win32con** (pywin32) - Windows-specific operations (shortcuts, registry)
  - **ctypes** - Access Windows API (SHGetFolderPath for proper paths)
  - **os.environ** - Access environment variables (%APPDATA%, %LOCALAPPDATA%)
- **macOS-Specific**:
  - **plistlib** (stdlib) - macOS property list files
  - **subprocess** - Launch Services (file associations)
  - **osascript** - AppleScript for shortcuts
  - **pathlib** - Access ~/Library directories
- **Linux-Specific**:
  - **xdg-utils** (via subprocess) - Desktop integration
  - **desktop-file-utils** - Desktop entry files
  - **mimeapps.list** - MIME type associations
  - **os.environ** - Access XDG environment variables ($XDG_DATA_HOME, $XDG_CONFIG_HOME, etc.)
- **Cross-Platform**:
  - **shutil** - File copying and installation operations
  - **pathlib** - Path handling for installation directories (cross-platform paths)
  - **json** - Store installation configuration

## Recommended Project Structure Dependencies

```
requirements.txt:
# Core (cross-platform)
customtkinter>=5.2.0
Pillow>=10.0.0  # Image processing, optimization, cropping, resizing
pywebview>=4.4.0
jinja2>=3.1.0
beautifulsoup4>=4.12.0
watchdog>=3.0.0
jsbeautifier>=1.14.0  # For formatting generated JS/JSX code
cssbeautifier>=1.14.0  # For formatting generated CSS code
pygments>=2.15.0  # Syntax highlighting for code editor
requests>=2.31.0  # API calls, deployment, external resources, Google Fonts API, GitHub Releases API
packaging>=23.0  # Version comparison for update checking
paramiko>=3.3.0  # SFTP/FTP deployment
gitpython>=3.1.0  # Git operations for GitHub Pages
python-dotenv>=1.0.0  # Environment variables
webcolors>=1.13.0  # Color utilities, contrast checking
fonttools>=4.42.0  # Font file manipulation
tinycss2>=1.2.0  # CSS parsing (alternative to cssutils)
keyring>=24.0.0  # Secure credential storage (API keys, passwords)

# Platform-specific (optional, installed only on target platform)
# Windows
pywin32>=306; sys_platform == "win32"  # Windows registry, shortcuts

# macOS (optional, for advanced features)
# pyobjc-framework-Cocoa>=10.0; sys_platform == "darwin"  # macOS integration

# Linux (optional, for advanced features)
# python-xdg>=0.28; sys_platform == "linux"  # Linux desktop integration
```
