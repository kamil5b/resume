# Kamil's CV Website

A modern, responsive CV website built with HTML, CSS, and JavaScript. This website showcases your professional experience, education, skills, and achievements in an elegant and interactive design.

## Features

- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **Modern UI**: Clean, professional design with smooth animations
- **Interactive Elements**: Hover effects, smooth scrolling, and dynamic navigation
- **Timeline Layout**: Professional work experience timeline
- **Skills Showcase**: Organized skill categories with interactive tags
- **Mobile Navigation**: Hamburger menu for mobile devices
- **Smooth Animations**: CSS animations and JavaScript interactions

## File Structure

```
resume-kamil5b/
├── index.html          # Main HTML file
├── styles.css          # CSS styles and responsive design
├── script.js           # JavaScript functionality
├── README.md           # This file
└── REQUIREMENT.md      # Your original requirements
```

## How to Use

1. **Open the website**: Simply open `index.html` in your web browser
2. **Customize content**: Edit the HTML file to update your information
3. **Modify styling**: Adjust colors, fonts, and layout in `styles.css`
4. **Add functionality**: Enhance interactivity in `script.js`

## Customization Guide

### Personal Information
Edit the following sections in `index.html`:

- **Hero Section**: Update name, title, and description
- **About Section**: Modify your personal description
- **Contact Information**: Update email, phone, and location
- **Social Links**: Add your actual social media profiles

### Work Experience
Update the timeline items in the experience section:

```html
<div class="timeline-item">
    <div class="timeline-marker"></div>
    <div class="timeline-content">
        <div class="timeline-header">
            <h3>Your Job Title</h3>
            <span class="company">Company Name</span>
            <span class="period">Date Range</span>
        </div>
        <p>Your job description and achievements.</p>
    </div>
</div>
```

### Skills
Modify the skills section to match your expertise:

```html
<div class="skill-category">
    <h3>Category Name</h3>
    <div class="skill-items">
        <span class="skill-tag">Skill 1</span>
        <span class="skill-tag">Skill 2</span>
        <span class="skill-tag">Skill 3</span>
    </div>
</div>
```

### Colors and Styling
The website uses a blue-purple gradient theme. To change colors, update these CSS variables in `styles.css`:

- Primary color: `#2563eb`
- Gradient: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- Background colors: `#f8fafc` for sections
- Text colors: `#1f2937` for headings, `#4b5563` for body text

## Browser Compatibility

- Chrome (recommended)
- Firefox
- Safari
- Edge
- Mobile browsers (iOS Safari, Chrome Mobile)

## Performance Features

- **Optimized Images**: Uses Font Awesome icons instead of heavy images
- **Smooth Scrolling**: CSS and JavaScript optimized for performance
- **Lazy Loading**: Elements animate as they come into view
- **Mobile Optimized**: Responsive design with touch-friendly interactions

## SEO and Accessibility

- Semantic HTML structure
- Proper heading hierarchy
- Alt text for images (when added)
- Keyboard navigation support
- Screen reader friendly

## Adding Your Photo

To add your profile photo:

1. Replace the profile placeholder in the hero section:
```html
<div class="hero-image">
    <img src="your-photo.jpg" alt="Kamil" class="profile-photo">
</div>
```

2. Add CSS for the photo:
```css
.profile-photo {
    width: 300px;
    height: 300px;
    border-radius: 50%;
    object-fit: cover;
    border: 3px solid rgba(255, 255, 255, 0.2);
}
```

## Deployment

To deploy your CV website:

1. **GitHub Pages**: Upload to a GitHub repository and enable GitHub Pages
2. **Netlify**: Drag and drop your files to Netlify
3. **Vercel**: Connect your repository to Vercel for automatic deployment
4. **Traditional Hosting**: Upload files to any web hosting service

## Future Enhancements

- Add a contact form
- Include a blog section
- Add a portfolio gallery
- Integrate with LinkedIn API
- Add dark mode toggle
- Include downloadable PDF version

## Support

If you need help customizing the website or encounter any issues, feel free to modify the code or reach out for assistance.

## License

This project is open source and available under the MIT License. 