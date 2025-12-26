# Jude Del Rosario - Portfolio

A stunning, modern portfolio website featuring smooth animations, 3D elements, and interactive mouse-tracking effects. Built with Vue 3, TypeScript, Vite, and Three.js.

## Features

✨ **Animations & Transitions**
- Smooth scroll animations
- Staggered entry animations
- Hover effects on all interactive elements
- Floating animations on components

🖱️ **Mouse Tracking Background**
- Interactive background that responds to cursor movement
- Floating orbs that follow the mouse
- Animated gradient mesh with blobs
- Twinkling stars background

🎲 **3D Elements**
- Three.js powered 3D scene
- Rotating cube, sphere, and torus
- Animated floating particles
- Dynamic lighting and reflections

📱 **Fully Responsive**
- Mobile-first design
- Optimized for all screen sizes
- Touch-friendly navigation

🚀 **Performance Optimized**
- Built with Vite for fast development
- Optimized build for production
- Lazy loading of components

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **TypeScript** - Type-safe JavaScript
- **Vite** - Next generation frontend tooling
- **Three.js** - 3D graphics library
- **GSAP** - Animation library (for future enhancements)

## Getting Started

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Installation

```bash
# Clone the repository
git clone <repository-url>

# Navigate to project
cd delrosario_jude_portfolio

# Install dependencies
npm install
```

### Development

```bash
# Start development server
npm run dev
```

The site will be available at `http://localhost:5173`

### Build

```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

## Deployment to Vercel

### Option 1: Using Vercel CLI

```bash
# Install Vercel CLI (if not already installed)
npm i -g vercel

# Deploy
vercel
```

### Option 2: Using GitHub Integration

1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Create a new project and import your GitHub repository
4. Vercel will automatically detect Vue + Vite and configure the build settings
5. Click "Deploy"

### Option 3: Git Push Deploy

1. Connect your GitHub repository to Vercel
2. Every push to the main branch automatically triggers a new deployment

## File Structure

```
src/
├── components/
│   ├── Canvas3D.vue              # 3D scene with Three.js
│   ├── MouseTrackingBackground.vue # Interactive background
│   └── ProjectCard.vue            # Project card component
├── App.vue                         # Main app component
├── main.ts                         # Application entry point
└── style.css                       # Global styles

```

## Customization

### Update Portfolio Information

Edit the arrays in `src/App.vue`:

- **stats**: Change the numbers and labels
- **projects**: Add/remove your projects
- **skillCategories**: Update your skills

### Change Colors

The color scheme is defined in the CSS:
- Primary: `#667eea` (Purple-blue)
- Secondary: `#764ba2` (Purple)
- Background: `#0a0e27` (Dark blue)

Update these hex values in `src/App.vue` and component files to customize colors.

### Modify 3D Scene

Edit `src/components/Canvas3D.vue` to:
- Add more 3D objects
- Change lighting
- Adjust animations
- Modify materials

## Performance Tips

1. **Image Optimization**: If adding images, use optimized formats (WebP)
2. **Code Splitting**: Vite automatically splits code for better loading
3. **Lazy Loading**: Use Vue's `defineAsyncComponent` for heavy components
4. **Animation Performance**: Use CSS transforms and will-change for smooth animations

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers

## Future Enhancements

- Add project filtering
- Implement dark/light theme toggle
- Add blog section
- Integrate with CMS
- Add contact form with email service
- Add more 3D elements
- Implement scroll parallax

## License

This project is open source and available under the MIT License.

## Contact

For questions or suggestions, feel free to reach out!

---

**Live Demo**: [Visit Portfolio](https://your-domain.vercel.app)

**Deployed on**: Vercel
