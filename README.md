# CO-web-builder

> Create websites from scratch with an intuitive visual editor—fast, easy, and frustration-free.

CO-web-builder is a powerful, cross-platform desktop application that allows you to build modern websites visually, without writing code. Drag and drop elements, customize styles, and export to any modern web framework.

![Platform Support](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)
![Python](https://img.shields.io/badge/python-3.10+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Features

### 🎨 Visual Editor

- **Drag & Drop Interface** - Intuitive visual editor with custom drag & drop implementation
- **WYSIWYG Editing** - What You See Is What You Get, with live preview
- **Element Library** - Rich set of components (containers, text, images, buttons, forms, etc.)
- **Properties Panel** - Comprehensive property editor for layout, styling, and content
- **Responsive Design Tools** - Preview and design for desktop, tablet, and mobile

### 💻 Code Generation

- **Multi-Framework Export** - Export to:
  - Vanilla HTML/CSS/JS
  - React (JSX, hooks, functional components)
  - Vue.js (Single File Components, Composition API)
  - Next.js (React with SSR/SSG)
  - Nuxt.js (Vue with SSR/SSG)
  - Svelte
  - Angular (TypeScript components)
- **Code Editor** - View and edit generated code with syntax highlighting
- **Code Formatting** - Beautiful, readable code output with optional minification

### 📥 Import & Export

- **HTML/CSS/JS Import** - Import existing projects (phased approach)
- **Project Templates** - Start from pre-built templates
- **Component Library** - Save and reuse custom components
- **Asset Management** - Organize images, fonts, and icons

### 🚀 Deployment

- **One-Click Deployment** - Deploy to:
  - Netlify
  - Vercel
  - GitHub Pages
  - FTP/SFTP servers
- **Secure Credential Storage** - API keys stored securely using OS keychain

### 🛠️ Advanced Features

- **Auto-Save & Version History** - Never lose your work
- **SEO Tools** - Meta tags, sitemap generation, SEO analysis
- **Accessibility Tools** - ARIA attributes, contrast checking, accessibility audits
- **Form Builder** - Create forms with validation and submission handling
- **Animation System** - Add animations and interactions
- **Theme Builder** - Create and apply design systems
- **Performance Analysis** - Optimize your projects for speed

## 🖥️ Platform Support

CO-web-builder is fully cross-platform:

- **Windows 10+** - Full support (Windows 11 recommended)
  - Windows 7/8: Best effort support (some features may not work)
- **macOS 10.14+** - Full support
- **Linux** - Full support (Ubuntu, Debian, Fedora, Arch, and other distributions)
  - Requires: `libwebkit2gtk-4.0-dev` for embedded preview (optional, falls back to external browser)

Built with Python and CustomTkinter for a consistent experience across all platforms.

## 📦 Installation

### Prerequisites

- **Python 3.10 or higher**
- **pip** (Python package manager)

### Linux Dependencies (Optional)

For embedded preview on Linux, install WebKitGTK:

```bash
# Ubuntu/Debian
sudo apt-get install libwebkit2gtk-4.0-dev

# Fedora
sudo dnf install webkit2gtk3-devel

# Arch Linux
sudo pacman -S webkit2gtk
```

*Note: If WebKitGTK is not installed, the preview will open in your default browser instead.*

### Install from Source

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/CO-web-builder.git
   cd CO-web-builder
   ```

2. **Create a virtual environment (recommended):**

   ```bash
   python -m venv venv
   
   # Windows
   venv\Scripts\activate
   
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**

   ```bash
   python src/main.py
   ```

### Installer Packages (Coming Soon)

- **Windows**: `.exe` installer (Inno Setup)
- **macOS**: `.dmg` disk image
- **Linux**: AppImage, Snap, Flatpak, or deb/rpm packages

## 🚀 Quick Start

1. **Launch CO-web-builder**
2. **Create a New Project** - Click "New Project" or use `Ctrl+N`
3. **Add Elements** - Drag elements from the sidebar onto the canvas
4. **Customize** - Select elements and edit properties in the right panel
5. **Preview** - Click the preview button to see your site in action
6. **Export** - Choose your framework and export your project

### Keyboard Shortcuts

- `Ctrl+N` - New project
- `Ctrl+O` - Open project
- `Ctrl+S` - Save project
- `Ctrl+Shift+S` - Save as
- `Ctrl+E` - Export
- `Ctrl+Z` - Undo
- `Ctrl+Y` - Redo
- `Ctrl+C` - Copy
- `Ctrl+V` - Paste
- `Ctrl+X` - Cut
- `Delete` - Delete selected
- `Ctrl+D` - Duplicate
- `Ctrl+F` - Find
- `Ctrl+P` - Toggle preview
- `F5` - Refresh preview

## 📁 Project Structure

```
CO-web-builder/
├── src/                    # Source code
│   ├── ui/                # User interface components
│   ├── core/              # Core functionality
│   ├── elements/          # UI element components
│   ├── export/            # Export functionality
│   ├── import/            # Import functionality
│   ├── assets/            # Asset management
│   ├── deploy/            # Deployment
│   ├── seo/               # SEO tools
│   ├── accessibility/     # Accessibility tools
│   ├── forms/             # Form functionality
│   ├── animations/        # Animation system
│   ├── components/        # Component library
│   ├── validation/        # Validation tools
│   ├── performance/       # Performance tools
│   ├── themes/            # Theme & design system
│   ├── templates/         # Template system
│   ├── setup/             # Setup wizard
│   └── utils/             # Utility functions
├── app_assets/            # Application resources
├── plans/                 # Planning documentation
├── tests/                 # Unit tests
├── docs/                  # Documentation
└── requirements.txt       # Python dependencies
```

## 🛠️ Development

### Setting Up Development Environment

1. **Clone and install dependencies** (see Installation above)

2. **Install development dependencies:**

   ```bash
   pip install -r requirements-dev.txt
   ```

3. **Run tests:**

   ```bash
   pytest
   ```

4. **Run with debug logging:**

   ```bash
   python src/main.py --debug
   ```

### Code Style

- Follow **PEP 8** style guide
- Use **type hints** where possible
- Add **docstrings** to all functions and classes
- Format code with **black**
- Lint with **pylint** or **flake8**

### Architecture

CO-web-builder follows a modular architecture:

- **UI Layer** - CustomTkinter-based interface
- **Core Layer** - Business logic and data models
- **Export Layer** - Framework-specific code generation
- **Utility Layer** - Cross-platform utilities and helpers

See `plans/` directory for detailed architecture documentation.

## 📚 Documentation

Comprehensive documentation is available in the `plans/` directory:

- **[Tech Stack](plans/techstack.md)** - Technologies and libraries used
- **[Project Structure](plans/structure.md)** - Directory layout and organization
- **[Modules](plans/modules.md)** - Module descriptions and responsibilities
- **[Functions](plans/functions.md)** - Feature list and capabilities
- **[Design](plans/design.md)** - UI/UX design specifications
- **[Styling](plans/styling.md)** - Styling system documentation
- **[Issues & Solutions](plans/issues_and_solutions.md)** - Known issues and workarounds
- **[Private Documentation](plans/private%20dcumentation.md)** - Implementation notes and technical decisions

## 🐛 Known Issues & Limitations

### Current Limitations

- **HTML/CSS Import**: Phase 1 supports structure only. Complex CSS may not import perfectly.
- **Code Editor Sync**: Phase 1 supports one-way sync (visual → code). Two-way sync coming in Phase 2.
- **Windows 7/8**: Best effort support. Some features may not work. Windows 10+ recommended.

### Performance

- Large projects (100+ elements) may experience slower performance
- Virtual scrolling and lazy rendering help mitigate this
- Performance optimizations are ongoing

See [Issues & Solutions](plans/issues_and_solutions.md) for detailed information and workarounds.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add some amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Contribution Guidelines

- Follow the code style guidelines
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass
- Test on multiple platforms if possible

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **CustomTkinter** - Modern GUI framework
- **pywebview** - Embedded browser for preview
- **Jinja2** - Template engine for code generation
- All the amazing open-source libraries that make this possible

## 📧 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/CO-web-builder/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/CO-web-builder/discussions)

## 🗺️ Roadmap

### Phase 1 (Current)

- ✅ Core visual editor
- ✅ Basic element types
- ✅ HTML/CSS/JS export
- ✅ Live preview
- ✅ Project management

### Phase 2 (In Progress)

- 🔄 Multi-framework export (React, Vue, Next.js, etc.)
- 🔄 Code editor with syntax highlighting
- 🔄 Import HTML/CSS/JS
- 🔄 Asset management
- 🔄 Auto-save & version history

### Phase 3 (Planned)

- 📋 Deployment integration
- 📋 SEO tools
- 📋 Accessibility tools
- 📋 Form builder
- 📋 Animation system

### Phase 4 (Future)

- 🔮 Component library
- 🔮 Theme builder
- 🔮 Template marketplace
- 🔮 Collaboration features
- 🔮 Plugin system

---

**Made with ❤️ for web developers and designers by cowebs.lb(https://cowebslb.com)**

*Build beautiful websites without writing code.*
