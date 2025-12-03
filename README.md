# GitHub SpecKit Info Site

A single-page website for the GitHub SpecKit meetup event in Zürich.

## Client-Side Logging

The site includes a comprehensive client-side logging system that helps track user interactions and debug issues.

### Features

- **Multi-level logging**: DEBUG, INFO, WARN, ERROR
- **Automatic event tracking**: Page lifecycle, navigation, user interactions
- **Error handling**: Global error and unhandled promise rejection capture
- **Session storage**: Logs are persisted in sessionStorage (last 100 entries)
- **Structured logging**: Each log entry includes timestamp, level, message, data, user agent, and URL

### Usage

The logger is available globally as `Logger` and can be used from the browser console:

```javascript
// Log at different levels
Logger.debug('Debug message', {additionalData: 'value'});
Logger.info('Info message');
Logger.warn('Warning message', {warningDetails: 'details'});
Logger.error('Error message', {errorDetails: 'details'});

// Retrieve all logs
Logger.getLogs();

// Clear all logs
Logger.clearLogs();
```

### Logged Events

The system automatically logs the following events:

#### Page Lifecycle
- Page load (with load time metrics)
- DOM content loaded
- User leaving page

#### Navigation & Interactions
- Navigation link clicks (with target)
- Smooth scroll events (with target and offset)
- Mobile navigation toggle
- Registration button clicks (with platform)

#### Scroll & Visibility
- Navbar scroll state changes
- Element visibility (Intersection Observer)

#### Errors
- JavaScript errors (with stack traces)
- Unhandled promise rejections

### Log Levels

- **DEBUG** (0): Detailed information for debugging (e.g., scroll events, element visibility)
- **INFO** (1): General informational messages (e.g., page load, navigation clicks) - Default level
- **WARN** (2): Warning messages
- **ERROR** (3): Error messages

The current log level is set to `INFO` by default. To change it:

```javascript
Logger.currentLevel = Logger.levels.DEBUG; // Show all logs including DEBUG
Logger.currentLevel = Logger.levels.WARN;  // Show only WARN and ERROR
```

### Log Entry Format

Each log entry contains:

```javascript
{
  "timestamp": "2025-12-03T09:49:16.100Z",
  "level": "INFO",
  "message": "Page fully loaded",
  "data": {
    "loadTime": 1234
  },
  "userAgent": "Mozilla/5.0...",
  "url": "http://localhost:8080/index.html"
}
```

### Browser Console Output

Logs are also displayed in the browser console with timestamps and appropriate console methods (console.debug, console.info, console.warn, console.error).

Example:
```
[2025-12-03T09:49:16.100Z] INFO: Page fully loaded {loadTime: 1234}
```

### Development

To test the logging implementation locally:

1. Start a local web server:
   ```bash
   python3 -m http.server 8080
   ```

2. Open the browser console (F12) and navigate to:
   ```
   http://localhost:8080/index.html
   ```

3. Watch the console for automatic log entries or use the `Logger` object to create custom logs.

## Technologies

- HTML5
- CSS3 (with animations and responsive design)
- Vanilla JavaScript
- Client-side logging with sessionStorage
