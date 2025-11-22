# Error Reporting & Crash Reporting

## Overview

Error and crash reporting system for CO-web-builder. All error reporting is local-only (no remote transmission).

## Error Handling Strategy

### Local Error Reporting

- **All Errors Stored Locally**: All errors and crashes logged to local files
- **No Remote Transmission**: No error data sent to external servers
- **User Privacy**: User has complete control over error data

## Error Logging

### Log File Location

- **Windows**: `%LOCALAPPDATA%\CO-web-builder\logs\error.log`
- **macOS**: `~/Library/Logs/CO-web-builder/error.log`
- **Linux**: `~/.local/state/CO-web-builder/logs/error.log`

### Log Format

```
[2024-01-01 12:00:00] ERROR: Module: core.project
Message: File not found: project.coweb
Traceback:
  File "core/project.py", line 45, in load_project
    with open(path, 'r') as f:
FileNotFoundError: [Errno 2] No such file or directory: 'project.coweb'
Context: {'project_path': '/path/to/project.coweb', 'user': 'john'}
```

### Error Categories

- **Critical**: Application crashes, fatal errors
- **Error**: Non-fatal errors that affect functionality
- **Warning**: Warnings that don't prevent functionality
- **Info**: Informational messages

## Crash Reporting

### Crash Detection

- **Unhandled Exceptions**: Catch all unhandled exceptions
- **Application Crashes**: Detect application crashes
- **System Errors**: Detect system-level errors

### Crash Information Collected

- **Timestamp**: When crash occurred
- **Error Message**: Error message
- **Traceback**: Full stack trace
- **System Information**: OS, Python version, app version
- **User Actions**: Last user actions before crash
- **Project State**: Project state at time of crash (if applicable)

### Crash Report Format

```json
{
  "timestamp": "2024-01-01T12:00:00Z",
  "version": "1.0.0",
  "platform": "Windows 11",
  "python_version": "3.10.0",
  "error_type": "FileNotFoundError",
  "error_message": "File not found: project.coweb",
  "traceback": "...",
  "context": {
    "last_action": "Open Project",
    "project_path": "/path/to/project.coweb",
    "memory_usage": "250 MB"
  },
  "system_info": {
    "os": "Windows",
    "os_version": "11",
    "cpu": "Intel Core i7",
    "ram": "16 GB"
  }
}
```

## Error Display

### User-Friendly Error Messages

- **Simple Language**: Use simple, non-technical language
- **Actionable**: Provide actionable solutions
- **Context**: Provide relevant context

### Error Dialog

```
┌─────────────────────────────────────────┐
│  Error                                  │
├─────────────────────────────────────────┤
│                                         │
│  Unable to open project file.          │
│                                         │
│  The file "project.coweb" could not    │
│  be found at the specified location.   │
│                                         │
│  Possible solutions:                    │
│  • Check if the file exists            │
│  • Verify the file path is correct     │
│  • Check file permissions              │
│                                         │
│  [Show Details] [OK]                   │
└─────────────────────────────────────────┘
```

### Error Details

- **Technical Details**: Show technical details in expandable section
- **Copy Error**: Allow user to copy error details
- **Report Error**: Option to save error report locally

## Error Recovery

### Automatic Recovery

- **Auto-Save Recovery**: Recover from auto-save if crash occurs
- **Project Recovery**: Recover unsaved project changes
- **State Recovery**: Recover application state

### Manual Recovery

- **Recovery Dialog**: Show recovery dialog on startup if crash detected
- **Recovery Options**: Options to recover or discard recovered data
- **Backup Restoration**: Restore from backup if available

## Error Prevention

### Input Validation

- **Validate Inputs**: Validate all user inputs
- **Sanitize Data**: Sanitize data before processing
- **Bounds Checking**: Check array/object bounds

### Defensive Programming

- **Try-Except Blocks**: Use try-except blocks for error-prone operations
- **Null Checks**: Check for null/None values
- **Type Checking**: Validate types before operations

### Testing

- **Error Scenarios**: Test error scenarios
- **Edge Cases**: Test edge cases
- **Stress Testing**: Test under stress conditions

## Error Reporting UI

### Error Notification

- **Status Bar**: Show error icon in status bar
- **Error Count**: Show error count if multiple errors
- **Error List**: View list of recent errors

### Error Viewer

- **Error History**: View error history
- **Filter Errors**: Filter by type, date, module
- **Search Errors**: Search error messages
- **Export Errors**: Export error log (for user to share if needed)

## User Consent

### Privacy-First Approach

- **No Automatic Reporting**: No automatic error reporting to external servers
- **User Control**: User has complete control
- **Local Only**: All errors stored locally only

### Optional Error Sharing

- **Manual Export**: User can manually export error log
- **User Choice**: User chooses if/when to share errors
- **No Tracking**: No tracking or analytics

## Error Analytics (Local)

### Local Analytics

- **Error Frequency**: Track error frequency locally
- **Error Patterns**: Identify error patterns
- **Common Errors**: Identify common errors

### Error Statistics

- **Error Count**: Count of errors by type
- **Error Trends**: Error trends over time
- **Module Errors**: Errors by module

## Implementation

### Error Handler

```python
# utils/error_handler.py
import logging
import traceback
from datetime import datetime
from pathlib import Path

class ErrorHandler:
    def __init__(self, log_path):
        self.log_path = Path(log_path)
        self.log_path.parent.mkdir(parents=True, exist_ok=True)
        self.setup_logging()
    
    def setup_logging(self):
        """Setup logging configuration"""
        logging.basicConfig(
            level=logging.ERROR,
            format='[%(asctime)s] %(levelname)s: %(message)s',
            handlers=[
                logging.FileHandler(self.log_path),
                logging.StreamHandler()
            ]
        )
    
    def handle_error(self, error, context=None):
        """Handle error and log it"""
        error_info = {
            'timestamp': datetime.now().isoformat(),
            'error_type': type(error).__name__,
            'error_message': str(error),
            'traceback': traceback.format_exc(),
            'context': context or {}
        }
        
        logging.error(f"Error: {error_info['error_message']}\n{error_info['traceback']}")
        
        return error_info
    
    def show_error_dialog(self, error_info):
        """Show user-friendly error dialog"""
        # Show error dialog with user-friendly message
        pass
```

### Crash Handler

```python
# utils/crash_handler.py
import sys
import traceback
from datetime import datetime
import json

class CrashHandler:
    def __init__(self, crash_log_path):
        self.crash_log_path = crash_log_path
        self.setup_crash_handler()
    
    def setup_crash_handler(self):
        """Setup global crash handler"""
        sys.excepthook = self.handle_crash
    
    def handle_crash(self, exc_type, exc_value, exc_traceback):
        """Handle unhandled exceptions"""
        crash_info = {
            'timestamp': datetime.now().isoformat(),
            'error_type': exc_type.__name__,
            'error_message': str(exc_value),
            'traceback': ''.join(traceback.format_exception(exc_type, exc_value, exc_traceback))
        }
        
        # Save crash report
        self.save_crash_report(crash_info)
        
        # Show crash dialog
        self.show_crash_dialog(crash_info)
    
    def save_crash_report(self, crash_info):
        """Save crash report to file"""
        with open(self.crash_log_path, 'a') as f:
            json.dump(crash_info, f, indent=2)
            f.write('\n')
    
    def show_crash_dialog(self, crash_info):
        """Show crash dialog to user"""
        # Show crash dialog
        pass
```

## Error Reporting Best Practices

### Do's

- ✅ Log all errors locally
- ✅ Provide user-friendly error messages
- ✅ Offer recovery options
- ✅ Maintain error history
- ✅ Respect user privacy

### Don'ts

- ❌ Send errors to external servers automatically
- ❌ Collect user data without consent
- ❌ Show technical errors to users
- ❌ Ignore errors silently
- ❌ Lose error context
