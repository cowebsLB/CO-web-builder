# Internationalization (i18n)

## Overview

Multi-language support for CO-web-builder application UI. Currently deferred to later phases, but planned for future implementation.

## Status

- **Current**: English only
- **Phase**: Future enhancement (Phase 4+)
- **Priority**: Medium (after core features are stable)

## Supported Languages (Planned)

### Initial Release

- English (en) - Default
- Spanish (es)
- French (fr)
- German (de)

### Future Additions

- Italian (it)
- Portuguese (pt)
- Japanese (ja)
- Chinese (zh)
- Arabic (ar) - RTL support needed

## Implementation Approach

### Translation Files

- **Format**: JSON files for simplicity
- **Location**: `app_assets/locales/{language_code}/messages.json`
- **Structure**:

```json
{
  "app_name": "CO-web-builder",
  "menu_file": "File",
  "menu_edit": "Edit",
  "menu_view": "View",
  "menu_help": "Help",
  "button_new": "New",
  "button_open": "Open",
  "button_save": "Save",
  "status_ready": "Ready",
  "error_file_not_found": "File not found: {filename}",
  "dialog_confirm_exit": "Are you sure you want to exit?",
  "splash_loading": "Loading...",
  "splash_initializing": "Initializing application...",
  "splash_loading_config": "Loading configuration...",
  "splash_loading_modules": "Loading modules...",
  "splash_initializing_ui": "Initializing UI framework...",
  "splash_loading_assets": "Loading asset manager...",
  "splash_checking_updates": "Checking for updates...",
  "splash_finalizing": "Finalizing...",
  "splash_ready": "Ready!"
}
```

### Translation Manager

```python
# utils/i18n.py
import json
from pathlib import Path

class TranslationManager:
    def __init__(self, locale='en'):
        self.locale = locale
        self.translations = {}
        self.load_translations(locale)
    
    def load_translations(self, locale):
        """Load translation file for locale"""
        locale_file = Path(f"app_assets/locales/{locale}/messages.json")
        if locale_file.exists():
            with open(locale_file, 'r', encoding='utf-8') as f:
                self.translations = json.load(f)
    
    def translate(self, key, **kwargs):
        """Translate key with optional parameters"""
        text = self.translations.get(key, key)
        if kwargs:
            text = text.format(**kwargs)
        return text
    
    def set_locale(self, locale):
        """Change locale"""
        self.locale = locale
        self.load_translations(locale)
```

### Usage in Code

```python
# Example usage
from utils.i18n import TranslationManager

i18n = TranslationManager('en')

# Simple translation
button_text = i18n.translate("button_save")

# Translation with parameters
error_msg = i18n.translate("error_file_not_found", filename="project.coweb")
```

## Language Selection

### Settings UI

- **Language Selector**: Dropdown in Settings → Preferences → Language
- **Available Languages**: List of supported languages
- **Language Names**: Display in native language (e.g., "Español" for Spanish)
- **Requires Restart**: Show notification that restart is required

### Language Detection

- **System Locale**: Detect system language on first launch
- **User Preference**: Remember user's language choice
- **Fallback**: Fall back to English if translation missing

## RTL (Right-to-Left) Support

### Languages Requiring RTL

- Arabic (ar)
- Hebrew (he)
- Persian (fa)
- Urdu (ur)

### Implementation

- **Layout Mirroring**: Mirror UI layout for RTL languages
- **Text Direction**: Set text direction in UI components
- **Icon Mirroring**: Mirror icons that have direction (arrows, etc.)
- **CustomTkinter RTL**: Check CustomTkinter RTL support or implement custom

## Translation Management

### Translation Workflow

1. **Extract Strings**: Extract all translatable strings from code
2. **Create Template**: Create base translation template (English)
3. **Translation**: Translate to target languages
4. **Review**: Review translations for accuracy
5. **Testing**: Test UI with translations
6. **Update**: Update translations as UI changes

### Translation Tools

- **Manual**: JSON files edited manually
- **Future**: Integration with translation platforms (Crowdin, Weblate, etc.)
- **Community**: Allow community contributions

### String Extraction

- **Mark Translatable Strings**: Use `i18n.translate()` wrapper
- **Extract Script**: Script to extract all translatable strings
- **Generate Template**: Generate translation template from code

## UI Components Translation

### Menu Items

- File, Edit, View, Help menus
- All menu items and submenus
- Keyboard shortcuts (keep same, translate labels)

### Dialogs

- All dialog titles and messages
- Button labels (OK, Cancel, Yes, No, etc.)
- Error messages
- Warning messages
- Confirmation dialogs

### Status Bar

- Status messages
- Element information
- Cursor position labels

### Tooltips

- All tooltips
- Help text
- Hover descriptions

### Splash Screen

- All status messages
- Loading text

## Date and Number Formatting

### Locale-Specific Formatting

- **Dates**: Format dates according to locale
- **Numbers**: Format numbers (decimal separator, thousands separator)
- **Currency**: If currency is used, format according to locale

## Testing

### Translation Testing

- **UI Testing**: Test UI with each language
- **Text Overflow**: Check for text overflow in different languages
- **RTL Testing**: Test RTL languages thoroughly
- **Missing Translations**: Handle missing translations gracefully

## Future Enhancements

- **Pluralization**: Handle plural forms correctly
- **Context**: Context-aware translations
- **Gender**: Gender-aware translations (if needed)
- **Regional Variants**: Support regional variants (e.g., en-US, en-GB)

