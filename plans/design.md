# Design & UI/UX

## Design Philosophy

- **Intuitive** - No coding knowledge required
- **Visual** - WYSIWYG (What You See Is What You Get)
- **Fast** - Responsive and lightweight
- **Modern** - Clean, contemporary interface

## Layout Structure

### Splash Screen Layout

```
┌─────────────────────────────────────────────────────────┐
│                                                          │
│                                                          │
│                    [Logo/Icon]                          │
│                                                          │
│                  CO-web-builder                         │
│                                                          │
│              Create websites visually                    │
│                                                          │
│                                                          │
│              ┌─────────────────────┐                    │
│              │ ████████░░░░░░░░░░░ │                    │
│              └─────────────────────┘                    │
│                                                          │
│              Loading modules...                          │
│                                                          │
│                                                          │
│                    Version 1.0.0                        │
│                                                          │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### Main Window Layout

```
┌─────────────────────────────────────────────────────────┐
│  Menu Bar / Toolbar                                     │
├──────┬──────────────────────────────────────┬───────────┤
│      │                                      │           │
│      │                                      │ Properties│
│ Side │         Canvas / Editor              │ Panel     │
│ Bar  │         (Drag & Drop Area)           │           │
│      │                                      │           │
│      │                                      │           │
├──────┴──────────────────────────────────────┴───────────┤
│  Status Bar                                             │
└─────────────────────────────────────────────────────────┘
```

## UI Components

### 0. Splash Screen

**Purpose**: Display during application startup/loading
**Responsibilities**:

- Show application branding (logo, name)
- Display loading progress
- Show version information
- Provide visual feedback during initialization
- Smooth transition to main window

**Components**:

- **Logo/Icon**: Application logo or icon (centered)
- **Application Name**: "CO-web-builder" (large, prominent)
- **Tagline**: "Create websites visually" or similar
- **Progress Bar**: Visual progress indicator
- **Status Text**: Current loading step (e.g., "Loading modules...", "Initializing UI...")
- **Version Number**: Application version (bottom, subtle)
- **Loading Animation**: Optional subtle animation (fade, pulse, etc.)

**Design Specifications**:

- **Size**: 600x400 pixels (or proportional)
- **Position**: Centered on screen
- **Background**:
  - Light theme: White or light gray with subtle gradient
  - Dark theme: Dark gray/black with subtle gradient
- **Logo**: Centered, 128x128 or 256x256 pixels
- **Typography**:
  - Application name: Large, bold (24-32px)
  - Tagline: Medium, regular (14-16px)
  - Status text: Small, regular (12px)
  - Version: Small, muted (10px)
- **Progress Bar**:
  - Width: 80% of window width
  - Height: 4-6 pixels
  - Color: Primary brand color
  - Smooth animation
- **Animation**:
  - Fade in on show
  - Fade out before closing
  - Optional: Subtle pulse on logo
  - Progress bar smooth fill animation

**Loading Steps** (Real-time, reflects actual background operations):

1. "Starting application..." (0-5%)
   - Parse command-line arguments
   - Check for `--no-splash` flag
   - Initialize logging system

2. "Loading configuration..." (5-15%)
   - Load user settings from config directory
   - Initialize configuration manager
   - Apply user preferences

3. "Initializing platform utilities..." (15-25%)
   - Detect operating system
   - Set up platform-specific paths
   - Create necessary directories (if missing)

4. "Loading modules..." (25-50%)
   - Import core modules (project, element, generators)
   - Import UI modules (main_window, toolbar, sidebar, etc.)
   - Import utility modules (file_manager, validators, etc.)
   - Initialize module dependencies

5. "Initializing UI framework..." (50-70%)
   - Initialize CustomTkinter
   - Set theme (light/dark based on user preference)
   - Create main window structure
   - Initialize UI components

6. "Loading asset manager..." (70-80%)
   - Initialize image library
   - Load font manager
   - Initialize icon library

7. "Checking for updates..." (80-85%)
   - Check GitHub Releases API (if enabled)
   - Compare versions
   - Prepare update notification (if available)

8. "Finalizing..." (85-95%)
   - Connect UI components
   - Initialize event handlers
   - Load recent projects list
   - Prepare welcome screen

9. "Ready!" (95-100%)
   - All initialization complete
   - Main window ready to display

**Behavior**:

- Show immediately on application start
- **Real-time updates**: Progress and status reflect actual background operations
- **Accurate progress**: Progress bar reflects actual completion percentage of real tasks
- **Dynamic status**: Status messages show what's actually happening (e.g., "Loading configuration from ~/.config/CO-web-builder/...")
- Hide automatically when main window is ready
- Minimum display time: 1-2 seconds (even if loading is fast)
- Maximum display time: 10 seconds (timeout if something goes wrong)
- Can be skipped with command-line flag: `--no-splash` (for development)
- **Error handling**: If initialization fails, show error message on splash screen before closing

## UI Components

### 1. Top Toolbar

- **File Operations**: New, Open, Save, Save As, Export
- **Edit Operations**: Undo, Redo, Cut, Copy, Paste, Delete
- **View Options**: Toggle Preview, Zoom In/Out, Grid Toggle
- **Preview Button**: Live preview toggle
- **Export Button**: Export to HTML/CSS/JS

### 2. Left Sidebar (Component Library)

- **Categories**:
  - Layout (Container, Row, Column, Section)
  - Text (Heading, Paragraph, List, Quote)
  - Media (Image, Video, Audio)
  - Forms (Input, Button, Textarea, Select)
  - Navigation (Link, Menu, Breadcrumb)
  - Advanced (Custom HTML, Embed)
- **Search Bar**: Filter components
- **Drag & Drop**: Drag components onto canvas

### 3. Central Canvas

- **Visual Editor**: WYSIWYG editing area
- **Grid/Guides**: Optional alignment guides
- **Selection**: Click to select elements
- **Multi-select**: Ctrl+Click for multiple selection
- **Resize Handles**: Visual resize controls
- **Context Menu**: Right-click for element options

### 4. Right Properties Panel

- **Element Properties**:
  - Content (text, image source, etc.)
  - Layout (width, height, margin, padding)
  - Style (colors, fonts, borders, shadows)
  - Advanced (ID, classes, custom CSS)
- **Tabs**: Content | Layout | Style | Advanced
- **Live Preview**: Changes reflect immediately

### 5. Preview Panel (Optional Split View)

- **Live Preview**: Real-time HTML preview
- **Responsive Views**: Desktop, Tablet, Mobile
- **Refresh Button**: Manual refresh if needed

### 6. Status Bar

- **Element Info**: Selected element details
- **Cursor Position**: X, Y coordinates
- **Zoom Level**: Current zoom percentage
- **Project Status**: Saved/Unsaved indicator

## Color Scheme

- **Primary**: Modern blue (#2196F3) or customizable
- **Background**: Light gray (#F5F5F5) or dark mode support
- **Canvas**: White (#FFFFFF) with optional grid
- **Accent**: Orange/Teal for highlights
- **Text**: Dark gray (#333333) on light, light on dark

## Typography

- **UI Font**: Segoe UI (Windows native) or Inter
- **Code Font**: Consolas or Fira Code (for code view)
- **Sizes**: 12px (UI), 14px (content), 16px+ (headings)

## Interaction Patterns

### Drag & Drop

- **From Sidebar**: Drag component to canvas
- **On Canvas**: Drag to reposition elements
- **Visual Feedback**: Highlight drop zones, ghost image

### Selection

- **Single Click**: Select element
- **Double Click**: Edit inline (for text)
- **Ctrl+Click**: Multi-select
- **Click+Drag**: Select multiple (marquee selection)

### Editing

- **Inline Editing**: Double-click text to edit
- **Properties Panel**: Edit all properties
- **Keyboard Shortcuts**: Standard (Ctrl+C, Ctrl+V, etc.)

## Responsive Design Tools

- **Viewport Switcher**: Desktop (1920px), Tablet (768px), Mobile (375px)
- **Breakpoint Editor**: Custom breakpoints
- **Responsive Properties**: Different values per breakpoint

## Accessibility

- **Keyboard Navigation**: Full keyboard support
- **Screen Reader**: Proper ARIA labels
- **High Contrast**: Optional high contrast mode
- **Tooltips**: Helpful tooltips on hover

## Themes

- **Light Theme**: Default
- **Dark Theme**: Dark mode support
- **Custom Themes**: User-defined color schemes

## Setup Wizard Design

### Wizard Layout

```
┌─────────────────────────────────────────────────────────┐
│  CO-web-builder Setup                                    │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  [Wizard Content Area]                                  │
│                                                          │
│  Welcome to CO-web-builder Setup                        │
│  This wizard will guide you through the installation... │
│                                                          │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  [< Back]  [Next >]  [Cancel]                           │
└─────────────────────────────────────────────────────────┘
```

### Wizard Pages

#### 1. Welcome Page

- **Logo/Icon**: Application logo at top
- **Title**: "Welcome to CO-web-builder Setup"
- **Description**: Brief introduction to the application
- **Version Info**: Display version number
- **Next Button**: Enabled, Back disabled

#### 2. License Agreement Page

- **Title**: "License Agreement"
- **Text Area**: Scrollable license text (read-only)
- **Checkbox**: "I accept the terms of the license agreement"
- **Next Button**: Disabled until checkbox is checked

#### 3. Installation Path Page

- **Title**: "Choose Installation Location"
- **Path Input**: Text field with current/default path
- **Browse Button**: Open folder selection dialog
- **Disk Space**: Show available/required disk space
- **Installation Type**: Radio buttons for "System-wide" (admin) or "User-only" (no admin)
- **Default Paths** (Platform-specific):
  - **Windows**:
    - System: `C:\Program Files\CO-web-builder\` (requires admin)
    - User: `%LOCALAPPDATA%\Programs\CO-web-builder\`
  - **macOS**: `/Applications/CO-web-builder.app`
  - **Linux**:
    - System: `/opt/CO-web-builder/` (requires root)
    - User: `~/.local/share/CO-web-builder/`
- **Info Text**: "Application data will be stored in the appropriate user directory"
  - Windows: `%APPDATA%\CO-web-builder\`
  - macOS: `~/Library/Application Support/CO-web-builder/`
  - Linux: `~/.local/share/CO-web-builder/`

#### 4. Component Selection Page

- **Title**: "Select Components"
- **Checkboxes**:
  - ☑ Desktop Shortcut (platform-specific location)
  - ☑ Application Menu Entry (Start Menu/Applications/Dock)
  - ☑ File Association (.coweb files)
  - ☐ Example Templates
  - ☐ Sample Projects
- **Description**: Brief description of each component
- **Platform-Specific Info**:
  - **Windows**: "Shortcuts will be created in Desktop and Start Menu"
  - **macOS**: "Application will be added to Applications folder and Dock"
  - **Linux**: "Desktop entry will be created in Applications menu"
- **Disk Space**: Update based on selected components

#### 5. Installation Progress Page

- **Title**: "Installing CO-web-builder"
- **Progress Bar**: Animated progress indicator
- **Status Text**: Current operation with details:
  - "Creating directory structure..."
  - "Copying application files..."
  - "Creating application data directories..."
  - "Registering file associations..."
  - "Creating shortcuts..."
  - "Registering uninstaller..."
- **File List**: Optional list of files being installed
- **Directory Info**: Show where files are being installed
  - Installation directory
  - Application data directory
  - Cache directory
- **Cancel Button**: Disabled during installation

#### 6. Completion Page

- **Title**: "Installation Complete"
- **Success Icon**: Checkmark or success graphic
- **Message**: "CO-web-builder has been successfully installed"
- **Installation Summary**:
  - Installation directory path
  - Application data directory path
  - Shortcuts created
  - File associations registered
- **Checkbox**: "Launch CO-web-builder now"
- **Finish Button**: Close wizard (and optionally launch app)
- **Info**: "You can uninstall CO-web-builder from [Add/Remove Programs/Applications/System Settings]"

### Wizard Navigation

- **Back Button**: Navigate to previous page (disabled on first page)
- **Next Button**: Navigate to next page (disabled when required fields not filled)
- **Cancel Button**: Exit wizard (with confirmation if installation started)
- **Finish Button**: Only on completion page

### Visual Design

- **Consistent Styling**: Match main application theme (CustomTkinter)
- **Progress Indicators**: Clear visual feedback during installation
- **Icons**: Use icons for different page types
- **Colors**: Success green for completion, warning yellow for errors
- **Typography**: Clear, readable fonts matching main app

### Error Handling UI

- **Error Dialog**: Modal dialog for critical errors
- **Warning Messages**: Non-blocking warnings
- **Retry Option**: Allow retry on failed operations
- **Rollback Message**: Inform user if rollback occurs

## Export Dialog Design

### Export Dialog Layout

```
┌─────────────────────────────────────────────────────────┐
│  Export Project                                          │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Select Framework:                                       │
│  ┌──────────────────────────────────────────────────┐  │
│  │  ○ Vanilla HTML/CSS/JS                           │  │
│  │  ○ React                                         │  │
│  │  ○ Vue.js                                        │  │
│  │  ○ Next.js                                       │  │
│  │  ○ Nuxt.js                                       │  │
│  │  ○ Svelte                                        │  │
│  │  ○ Angular                                       │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Framework Description:                                  │
│  [Description of selected framework and what will be    │
│   generated...]                                          │
│                                                          │
│  Output Options:                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Output Format:                                   │  │
│  │  ○ Folder  ○ ZIP Archive                         │  │
│  │                                                    │  │
│  │  Code Formatting:                                 │  │
│  │  ☑ Format/Beautify code                          │  │
│  │  ☐ Minify CSS/JS                                 │  │
│  │                                                    │  │
│  │  Additional Options:                              │  │
│  │  ☑ Include package.json                          │  │
│  │  ☑ Include README.md                             │  │
│  │  ☑ Copy assets                                   │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Output Location:                                        │
│  ┌──────────────────────────────────────────────────┐  │
│  │  C:\Users\...\Documents\my-project                │  │
│  └──────────────────────────────────────────────────┘  │
│  [Browse...]                                            │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  [Cancel]  [Export]                                      │
└─────────────────────────────────────────────────────────┘
```

### Export Dialog Components

#### Framework Selection

- **Radio Buttons**: Select one framework
- **Framework Icons**: Visual icons for each framework (optional)
- **Description Panel**: Dynamic description of selected framework
  - What will be generated
  - Framework structure
  - Dependencies included
  - Setup instructions preview

#### Output Options

- **Output Format**:
  - Folder (uncompressed, ready to use)
  - ZIP Archive (compressed for distribution)
- **Code Formatting**:
  - Format/Beautify (readable, indented code)
  - Minify (compressed for production)
- **Additional Options**:
  - Include package.json (for Node.js frameworks)
  - Include README.md (setup instructions)
  - Copy assets (images, fonts, etc.)
  - Generate TypeScript (if framework supports it)

#### Output Location

- **Path Input**: Text field with output directory path
- **Browse Button**: Open folder selection dialog
- **Validation**: Check if path is writable, show error if not

#### Export Progress

- **Progress Bar**: Show export progress
- **Status Text**: Current operation (e.g., "Generating React components...", "Creating folder structure...")
- **File List**: Optional list of files being created
- **Cancel Button**: Allow cancellation during export

#### Export Complete

- **Success Message**: "Export completed successfully!"
- **Open Folder Button**: Open exported folder in file explorer
- **Open in IDE Button**: Open in VS Code/other IDE (if detected)
- **Close Button**: Close dialog

### Framework-Specific Options

#### React Export Options

- Component structure (functional/class)
- CSS approach (CSS modules, styled-components, plain CSS)
- TypeScript support
- Hooks usage

#### Vue.js Export Options

- API style (Composition API / Options API)
- TypeScript support
- CSS scoping (scoped, module, global)

#### Next.js Export Options

- Export mode (static/SSR)
- App Router vs Pages Router
- Image optimization

#### Angular Export Options

- Standalone components vs NgModules
- TypeScript version
- Angular CLI version

### Visual Design

- **Modal Dialog**: Centered, non-resizable (or resizable)
- **Framework Icons**: Visual representation of each framework
- **Color Coding**: Different colors for different frameworks
- **Progress Animation**: Smooth progress bar animation
- **Success Animation**: Checkmark or success icon on completion

## Import Dialog Design

### Import Dialog Layout

```
┌─────────────────────────────────────────────────────────┐
│  Import Project                                         │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Select Files:                                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │  HTML File: [Browse...] [index.html]            │  │
│  │  CSS Files: [Browse...] [style.css, theme.css]  │  │
│  │  JS Files:  [Browse...] [script.js]             │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Import Options:                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │  ☑ Preserve structure                            │  │
│  │  ☑ Merge styles                                  │  │
│  │  ☑ Import assets                                 │  │
│  │  ☐ Handle external resources                     │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Preview:                                                │
│  ┌──────────────────────────────────────────────────┐  │
│  │  [Preview of imported structure...]              │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  [Cancel]  [Import]                                      │
└─────────────────────────────────────────────────────────┘
```

## Code Editor Design

### Code Editor Layout

```
┌─────────────────────────────────────────────────────────┐
│  Code Editor                              [HTML] [CSS] [JS]│
├─────────────────────────────────────────────────────────┤
│  1  <!DOCTYPE html>                                      │
│  2  <html>                                               │
│  3    <head>                                             │
│  4      <title>My Page</title>                           │
│  5    </head>                                            │
│  6    <body>                                             │
│  7      <div class="container">                          │
│  8        <h1>Hello World</h1>                           │
│  9      </div>                                           │
│  10   </body>                                            │
│  11 </html>                                              │
│                                                          │
│  [Syntax highlighting, line numbers, error markers]      │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  [Sync with Visual] [Validate] [Format] [Find & Replace]│
└─────────────────────────────────────────────────────────┘
```

### Split View

- **Side-by-Side**: Visual editor on left, code editor on right
- **Toggle**: Switch between visual-only, code-only, split view
- **Sync**: Real-time sync between views
- **Independent Scrolling**: Or synchronized scrolling option

## Asset Manager Design

### Asset Manager Panel

```
┌─────────────────────────────────────────────────────────┐
│  Assets                          [Images] [Fonts] [Icons]│
├─────────────────────────────────────────────────────────┤
│  [Search assets...]                    [+ Upload]        │
│                                                          │
│  ┌──────┬──────┬──────┬──────┐                          │
│  │ [img]│ [img]│ [img]│ [img]│                          │
│  │ img1 │ img2 │ img3 │ img4 │                          │
│  └──────┴──────┴──────┴──────┘                          │
│                                                          │
│  Selected: image.jpg                                     │
│  Size: 1920x1080 | 2.3 MB                               │
│  [Optimize] [Crop] [Resize] [Delete]                    │
└─────────────────────────────────────────────────────────┘
```

### Font Manager

- **Font List**: Scrollable list with preview
- **Font Preview**: Sample text in each font
- **Categories**: System fonts, Google Fonts, Custom fonts
- **Search**: Filter fonts by name
- **Font Details**: Family, weights, styles

### Icon Library

- **Icon Grid**: Visual grid of icons
- **Icon Sets**: Tabs for different icon sets
- **Search**: Search icons by name
- **Icon Preview**: Large preview on selection
- **Customization**: Color, size controls

## Version History Design

### Version Browser

```
┌─────────────────────────────────────────────────────────┐
│  Version History                                         │
├─────────────────────────────────────────────────────────┤
│  ┌──────────────────────────────────────────────────┐  │
│  │  Version 5 - Today 3:45 PM                      │  │
│  │  Version 4 - Today 2:30 PM                      │  │
│  │  Version 3 - Yesterday 5:20 PM                  │  │
│  │  Version 2 - 2 days ago                         │  │
│  │  Version 1 - 3 days ago                         │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Selected: Version 3                                     │
│  [Preview] [Restore] [Delete]                           │
└─────────────────────────────────────────────────────────┘
```

## Deployment Dialog Design

### Deployment Dialog

```
┌─────────────────────────────────────────────────────────┐
│  Deploy Project                                          │
├─────────────────────────────────────────────────────────┤
│  Select Service:                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │  ○ Netlify                                       │  │
│  │  ○ Vercel                                        │  │
│  │  ○ GitHub Pages                                  │  │
│  │  ○ FTP/SFTP                                      │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Settings:                                               │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Site Name: [my-website]                         │  │
│  │  Build Command: [npm run build]                  │  │
│  │  Output Directory: [dist]                        │  │
│  │  Environment Variables: [Manage...]              │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  [Cancel]  [Deploy]                                      │
└─────────────────────────────────────────────────────────┘
```

## SEO Tools Design

### SEO Panel

```
┌─────────────────────────────────────────────────────────┐
│  SEO Tools                                    [Score: 85]│
├─────────────────────────────────────────────────────────┤
│  Meta Tags:                                              │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Title: [My Website]                             │  │
│  │  Description: [Enter description...]             │  │
│  │  Keywords: [keyword1, keyword2]                  │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Open Graph:                                             │
│  ┌──────────────────────────────────────────────────┐  │
│  │  OG Title: [My Website]                          │  │
│  │  OG Image: [Browse...]                           │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Issues:                                                 │
│  ⚠ Missing meta description                             │
│  ⚠ Image missing alt text                               │
│                                                          │
│  [Generate Sitemap] [Generate robots.txt]               │
└─────────────────────────────────────────────────────────┘
```

## Accessibility Tools Design

### Accessibility Panel

```
┌─────────────────────────────────────────────────────────┐
│  Accessibility                           [Score: 92/100]│
├─────────────────────────────────────────────────────────┤
│  ARIA Attributes:                                        │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Role: [button]                                  │  │
│  │  aria-label: [Submit form]                       │  │
│  │  aria-describedby: [help-text]                   │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Issues:                                                 │
│  ⚠ Color contrast ratio: 3.2:1 (needs 4.5:1)          │
│  ✓ All images have alt text                            │
│  ⚠ Missing heading hierarchy                           │
│                                                          │
│  [Run Full Audit] [Fix Issues]                         │
└─────────────────────────────────────────────────────────┘
```

## Animation Timeline Design

### Timeline Editor

```
┌─────────────────────────────────────────────────────────┐
│  Animation Timeline                                      │
├─────────────────────────────────────────────────────────┤
│  Element: Button 1                                       │
│  ┌──────────────────────────────────────────────────┐  │
│  │  0s    0.5s    1s    1.5s    2s                  │  │
│  │  |-----|-----|-----|-----|                       │  │
│  │  ●─────────●─────────●                           │  │
│  │  Keyframe  Keyframe  Keyframe                    │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Properties:                                             │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Opacity: 0 → 1                                  │  │
│  │  Transform: translateY(20px) → translateY(0)     │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  [Play] [Stop] [Add Keyframe] [Delete]                 │
└─────────────────────────────────────────────────────────┘
```

## Component Library Design

### Component Browser

```
┌─────────────────────────────────────────────────────────┐
│  Component Library                    [+ Save Component]│
├─────────────────────────────────────────────────────────┤
│  [Search...]  [Category: All ▼]                         │
│                                                          │
│  ┌──────────┬──────────┬──────────┐                    │
│  │ [Preview]│ [Preview]│ [Preview]│                    │
│  │ Header   │ Footer   │ Card     │                    │
│  └──────────┴──────────┴──────────┘                    │
│                                                          │
│  Selected: Header Component                             │
│  [Insert] [Edit] [Delete] [Export]                      │
└─────────────────────────────────────────────────────────┘
```

## Theme Builder Design

### Theme Editor

```
┌─────────────────────────────────────────────────────────┐
│  Theme Builder                                           │
├─────────────────────────────────────────────────────────┤
│  Color Palette:                                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Primary:   [████] #2196F3                       │  │
│  │  Secondary: [████] #FF9800                       │  │
│  │  Accent:    [████] #4CAF50                       │  │
│  │  Background:[████] #FFFFFF                       │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  Design Tokens:                                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Spacing: 4px, 8px, 16px, 32px                  │  │
│  │  Typography: 12px, 14px, 16px, 24px, 32px       │  │
│  │  Border Radius: 4px, 8px, 16px                  │  │
│  └──────────────────────────────────────────────────┘  │
│                                                          │
│  [Save Theme] [Apply to Project] [Export]               │
└─────────────────────────────────────────────────────────┘
```

## Template Browser Design

### Template Gallery

```
┌─────────────────────────────────────────────────────────┐
│  Templates                    [Category: All ▼]         │
├─────────────────────────────────────────────────────────┤
│  ┌──────────┬──────────┬──────────┬──────────┐         │
│  │ [Preview]│ [Preview]│ [Preview]│ [Preview]│         │
│  │ Landing  │ Portfolio│ Blog     │ Business │         │
│  └──────────┴──────────┴──────────┴──────────┘         │
│                                                          │
│  Selected: Landing Page Template                         │
│  [Preview] [Use Template] [Save as Template]            │
└─────────────────────────────────────────────────────────┘
```
