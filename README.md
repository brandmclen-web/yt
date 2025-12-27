# YouTube Audio Equalizer App

A powerful, feature-rich audio equalizer extension for YouTube that allows users to customize and enhance their listening experience with professional-grade audio controls.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

## 🎯 Project Overview

The YouTube Audio Equalizer App is a browser extension designed to enhance the audio quality and customization of YouTube videos. It provides users with intuitive controls to adjust audio frequencies, manage presets, and optimize sound settings for different content types and personal preferences.

This project aims to bridge the gap between YouTube's basic audio controls and professional audio processing capabilities, making advanced sound engineering tools accessible to everyday users.

### Goals

- Provide an intuitive interface for audio equalization
- Support multiple preset configurations
- Maintain low latency and high performance
- Ensure compatibility across major browsers
- Deliver a seamless, non-intrusive user experience

## ✨ Features

### Core Equalizer Features

- **10-Band Equalizer**: Professional 10-band frequency adjustment (60Hz - 16kHz)
- **Preset Library**: Pre-configured equalizer profiles for different content types
  - Music (Rock, Pop, Jazz, Classical, Electronic)
  - Podcasts & Audiobooks
  - Movies & Gaming
  - Speech Enhancement
  - Custom user presets
- **Real-time Audio Processing**: Instant audio adjustments with no latency
- **Gain Control**: Master volume and boost controls
- **Bass Boost**: Enhanced bass enhancement with separate control

### User Experience Features

- **Persistent Settings**: Automatically save user preferences and presets
- **Quick Toggle**: Enable/disable equalizer with one click
- **Visual Feedback**: Interactive frequency response visualization
- **Keyboard Shortcuts**: Quick access to common functions
- **Dark/Light Theme**: Adaptive theme support matching system preferences
- **Settings Export/Import**: Backup and share configurations

### Advanced Features

- **Frequency Response Graph**: Real-time visualization of audio adjustments
- **Volume Normalization**: Automatic loudness adjustment across videos
- **Compressor**: Dynamic range compression for consistent audio levels
- **Reverb Control**: Add or remove reverb effects
- **Site-Specific Settings**: Different profiles for different YouTube channels or playlists

## 🏗️ Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Browser Extension                        │
├──────────────────┬──────────────────────────┬───────────────┤
│  Content Script  │   Background Service     │   Popup UI    │
│  - DOM Injection │   - Settings Management  │ - Controls    │
│  - Audio API     │   - Preset Storage       │ - Presets     │
│                  │   - Sync & Updates       │ - Settings    │
└──────────────────┴──────────────────────────┴───────────────┘
                           │
                    ┌──────▼────────┐
                    │  Web Audio API │
                    │  (Core Engine) │
                    └────────────────┘
                           │
                    ┌──────▼────────┐
                    │ YouTube Player │
                    └────────────────┘
```

### Component Description

- **Content Script**: Injects the equalizer into the YouTube player and captures audio stream
- **Background Service Worker**: Manages settings persistence, preset synchronization, and extension lifecycle
- **Popup UI**: Provides the main user interface for controls and settings
- **Web Audio API**: Core audio processing engine using native browser APIs
- **Storage Layer**: IndexedDB for local persistence, Chrome Sync API for cross-device sync

### Data Flow

1. User adjusts equalizer settings via UI
2. Popup communicates with background service
3. Background service updates storage and broadcasts changes
4. Content script receives update and applies filters to audio context
5. Real-time audio processing occurs via Web Audio nodes
6. Visual feedback updates in real-time

## 🛠️ Tech Stack

### Frontend

- **HTML5**: Semantic markup for UI structure
- **CSS3**: Modern styling with flexbox and grid layouts
- **JavaScript (ES6+)**: Core extension logic
- **Canvas API**: Audio visualization rendering
- **Material Design Icons**: UI iconography

### Audio Processing

- **Web Audio API**: Native browser audio processing
- **BiquadFilterNode**: Frequency-based filtering for EQ
- **GainNode**: Volume and boost control
- **DynamicsCompressorNode**: Audio compression
- **ConvolverNode**: Reverb effects

### Storage & Sync

- **Chrome Storage API**: Configuration persistence
- **IndexedDB**: Local database for presets
- **Chrome Sync Storage**: Cross-device synchronization

### Build & Development

- **Webpack**: Module bundling and asset management
- **Babel**: JavaScript transpilation for compatibility
- **ESLint**: Code quality and style enforcement
- **Jest**: Unit testing framework
- **Prettier**: Code formatting

### Browser Compatibility

- Chrome/Chromium 90+
- Firefox 88+
- Edge 90+
- Opera 76+

## 💾 Installation

### Development Setup

#### Prerequisites

- Node.js 16+ and npm/yarn
- Git
- Chrome/Chromium, Firefox, or Edge browser
- Git

#### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/brandmclen-web/yt.git
   cd yt
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Build the extension**
   ```bash
   npm run build
   # or for development with watch mode
   npm run dev
   ```

4. **Load the extension in your browser**

   **Chrome/Edge:**
   - Open `chrome://extensions` or `edge://extensions`
   - Enable "Developer mode" (top right corner)
   - Click "Load unpacked"
   - Select the `dist/` folder from the project

   **Firefox:**
   - Open `about:debugging`
   - Click "This Firefox"
   - Click "Load Temporary Add-on"
   - Select the `manifest.json` file from the `dist/` folder

5. **Verify installation**
   - Navigate to YouTube.com
   - You should see the equalizer icon in your extensions menu
   - Click it to open the popup interface

### User Installation

Users can install the extension from official browser stores:

- **Chrome Web Store**: [Link to store listing]
- **Firefox Add-ons**: [Link to add-ons listing]
- **Edge Add-ons**: [Link to store listing]

## 🚀 Usage

### Basic Usage

1. **Enable the Equalizer**
   - Click the extension icon in your browser toolbar
   - Toggle the "Enable" switch

2. **Adjust Frequencies**
   - Use the sliders to boost or cut specific frequency bands
   - Slider range: -20dB to +20dB
   - Center position (0dB) = no adjustment

3. **Apply Presets**
   - Select a preset from the dropdown menu
   - Presets instantly apply to current and future videos

4. **Create Custom Preset**
   - Adjust equalizer to your preference
   - Click "Save as Preset"
   - Enter a name and save

### Keyboard Shortcuts

- `Alt + E`: Toggle equalizer on/off
- `Alt + R`: Reset to default settings
- `Alt + P`: Open preset menu
- `Alt + S`: Open settings

### Settings

- **Auto-enable**: Automatically enable on YouTube pages
- **Remember Settings**: Persist across sessions
- **Volume Normalization**: Normalize loudness levels
- **Theme**: Choose dark or light mode
- **Notifications**: Show/hide notifications on preset changes

## 📦 Deployment

### Build Process

```bash
# Clean build
npm run clean

# Production build with optimizations
npm run build:prod

# Generate distribution package
npm run package
```

### Staging Deployment

1. Build the extension for production
2. Upload to Chrome Web Store developer console
3. Submit for review (typically 1-3 hours)
4. Monitor for any review issues

### Production Release

1. **Version Management**
   - Update version in `manifest.json`
   - Update `CHANGELOG.md` with release notes
   - Commit changes: `git commit -m "Release v1.x.x"`

2. **Create Release Tag**
   ```bash
   git tag -a v1.x.x -m "Release version 1.x.x"
   git push origin v1.x.x
   ```

3. **Build for All Platforms**
   ```bash
   npm run build:all
   ```

4. **Submit to Store**
   - Chrome Web Store: Upload `dist/` folder
   - Firefox: Upload signed package
   - Edge: Upload via Edge Add-ons dashboard

5. **Publish and Announce**
   - Publish on all store platforms
   - Create GitHub release with changelog
   - Announce via social media/blog

### Continuous Integration

The project uses GitHub Actions for automated builds and testing:

- **On Pull Request**: Run tests, linting, and build verification
- **On Push to Main**: Auto-deploy to staging
- **On Release Tag**: Build and create release artifacts

## 🤝 Contributing

We welcome contributions from the community! Whether it's bug reports, feature requests, or code contributions, your input helps improve the project.

### Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/yt.git
   cd yt
   ```

3. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make your changes** following the style guide

5. **Test your changes**:
   ```bash
   npm test
   npm run lint
   npm run build
   ```

6. **Commit your changes**:
   ```bash
   git commit -m "Add feature: description of changes"
   ```

7. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

8. **Open a Pull Request** with a clear description of your changes

### Development Guidelines

#### Code Style

- Follow ESLint configuration automatically
- Run `npm run format` to auto-format code
- Use meaningful variable and function names
- Add comments for complex logic

#### Testing

- Write unit tests for new features
- Maintain minimum 80% code coverage
- Test across all supported browsers
- Include integration tests for UI changes

#### Commit Messages

Follow conventional commits format:

```
type(scope): subject

body

footer
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

Example:
```
feat(equalizer): add 10-band frequency control

Implement BiquadFilterNode for each frequency band
Add slider UI for intuitive control

Fixes #123
```

#### Pull Request Process

1. Update documentation if needed
2. Add/update tests for changes
3. Ensure all checks pass
4. Request review from maintainers
5. Address review feedback
6. Squash commits if requested

### Reporting Issues

When reporting bugs, please include:

- Browser and version
- Extension version
- Steps to reproduce
- Expected vs. actual behavior
- Console error messages (if any)
- Screenshots or video

### Feature Requests

Describe the feature including:

- Use case/problem it solves
- Expected behavior
- Potential implementation approach
- Mock-ups or examples (optional)

### Code Review Process

All contributions require code review by at least one maintainer:

- Automated tests must pass
- Code should follow style guide
- Documentation must be updated
- At least one approval required before merge

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Getting Help

- **Documentation**: Check the [docs/](docs/) folder for detailed guides
- **FAQ**: See [docs/FAQ.md](docs/FAQ.md) for common questions
- **Issues**: Search [GitHub Issues](https://github.com/brandmclen-web/yt/issues) for similar problems
- **Discussions**: Join our [GitHub Discussions](https://github.com/brandmclen-web/yt/discussions)

### Reporting Bugs

Found a bug? Please report it on [GitHub Issues](https://github.com/brandmclen-web/yt/issues) with:
- Clear description of the issue
- Steps to reproduce
- Expected behavior
- Actual behavior
- Browser/version information

### Security Issues

For security vulnerabilities, please email security@example.com instead of using the public issue tracker.

## 📊 Project Statistics

- **Languages**: JavaScript, HTML, CSS
- **Total Files**: ~50+
- **Lines of Code**: ~5000+
- **Test Coverage**: 85%+
- **Active Contributors**: Community-driven

## 🎉 Acknowledgments

- YouTube for providing the platform
- Web Audio API community for excellent documentation
- Open-source community for inspiring patterns and libraries
- All contributors and users for feedback and support

---

**Made with ❤️ by [brandmclen-web](https://github.com/brandmclen-web)**

For the latest updates, visit the [GitHub repository](https://github.com/brandmclen-web/yt).
