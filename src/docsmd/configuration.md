# Configuration

Customize Platform Akademik to fit your needs.

## Configuration File

Create or edit `config.js` in your project root:

```javascript
export default {
  appName: 'Platform Akademik',
  apiUrl: 'https://api.example.com',

  features: {
    darkMode: true,
    analytics: false,
    notifications: true,
  },

  auth: {
    tokenExpiry: 3600,
    refreshEnabled: true,
  },

  pagination: {
    defaultLimit: 10,
    maxLimit: 100,
  }
}
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `VITE_API_URL` | Backend API endpoint | `http://localhost:3000` |
| `VITE_APP_NAME` | Application display name | `Platform Akademik` |
| `VITE_DEBUG_MODE` | Enable debug logging | `false` |
| `VITE_ANALYTICS_ID` | Analytics tracking ID | - |

## Theme Configuration

Customize the look and feel:

```javascript
// theme.config.js
export const theme = {
  colors: {
    primary: '#1C4D8D',
    secondary: '#4988C4',
    accent: '#BDE8F5',
  },

  fonts: {
    sans: 'Inter, system-ui, sans-serif',
    mono: 'JetBrains Mono, monospace',
  },

  borderRadius: {
    sm: '0.375rem',
    md: '0.5rem',
    lg: '0.75rem',
  }
}
```

## Feature Flags

Enable or disable features dynamically:

```javascript
const features = {
  // Core features
  courseManagement: true,
  gradeBook: true,
  attendance: true,

  // Beta features
  aiAssistant: false,
  videoConference: false,

  // Experimental
  offlineMode: false,
}
```

> **Warning:** Experimental features may be unstable. Use at your own risk.
