# Private Documentation (Internal Notes)

## Implementation Notes

### Phase 1: Core Foundation

1. **Setup Project Structure**
   - Create directory structure
   - Rename `assets/` to `app_assets/` (avoid conflict with `src/assets/`)
   - Remove `user_data/` from source (use runtime directories)
   - Set up Python environment
   - Install dependencies
   - Create basic main.py entry point

2. **Error Handling & Logging Foundation**
   - Set up logging system (`utils/logger.py`)
   - Create error handler (`utils/error_handler.py`)
   - Configure log file location (via platform_utils)
   - Error reporting UI
   - Test error handling on all platforms

3. **Configuration Management**
   - Create configuration manager (`core/config.py`)
   - Default configuration structure
   - User configuration loading/saving
   - Configuration file location (via platform_utils)
   - Settings validation

4. **Platform Utilities**
   - Implement `platform_utils.py` with all path functions
   - Test on all platforms (Windows, macOS, Linux)
   - Verify proper directory detection
   - Handle edge cases (missing directories, permissions)

5. **Basic UI Framework**
   - Set up CustomTkinter main window
   - Create basic layout (toolbar, sidebar, canvas, properties)
   - Implement window resizing
   - Basic styling/theming
   - Integrate error handling and logging

6. **Element System Foundation**
   - Create BaseElement class
   - Implement element data model
   - Element serialization (to dict/JSON)
   - Element deserialization (from dict/JSON)
   - Include version in serialization

7. **Project Management**
   - Project class structure
   - Save/load project files (.coweb JSON format)
   - Project versioning (include version in file)
   - Migration system foundation (`core/migration.py`)
   - Basic file operations
   - Backup before save (via backup manager)

### Phase 2: Visual Editor

1. **Canvas Implementation**
   - Canvas widget with CustomTkinter
   - Render elements visually
   - Basic selection system
   - Click to select elements

2. **Element Rendering**
   - Visual representation of elements
   - Different visuals for different element types
   - Selection highlighting
   - Resize handles (visual only initially)

3. **Drag & Drop**
   - **Primary**: Scrap tkinterdnd2, implement custom drag & drop manager
     - Track mouse down → start drag
     - Track motion → move overlay widget (semi-transparent rectangle)
     - Track mouse up → drop logic, snap to grid if needed
     - Debounce motion events (don't move widget every pixel)
     - Visual feedback: overlay widget showing what's being dragged
   - **Default**: Custom implementation always enabled
   - **Optional**: tkinterdnd2 fallback (feature flag, user must explicitly enable)
   - Drag from sidebar to canvas
   - Drag elements on canvas to reposition
   - Predictable behavior across all OSes
   - CustomTkinter styling works perfectly

4. **Properties Panel**
   - Basic property editor
   - Text inputs for properties
   - Update element on change
   - Reflect changes in canvas

### Phase 3: Element Types

1. **Basic Elements**
   - TextElement (paragraph)
   - HeadingElement (H1-H6)
   - ImageElement
   - ButtonElement
   - ContainerElement (div)

2. **Element Properties**
   - Content properties (text, src, etc.)
   - Basic layout properties (width, height)
   - Basic style properties (color, background)

3. **Element Hierarchy**
   - Parent/child relationships
   - Nesting elements
   - Visual hierarchy in canvas

### Phase 4: HTML/CSS Generation

1. **HTML Generator**
   - Traverse element tree
   - Generate HTML structure
   - Handle attributes
   - Format output

2. **CSS Generator**
   - Convert style properties to CSS
   - Generate class-based CSS
   - Handle element-specific styles
   - Format output

3. **Preview System**
   - **Backend Detection**: Check webview availability on startup
     - Try to import webview and create test window
     - Log warnings if unavailable
   - **Platform Handling**:
     - Windows: EdgeWebView2 (straightforward)
     - macOS: WebKit (straightforward)
     - Linux: WebKitGTK (finicky, check for libwebkit2gtk-4.0-dev)
   - **Fallback**: Use external browser if webview unavailable
     - Create temp HTML file
     - Open with webbrowser module
   - **Linux Dependencies**: Detect distro and warn if library missing
   - Generate temporary HTML/CSS
   - Load in preview
   - Basic refresh mechanism

### Phase 5: Advanced Editing

1. **Inline Editing**
   - Double-click to edit text
   - Inline text input
   - Update on change

2. **Advanced Properties**
   - Color picker
   - Font selector
   - Spacing visual editor
   - Border editor

3. **Undo/Redo**
   - Action history system
   - Track changes
   - Undo/redo functionality

### Phase 6: Styling System

1. **Style Properties**
   - Typography controls
   - Color/background controls
   - Layout/spacing controls
   - Border controls

2. **Responsive Design**
   - Breakpoint system
   - Responsive property values
   - Viewport switcher

3. **Advanced CSS**
   - Custom CSS editor
   - CSS variables
   - Media queries

### Phase 7: Export & Polish

1. **Basic Export System**
   - Export to HTML file
   - Export to folder structure
   - Copy assets
   - Basic export options

2. **Multi-Framework Export System**
   - **Export Dialog UI**
     - Framework selection (radio buttons)
     - Framework descriptions
     - Output options (folder/ZIP, formatting, etc.)
     - Output location selection
     - Progress tracking

   - **Framework Exporters**
     - Base exporter class (abstract interface)
     - HTML/CSS/JS exporter (vanilla)
     - React exporter (JSX components, hooks)
     - Vue.js exporter (SFC, Composition API)
     - Next.js exporter (React with SSR/SSG)
     - Nuxt.js exporter (Vue with SSR/SSG)
     - Svelte exporter (Svelte components)
     - Angular exporter (TypeScript components)

   - **Code Generation**
     - Convert elements to framework components
     - Generate framework-specific structure
     - Create configuration files (package.json, etc.)
     - Generate README with setup instructions
     - Handle assets and dependencies

   - **Template System**
     - Jinja2 templates for each framework
     - Component templates
     - Configuration file templates
     - README templates

   - **Export Features**
     - Folder or ZIP output
     - Code formatting/beautification
     - Minification option
     - TypeScript support (where applicable)
     - Framework-specific options

3. **UI Polish**
   - Improve visual design
   - Add icons
   - Improve tooltips
   - Keyboard shortcuts

4. **Testing & Bug Fixes**
   - Test all features
   - Test framework exports
   - Fix bugs
   - Performance optimization

### Phase 8: Setup Wizard (Cross-Platform)

1. **Setup Wizard UI (Cross-Platform)**
   - Create CustomTkinter-based wizard window
   - Multi-page wizard interface
   - Navigation (Back/Next/Cancel)
   - Progress indicator
   - Platform detection

2. **Wizard Pages**
   - Welcome page (intro and overview)
   - License agreement page (read and accept)
   - Installation path selection (platform-appropriate defaults)
   - Component selection (checkboxes for optional features)
   - Installation progress page (progress bar, status text)
   - Completion page (success message, launch option)

3. **Platform-Specific Installation Operations (Following OS Conventions)**
   - **Windows**:
     - **Installation Directory**:
       - System: `C:\Program Files\CO-web-builder\` (requires admin)
       - User: `%LOCALAPPDATA%\Programs\CO-web-builder\` (no admin)
     - **Application Data**: `%APPDATA%\CO-web-builder\` (settings, preferences)
     - **Cache**: `%LOCALAPPDATA%\CO-web-builder\cache\` (temp files, cache)
     - **Logs**: `%LOCALAPPDATA%\CO-web-builder\logs\` (application logs)
     - File copying to installation directory
     - Create proper directory structure
     - Create desktop shortcut (pywin32, `%USERPROFILE%\Desktop\`)
     - Create Start Menu entry (`%APPDATA%\Microsoft\Windows\Start Menu\Programs\`)
     - Register file associations (.coweb files via HKEY_CLASSES_ROOT)
     - Register in Add/Remove Programs (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\)
     - Store installation info in registry
     - Create uninstaller executable
   - **macOS**:
     - **Installation Directory**: `/Applications/CO-web-builder.app`
     - **Application Support**: `~/Library/Application Support/CO-web-builder/`
     - **Caches**: `~/Library/Caches/CO-web-builder/`
     - **Preferences**: `~/Library/Preferences/com.coweb.builder.plist`
     - **Logs**: `~/Library/Logs/CO-web-builder/`
     - Create .app bundle with proper structure
     - Copy to Applications folder
     - Set bundle identifier in Info.plist
     - Register file associations (UTI in Info.plist, Launch Services)
     - Create Dock shortcut (optional, via plist)
     - Create uninstaller script
   - **Linux** (Following XDG Base Directory Specification):
     - **Installation Directory**:
       - System: `/opt/CO-web-builder/` or `/usr/local/CO-web-builder/` (requires root)
       - User: `~/.local/share/CO-web-builder/` (no root)
     - **Data Home**: `$XDG_DATA_HOME/CO-web-builder/` (default: `~/.local/share/CO-web-builder/`)
     - **Config Home**: `$XDG_CONFIG_HOME/CO-web-builder/` (default: `~/.config/CO-web-builder/`)
     - **Cache Home**: `$XDG_CACHE_HOME/CO-web-builder/` (default: `~/.cache/CO-web-builder/`)
     - **State Home**: `$XDG_STATE_HOME/CO-web-builder/` (default: `~/.local/state/CO-web-builder/`)
     - Install to proper directory
     - Create proper directory structure
     - Create desktop entry file (`~/.local/share/applications/CO-web-builder.desktop`)
     - Add to Applications menu (via desktop file)
     - Register MIME type (.coweb files via xdg-mime)
     - Create uninstaller script
     - Store installation info in config file

4. **Error Handling & Validation (Cross-Platform)**
   - Check disk space
   - Validate installation path
   - Handle permission errors
   - Rollback on failure
   - Admin/root rights detection/request
     - Windows: UAC elevation
     - macOS: Admin password prompt
     - Linux: sudo/root privileges

5. **Cross-Platform Packaging**
   - **Windows**:
     - Bundle with PyInstaller (.exe)
     - Create installer with Inno Setup or NSIS
   - **macOS**:
     - Bundle with PyInstaller (.app)
     - Create .dmg disk image
     - Code signing (optional)
   - **Linux**:
     - Bundle with PyInstaller
     - Create AppImage, Snap, Flatpak, or deb/rpm packages
   - Include setup wizard in distribution
   - Test installation process on all platforms

### Phase 9: Import Functionality

1. **HTML/CSS/JS Import**
   - **Phase 1: Import Structure Only**
     - Parse basic elements: `<div>`, `<p>`, `<h1-h6>`, `<img>`, `<a>`, `<button>` → your elements
     - Ignore inline scripts, style quirks, external CSS for now
     - Warn user: "Complex CSS may not import perfectly"
     - Show import preview before applying
   - **Phase 2: Gradual CSS Mapping**
     - Map colors, font sizes, padding/margins
     - Ignore complex selectors/media queries for first stable release
     - Add more CSS support incrementally
   - **Backup**: Always keep backup copy of original HTML/CSS files
     - You'll thank yourself later when debugging import issues
   - HTML parser (BeautifulSoup4)
   - CSS parser (tinycss2/cssutils)
   - Element reconstruction from HTML
   - Import dialog UI
   - Import validation and preview

2. **Import Features**
   - Import from files (HTML, CSS, JS)
   - Handle external resources
   - Preserve structure option
   - Merge styles option
   - Import assets

### Phase 10: Code Editor & Auto-Save

1. **Code Editor**
   - Code editor widget (tkinter.scrolledtext + Pygments)
   - Syntax highlighting
   - HTML/CSS/JS code views
   - **Phase 1: One-Way Sync Only**
     - Visual → Code: Always reliable, always works
     - Add "Reload from code" button for manual user sync
     - Warn user when code is manually edited (may lose sync)
   - **Phase 2: Two-Way Sync (Later)**
     - Debounce edits (e.g., 500ms wait after last change)
     - Validate code before applying
     - Warn user if parsing fails
     - Keep visual elements immutable until code validated
     - This prevents instant corruption while keeping the feature possible
   - Code validation
   - Split view (visual + code)
   - Feature flag: Allow users to disable two-way sync if it causes issues

2. **Auto-Save & Version History**
   - Auto-save system (background thread using threading)
   - Thread-safe communication (queue.Queue)
   - Auto-save settings (interval, triggers)
   - Version snapshots (with compression for old versions)
   - Version browser UI
   - Restore previous versions
   - Version cleanup (limit to last 50, auto-delete old versions)
   - Crash recovery system
   - Backup system integration

### Phase 11: Asset Management

1. **Image Library**
   - Image upload and management
   - Image gallery UI
   - Image optimization (Pillow)
   - Image cropping/resizing
   - Image search and organization
   - Asset usage tracking

2. **Font Manager**
   - System fonts list
   - Google Fonts integration
   - Font preview
   - Custom font upload
   - Font organization

3. **Icon Library**
   - Built-in icon sets (Font Awesome, Material Icons)
   - Icon search
   - Icon customization (color, size)
   - SVG icon support

### Phase 12: User Onboarding & Help

1. **Tutorial System**
   - Interactive walkthrough
   - Step-by-step guide
   - UI element highlighting
   - Tutorial completion tracking

2. **Help System**
   - Help menu
   - Keyboard shortcuts reference
   - Context-sensitive help (F1)
   - User guide/documentation
   - Tooltips system

3. **Welcome Screen**
   - Recent projects
   - Quick start options
   - Tips and tricks
   - First-time user experience

### Phase 13: Deployment Integration

1. **Deployment Services**
   - Netlify deployment (API integration)
   - Vercel deployment (API integration)
   - GitHub Pages (GitPython)
   - FTP/SFTP deployment (paramiko)
   - **Secure credential storage**: Use keyring library for API keys
   - Never store credentials in plain text
   - Credential management UI

2. **Deployment UI**
   - Deployment dialog
   - Service selection
   - Deployment settings
   - Environment variables management
   - Deployment history

3. **Deployment Features**
   - Build settings configuration
   - Custom domain setup
   - Deployment status tracking
   - Rollback functionality

### Phase 14: SEO Tools

1. **Meta Tags Editor**
   - Basic meta tags (title, description, keywords)
   - Open Graph tags
   - Twitter Card tags
   - Canonical URLs
   - Meta tags UI panel

2. **SEO Analysis**
   - SEO score calculation
   - Missing meta tags detection
   - Alt text validation
   - Heading structure validation
   - SEO suggestions

3. **Sitemap & Robots**
   - Sitemap.xml generation
   - robots.txt generation
   - SEO reporting

### Phase 15: Accessibility Tools

1. **ARIA Attributes Editor**
   - ARIA role editor
   - aria-label, aria-describedby
   - ARIA live regions
   - Keyboard navigation support

2. **Accessibility Checker**
   - Color contrast checking (webcolors)
   - Alt text validation
   - Heading hierarchy check
   - Accessibility score
   - WCAG compliance checking

3. **Accessibility UI**
   - Accessibility panel
   - Real-time warnings
   - Fix suggestions
   - Accessibility report

### Phase 16: Form Functionality

1. **Form Builder**
   - Form element types (input, textarea, select, etc.)
   - Form validation rules
   - Required field indicators
   - Form layout options

2. **Form Submission**
   - Generate form code with configurable action URL
   - API endpoint integration (generate code pointing to user's backend)
   - Generate example backend code (Node.js, Python, PHP)
   - Form data handling
   - Success/error messages
   - Form actions configuration
   - **Email submission**: Optional, for testing only (with security warnings)
   - Use secure credential storage for SMTP settings (if used)

### Phase 17: Animation & Interactions

1. **Animation System**
   - Animation timeline editor
   - Keyframe management
   - Animation types (fade, slide, scale, etc.)
   - Duration and easing controls
   - Animation triggers

2. **Interaction Builder**
   - Click actions
   - Hover effects
   - Scroll animations
   - Modal/dialog triggers
   - Interaction editor UI

### Phase 18: Component Library

1. **Component System**
   - Save element groups as components
   - Component data model
   - Component library browser
   - Component search and categories

2. **Component Features**
   - Component properties (editable props)
   - Component variants
   - Component import/export
   - Component usage tracking

### Phase 19: Validation & Testing

1. **Validation Tools**
   - HTML validation (W3C)
   - CSS validation
   - Real-time validation
   - Error highlighting

2. **Link Checking**
   - Check all links
   - Broken link detection
   - External link validation
   - Link status reporting

3. **Browser Compatibility**
   - Browser compatibility checking
   - Feature support notes
   - Compatibility warnings

### Phase 20: Performance Tools

1. **Performance Analysis**
   - Page load time estimation
   - Asset size analysis
   - Number of requests tracking
   - Performance score calculation

2. **Optimization Tools**
   - Unused CSS detection
   - Image optimization suggestions
   - Code optimization suggestions
   - Performance report generation

### Phase 21: Theme & Design System

1. **Color Palette Manager**
   - Color palette creation
   - Primary/secondary colors
   - Color swatches
   - Color picker with palette

2. **Design Tokens**
   - Spacing scale
   - Typography scale
   - Border radius scale
   - Shadow presets
   - Token management UI

3. **Theme Builder**
   - Theme creation UI
   - Theme preview
   - Theme save/load
   - Theme export
   - Apply theme to project

### Phase 22: Template System

1. **Template Library**
   - Template categories (landing pages, portfolios, blogs, etc.)
   - Template browser UI
   - Template preview
   - Template loading

2. **Template Management**
   - Save current project as template
   - Template organization
   - Template search
   - Template marketplace (future)

## Technical Decisions

### Why CustomTkinter?

- Modern, customizable appearance
- Better than standard tkinter
- **Cross-platform**: Windows 11/10, macOS, Linux
- Active development
- Good documentation
- Consistent look across platforms

### Why JSON for Project Files?

- Human-readable
- Easy to parse
- Version control friendly
- Can be edited manually if needed
- Standard format

### Setup Wizard Approach (Cross-Platform, Following OS Conventions)

- **CustomTkinter UI**: Matches main application style, consistent user experience across platforms
- **Standalone Executable**: Setup wizard runs independently before main app installation
- **Cross-Platform Support** (Following OS Best Practices):
  - **Windows**:
    - Uses `SHGetFolderPath` or environment variables for proper paths
    - Uses pywin32 for registry, shortcuts, file associations
    - Follows Windows installer conventions
    - Registers in Add/Remove Programs
    - Uses proper CSIDL constants for special folders
  - **macOS**:
    - Uses Launch Services, plist files for file associations
    - Follows macOS application bundle structure
    - Uses proper Library directories
    - Registers bundle identifier
    - Follows macOS sandboxing guidelines (if applicable)
  - **Linux**:
    - Follows XDG Base Directory Specification
    - Uses xdg-utils for desktop integration
    - Creates proper desktop files
    - Registers MIME types correctly
    - Follows Filesystem Hierarchy Standard (FHS)
- **Platform Detection**: Automatically detects OS and uses appropriate installer
- **Proper Directory Management**:
  - Installation directory (executables, libraries)
  - Application data directory (user settings, projects)
  - Cache directory (temporary files, preview cache)
  - Logs directory (application logs)
  - Configuration directory (preferences, settings)
  - All directories created following OS conventions
- **Multi-Page Flow**: Step-by-step installation process (welcome → license → path → components → install → complete)
- **Installation Metadata**: Stores installation info in proper location
  - Windows: Registry
  - macOS: plist file
  - Linux: Config file
- **Error Recovery**: Rollback capability if installation fails
- **Admin Rights**: Detects and requests administrator/root privileges when needed
  - Windows: UAC elevation (for Program Files installation)
  - macOS: Admin password prompt (for Applications folder)
  - Linux: sudo/root privileges (for system-wide installation)
- **Uninstaller Registration**: Properly registers uninstaller in OS-specific location

### Multi-Framework Export Approach

- **Template-Based Generation**: Use Jinja2 templates for each framework to generate code
- **Base Exporter Pattern**: Abstract base class defines interface, each framework implements its own exporter
- **Element-to-Component Mapping**: Convert visual elements to framework-specific components
  - Containers → Components/Divs
  - Text → Typography components or text nodes
  - Images → Image components with proper imports
  - Buttons → Button components with event handlers
- **Framework Structure**: Generate proper folder structure for each framework
  - React: components/, pages/, styles/, assets/
  - Vue: components/, views/, assets/, styles/
  - Next.js: app/ or pages/, components/, public/
  - Angular: src/app/components/, src/app/services/, src/assets/
- **Configuration Files**: Generate framework-specific config files
  - package.json with correct dependencies and scripts
  - Framework config files (vite.config.js, next.config.js, angular.json, etc.)
  - TypeScript config (tsconfig.json) if TypeScript is selected
- **Code Quality**:
  - Format generated code with jsbeautifier/cssbeautifier
  - Follow framework best practices and conventions
  - Generate semantic, maintainable code
- **Asset Handling**: Copy assets to framework-appropriate locations
  - React/Vue: public/ or assets/ folder
  - Next.js: public/ folder
  - Angular: src/assets/ folder
- **Dependencies**: Include all necessary dependencies in package.json
  - Framework core libraries
  - Styling libraries (if used)
  - Utility libraries
- **Documentation**: Generate README.md with setup and run instructions for each framework

### Project File Format (Versioned)

```json
{
  "version": "1.0",              // Project file format version
  "app_version": "1.2.3",        // App version that created this file
  "name": "Project Name",
  "created": "2024-01-01T00:00:00",
  "modified": "2024-01-01T00:00:00",
  "elements": [...],
  "styles": {...},
  "settings": {...}
}
```

### Element Tree Structure

```python
{
  "type": "container",
  "id": "main-container",
  "classes": ["wrapper"],
  "styles": {...},
  "children": [
    {
      "type": "heading",
      "content": "Hello World",
      "styles": {...}
    }
  ]
}
```

### Style Property Format

```python
{
  "width": "100%",
  "height": "auto",
  "margin": {"top": "10px", "right": "10px", "bottom": "10px", "left": "10px"},
  "padding": "20px",
  "color": "#333333",
  "font-size": "16px",
  "background-color": "#ffffff"
}
```

## Platform Support Policy

### Windows Support

- **Target**: Windows 10+ (fully supported)
- **Windows 7/8**: "Best effort" fallback only
- **Warning**: Show warning to users on older OS:
  ```
  "You are running an unsupported version of Windows. 
   Some features may not work. Please upgrade to Windows 10 or later."
  ```
- **Feature Flags**: Disable features that don't work on older OSes
  - Webview may fallback to external browser
  - Some registry operations may fail gracefully
- **Documentation**: Clearly state Windows 10+ requirement
- **Only implement full Windows 7/8 support if you're feeling masochistic**

### Feature Flags Strategy

**Deadpool Tip**: For all complex features, use feature flags. Turn off fancy things (two-way sync, complex import, custom drag-drop) if platform/user can't handle it. Keeps your app alive while you tweak the hard stuff.

**Feature Flags**:
- `two_way_code_sync`: Phase 1: False, Phase 2: True
- `complex_css_import`: Phase 1: False, Phase 2: True
- `custom_drag_drop`: Always True (default)
- `tkinterdnd2_fallback`: False (optional, user must enable)
- `webview_embedded`: True (if available)
- `virtual_scrolling`: True (for performance)

## Cross-Platform Considerations

### Proper Directory Structure (Following OS Conventions)

#### Windows Directory Structure

**Installation Directory** (User Choice):

- **System-wide (Admin)**: `C:\Program Files\CO-web-builder\`
- **User-only**: `C:\Users\<Username>\AppData\Local\Programs\CO-web-builder\`

**Application Data** (Automatic, User-specific):

- **AppData (Roaming)**: `%APPDATA%\CO-web-builder\` (`C:\Users\<Username>\AppData\Roaming\CO-web-builder\`)
  - User settings
  - User preferences
  - User templates
  - User components
- **LocalAppData**: `%LOCALAPPDATA%\CO-web-builder\` (`C:\Users\<Username>\AppData\Local\CO-web-builder\`)
  - Cache files
  - Temporary files
  - Logs
  - Version history
  - Projects (default location)

**Registry Entries**:

- **Uninstaller**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\CO-web-builder` (system) or `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\CO-web-builder` (user)
- **File Associations**: `HKEY_CLASSES_ROOT\.coweb`
- **Application Paths**: `HKEY_CURRENT_USER\SOFTWARE\CO-web-builder\` or `HKEY_LOCAL_MACHINE\SOFTWARE\CO-web-builder\`

#### macOS Directory Structure

**Installation Directory**:

- **System-wide**: `/Applications/CO-web-builder.app`
- **User-only**: `~/Applications/CO-web-builder.app` (optional)

**Application Support** (Automatic):

- **Application Support**: `~/Library/Application Support/CO-web-builder/`
  - User settings
  - User preferences
  - User templates
  - User components
  - Projects (default location)
  - Version history
- **Caches**: `~/Library/Caches/CO-web-builder/`
  - Cache files
  - Temporary files
- **Preferences**: `~/Library/Preferences/com.coweb.builder.plist`
  - Application preferences
- **Logs**: `~/Library/Logs/CO-web-builder/`
  - Application logs
  - Error logs

**Info.plist** (in .app bundle):

- Bundle identifier: `com.coweb.builder`
- File type declarations (UTI)
- Launch Services registration

#### Linux Directory Structure

**Installation Directory** (User Choice):

- **System-wide (Root)**: `/opt/CO-web-builder/` or `/usr/local/CO-web-builder/`
- **User-only**: `~/.local/share/CO-web-builder/` or `~/.local/opt/CO-web-builder/`

**Application Data** (Following XDG Base Directory Specification):

- **Data Home**: `$XDG_DATA_HOME/CO-web-builder/` (default: `~/.local/share/CO-web-builder/`)
  - User settings
  - User templates
  - User components
  - Projects (default location)
  - Version history
- **Config Home**: `$XDG_CONFIG_HOME/CO-web-builder/` (default: `~/.config/CO-web-builder/`)
  - Configuration files
  - User preferences
- **Cache Home**: `$XDG_CACHE_HOME/CO-web-builder/` (default: `~/.cache/CO-web-builder/`)
  - Cache files
  - Temporary files
- **State Home**: `$XDG_STATE_HOME/CO-web-builder/` (default: `~/.local/state/CO-web-builder/`)
  - Application state
  - Logs

**Desktop Integration**:

- **Desktop Entry**: `~/.local/share/applications/CO-web-builder.desktop`
- **MIME Types**: `~/.config/mimeapps.list` or system-wide `/usr/share/mime/`
- **Icons**: `~/.local/share/icons/` or `/usr/share/pixmaps/`

### Directory Structure Details

```
Installation Directory (Program Files/Applications/opt):
├── CO-web-builder.exe/.app/binary
├── lib/                    # Libraries
├── resources/              # Resources (icons, assets)
└── uninstall.exe/.app/script

Application Data Directory (AppData/Library/.local/share):
├── settings/
│   ├── preferences.json
│   └── user_settings.json
├── projects/              # User projects
├── templates/             # User templates
├── components/            # User components
├── themes/                # User themes
└── versions/              # Version history

Cache Directory (LocalAppData/Caches/.cache):
├── temp/                  # Temporary files
├── preview/               # Preview cache
├── images/                # Image cache
└── fonts/                 # Font cache

Logs Directory (LocalAppData/Logs/.local/state):
├── app.log
├── error.log
└── install.log
```

### Application Runtime Directory Management

The application must use proper directories at runtime:

1. **On First Launch**:
   - Detect if directories exist
   - Create directories if missing
   - Migrate data from old locations (if upgrading)

2. **Directory Usage**:
   - **Settings**: Store in config directory
   - **Projects**: Store in data directory
   - **Cache**: Store in cache directory
   - **Logs**: Write to logs directory
   - **Temporary Files**: Use cache/temp directory

3. **Path Resolution**:
   - Use `platform_utils.py` functions to get proper paths
   - Never hardcode paths
   - Handle environment variables correctly
   - Respect XDG variables on Linux

4. **Permissions**:
   - Ensure user has write permissions to data directories
   - Handle permission errors gracefully
   - Request permissions if needed

5. **Installation Metadata**:
   - Store installation path in proper location:
     - Windows: Registry (`HKEY_CURRENT_USER\SOFTWARE\CO-web-builder\InstallPath`)
     - macOS: plist file (`~/Library/Preferences/com.coweb.builder.plist`)
     - Linux: Config file (`~/.config/CO-web-builder/install.conf`)
   - Application reads metadata on startup to know:
     - Where it's installed
     - Where to store data
     - Installation version
     - Installation date

### File Associations

- **Windows**: Registry entries (HKEY_CLASSES_ROOT)
- **macOS**: Launch Services (UTI, Info.plist)
- **Linux**: MIME types, desktop files, xdg-mime

### Shortcuts/Desktop Entries

- **Windows**: `.lnk` files, Start Menu shortcuts
- **macOS**: Applications folder, Dock (optional), aliases
- **Linux**: `.desktop` files, Applications menu

### Permissions

- **Windows**: UAC elevation for system-wide installation
- **macOS**: Admin password for Applications folder
- **Linux**: sudo/root for system-wide installation

### Path Handling

- Use `pathlib.Path` for cross-platform path handling
- Normalize paths: `Path(path).resolve()`
- Handle path separators automatically
- Be aware of case sensitivity (Windows: case-insensitive, Linux/macOS: case-sensitive)

### Platform Detection

```python
import platform
import sys

def get_platform():
    system = platform.system()
    if system == "Windows":
        return "windows"
    elif system == "Darwin":
        return "macos"
    elif system == "Linux":
        return "linux"
    return "unknown"
```

### Conditional Imports

```python
import sys

if sys.platform == "win32":
    import winreg
    from win32api import ...
elif sys.platform == "darwin":
    import plistlib
    # macOS-specific imports
elif sys.platform.startswith("linux"):
    # Linux-specific imports
```

## Potential Challenges

### 1. Drag & Drop in Tkinter 😬

- **Challenge**: tkinterdnd2 works but is quirky and can be finicky
- **Early Warning Signs**:
  - Drag events not firing consistently
  - Drop zones not detecting properly
  - Conflicts with CustomTkinter styling
- **Solution Strategy**:
  - Try tkinterdnd2 first (it's the easiest path)
  - If you hit walls early, **switch to custom mouse events** before investing too much time
  - Custom implementation: Track mouse down → mouse move → mouse up events
  - Use visual feedback (ghost image, highlight drop zones)
- **Alternative**: Use PyQt6 which has native, robust drag & drop (but heavier dependency)
- **Implementation Tip**: Start with simple drag-to-reposition, then add drag-from-sidebar

### 2. Live Preview Performance ⚡

- **Challenge**: pywebview + lots of DOM updates can cause lag and stuttering
- **Performance Issues**:
  - Every property change triggers full HTML/CSS regeneration
  - Preview reloads on every keystroke
  - Large projects with many elements become slow
- **Solution Strategy**:
  - **Batch updates**: Collect changes and update preview every 300-500ms (debounce)
  - **Throttle updates**: Limit preview refreshes to max 2-3 per second
  - **Incremental updates**: Only regenerate changed elements, not entire DOM
  - **Lazy loading**: Don't render hidden/off-screen elements in preview
  - **Manual refresh option**: Let users toggle auto-refresh vs manual refresh
- **Implementation**:

  ```python
  # Use threading.Timer or queue for debouncing
  # Only regenerate HTML/CSS when user stops typing for X ms
  ```

- **Alternative**: Use PyQt6.QtWebEngineWidgets (better performance, but larger)

### 3. Flex/Grid Visuals 🕹

- **Challenge**: Representing CSS flexbox/grid visually in the canvas is tricky
- **Complexity**:
  - Flex direction, wrap, justify-content, align-items all affect layout
  - Grid columns/rows, gaps, areas are hard to visualize
  - Visual representation may not match actual rendered output
- **Solution Strategy**:
  - **Start simple**: Just show boxes with basic alignment handles
  - **Visual indicators**:
    - Show flex direction with arrows
    - Show grid lines as dashed borders
    - Highlight flex/grid containers differently
  - **Properties panel focus**: Don't try to show everything visually; rely on properties panel for detailed control
  - **Expand gradually**: Add more visual feedback as you learn what works
- **Phase 1**: Basic container boxes
- **Phase 2**: Simple alignment indicators
- **Phase 3**: Advanced visual tools (if needed)

### 4. Performance with Large Projects 🐌

- **Challenge**: Large projects with many elements can become slow
- **Performance Bottlenecks**:
  - Rendering many elements on canvas
  - Generating large HTML/CSS files
  - Preview rendering complex layouts
  - Undo/redo history storage
- **Solution Strategy**:
  - **Virtual scrolling**: Only render visible elements in canvas
  - **Lazy rendering**: Render elements on-demand as they come into view
  - **Optimization**: Profile early, identify bottlenecks
  - **Limit undo history**: Cap undo stack at 50-100 actions
  - **Efficient data structures**: Use efficient tree structures for element hierarchy
- **Future**: Performance profiling tools, optimization passes

### 5. CSS Complexity 💀

- **Challenge**: Full CSS support is massive and overwhelming
- **Reality Check**:
  - CSS has 500+ properties
  - Many properties have complex syntax
  - Browser compatibility varies
  - Validation is non-trivial
- **Solution Strategy**:
  - **Start with the most common properties** (80/20 rule):
    - Layout: width, height, margin, padding, display, position
    - Typography: font-family, font-size, color, text-align, line-height
    - Colors: background-color, color, border-color
    - Borders: border-width, border-style, border-radius
    - Effects: box-shadow, opacity
  - **Add advanced stuff later**:
    - Flexbox properties (Phase 2)
    - Grid properties (Phase 3)
    - Animations (Phase 4)
    - Advanced selectors (Phase 5)
  - **Custom CSS escape hatch**: Always allow raw CSS for power users
  - **Validation**: Start simple, add validation as you add properties
- **Priority Order**:
  1. Essential layout (width, height, margin, padding)
  2. Typography basics
  3. Colors and backgrounds
  4. Borders and shadows
  5. Flexbox
  6. Grid
  7. Advanced (animations, transforms, etc.)

### 6. Framework Export Complexity 🚀

- **Challenge**: Converting visual elements to framework-specific code is complex
- **Complexity Factors**:
  - Each framework has different syntax and conventions
  - Component structure varies (React JSX, Vue SFC, Angular TypeScript)
  - State management approaches differ
  - Styling approaches differ (CSS modules, styled-components, scoped CSS)
  - Build tools and configurations vary
- **Solution Strategy**:
  - **Start with one framework** (React or Vue) and perfect it
  - **Template-based approach**: Use Jinja2 templates for code generation
  - **Base exporter pattern**: Common interface, framework-specific implementations
  - **Incremental support**: Add frameworks one at a time
  - **Focus on common patterns**: Start with static components, add interactivity later
  - **Test exports**: Manually test each framework export to ensure it works
- **Implementation Priority**:
  1. Vanilla HTML/CSS/JS (simplest, foundation)
  2. React (most popular, good starting point)
  3. Vue.js (similar to React, different syntax)
  4. Next.js/Nuxt.js (extend React/Vue with SSR)
  5. Svelte/Angular (more complex, add later)
- **Code Quality**:
  - Generate clean, readable code
  - Follow framework best practices
  - Include proper imports and dependencies
  - Add comments where helpful
- **Testing Strategy**:
  - Export test projects for each framework
  - Verify generated code runs correctly
  - Test with different project complexities
  - Get feedback from framework users

## Future Enhancements

### Short Term

- More element types (forms, navigation, etc.)
- Template system
- Asset management
- Better preview system
- Additional framework exports (Svelte, Angular, etc.)
- Framework export improvements (better code generation, more options)

### Medium Term

- Code editor view (see generated HTML/CSS)
- Component library (save reusable components)
- Responsive design tools
- Animation support

### Long Term

- Collaboration features
- Version control integration
- Plugin system
- Cloud sync
- AI-assisted design

## Development Workflow

### Git Workflow

- Main branch: stable releases
- Develop branch: active development
- Feature branches: new features
- Hotfix branches: bug fixes

### Testing Strategy

- Unit tests for core logic (elements, generators)
- Integration tests for UI components
- Manual testing for visual editor
- User acceptance testing

### Cross-Platform Testing

- **Platform-Specific Testing**:
  - Test on Windows 11
  - Test on Windows 10
  - Test on macOS (latest and older versions)
  - Test on Linux (Ubuntu, Debian, Fedora, Arch)
- **Platform-Specific Features**:
  - Setup wizard on each platform
  - File associations on each platform
  - Shortcuts/desktop entries on each platform
  - Path handling (Windows vs Unix-style)
  - Permissions and admin/root access
- **Continuous Integration**:
  - GitHub Actions for Windows, macOS, Linux
  - Automated testing on multiple platforms
  - Build verification on all platforms

### Code Standards

- Follow PEP 8
- Type hints where possible
- Docstrings for all functions/classes
- Comments for complex logic

## Resources & References

### Documentation

- CustomTkinter: <https://customtkinter.tomschimansky.com/>
- Python tkinter: <https://docs.python.org/3/library/tkinter.html>
- pywebview: <https://pywebview.flowrl.com/>
- CSS Reference: <https://developer.mozilla.org/en-US/docs/Web/CSS>

### Inspiration

- Webflow (visual web builder)
- Figma (design tool)
- WordPress Gutenberg (block editor)
- Wix Editor (drag & drop)

## Critical Issues & Solutions

See `issues_and_solutions.md` for comprehensive list of identified issues and workarounds.

### Key Issues Addressed

1. **Directory Structure**: Renamed `assets/` to `app_assets/`, removed `user_data/` from source
2. **Drag & Drop**: Custom implementation instead of tkinterdnd2 (more reliable)
3. **Error Handling**: Added centralized error handling and logging
4. **Configuration**: Added configuration management system
5. **Security**: Added secure credential storage (keyring)
6. **Project Versioning**: Added project file versioning and migration system
7. **Threading**: Added threading strategy for background operations
8. **Webview Fallback**: Added fallback for webview unavailability
9. **Code Editor Sync**: Phased approach (one-way first, two-way later)
10. **Form Submission**: Generate code with action URLs, not direct email

## Notes

- Start simple, iterate
- Focus on core functionality first
- User experience is priority
- Keep code modular and extensible
- Document as you go
- **Always check `issues_and_solutions.md` before implementing new features**
