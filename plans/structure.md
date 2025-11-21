# Project Structure

## Directory Layout

```
CO-web-builder/
├── src/
│   ├── __init__.py
│   ├── main.py                 # Application entry point
│   ├── app.py                  # Main application class
│   │
│   ├── ui/                     # User interface components
│   │   ├── __init__.py
│   │   ├── main_window.py      # Main window container
│   │   ├── toolbar.py          # Top toolbar
│   │   ├── sidebar.py          # Left sidebar (components/elements)
│   │   ├── properties_panel.py # Right panel (element properties)
│   │   ├── canvas.py           # Central canvas/editor area
│   │   ├── preview_panel.py    # Preview window/panel
│   │   └── statusbar.py        # Bottom status bar
│   │
│   ├── core/                   # Core functionality
│   │   ├── __init__.py
│   │   ├── project.py          # Project management
│   │   ├── element.py          # Base element class
│   │   ├── html_generator.py   # HTML code generation
│   │   ├── css_generator.py    # CSS code generation
│   │   ├── js_generator.py     # JavaScript generation (if needed)
│   │   ├── config.py           # Configuration management
│   │   └── migration.py        # Project file version migration
│   │
│   ├── elements/               # UI element components
│   │   ├── __init__.py
│   │   ├── base_element.py     # Base class for all elements
│   │   ├── text_element.py     # Text/paragraph elements
│   │   ├── image_element.py    # Image elements
│   │   ├── button_element.py   # Button elements
│   │   ├── container_element.py # Div/container elements
│   │   ├── heading_element.py  # H1-H6 elements
│   │   ├── link_element.py     # Anchor/link elements
│   │   └── form_elements.py    # Form inputs, etc.
│   │
│   ├── utils/                  # Utility functions
│   │   ├── __init__.py
│   │   ├── file_manager.py     # File operations
│   │   ├── validators.py       # Input validation
│   │   ├── helpers.py          # Helper functions
│   │   ├── constants.py        # Constants and enums
│   │   ├── platform_utils.py   # Cross-platform utilities
│   │   ├── error_handler.py    # Centralized error handling
│   │   ├── logger.py           # Logging configuration
│   │   ├── drag_drop.py        # Custom drag & drop implementation
│   │   └── backup.py           # Backup and recovery
│   │
│   ├── preview/                # Preview functionality
│   │   ├── __init__.py
│   │   ├── preview_engine.py   # Preview rendering engine
│   │   └── live_reload.py      # Live preview updates
│   │
│   └── export/                 # Export functionality
│       ├── __init__.py
│       ├── exporter.py         # Main export coordinator
│       ├── export_dialog.py    # Framework selection dialog
│       ├── frameworks/         # Framework-specific exporters
│       │   ├── __init__.py
│       │   ├── base_exporter.py    # Base exporter class
│       │   ├── html_exporter.py    # Vanilla HTML/CSS/JS
│       │   ├── react_exporter.py   # React/JSX
│       │   ├── vue_exporter.py     # Vue.js
│       │   ├── nextjs_exporter.py  # Next.js
│       │   ├── nuxt_exporter.py    # Nuxt.js
│       │   ├── svelte_exporter.py  # Svelte
│       │   └── angular_exporter.py # Angular
│       └── templates/          # Jinja2 templates for frameworks
│           ├── react/
│           ├── vue/
│           ├── nextjs/
│           ├── nuxt/
│           ├── svelte/
│           └── angular/
│   │
│   └── setup/                  # Setup wizard (cross-platform)
│       ├── __init__.py
│       ├── setup_wizard.py     # Main setup wizard (cross-platform)
│       ├── wizard_pages.py     # Individual wizard pages
│       ├── installer.py        # Cross-platform installation operations
│       ├── platform_installers/ # Platform-specific installers
│       │   ├── __init__.py
│       │   ├── windows_installer.py  # Windows-specific operations
│       │   ├── macos_installer.py    # macOS-specific operations
│       │   └── linux_installer.py    # Linux-specific operations
│       └── uninstaller.py      # Uninstaller script (platform-specific)
│   │
│   ├── import/                 # Import functionality
│   │   ├── __init__.py
│   │   ├── importer.py         # Main importer
│   │   ├── html_parser.py      # HTML parsing
│   │   ├── css_parser.py       # CSS parsing
│   │   └── element_reconstructor.py # Convert HTML to elements
│   │
│   ├── assets/                 # Asset management
│   │   ├── __init__.py
│   │   ├── asset_manager.py    # Main asset manager
│   │   ├── image_library.py    # Image management
│   │   ├── font_manager.py     # Font management
│   │   └── icon_library.py     # Icon library
│   │
│   ├── deploy/                 # Deployment
│   │   ├── __init__.py
│   │   ├── deployment_manager.py # Main deployment coordinator
│   │   ├── netlify_deployer.py # Netlify deployment
│   │   ├── vercel_deployer.py  # Vercel deployment
│   │   ├── github_pages_deployer.py # GitHub Pages
│   │   └── ftp_deployer.py     # FTP/SFTP deployment
│   │
│   ├── seo/                    # SEO tools
│   │   ├── __init__.py
│   │   ├── seo_manager.py      # Main SEO coordinator
│   │   ├── meta_tags_editor.py # Meta tags UI
│   │   ├── seo_analyzer.py     # SEO analysis
│   │   └── sitemap_generator.py # Sitemap generation
│   │
│   ├── accessibility/          # Accessibility tools
│   │   ├── __init__.py
│   │   ├── accessibility_tools.py # Main accessibility coordinator
│   │   ├── aria_editor.py      # ARIA attributes editor
│   │   ├── accessibility_checker.py # Accessibility checking
│   │   └── contrast_checker.py # Color contrast checking
│   │
│   ├── forms/                  # Form functionality
│   │   ├── __init__.py
│   │   ├── form_handler.py     # Form management
│   │   ├── form_validator.py   # Validation rules
│   │   └── form_submitter.py   # Submission handling
│   │
│   ├── animations/             # Animation system
│   │   ├── __init__.py
│   │   ├── animation_system.py # Main animation coordinator
│   │   ├── timeline_editor.py  # Timeline UI
│   │   ├── keyframe_manager.py # Keyframe management
│   │   └── interaction_builder.py # Interaction builder
│   │
│   ├── components/             # Component library
│   │   ├── __init__.py
│   │   ├── component_library.py # Main component manager
│   │   ├── component_saver.py  # Save components
│   │   └── component_browser.py # Browse components
│   │
│   ├── validation/             # Validation tools
│   │   ├── __init__.py
│   │   ├── validation_tools.py # Main validation coordinator
│   │   ├── html_validator.py   # HTML validation
│   │   ├── css_validator.py    # CSS validation
│   │   └── link_checker.py     # Link checking
│   │
│   ├── performance/            # Performance tools
│   │   ├── __init__.py
│   │   ├── performance_analyzer.py # Main analyzer
│   │   ├── load_time_estimator.py # Load time estimation
│   │   └── optimization_suggester.py # Optimization suggestions
│   │
│   ├── themes/                 # Theme & design system
│   │   ├── __init__.py
│   │   ├── theme_manager.py    # Main theme coordinator
│   │   ├── color_palette_manager.py # Color palettes
│   │   └── design_token_manager.py # Design tokens
│   │
│   └── templates/              # Template system
│       ├── __init__.py
│       ├── template_manager.py # Main template coordinator
│       ├── template_browser.py # Browse templates
│       └── template_loader.py  # Load templates
│
├── app_assets/                 # Application resources (bundled with app)
│   ├── icons/                  # Application icons
│   ├── templates/              # Default project templates
│   ├── themes/                 # UI themes
│   ├── fonts/                  # Custom fonts
│   └── icons_library/          # Icon sets (Font Awesome, etc.)
│
├── projects/                   # Example projects (for development/testing)
│   └── .gitkeep
│
# Note: User data is stored in OS-appropriate directories at runtime:
# Windows: %APPDATA%\CO-web-builder\ (settings, projects, components, etc.)
# macOS: ~/Library/Application Support/CO-web-builder/
# Linux: ~/.local/share/CO-web-builder/
│
├── tests/                      # Unit tests
│   ├── __init__.py
│   ├── test_elements.py
│   ├── test_generators.py
│   └── test_project.py
│
├── docs/                       # Documentation
│   └── user_guide.md
│
├── requirements.txt            # Python dependencies (cross-platform)
├── requirements-windows.txt    # Windows-specific dependencies
├── requirements-macos.txt      # macOS-specific dependencies
├── requirements-linux.txt      # Linux-specific dependencies
├── setup.py                    # Package setup
├── setup_wizard.py             # Setup wizard entry point (standalone, cross-platform)
├── build_installer.py          # Script to build installer packages (cross-platform)
├── build_windows.py            # Windows installer build script
├── build_macos.py              # macOS installer build script
├── build_linux.py              # Linux package build script
├── README.md
├── LICENSE
└── .gitignore
```

## File Organization Principles

1. **Separation of Concerns** - UI, core logic, and utilities are separated
2. **Modular Design** - Each element type is its own module
3. **Extensibility** - Easy to add new element types
4. **Testability** - Core logic separated from UI for easier testing

## Data Flow

```
User Action → UI Component → Core Logic → Element Model → Generator → Preview/Export
```

## Project File Format (.coweb)

```json
{
  "version": "1.0",
  "name": "Project Name",
  "created": "2024-01-01T00:00:00",
  "modified": "2024-01-01T00:00:00",
  "elements": [...],
  "styles": {...},
  "settings": {...}
}
```
