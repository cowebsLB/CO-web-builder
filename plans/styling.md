# Styling System

## Styling Approach

### Visual Style Editor

- **WYSIWYG Editing**: Visual property editors (no code required)
- **Live Preview**: See changes immediately
- **Property Panels**: Organized by category (Content, Layout, Style, Advanced)

## Style Categories

### 1. Typography

**Properties**:

- Font Family (system fonts + web fonts)
- Font Size (px, em, rem, %, vw, vh)
- Font Weight (100-900, normal, bold)
- Font Style (normal, italic, oblique)
- Line Height (number, px, em, %)
- Letter Spacing (px, em)
- Text Align (left, center, right, justify)
- Text Decoration (none, underline, overline, line-through)
- Text Transform (none, uppercase, lowercase, capitalize)
- Text Color (color picker)

**UI Components**:

- Font dropdown selector
- Size input with unit selector
- Color picker (hex, rgb, hsl)
- Text alignment buttons
- Font weight slider/dropdown

### 2. Colors & Backgrounds

**Properties**:

- Background Color (solid color)
- Background Image (image URL or upload)
- Background Position (top, center, bottom, left, right, custom)
- Background Size (cover, contain, auto, custom)
- Background Repeat (no-repeat, repeat, repeat-x, repeat-y)
- Background Attachment (scroll, fixed)
- Gradient Background (linear, radial, conic)
  - Gradient Colors
  - Gradient Direction/Angle
  - Gradient Stops

**UI Components**:

- Color picker (visual + hex input)
- Image upload/URL input
- Gradient editor (visual gradient builder)
- Background position controls

### 3. Layout & Spacing

**Properties**:

- Width (px, %, em, rem, vw, auto)
- Height (px, %, em, rem, vh, auto)
- Min/Max Width/Height
- Margin (top, right, bottom, left)
- Padding (top, right, bottom, left)
- Box Sizing (content-box, border-box)

**UI Components**:

- Visual spacing editor (4-way input)
- Size inputs with unit selector
- Linked/unlinked toggle (same value for all sides)

### 4. Positioning

**Properties**:

- Position (static, relative, absolute, fixed, sticky)
- Top, Right, Bottom, Left (offset values)
- Z-Index (layer order)
- Display (block, inline, inline-block, flex, grid, none)
- Float (left, right, none)

**UI Components**:

- Position dropdown
- Offset inputs
- Z-index input
- Display type selector

### 5. Flexbox

**Properties** (when display: flex):

- Flex Direction (row, column, row-reverse, column-reverse)
- Flex Wrap (nowrap, wrap, wrap-reverse)
- Justify Content (flex-start, center, flex-end, space-between, space-around, space-evenly)
- Align Items (flex-start, center, flex-end, stretch, baseline)
- Align Content (for multi-line)
- Gap (row gap, column gap)

**UI Components**:

- Visual flexbox editor
- Direction buttons
- Alignment controls

### 6. Grid

**Properties** (when display: grid):

- Grid Template Columns (track sizes)
- Grid Template Rows (track sizes)
- Grid Gap (row gap, column gap)
- Grid Auto Flow (row, column, dense)
- Justify Items (start, center, end, stretch)
- Align Items (start, center, end, stretch)

**UI Components**:

- Visual grid builder
- Track size inputs
- Gap controls

### 7. Borders

**Properties**:

- Border Width (top, right, bottom, left)
- Border Style (solid, dashed, dotted, double, none)
- Border Color (color picker)
- Border Radius (top-left, top-right, bottom-right, bottom-left)
- Border Collapse (for tables)

**UI Components**:

- Border width inputs (4-way)
- Border style dropdown
- Color picker
- Border radius visual editor

### 8. Effects

**Properties**:

- Box Shadow:
  - X offset
  - Y offset
  - Blur radius
  - Spread radius
  - Color
  - Inset (optional)
- Opacity (0-1)
- Visibility (visible, hidden)
- Overflow (visible, hidden, scroll, auto)
- Transform (translate, rotate, scale, skew)
- Transition (property, duration, timing, delay)
- Animation (name, duration, timing, delay, iteration, direction)

**UI Components**:

- Shadow editor (visual + inputs)
- Opacity slider
- Transform controls
- Transition/animation builder

### 9. Advanced CSS

**Properties**:

- Custom CSS (raw CSS code)
- CSS Variables (custom properties)
- Media Queries (responsive styles)
- Pseudo-classes (hover, focus, active, etc.)
- Pseudo-elements (::before, ::after)

**UI Components**:

- Code editor (syntax highlighted)
- CSS variable manager
- Media query builder
- Pseudo-selector editor

## Style Inheritance

### Cascading Rules

- **Inheritance**: Some properties inherit from parent (font, color, etc.)
- **Override**: Child elements can override parent styles
- **Specificity**: More specific selectors override less specific
- **Visual Indicator**: Show inherited vs. overridden styles

## Responsive Styling

### Breakpoint System

- **Default**: Base styles (mobile-first)
- **Tablet**: Styles for ≥768px
- **Desktop**: Styles for ≥1024px
- **Large Desktop**: Styles for ≥1920px
- **Custom**: User-defined breakpoints

### Responsive Properties

- Different values per breakpoint
- Visual breakpoint switcher
- Preview at different sizes
- Copy styles between breakpoints

## Style Generation

### CSS Output Format

```css
/* Generated CSS */
.element-id {
  /* Layout */
  width: 100%;
  height: auto;
  margin: 10px;
  padding: 20px;
  
  /* Typography */
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: #333333;
  
  /* Background */
  background-color: #ffffff;
  
  /* Borders */
  border: 1px solid #cccccc;
  border-radius: 4px;
  
  /* Effects */
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Responsive */
@media (min-width: 768px) {
  .element-id {
    font-size: 18px;
    padding: 30px;
  }
}
```

### CSS Organization

- **Class-based**: Generate reusable classes
- **ID-based**: Element-specific styles
- **Inline Styles**: Option for inline CSS
- **External File**: Separate CSS file
- **Minification**: Optional CSS minification

## Style Validation

### Validation Rules

- **Valid CSS Properties**: Check against CSS spec
- **Valid Values**: Validate property values
- **Unit Validation**: Ensure correct units
- **Color Validation**: Valid color formats
- **URL Validation**: Valid image/asset URLs

### Error Handling

- **Invalid Property Warning**: Highlight invalid properties
- **Suggestion System**: Suggest corrections
- **Auto-fix**: Fix common mistakes automatically

## Style Presets

### Predefined Styles

- **Button Styles**: Primary, secondary, success, danger, etc.
- **Text Styles**: Heading styles, body text, captions
- **Card Styles**: Card components with shadows
- **Form Styles**: Input field styles
- **Navigation Styles**: Menu/nav styles

### Custom Presets

- **Save Style**: Save current style as preset
- **Apply Preset**: Apply saved preset to element
- **Preset Library**: Manage style presets

## Theme System

### Color Themes

- **Primary Color**: Main brand color
- **Secondary Color**: Accent color
- **Background Colors**: Light/dark backgrounds
- **Text Colors**: Primary/secondary text
- **Link Colors**: Link states

### Typography Themes

- **Heading Font**: Font for headings
- **Body Font**: Font for body text
- **Font Scale**: Heading size scale

### Apply Theme

- Apply theme to entire project
- Override individual elements
- Export theme as CSS variables
