# Frontend Mentor - Blog preview card solution

This is a solution to the [Blog preview card challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/blog-preview-card-ckPaj01IcS). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- View the blog preview card component as designed
- See hover and focus states for all interactive elements on the card

### Screenshot

- [Mobile screenshot](./screenshots/mobile.png)
- [Desktop screenshot](./screenshots/desktop.png)
- [Hover state screenshot](./screenshots/hover_state.png)

### Links

- Solution URL: [GitHub Repository](https://github.com/amjadham001/frontend_mentor-blog_preview_card)
- Live Site URL: [Live Demo](https://amjadham001.github.io/frontend_mentor-blog_preview_card/)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- [Tailwindcss](https://tailwindcss.com/) - CSS framework
- Mobile-first workflow

### What I learned

- **Font loading:** I gained experience in properly loading and applying custom fonts to maintain design consistency. This included using web-safe fonts and optimizing font delivery for better performance and user experience.

Application from this project (input.css):

```css
@font-face {
  font-family: "Figtree";
  src:
   url("../assets/fonts/Figtree-VariableFont_wght.ttf") format("truetype-variations"),
   url("../assets/fonts/Figtree-VariableFont_wght.ttf") format("truetype");
  font-weight: 300 900; /* Weight range - only works with truetype-variations */
  font-style: normal;
  font-display: swap; /* Show fallback font immediately, swap when loaded */
}

@theme {
  --font-figtree:
   "Figtree", "Figtree-Static", "Segoe UI", "Roboto", "Helvetica Neue",
   "Arial", "Noto Sans", ui-sans-serif, system-ui, -apple-system, sans-serif;
}
```

For a detailed explanation of the font loading strategy used in this project, see [FONT_LOADING_GUIDE.md](assets/fonts/FONT_LOADING_GUIDE.md).

- **Design implementation direction (Top To Bottom):** I discovered the value of consciously choosing a direction for implementing the design. By working from the top of the layout down to the bottom ("Top To Bottom"), It allow you to maintain focus, reduce distractions, and achieve faster and more accurate results. This approach helped me build the structure step by step, ensuring each section was completed before moving on to the next.

### Continued development

Areas for Continued Development:

- Adding smooth animations to UI components (e.g., animating the blog card cover).
- Creating more advanced and accessible hover, focus, and active state effects to improve interactivity and usability across devices.

### Useful resources

- [Figma](https://www.figma.com/) - This tool helped me to view and inspect the design in more detail such as `font-size`, `padding` and `margin`, to get a perfect and consistent result.

## Author

- Github - [@amjadham001](https://github.com/amjadham001)
- Frontend Mentor - [@amjadham001](https://www.frontendmentor.io/profile/amjadham001)
- Twitter - [@amjadham001](https://x.com/amjadham001)
- Codepen - [@amjadham001](https://codepen.io/amjadham001)

## Acknowledgments

To everyone who taught me a letter 🌹...
