# Font Loading Guide

## 📋 Table of Contents

1. [Overview](#overview)
2. [Font Types Explained](#font-types-explained)
3. [Browser Compatibility](#browser-compatibility)
4. [Implementation Strategy](#implementation-strategy)
5. [File Structure](#file-structure)
6. [CSS Implementation](#css-implementation)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)
9. [Resources](#resources)

---

## 🎯 Overview

This guide explains the comprehensive font loading strategy implemented in this project, covering variable fonts, static fonts, browser compatibility, and fallback systems.

### Key Concepts

- **Progressive Enhancement**: Modern browsers get variable fonts, older browsers get static fonts
- **Fallback Chain**: Multiple layers of font fallbacks for maximum compatibility
- **Performance Optimization**: Efficient loading with `font-display: swap`
- **Cross-Platform Consistency**: System fonts as ultimate fallback

---

## 🎨 Font Types Explained

### Variable Fonts

**What they are:**

- Single font file containing multiple weights/styles
- More efficient than multiple static font files
- Modern technology (2016+)

**Benefits:**

- ✅ Smaller total file size
- ✅ Single HTTP request
- ✅ Smooth weight transitions
- ✅ Better performance

**Limitations:**

- ❌ Requires modern browser support
- ❌ Larger individual file size
- ❌ Complex fallback handling

**File Examples:**

```
Figtree-VariableFont_wght.ttf (61KB) - All weights 300-900
Figtree-Italic-VariableFont_wght.ttf (62KB) - All italic weights 300-900
```

### Static Fonts

**What they are:**

- Traditional font files - one file per weight/style
- Universal browser support
- Simpler loading behavior

**Benefits:**

- ✅ Universal compatibility
- ✅ Smaller individual files
- ✅ Simpler fallback logic
- ✅ Faster perceived loading

**Limitations:**

- ❌ Multiple HTTP requests needed
- ❌ Larger total file size
- ❌ Limited weight options

**File Examples:**

```
static/Figtree-Medium.ttf (40KB) - Weight 500 only
static/Figtree-ExtraBold.ttf (40KB) - Weight 800 only
```

---

## 🌐 Browser Compatibility

### Variable Font Support

| Browser | Version | Support |
|---------|---------|---------|
| Chrome | 62+ | ✅ Full support |
| Firefox | 62+ | ✅ Full support |
| Safari | 11+ | ✅ Full support |
| Edge | 17+ | ✅ Full support |
| Internet Explorer | All | ❌ No support |

### Static Font Support

| Browser | Version | Support |
|---------|---------|---------|
| All browsers | All versions | ✅ Universal support |

---

## 🚀 Implementation Strategy

### Three-Tier Fallback System

1. **Variable Fonts** (Modern browsers)
   - Primary choice for Chrome 62+, Firefox 62+, Safari 11+
   - Efficient single-file loading
   - Full weight range (300-900)

2. **Static Fonts** (Older browsers)
   - Fallback for browsers that don't support variable fonts
   - Individual files for specific weights
   - Universal compatibility

3. **System Fonts** (Ultimate fallback)
   - Platform-specific fonts (Segoe UI, Roboto, etc.)
   - Always available
   - Consistent with OS design

### Progressive Enhancement Flow

```
Modern Browser → Variable Font → Full functionality
     ↓
Older Browser → Static Font → Limited weights
     ↓
Very Old Browser → System Font → Basic functionality
```

---

## 📁 File Structure

```
assets/fonts/
├── Figtree-VariableFont_wght.ttf          # Variable font (normal)
├── Figtree-Italic-VariableFont_wght.ttf   # Variable font (italic)
├── static/
│   ├── Figtree-Medium.ttf                 # Static font (weight 500)
│   └── Figtree-ExtraBold.ttf              # Static font (weight 800)
├── OFL.txt                                # Open Font License
├── README.txt                             # Font documentation
└── FONT_LOADING_GUIDE.md                  # This guide
```

### Missing Static Fonts

The following static fonts are mentioned in `README.txt` but not included:

**Normal Weights:**

- `Figtree-Light.ttf` (300)
- `Figtree-Regular.ttf` (400)
- `Figtree-SemiBold.ttf` (600)
- `Figtree-Bold.ttf` (700)
- `Figtree-Black.ttf` (900)

**Italic Weights:**

- `Figtree-LightItalic.ttf` (300)
- `Figtree-Italic.ttf` (400)
- `Figtree-MediumItalic.ttf` (500)
- `Figtree-SemiBoldItalic.ttf` (600)
- `Figtree-BoldItalic.ttf` (700)
- `Figtree-ExtraBoldItalic.ttf` (800)
- `Figtree-BlackItalic.ttf` (900)

---

## 💻 CSS Implementation

### Variable Fonts (Modern Browsers)

```css
@font-face {
  font-family: "Figtree";
  src: url("../assets/fonts/Figtree-VariableFont_wght.ttf") format("truetype-variations"),
       url("../assets/fonts/Figtree-VariableFont_wght.ttf") format("truetype");
  font-weight: 300 900;
  font-style: normal;
  font-display: swap; /* Critical for variable fonts */
}

@font-face {
  font-family: "Figtree";
  src: url("../assets/fonts/Figtree-Italic-VariableFont_wght.ttf") format("truetype-variations"),
       url("../assets/fonts/Figtree-Italic-VariableFont_wght.ttf") format("truetype");
  font-weight: 300 900;
  font-style: italic;
  font-display: swap; /* Critical for variable fonts */
}
```

**Why two formats?**

- `truetype-variations`: Modern browsers that understand variable fonts
- `truetype`: Older browsers that load the file but treat it as regular font

**Why font-display: swap?**

- Variable fonts are larger and more complex
- Prevents invisible text while loading
- Shows fallback font immediately

### Static Fonts (Older Browsers)

```css
@font-face {
  font-family: "Figtree-Static";
  src: url("../assets/fonts/static/Figtree-Medium.ttf") format("truetype");
  font-weight: 500;
  font-style: normal;
  /* No font-display needed - browser handles loading efficiently */
}

@font-face {
  font-family: "Figtree-Static";
  src: url("../assets/fonts/static/Figtree-ExtraBold.ttf") format("truetype");
  font-weight: 800;
  font-style: normal;
  /* No font-display needed - browser handles loading efficiently */
}
```

**Why only one format?**

- Static fonts are traditional technology with universal browser support
- No need for format fallbacks like variable fonts

**Why no font-display?**

- Static fonts are smaller and load faster
- No complex fallback chain needed
- Browser's default behavior is sufficient

### Custom Design Token

```css
@theme {
  --font-figtree: "Figtree", "Figtree-Static", "Segoe UI", "Roboto", "Helvetica Neue", "Arial", "Noto Sans", ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}
```

**Fallback Chain:**

1. `"Figtree"` - Variable fonts (modern browsers)
2. `"Figtree-Static"` - Static fonts (older browsers)
3. System fonts - Ultimate fallback (always available)

### Usage Examples

```css
/* In CSS */
.heading {
  font-family: theme(font-figtree);
  font-weight: 800;
}

.body-text {
  font-family: theme(font-figtree);
  font-weight: 400;
}

/* In Tailwind classes */
.text-element {
  font-family: theme(font-figtree);
}
```

---

## ✅ Best Practices

### 1. Progressive Enhancement

- Start with system fonts as base
- Add static fonts for older browsers
- Use variable fonts for modern browsers

### 2. Performance Optimization

- Use `font-display: swap` for variable fonts
- Skip `font-display` for static fonts
- Implement proper fallback chains

### 3. Browser Compatibility

- Test on multiple browsers and versions
- Use feature detection when possible
- Provide graceful degradation

### 4. File Organization

- Keep variable and static fonts separate
- Use descriptive file names
- Document font weights and styles

### 5. Loading Strategy

- Load critical fonts first
- Use preload for important fonts
- Implement proper caching headers

---

## 🔧 Troubleshooting

### Common Issues

**Font not loading:**

- Check file paths are correct
- Verify font files exist
- Check browser console for errors

**Variable fonts not working:**

- Ensure browser supports variable fonts
- Check format declarations
- Verify font-weight ranges

**Static fonts not loading:**

- Check file permissions
- Verify font file integrity
- Test with different browsers

**Fallback not working:**

- Check font-family order
- Verify system font names
- Test with network throttling

### Debugging Tips

1. **Browser DevTools:**
   - Check Network tab for font loading
   - Inspect computed styles
   - Test with different network conditions

2. **Font Loading API:**

   ```javascript
   document.fonts.ready.then(() => {
     console.log('All fonts loaded');
   });
   ```

3. **Feature Detection:**

   ```javascript
   if (CSS.supports('font-variation-settings', 'normal')) {
     console.log('Variable fonts supported');
   }
   ```

---

## 📚 Resources

### Official Documentation

- [MDN Variable Fonts Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide)
- [Google Fonts Variable Fonts](https://developers.google.com/fonts/docs/getting_started)
- [CSS Font Display](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display)

### Browser Support

- [Can I Use Variable Fonts](https://caniuse.com/variable-fonts)
- [Can I Use Font Display](https://caniuse.com/css-font-display)

### Tools

- [Variable Fonts Inspector](https://variable-fonts.typenetwork.com)
- [Font Loading API](https://developer.mozilla.org/en-US/docs/Web/API/FontFace)

### Learning Resources

- [Variable Fonts Guide](https://developers.google.com/web/fundamentals/design-and-ux/typography/variable-fonts)
- [Font Loading Best Practices](https://web.dev/font-display/)
- [Web Font Optimization](https://web.dev/optimize-webfont-loading/)

---

## 📄 License

This font loading implementation uses the Figtree font family, which is licensed under the SIL Open Font License, Version 1.1. See `OFL.txt` for complete license details.

**Key permissions:**

- ✅ Use in commercial projects
- ✅ Modify and redistribute
- ✅ Bundle with software

**Key restrictions:**

- ❌ Cannot sell font files by themselves
- ❌ Must keep under same license if modified
- ❌ Cannot use author's name to promote modified versions

---

*Last updated: Jun 30 2023*
*Version: 1.0*
