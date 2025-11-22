# CI/CD & Release Process

## Overview

Continuous Integration/Continuous Deployment (CI/CD) pipeline and release process for CO-web-builder.

## Version Numbering

### Semantic Versioning

- **Format**: `MAJOR.MINOR.PATCH` (e.g., `1.2.3`)
- **MAJOR**: Breaking changes, incompatible API changes
- **MINOR**: New features, backward compatible
- **PATCH**: Bug fixes, backward compatible

### Version Examples

- `1.0.0`: Initial release
- `1.0.1`: Bug fix release
- `1.1.0`: New features, backward compatible
- `2.0.0`: Major release with breaking changes

### Pre-release Versions

- `1.0.0-alpha.1`: Alpha release
- `1.0.0-beta.1`: Beta release
- `1.0.0-rc.1`: Release candidate

## CI/CD Pipeline

### GitHub Actions Workflow

#### Workflow Triggers

- **Push to main**: Run tests and build
- **Pull Request**: Run tests
- **Tag Creation**: Create release build
- **Manual**: Manual workflow dispatch

#### Workflow Steps

1. **Checkout Code**: Checkout repository
2. **Setup Python**: Setup Python environment
3. **Install Dependencies**: Install dependencies
4. **Run Tests**: Run unit and integration tests
5. **Lint Code**: Run linters (pylint, flake8)
6. **Build**: Build application for all platforms
7. **Package**: Create installers/packages
8. **Upload Artifacts**: Upload build artifacts
9. **Create Release**: Create GitHub release (on tag)

### Platform-Specific Builds

#### Windows Build

```yaml
- name: Build Windows
  run: |
    pip install pyinstaller
    pyinstaller --onefile --windowed src/main.py
    # Create installer with Inno Setup
```

#### macOS Build

```yaml
- name: Build macOS
  run: |
    pip install pyinstaller
    pyinstaller --onefile --windowed src/main.py
    # Create .app bundle
    # Create .dmg
```

#### Linux Build

```yaml
- name: Build Linux
  run: |
    pip install pyinstaller
    pyinstaller --onefile src/main.py
    # Create AppImage
    # Create deb/rpm packages
```

## Release Process

### Release Checklist

#### Pre-Release

- [ ] All tests passing
- [ ] Code reviewed and approved
- [ ] Documentation updated
- [ ] Changelog updated
- [ ] Version number updated
- [ ] Release notes prepared

#### Release

- [ ] Create release branch
- [ ] Update version numbers
- [ ] Create git tag
- [ ] Push tag to trigger CI/CD
- [ ] Wait for builds to complete
- [ ] Verify build artifacts
- [ ] Create GitHub release
- [ ] Upload build artifacts
- [ ] Publish release notes

#### Post-Release

- [ ] Monitor for issues
- [ ] Update documentation
- [ ] Announce release
- [ ] Update download links

### Release Types

#### Stable Release

- **Version**: `MAJOR.MINOR.PATCH`
- **Tag Format**: `v1.2.3`
- **Release Notes**: Full release notes
- **Distribution**: All platforms

#### Beta Release

- **Version**: `MAJOR.MINOR.PATCH-beta.N`
- **Tag Format**: `v1.2.3-beta.1`
- **Release Notes**: Beta release notes
- **Distribution**: All platforms (optional)

#### Alpha Release

- **Version**: `MAJOR.MINOR.PATCH-alpha.N`
- **Tag Format**: `v1.2.3-alpha.1`
- **Release Notes**: Alpha release notes
- **Distribution**: Developer builds only

## Build Automation

### Build Scripts

#### Windows Build Script

```python
# build_windows.py
import subprocess
import shutil
from pathlib import Path

def build_windows():
    # Build with PyInstaller
    subprocess.run(['pyinstaller', '--onefile', '--windowed', 'src/main.py'])
    
    # Create installer with Inno Setup
    subprocess.run(['iscc', 'installer.iss'])
    
    # Copy to dist/
    shutil.copy('dist/CO-web-builder.exe', 'dist/windows/')
```

#### macOS Build Script

```python
# build_macos.py
import subprocess
import shutil

def build_macos():
    # Build with PyInstaller
    subprocess.run(['pyinstaller', '--onefile', '--windowed', 'src/main.py'])
    
    # Create .app bundle
    # Create .dmg
    subprocess.run(['create-dmg', 'dist/CO-web-builder.dmg', 'dist/CO-web-builder.app'])
```

#### Linux Build Script

```python
# build_linux.py
import subprocess

def build_linux():
    # Build with PyInstaller
    subprocess.run(['pyinstaller', '--onefile', 'src/main.py'])
    
    # Create AppImage
    # Create deb/rpm packages
```

### Build Configuration

#### PyInstaller Spec File

```python
# CO-web-builder.spec
a = Analysis(
    ['src/main.py'],
    pathex=[],
    binaries=[],
    datas=[('app_assets', 'app_assets')],
    hiddenimports=[],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    win_no_prefer_redirects=False,
    win_private_assemblies=False,
    cipher=block_cipher,
    noarchive=False,
)
pyz = PYZ(a.pure, a.zipped_data, cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    a.binaries,
    a.zipfiles,
    a.datas,
    [],
    name='CO-web-builder',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    upx_exclude=[],
    runtime_tmpdir=None,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
)
```

## Release Notes Generation

### Changelog Format

```markdown
# Changelog

## [1.2.3] - 2024-01-01

### Added
- New feature X
- New feature Y

### Changed
- Improved performance
- Updated dependencies

### Fixed
- Fixed bug A
- Fixed bug B

### Removed
- Removed deprecated feature
```

### Automated Release Notes

- **Git Commits**: Generate from git commits
- **Pull Requests**: Include PR descriptions
- **Issues**: Link to related issues
- **Format**: Markdown format

## Testing in CI/CD

### Test Suite

- **Unit Tests**: Run all unit tests
- **Integration Tests**: Run integration tests
- **Platform Tests**: Test on all platforms
- **Performance Tests**: Run performance benchmarks

### Test Coverage

- **Target**: > 80% code coverage
- **Report**: Generate coverage report
- **Threshold**: Fail if coverage drops below threshold

## Deployment

### GitHub Releases

- **Automatic**: Create release on tag push
- **Artifacts**: Upload build artifacts
- **Release Notes**: Include release notes
- **Draft Releases**: Create draft releases for review

### Distribution

- **GitHub Releases**: Primary distribution method
- **Website**: Download links on website
- **Package Managers**: Future: Homebrew, Chocolatey, etc.

## Version Management

### Version File

```python
# src/version.py
__version__ = "1.2.3"
```

### Version Updates

- **Automated**: Update version in CI/CD
- **Manual**: Update version before release
- **Sync**: Sync version across all files

## Release Schedule

### Release Cadence

- **Major Releases**: Every 6-12 months
- **Minor Releases**: Every 1-2 months
- **Patch Releases**: As needed (bug fixes)

### Release Planning

- **Roadmap**: Plan releases based on roadmap
- **Milestones**: Use GitHub milestones
- **Sprints**: Plan releases in sprints

## Quality Assurance

### Pre-Release Testing

- **Manual Testing**: Manual testing checklist
- **Automated Testing**: All automated tests passing
- **Platform Testing**: Test on all platforms
- **User Testing**: Beta testing with users

### Release Criteria

- [ ] All tests passing
- [ ] No critical bugs
- [ ] Documentation complete
- [ ] Release notes prepared
- [ ] Builds successful on all platforms

## Rollback Plan

### Rollback Procedure

- **Identify Issue**: Identify critical issue
- **Create Hotfix**: Create hotfix branch
- **Fix Issue**: Fix the issue
- **Test Fix**: Test the fix
- **Release Hotfix**: Release hotfix version
- **Communicate**: Communicate rollback to users

## Future Enhancements

- **Automated Testing**: More automated tests
- **Beta Program**: Beta testing program
- **Auto-Update**: Automatic update distribution
- **Analytics**: Release analytics (optional, user consent)

