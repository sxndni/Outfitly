# Outfitly 

A modern, Pinterest-inspired web application that uses AI to analyze outfit photos and provide personalized styling recommendations. Users can upload outfit images, receive AI-generated suggestions for accessories and hairstyles, and organize their favorite styles into beautiful boards.

## Features

- **AI-Powered Analysis**: Upload outfit photos and receive intelligent recommendations for accessories, hairstyles, footwear, and makeup
- **Pinterest-Style Interface**: Beautiful grid layouts with smooth animations and hover effects
- **Personal Style Boards**: Create and organize collections of outfits and inspirations
- **User Authentication**: Secure sign-up and login system
- **Responsive Design**: Optimized for all devices from mobile to desktop
- **Dark/Light Theme**: Toggle between themes with smooth transitions
- **Image Upload**: Drag-and-drop interface with real-time preview

## Tech Stack

- **Frontend**: React 18 + TypeScript + Tailwind CSS
- **Backend**: Supabase (Database, Auth, Storage)
- **AI Service**: Mock AI analyzer (simulates computer vision recommendations)
- **Build Tool**: Vite
- **Icons**: Lucide React
- **File Upload**: React Dropzone

## Design Features

- **Modern UI**: Clean, sophisticated interface inspired by Pinterest
- **Smooth Animations**: Subtle hover effects and transitions throughout
- **Responsive Grid**: Adaptive layouts for different screen sizes
- **Dark Mode**: Beautiful dark theme with proper contrast ratios
- **Micro-interactions**: Engaging button states and loading animations

## AI Integration

The current implementation includes a sophisticated mock AI service that simulates:
- Outfit analysis and style categorization
- Accessory recommendations based on outfit aesthetics
- Hairstyle suggestions that complement the look
- Footwear and makeup recommendations
- Confidence scoring for each recommendation

For production use, integrate with real AI services like:
- OpenAI's CLIP model for image analysis
- Google Cloud Vision API
- Custom fashion-trained computer vision models

## Authentication

- Email/password authentication via Supabase Auth
- User profiles with avatar support
- Secure session management
- Protected routes and data access

## Mobile Experience

- Touch-optimized interface
- Bottom navigation for mobile devices
- Responsive image uploads
- Swipe-friendly interactions

## Deployment

The app is ready for deployment to platforms like:
- Vercel
- Netlify
- Supabase Hosting

Remember to set up your production Supabase environment variables in your hosting platform.

## Configuration

Key configuration files:
- `tailwind.config.js`: Tailwind CSS customization
- `src/lib/supabase.ts`: Supabase client configuration
- `src/types/index.ts`: TypeScript type definitions

## 📄 License

MIT License - feel free to use this project for personal or commercial purposes.
