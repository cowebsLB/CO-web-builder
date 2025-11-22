# Project File Format (.coweb)

## Overview

JSON-based project file format for CO-web-builder projects.

## File Structure

### Root Schema

```json
{
  "version": "1.0",
  "app_version": "1.2.3",
  "name": "Project Name",
  "description": "Project description",
  "created": "2024-01-01T00:00:00Z",
  "modified": "2024-01-01T00:00:00Z",
  "author": "Author Name",
  "settings": {},
  "elements": [],
  "styles": {},
  "assets": [],
  "meta": {}
}
```

## Schema Definition

### Version Information

```json
{
  "version": "1.0",           // Project file format version
  "app_version": "1.2.3"      // App version that created this file
}
```

### Project Metadata

```json
{
  "name": "My Website",                    // Project name
  "description": "A beautiful website",    // Project description
  "created": "2024-01-01T00:00:00Z",      // ISO 8601 timestamp
  "modified": "2024-01-01T00:00:00Z",     // ISO 8601 timestamp
  "author": "John Doe"                     // Author name
}
```

### Settings

```json
{
  "settings": {
    "viewport": {
      "width": 1920,
      "height": 1080
    },
    "responsive": {
      "breakpoints": [
        {
          "name": "mobile",
          "width": 375
        },
        {
          "name": "tablet",
          "width": 768
        },
        {
          "name": "desktop",
          "width": 1920
        }
      ]
    },
    "seo": {
      "title": "My Website",
      "description": "Website description",
      "keywords": ["keyword1", "keyword2"],
      "og_title": "My Website",
      "og_description": "Website description",
      "og_image": "path/to/image.jpg"
    },
    "export": {
      "framework": "html",
      "minify": false,
      "format_code": true
    }
  }
}
```

### Elements

```json
{
  "elements": [
    {
      "id": "element-1",
      "type": "container",
      "parent": null,
      "children": ["element-2", "element-3"],
      "content": {},
      "styles": {},
      "attributes": {},
      "responsive": {}
    }
  ]
}
```

### Element Schema

#### Base Element

```json
{
  "id": "unique-element-id",        // Unique identifier
  "type": "container",              // Element type
  "parent": "parent-element-id",    // Parent element ID (null for root)
  "children": ["child-1", "child-2"], // Child element IDs
  "content": {},                    // Element-specific content
  "styles": {},                     // Element styles
  "attributes": {},                 // HTML attributes
  "responsive": {}                  // Responsive styles
}
```

#### Container Element

```json
{
  "id": "container-1",
  "type": "container",
  "content": {
    "tag": "div"
  },
  "styles": {
    "width": "100%",
    "height": "auto",
    "margin": {
      "top": "0",
      "right": "0",
      "bottom": "0",
      "left": "0"
    },
    "padding": {
      "top": "20px",
      "right": "20px",
      "bottom": "20px",
      "left": "20px"
    },
    "background-color": "#ffffff",
    "display": "flex",
    "flex-direction": "row",
    "justify-content": "center",
    "align-items": "center"
  },
  "attributes": {
    "class": "container",
    "id": "main-container"
  }
}
```

#### Text Element

```json
{
  "id": "text-1",
  "type": "text",
  "content": {
    "text": "Hello, World!",
    "tag": "p"
  },
  "styles": {
    "font-family": "Arial, sans-serif",
    "font-size": "16px",
    "color": "#333333",
    "text-align": "left",
    "line-height": "1.5"
  }
}
```

#### Heading Element

```json
{
  "id": "heading-1",
  "type": "heading",
  "content": {
    "text": "Welcome",
    "level": 1,
    "tag": "h1"
  },
  "styles": {
    "font-family": "Arial, sans-serif",
    "font-size": "32px",
    "font-weight": "bold",
    "color": "#000000",
    "margin": {
      "bottom": "20px"
    }
  }
}
```

#### Image Element

```json
{
  "id": "image-1",
  "type": "image",
  "content": {
    "src": "assets/images/logo.png",
    "alt": "Logo",
    "tag": "img"
  },
  "styles": {
    "width": "200px",
    "height": "auto",
    "object-fit": "contain"
  },
  "attributes": {
    "loading": "lazy"
  }
}
```

#### Button Element

```json
{
  "id": "button-1",
  "type": "button",
  "content": {
    "text": "Click Me",
    "tag": "button"
  },
  "styles": {
    "padding": {
      "top": "10px",
      "right": "20px",
      "bottom": "10px",
      "left": "20px"
    },
    "background-color": "#007bff",
    "color": "#ffffff",
    "border": "none",
    "border-radius": "4px",
    "cursor": "pointer"
  },
  "attributes": {
    "type": "button",
    "onclick": "handleClick()"
  }
}
```

#### Link Element

```json
{
  "id": "link-1",
  "type": "link",
  "content": {
    "text": "Learn More",
    "href": "https://example.com",
    "tag": "a"
  },
  "styles": {
    "color": "#007bff",
    "text-decoration": "none"
  },
  "attributes": {
    "target": "_blank",
    "rel": "noopener noreferrer"
  }
}
```

### Styles

```json
{
  "styles": {
    "global": {
      "font-family": "Arial, sans-serif",
      "font-size": "16px",
      "color": "#333333",
      "line-height": "1.5"
    },
    "classes": {
      ".container": {
        "max-width": "1200px",
        "margin": "0 auto"
      },
      ".button-primary": {
        "background-color": "#007bff",
        "color": "#ffffff"
      }
    },
    "custom": "/* Custom CSS */"
  }
}
```

### Assets

```json
{
  "assets": [
    {
      "id": "asset-1",
      "type": "image",
      "path": "assets/images/logo.png",
      "name": "logo.png",
      "size": 12345,
      "width": 200,
      "height": 200,
      "format": "png"
    },
    {
      "id": "asset-2",
      "type": "font",
      "path": "assets/fonts/custom-font.woff2",
      "name": "custom-font.woff2",
      "family": "Custom Font"
    }
  ]
}
```

### Responsive Styles

```json
{
  "responsive": {
    "mobile": {
      "width": "100%",
      "font-size": "14px"
    },
    "tablet": {
      "width": "768px",
      "font-size": "16px"
    },
    "desktop": {
      "width": "100%",
      "font-size": "18px"
    }
  }
}
```

### Meta Information

```json
{
  "meta": {
    "tags": ["website", "portfolio"],
    "notes": "Project notes",
    "custom": {}
  }
}
```

## Validation Rules

### Required Fields

- `version`: Must be present and valid version string
- `name`: Must be present and non-empty
- `created`: Must be valid ISO 8601 timestamp
- `modified`: Must be valid ISO 8601 timestamp
- `elements`: Must be an array

### Element Validation

- `id`: Must be unique within project
- `type`: Must be valid element type
- `parent`: Must be valid element ID or null
- `children`: Must be array of valid element IDs

### Style Validation

- CSS property names must be valid
- CSS property values must be valid
- Units must be valid (px, em, rem, %, etc.)
- Colors must be valid (hex, rgb, rgba, named colors)

## Example Project File

```json
{
  "version": "1.0",
  "app_version": "1.0.0",
  "name": "My First Website",
  "description": "A simple landing page",
  "created": "2024-01-01T10:00:00Z",
  "modified": "2024-01-01T12:00:00Z",
  "author": "John Doe",
  "settings": {
    "viewport": {
      "width": 1920,
      "height": 1080
    },
    "responsive": {
      "breakpoints": [
        {"name": "mobile", "width": 375},
        {"name": "tablet", "width": 768},
        {"name": "desktop", "width": 1920}
      ]
    }
  },
  "elements": [
    {
      "id": "container-1",
      "type": "container",
      "parent": null,
      "children": ["heading-1", "text-1"],
      "content": {"tag": "div"},
      "styles": {
        "width": "100%",
        "padding": {"top": "40px", "right": "20px", "bottom": "40px", "left": "20px"},
        "background-color": "#f5f5f5"
      },
      "attributes": {"class": "main-container"}
    },
    {
      "id": "heading-1",
      "type": "heading",
      "parent": "container-1",
      "children": [],
      "content": {
        "text": "Welcome to My Website",
        "level": 1,
        "tag": "h1"
      },
      "styles": {
        "font-size": "32px",
        "color": "#333333",
        "text-align": "center",
        "margin": {"bottom": "20px"}
      }
    },
    {
      "id": "text-1",
      "type": "text",
      "parent": "container-1",
      "children": [],
      "content": {
        "text": "This is a simple landing page created with CO-web-builder.",
        "tag": "p"
      },
      "styles": {
        "font-size": "16px",
        "color": "#666666",
        "text-align": "center",
        "line-height": "1.6"
      }
    }
  ],
  "styles": {
    "global": {
      "font-family": "Arial, sans-serif",
      "margin": "0",
      "padding": "0"
    }
  },
  "assets": [],
  "meta": {
    "tags": ["landing-page", "simple"]
  }
}
```

## Version Migration

### Migration System

- **Version Detection**: Detect project file version on load
- **Migration Scripts**: Scripts to migrate between versions
- **Backup**: Create backup before migration
- **Validation**: Validate migrated project file

### Migration Example

```python
# core/migration.py
def migrate_project(data, from_version, to_version):
    """Migrate project from one version to another"""
    if from_version == "1.0" and to_version == "1.1":
        # Migration logic
        data = migrate_1_0_to_1_1(data)
    return data
```

## File Size Considerations

### Optimization

- **Compression**: Option to compress project files (gzip)
- **Minification**: Remove unnecessary whitespace
- **Asset References**: Store asset references, not full paths

### Size Limits

- **Recommended**: < 10 MB
- **Maximum**: < 50 MB
- **Warning**: Warn if project file > 10 MB

