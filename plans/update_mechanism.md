# Update Mechanism

## Overview

CO-web-builder uses an auto-update system that checks for new GitHub releases and allows users to update seamlessly.

## Update Detection

### Automatic Check

- **On Startup**: Check for updates when application starts (optional, user setting)
- **Periodic Check**: Check for updates every 24 hours (optional, user setting)
- **Manual Check**: User can manually check for updates via menu (Help → Check for Updates)

### Update Source

- **GitHub Releases API**: `https://api.github.com/repos/yourusername/CO-web-builder/releases/latest`
- **Version Comparison**: Compare current version with latest release tag
- **Semantic Versioning**: Uses semantic versioning (MAJOR.MINOR.PATCH)

## Update Process

### 1. Version Check

```python
# utils/update_checker.py
import requests
from packaging import version

def check_for_updates(current_version):
    """Check GitHub Releases for new version"""
    api_url = "https://api.github.com/repos/yourusername/CO-web-builder/releases/latest"
    try:
        response = requests.get(api_url, timeout=5)
        latest_release = response.json()
        latest_version = latest_release['tag_name'].lstrip('v')
        
        if version.parse(latest_version) > version.parse(current_version):
            return {
                'available': True,
                'version': latest_version,
                'download_url': latest_release['assets'][0]['browser_download_url'],
                'release_notes': latest_release['body'],
                'release_date': latest_release['published_at']
            }
    except Exception as e:
        log_error(f"Update check failed: {e}")
    
    return {'available': False}
```

### 2. Update Notification

- **Non-Blocking**: Notification appears in status bar or as a dialog
- **Update Available Dialog**:
  - Show new version number
  - Display release notes (formatted)
  - Options: "Update Now", "Update Later", "Skip This Version"
  - Checkbox: "Automatically download updates in the future"

### 3. Download Process

- **Background Download**: Download update file in background
- **Progress Indicator**: Show download progress in notification
- **Resume Support**: Resume interrupted downloads
- **Verification**: Verify download integrity (checksum/hash)

### 4. Installation

#### Windows

- Download `.exe` installer
- Run installer with silent flags
- Close application
- Install new version
- Restart application

#### macOS

- Download `.dmg` disk image
- Mount DMG
- Copy `.app` bundle to Applications folder
- Replace existing installation
- Restart application

#### Linux

- Download AppImage/Snap/package
- Install via package manager or replace AppImage
- Restart application

### 5. Rollback

- **Keep Previous Version**: Store previous version for rollback
- **Rollback Option**: Allow user to rollback if update causes issues
- **Automatic Rollback**: Auto-rollback if update fails to start

## User Settings

### Update Preferences

- **Auto-Check for Updates**: Enable/disable automatic checking
- **Auto-Download Updates**: Automatically download when available
- **Auto-Install Updates**: Automatically install (requires user confirmation)
- **Check Frequency**: Daily, Weekly, Monthly, Never
- **Update Channel**: Stable, Beta, Alpha (if applicable)

### Update Dialog Options

- **Update Now**: Download and install immediately
- **Update Later**: Remind me later (1 hour, 1 day, 1 week)
- **Skip This Version**: Don't notify about this version again
- **View Release Notes**: Open release notes in browser

## Error Handling

- **Network Errors**: Handle offline/network issues gracefully
- **Download Failures**: Retry mechanism (3 attempts)
- **Installation Failures**: Rollback to previous version
- **Version Conflicts**: Handle version conflicts during installation
- **Permission Issues**: Request appropriate permissions

## Security

- **HTTPS Only**: All downloads via HTTPS
- **Signature Verification**: Verify update file signatures (if implemented)
- **Checksum Verification**: Verify file integrity
- **No User Data**: Update check doesn't send user data

## Implementation

### Update Checker Module

```python
# utils/update_checker.py
class UpdateChecker:
    def __init__(self, current_version, config):
        self.current_version = current_version
        self.config = config
        self.repo_url = "https://api.github.com/repos/yourusername/CO-web-builder"
    
    def check_for_updates(self):
        """Check for available updates"""
        pass
    
    def download_update(self, download_url, progress_callback):
        """Download update file"""
        pass
    
    def install_update(self, update_file_path):
        """Install update (platform-specific)"""
        pass
    
    def rollback(self):
        """Rollback to previous version"""
        pass
```

### Update Notification UI

```python
# ui/update_dialog.py
class UpdateDialog:
    def __init__(self, update_info):
        """Show update available dialog"""
        pass
    
    def show_release_notes(self):
        """Display release notes"""
        pass
```

## Update Channels (Future)

- **Stable**: Production releases
- **Beta**: Pre-release testing
- **Alpha**: Early development builds

## Privacy

- **No User Data**: Update check only sends version query
- **No Tracking**: No analytics or tracking
- **Local Only**: All update logic runs locally
- **User Control**: User can disable auto-updates

