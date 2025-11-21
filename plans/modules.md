# Modules & Components

## Core Modules

### 1. Main Application (`app.py`)

**Purpose**: Application entry point and main controller
**Responsibilities**:

- Initialize application
- Manage application lifecycle
- Coordinate between modules
- Handle global events

**Key Classes**:

- `WebBuilderApp`: Main application class

### 2. Project Management (`core/project.py`)

**Purpose**: Handle project creation, loading, saving
**Responsibilities**:

- Create new projects
- Load existing projects (.coweb files)
- Save project state
- Manage project metadata
- Export to HTML/CSS/JS
- Project versioning and migration

**Key Classes**:

- `Project`: Project data model
- `ProjectManager`: Project operations
- `ProjectMigrator`: Handle project file version migrations

**Key Functions**:

- `load_project(path)`: Load project with version checking
- `migrate_project(data, from_version, to_version)`: Migrate project format

### 2b. Configuration Manager (`core/config.py`)

**Purpose**: Centralized configuration management
**Responsibilities**:

- Load and save user settings
- Default configuration
- Configuration validation
- Settings UI integration

**Key Classes**:

- `ConfigManager`: Main configuration manager
- `Config`: Configuration data model

**Key Functions**:

- `load_config()`: Load user configuration
- `save_config()`: Save configuration
- `get_setting(key)`: Get setting value
- `set_setting(key, value)`: Set setting value
- `reset_to_defaults()`: Reset to default settings

### 3. Element System (`core/element.py`, `elements/`)

**Purpose**: Define and manage UI elements
**Responsibilities**:

- Base element structure
- Element properties
- Element hierarchy (parent/child)
- Element serialization/deserialization

**Key Classes**:

- `BaseElement`: Abstract base class
- `TextElement`: Text/paragraph elements
- `ImageElement`: Image elements
- `ButtonElement`: Button elements
- `ContainerElement`: Container/div elements
- `HeadingElement`: H1-H6 headings
- `LinkElement`: Anchor/link elements
- `FormElement`: Form inputs

**Element Properties**:

- ID, classes, attributes
- Content (text, src, href, etc.)
- Layout (position, size, margin, padding)
- Style (colors, fonts, borders, etc.)

### 4. HTML Generator (`core/html_generator.py`)

**Purpose**: Convert element tree to HTML
**Responsibilities**:

- Traverse element tree
- Generate semantic HTML
- Handle attributes
- Format output

**Key Functions**:

- `generate_html(element_tree)`: Main generation function
- `element_to_html(element)`: Convert single element

### 5. CSS Generator (`core/css_generator.py`)

**Purpose**: Generate CSS from element styles
**Responsibilities**:

- Convert style properties to CSS
- Handle responsive breakpoints
- Generate class-based CSS
- Minify output (optional)

**Key Functions**:

- `generate_css(element_tree)`: Main generation function
- `styles_to_css(styles)`: Convert style dict to CSS

### 6. Preview Engine (`preview/preview_engine.py`)

**Purpose**: Render live preview
**Responsibilities**:

- Generate temporary HTML/CSS
- Load in webview (with fallback to external browser)
- Handle live updates
- Responsive preview modes
- Detect webview backend availability
- Check Linux dependencies

**Key Classes**:

- `PreviewEngine`: Preview rendering
- `LiveReload`: Auto-refresh on changes
- `WebviewBackend`: Webview backend detection and management
- `BrowserFallback`: External browser fallback

**Key Functions**:

- `check_webview_availability()`: Detect if webview backend is available
- `check_linux_dependencies()`: Check for WebKitGTK on Linux
- `show_preview(html_content)`: Show preview (webview or external browser)
- `open_external_browser(html_content)`: Fallback to external browser
- `warn_missing_dependencies()`: Warn user about missing dependencies

## UI Modules

### 7. Main Window (`ui/main_window.py`)

**Purpose**: Main application window container
**Responsibilities**:

- Window setup and layout
- Menu bar
- Window management
- Event coordination

**Key Classes**:

- `MainWindow`: Main window class

### 8. Toolbar (`ui/toolbar.py`)

**Purpose**: Top toolbar with actions
**Responsibilities**:

- File operations buttons
- Edit operations
- View controls
- Quick actions

**Key Classes**:

- `Toolbar`: Toolbar widget

### 9. Sidebar (`ui/sidebar.py`)

**Purpose**: Component library panel
**Responsibilities**:

- Display available components
- Component categories
- Search/filter
- Drag source for components

**Key Classes**:

- `Sidebar`: Sidebar widget
- `ComponentLibrary`: Component list

### 10. Canvas (`ui/canvas.py`)

**Purpose**: Visual editing area
**Responsibilities**:

- Render elements visually
- Handle drag & drop
- Selection management
- Inline editing
- Resize handles

**Key Classes**:

- `Canvas`: Main canvas widget
- `ElementWidget`: Visual representation of element

### 11. Properties Panel (`ui/properties_panel.py`)

**Purpose**: Element property editor
**Responsibilities**:

- Display selected element properties
- Property input fields
- Live updates
- Tabbed interface (Content/Layout/Style/Advanced)

**Key Classes**:

- `PropertiesPanel`: Properties editor
- `PropertyEditor`: Individual property editor

### 12. Preview Panel (`ui/preview_panel.py`)

**Purpose**: Live HTML preview
**Responsibilities**:

- Embed webview
- Display preview
- Handle responsive views
- Refresh controls

**Key Classes**:

- `PreviewPanel`: Preview widget

### 13. Status Bar (`ui/statusbar.py`)

**Purpose**: Status information display
**Responsibilities**:

- Show selected element info
- Display cursor position
- Show zoom level
- Project status indicator

**Key Classes**:

- `StatusBar`: Status bar widget

## Utility Modules

### 14. File Manager (`utils/file_manager.py`)

**Purpose**: File operations
**Responsibilities**:

- Save/load project files
- Export HTML/CSS/JS
- File dialogs
- Recent files

**Key Functions**:

- `save_project(project, path)`
- `load_project(path)`
- `export_project(project, output_dir)`

### 15. Validators (`utils/validators.py`)

**Purpose**: Input validation
**Responsibilities**:

- Validate CSS values
- Validate HTML attributes
- Validate file paths
- Validate URLs

**Key Functions**:

- `validate_color(value)`
- `validate_size(value)`
- `validate_url(value)`

### 16. Helpers (`utils/helpers.py`)

**Purpose**: Common utility functions
**Responsibilities**:

- Color conversion
- Unit conversion
- String formatting
- Common calculations

**Key Functions**:

- `hex_to_rgb(hex)`
- `px_to_em(px, base)`
- `sanitize_filename(name)`

### 16b. Error Handler (`utils/error_handler.py`)

**Purpose**: Centralized error handling and user-friendly error messages
**Responsibilities**:

- Catch and log errors
- Display user-friendly error messages
- Error reporting UI
- Error recovery suggestions

**Key Functions**:

- `handle_error(error, context)`: Handle and log error
- `show_error_dialog(message, details)`: Display error to user
- `log_error(error, context)`: Log error to file

### 16c. Logger (`utils/logger.py`)

**Purpose**: Application logging configuration
**Responsibilities**:

- Configure logging system
- Log to file and console
- Log rotation
- Log levels

**Key Functions**:

- `setup_logging()`: Initialize logging
- `get_logger(name)`: Get logger instance
- `set_log_level(level)`: Set logging level

### 16d. Drag & Drop (`utils/drag_drop.py`)

**Purpose**: Custom drag & drop implementation (replaces tkinterdnd2)
**Responsibilities**:

- Mouse event tracking (Button-1 press → Motion → Button-1 release)
- Drag state management
- Visual feedback (semi-transparent overlay widget)
- Drop zone detection
- Grid snapping (optional)
- Motion event debouncing (don't move widget every pixel)

**Key Classes**:

- `DragDropHandler`: Main drag & drop handler
- `DragState`: Drag state tracking
- `OverlayWidget`: Semi-transparent rectangle showing what's being dragged

**Key Functions**:

- `start_drag(widget, data)`: Start drag operation (on mouse down)
- `handle_drag(event)`: Handle drag motion (debounced)
- `handle_drop(event)`: Handle drop (on mouse up)
- `snap_to_grid(position)`: Snap position to grid if enabled
- `show_overlay(data)`: Show visual feedback overlay
- `hide_overlay()`: Hide overlay

**Implementation Notes**:
- Default: Custom implementation always enabled
- Optional: tkinterdnd2 fallback (feature flag, user must explicitly enable)
- Predictable behavior across all OSes
- CustomTkinter styling works perfectly

### 16e. Backup Manager (`utils/backup.py`)

**Purpose**: Backup and recovery system
**Responsibilities**:

- Auto-backup before major operations
- Periodic backups
- Backup restoration
- Backup management

**Key Functions**:

- `create_backup(project)`: Create backup
- `restore_backup(backup_id)`: Restore from backup
- `list_backups()`: List available backups
- `cleanup_old_backups()`: Remove old backups

### 16f. Platform Utilities (`utils/platform_utils.py`)

**Purpose**: Cross-platform utilities and platform detection
**Responsibilities**:

- Platform detection
- Platform-specific path handling (following OS conventions)
- Platform-specific operations
- Cross-platform compatibility layer
- Proper directory management

**Key Functions**:

- `get_platform()`: Detect current platform (Windows/macOS/Linux)
- `get_install_path()`: Get installation directory (from registry/config)
- `get_app_data_path()`: Get application data directory (following OS conventions)
  - Windows: Uses `%APPDATA%` environment variable or `SHGetFolderPath`
  - macOS: Uses `~/Library/Application Support/`
  - Linux: Uses `$XDG_DATA_HOME` or `~/.local/share/`
- `get_config_path()`: Get configuration directory
  - Windows: `%APPDATA%\CO-web-builder\`
  - macOS: `~/Library/Preferences/` (plist) or `~/Library/Application Support/CO-web-builder/`
  - Linux: `$XDG_CONFIG_HOME/CO-web-builder/` or `~/.config/CO-web-builder/`
- `get_cache_path()`: Get cache directory
  - Windows: `%LOCALAPPDATA%\CO-web-builder\cache\`
  - macOS: `~/Library/Caches/CO-web-builder/`
  - Linux: `$XDG_CACHE_HOME/CO-web-builder/` or `~/.cache/CO-web-builder/`
- `get_logs_path()`: Get logs directory
  - Windows: `%LOCALAPPDATA%\CO-web-builder\logs\`
  - macOS: `~/Library/Logs/CO-web-builder/`
  - Linux: `$XDG_STATE_HOME/CO-web-builder/` or `~/.local/state/CO-web-builder/`
- `get_default_install_path()`: Get default installation path
  - Windows: `C:\Program Files\CO-web-builder\` (admin) or `%LOCALAPPDATA%\Programs\CO-web-builder\` (user)
  - macOS: `/Applications/CO-web-builder.app`
  - Linux: `/opt/CO-web-builder/` (system) or `~/.local/share/CO-web-builder/` (user)
- `is_admin()`: Check if running with admin/root privileges
- `request_admin()`: Request admin/root privileges (platform-specific)
- `normalize_path(path)`: Normalize path for current platform
- `ensure_directories()`: Create all necessary directories following OS conventions
- `get_windows_special_folder(csidl)`: Get Windows special folder (Program Files, AppData, etc.)
- `get_xdg_directory(type)`: Get XDG directory (Linux, following XDG Base Directory spec)

## Export Module

### 17. Exporter (`export/exporter.py`)

**Purpose**: Export project to files and frameworks
**Responsibilities**:

- Framework selection dialog
- Generate framework-specific code
- Create framework folder structure
- Copy assets to appropriate locations
- Generate configuration files (package.json, vite.config.js, etc.)
- Create zip archives (optional)

**Key Classes**:

- `ProjectExporter`: Main export coordinator
- `ExportDialog`: Framework selection and options dialog
- `BaseFrameworkExporter`: Abstract base class for framework exporters
- `HTMLExporter`: Vanilla HTML/CSS/JS exporter
- `ReactExporter`: React/JSX exporter
- `VueExporter`: Vue.js/SFC exporter
- `NextJSExporter`: Next.js exporter
- `NuxtExporter`: Nuxt.js exporter
- `SvelteExporter`: Svelte exporter
- `AngularExporter`: Angular exporter

**Key Functions**:

- `export_project(project, framework, output_path, options)`: Main export function
- `show_export_dialog()`: Display framework selection dialog
- `generate_framework_code(project, framework)`: Generate framework-specific code
- `create_project_structure(framework, output_path)`: Create framework folder structure

## Setup Wizard Module (Cross-Platform)

### 18. Setup Wizard (`setup/setup_wizard.py`)

**Purpose**: Cross-platform custom installation wizard for the application
**Responsibilities**:

- Welcome screen
- License agreement
- Installation path selection (platform-appropriate defaults)
- Component selection (optional features)
- Installation progress
- Desktop shortcut creation (platform-specific)
- Application menu entry creation (platform-specific)
- File association (.coweb files, platform-specific)
- Completion screen

**Key Classes**:

- `SetupWizard`: Main wizard window (cross-platform)
- `WizardPage`: Base class for wizard pages
- `WelcomePage`: Welcome/intro page
- `LicensePage`: License agreement page
- `PathSelectionPage`: Installation directory selection
- `ComponentsPage`: Optional component selection
- `ProgressPage`: Installation progress
- `CompletionPage`: Installation complete
- `PlatformDetector`: Detect current platform
- `WindowsInstaller`: Windows-specific installation operations
- `MacOSInstaller`: macOS-specific installation operations
- `LinuxInstaller`: Linux-specific installation operations

**Key Functions**:

- `install_application(install_path, components)`: Main installation function (platform-aware)
- `get_proper_directories()`: Get all proper OS directories (install, appdata, cache, logs)
- `create_directory_structure()`: Create proper directory structure following OS conventions
- `create_shortcuts(install_path)`: Create shortcuts (platform-specific)
  - Windows: Desktop + Start Menu shortcuts
  - macOS: Applications folder + Dock (optional)
  - Linux: Desktop entry + Applications menu
- `register_file_associations()`: Register .coweb file type (platform-specific)
  - Windows: Registry entries (HKEY_CLASSES_ROOT)
  - macOS: Launch Services (UTI, Info.plist)
  - Linux: MIME type + desktop file (xdg-mime)
- `register_uninstaller()`: Register uninstaller (platform-specific)
  - Windows: Add/Remove Programs registry entry
  - macOS: Create uninstaller script
  - Linux: Create uninstaller script
- `copy_files(source, destination)`: Copy application files (cross-platform)
- `get_default_install_path()`: Get platform-appropriate default path
  - Windows: `C:\Program Files\CO-web-builder\` (admin) or `%LOCALAPPDATA%\Programs\CO-web-builder\` (user)
  - macOS: `/Applications/CO-web-builder.app`
  - Linux: `/opt/CO-web-builder/` (system) or `~/.local/share/CO-web-builder/` (user)
- `get_app_data_path()`: Get application data directory
  - Windows: `%APPDATA%\CO-web-builder\`
  - macOS: `~/Library/Application Support/CO-web-builder/`
  - Linux: `$XDG_DATA_HOME/CO-web-builder/` or `~/.local/share/CO-web-builder/`
- `get_cache_path()`: Get cache directory
  - Windows: `%LOCALAPPDATA%\CO-web-builder\cache\`
  - macOS: `~/Library/Caches/CO-web-builder/`
  - Linux: `$XDG_CACHE_HOME/CO-web-builder/` or `~/.cache/CO-web-builder/`
- `get_logs_path()`: Get logs directory
  - Windows: `%LOCALAPPDATA%\CO-web-builder\logs\`
  - macOS: `~/Library/Logs/CO-web-builder/`
  - Linux: `$XDG_STATE_HOME/CO-web-builder/` or `~/.local/state/CO-web-builder/`
- `write_installation_info()`: Write installation metadata to proper location

## Import Module

### 19. HTML/CSS/JS Importer (`import/importer.py`)

**Purpose**: Import existing HTML/CSS/JS files into visual editor
**Responsibilities**:

- Parse HTML structure (phased approach)
- Extract CSS styles (gradual mapping)
- Convert HTML elements to visual elements
- Map styles to element properties
- Handle external CSS/JS files
- Import from other builders (Webflow, Wix exports)
- Backup original HTML/CSS files

**Key Classes**:

- `ProjectImporter`: Main import coordinator
- `HTMLParser`: Parse HTML structure
- `CSSParser`: Extract and parse CSS
- `ElementReconstructor`: Convert HTML to elements
- `StyleMapper`: Map CSS to element properties (phased)
- `ImportBackup`: Backup original files

**Key Functions**:

- `import_html(html_path, css_paths, js_paths)`: Import from files
- `parse_html_structure(html_content)`: Parse HTML (Phase 1: basic elements only)
  - Parse: `<div>`, `<p>`, `<h1-h6>`, `<img>`, `<a>`, `<button>`
  - Ignore: inline scripts, style quirks, external CSS (Phase 1)
- `extract_styles(css_content)`: Extract CSS rules (Phase 2: gradual mapping)
  - Phase 2: Map colors, font sizes, padding/margins
  - Ignore: complex selectors, media queries (first stable release)
- `reconstruct_elements(html_tree)`: Convert to elements
- `backup_original_files(html_path, css_paths)`: Keep backup copy of original files
- `show_import_preview(elements, warnings)`: Show preview with warnings
- `warn_complex_css()`: Warn user about complex CSS limitations

**Implementation Notes**:
- **Phase 1**: Import structure only, warn about CSS limitations
- **Phase 2**: Gradual CSS mapping, ignore complex features initially
- Always keep backup copy of original HTML/CSS (you'll thank yourself later)
- Show import preview before applying
- Warn user: "Complex CSS may not import perfectly"

## Code Editor Module

### 20. Code Editor (`ui/code_editor.py`)

**Purpose**: View and edit generated code
**Responsibilities**:

- Display HTML/CSS/JS code
- Syntax highlighting
- Code editing (phased sync approach)
- Code validation
- Error highlighting
- Split view (visual + code)

**Key Classes**:

- `CodeEditor`: Main code editor widget
- `SyntaxHighlighter`: Syntax highlighting using Pygments
- `CodeValidator`: Validate code syntax
- `CodeSync`: Sync between visual and code (phased approach)

**Key Functions**:

- `display_code(code, language)`: Display code with highlighting
- `sync_to_code()`: Update code from visual editor (Phase 1: always works, always reliable)
- `reload_from_code()`: Manual "Reload from code" button (Phase 1)
- `sync_from_code()`: Update visual editor from code (Phase 2: with debouncing and validation)
- `validate_code(code, language)`: Validate syntax before applying
- `warn_manual_edit()`: Warn when code is manually edited (may lose sync)
- `debounce_sync()`: Debounce code changes (500ms wait after last change, Phase 2)

**Implementation Notes**:
- **Phase 1**: One-way sync only (visual → code), always reliable
- **Phase 2**: Two-way sync with debouncing (500ms), validation, and safeguards
- Keep visual elements immutable until code validated
- Feature flag: Allow users to disable two-way sync if it causes issues

## Asset Management Module

### 21. Asset Manager (`assets/asset_manager.py`)

**Purpose**: Manage project assets (images, fonts, icons)
**Responsibilities**:

- Image library management
- Font management (system + web fonts)
- Icon library
- Asset organization (folders, tags)
- Asset optimization
- Asset usage tracking

**Key Classes**:

- `AssetManager`: Main asset manager
- `ImageLibrary`: Image management
- `FontManager`: Font management
- `IconLibrary`: Icon library
- `AssetOrganizer`: Organization and search

**Key Functions**:

- `add_image(image_path)`: Add image to library
- `optimize_image(image_path)`: Compress/optimize image
- `get_fonts()`: Get available fonts
- `search_assets(query)`: Search assets
- `get_asset_usage(asset_id)`: Track usage

## Auto-Save & Version History Module

### 22. Version Manager (`core/version_manager.py`)

**Purpose**: Auto-save and version history
**Responsibilities**:

- Auto-save at intervals
- Version snapshots
- Version browser
- Restore previous versions
- Crash recovery

**Key Classes**:

- `VersionManager`: Version management
- `AutoSave`: Background auto-save
- `VersionSnapshot`: Version data model
- `VersionBrowser`: UI for browsing versions

**Key Functions**:

- `auto_save(project)`: Save automatically
- `create_snapshot(project)`: Create version snapshot
- `restore_version(version_id)`: Restore version
- `get_version_history()`: Get all versions

## User Onboarding & Help Module

### 23. Onboarding System (`ui/onboarding.py`)

**Purpose**: First-time user tutorial and help system
**Responsibilities**:

- Interactive tutorial
- Help menu and documentation
- Keyboard shortcuts reference
- Context-sensitive help
- Welcome screen

**Key Classes**:

- `OnboardingTutorial`: Interactive walkthrough
- `HelpSystem`: Help menu and docs
- `ShortcutsReference`: Keyboard shortcuts UI
- `WelcomeScreen`: First-time welcome

**Key Functions**:

- `start_tutorial()`: Begin tutorial
- `show_help(topic)`: Show help topic
- `show_shortcuts()`: Display shortcuts

## Deployment Module

### 24. Deployment Manager (`deploy/deployment_manager.py`)

**Purpose**: Deploy projects to hosting services
**Responsibilities**:

- Deploy to Netlify, Vercel, GitHub Pages
- FTP/SFTP upload
- Deployment settings
- Deployment history
- Environment variables
- Secure credential storage

**Key Classes**:

- `DeploymentManager`: Main deployment coordinator
- `NetlifyDeployer`: Netlify deployment
- `VercelDeployer`: Vercel deployment
- `GitHubPagesDeployer`: GitHub Pages deployment
- `FTPDeployer`: FTP/SFTP deployment
- `DeploymentSettings`: Deployment configuration
- `CredentialManager`: Secure credential storage (using keyring)

**Key Functions**:

- `deploy_to_netlify(project, settings)`: Deploy to Netlify
- `deploy_to_vercel(project, settings)`: Deploy to Vercel
- `deploy_via_ftp(project, ftp_settings)`: FTP deployment
- `get_deployment_history()`: Get deployment history
- `store_credentials(service, credentials)`: Store credentials securely
- `get_credentials(service)`: Retrieve credentials

## SEO Tools Module

### 25. SEO Manager (`seo/seo_manager.py`)

**Purpose**: SEO tools and meta tags management
**Responsibilities**:

- Meta tags editor
- SEO analysis
- Sitemap generation
- robots.txt generation
- SEO score calculation

**Key Classes**:

- `SEOManager`: Main SEO coordinator
- `MetaTagsEditor`: Meta tags UI
- `SEOAnalyzer`: SEO analysis
- `SitemapGenerator`: Generate sitemap.xml

**Key Functions**:

- `edit_meta_tags(project)`: Edit meta tags
- `analyze_seo(project)`: Analyze SEO
- `generate_sitemap(project)`: Generate sitemap
- `calculate_seo_score(project)`: Calculate score

## Accessibility Module

### 26. Accessibility Tools (`accessibility/accessibility_tools.py`)

**Purpose**: Accessibility checking and ARIA attributes
**Responsibilities**:

- ARIA attributes editor
- Accessibility checker
- Color contrast checking
- Alt text validation
- Accessibility warnings

**Key Classes**:

- `AccessibilityManager`: Main accessibility coordinator
- `ARIAEditor`: ARIA attributes editor
- `AccessibilityChecker`: Check accessibility
- `ContrastChecker`: Color contrast validation

**Key Functions**:

- `check_accessibility(project)`: Run accessibility check
- `check_contrast(color1, color2)`: Check color contrast
- `validate_alt_text()`: Validate alt attributes
- `get_accessibility_warnings()`: Get warnings

## Form Functionality Module

### 27. Form Handler (`forms/form_handler.py`)

**Purpose**: Form building and submission handling
**Responsibilities**:

- Form validation rules
- Form submission code generation
- API endpoint configuration
- Email submission (optional, for testing)
- Success/error messages
- Backend code generation (example code)

**Key Classes**:

- `FormHandler`: Form management
- `FormValidator`: Validation rules
- `FormCodeGenerator`: Generate form submission code
- `BackendCodeGenerator`: Generate example backend code

**Key Functions**:

- `add_validation_rule(field, rule)`: Add validation
- `generate_form_code(form, action_url)`: Generate form HTML with action
- `generate_backend_example(form, language)`: Generate example backend (Node.js, Python, PHP)
- `configure_email_submission(form, smtp_settings)`: Configure email (testing only, with warnings)

## Animation & Interactions Module

### 28. Animation System (`animations/animation_system.py`)

**Purpose**: Animation and interaction builder
**Responsibilities**:

- Animation timeline editor
- Keyframe management
- Transition effects
- Interaction triggers
- Animation preview

**Key Classes**:

- `AnimationSystem`: Main animation coordinator
- `TimelineEditor`: Animation timeline UI
- `KeyframeManager`: Keyframe management
- `TransitionBuilder`: Transition effects
- `InteractionBuilder`: Interaction triggers

**Key Functions**:

- `create_animation(element, keyframes)`: Create animation
- `add_transition(element, transition)`: Add transition
- `set_interaction(element, trigger, action)`: Set interaction

## Component Library Module

### 29. Component Library (`components/component_library.py`)

**Purpose**: Save and reuse components
**Responsibilities**:

- Save element groups as components
- Component library browser
- Component search and categories
- Component properties
- Component import/export

**Key Classes**:

- `ComponentLibrary`: Main component manager
- `ComponentSaver`: Save components
- `ComponentBrowser`: Browse components
- `Component`: Component data model

**Key Functions**:

- `save_component(elements, name)`: Save component
- `load_component(component_id)`: Load component
- `search_components(query)`: Search components
- `export_component(component_id)`: Export component

## Validation & Testing Module

### 30. Validation Tools (`validation/validation_tools.py`)

**Purpose**: HTML/CSS validation and link checking
**Responsibilities**:

- HTML validation (W3C)
- CSS validation
- Link checking
- Browser compatibility checking
- Real-time validation

**Key Classes**:

- `ValidationManager`: Main validation coordinator
- `HTMLValidator`: HTML validation
- `CSSValidator`: CSS validation
- `LinkChecker`: Check links
- `BrowserCompatibilityChecker`: Browser checks

**Key Functions**:

- `validate_html(html)`: Validate HTML
- `validate_css(css)`: Validate CSS
- `check_links(project)`: Check all links
- `get_validation_errors()`: Get errors

## Performance Tools Module

### 31. Performance Analyzer (`performance/performance_analyzer.py`)

**Purpose**: Performance analysis and optimization
**Responsibilities**:

- Page load time estimation
- Asset size analysis
- Optimization suggestions
- Unused CSS detection
- Performance reports

**Key Classes**:

- `PerformanceAnalyzer`: Main analyzer
- `LoadTimeEstimator`: Estimate load times
- `AssetAnalyzer`: Analyze assets
- `OptimizationSuggester`: Suggest optimizations

**Key Functions**:

- `analyze_performance(project)`: Run analysis
- `estimate_load_time(project)`: Estimate load time
- `get_optimization_suggestions()`: Get suggestions

## Theme & Design System Module

### 32. Theme Manager (`themes/theme_manager.py`)

**Purpose**: Theme and design system management
**Responsibilities**:

- Color palette management
- Design tokens (spacing, typography, etc.)
- Theme builder
- Theme save/load
- Theme export

**Key Classes**:

- `ThemeManager`: Main theme coordinator
- `ColorPaletteManager`: Color palettes
- `DesignTokenManager`: Design tokens
- `ThemeBuilder`: Theme creation UI

**Key Functions**:

- `create_palette(colors)`: Create color palette
- `define_tokens(tokens)`: Define design tokens
- `save_theme(theme)`: Save theme
- `apply_theme(theme)`: Apply to project

## Template System Module

### 33. Template Manager (`templates/template_manager.py`)

**Purpose**: Project template management
**Responsibilities**:

- Template categories
- Template preview
- Template loading
- Template marketplace (future)

**Key Classes**:

- `TemplateManager`: Main template coordinator
- `TemplateBrowser`: Browse templates
- `TemplateLoader`: Load templates
- `Template`: Template data model

**Key Functions**:

- `get_templates(category)`: Get templates by category
- `preview_template(template_id)`: Preview template
- `load_template(template_id)`: Load template

## Module Dependencies

```
app.py
  ├── ui/main_window.py
  │     ├── ui/toolbar.py
  │     ├── ui/sidebar.py
  │     ├── ui/canvas.py
  │     ├── ui/properties_panel.py
  │     ├── ui/preview_panel.py
  │     ├── ui/code_editor.py
  │     ├── ui/statusbar.py
  │     └── ui/onboarding.py
  ├── core/project.py
  │     ├── core/element.py
  │     ├── core/html_generator.py
  │     ├── core/css_generator.py
  │     └── core/version_manager.py
  ├── preview/preview_engine.py
  ├── export/
  │     ├── exporter.py
  │     ├── export_dialog.py
  │     └── frameworks/
  ├── import/
  │     └── importer.py
  ├── assets/
  │     └── asset_manager.py
  ├── deploy/
  │     └── deployment_manager.py
  ├── seo/
  │     └── seo_manager.py
  ├── accessibility/
  │     └── accessibility_tools.py
  ├── forms/
  │     └── form_handler.py
  ├── animations/
  │     └── animation_system.py
  ├── components/
  │     └── component_library.py
  ├── validation/
  │     └── validation_tools.py
  ├── performance/
  │     └── performance_analyzer.py
  ├── themes/
  │     └── theme_manager.py
  ├── templates/
  │     └── template_manager.py
  ├── setup/setup_wizard.py
  └── utils/
```
