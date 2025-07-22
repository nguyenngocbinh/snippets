# Documentation Directory

This directory contains the website configuration, themes, and documentation-related files for the snippets project.

## 📁 Contents

### Configuration Files
- **`_quarto.yml`**: Main Quarto configuration file defining the website structure, navigation, and formatting
- **`index.qmd`**: Homepage content and introduction
- **`include-files.lua`**: Quarto filter for custom functionality

### Styling
- **`theme.scss`**: Light theme styles
- **`theme-dark.scss`**: Dark theme styles

### Assets
- **`assets/images/`**: Website images, logos, and visual assets

## 🔧 Configuration Overview

The `_quarto.yml` file defines:
- Website metadata and navigation
- Sidebar structure and content organization
- Theme configuration (light/dark modes)
- HTML formatting options
- Custom filters and extensions

## 🎨 Theming

The project uses customized Cosmo theme with:
- Custom color schemes for light and dark modes
- Responsive design elements
- Code syntax highlighting
- Search functionality

## 📱 Assets Management

Images and static assets are stored in `assets/` and referenced using relative paths from the docs directory. This ensures proper asset loading in both development and production environments.

## 🚀 Development

To work with the documentation:
1. Modify content in the `../content/` directory
2. Update navigation in `_quarto.yml` if adding new sections
3. Customize themes in the `.scss` files
4. Run `quarto preview` from the project root to see changes
5. Run `quarto render` to build the static site
