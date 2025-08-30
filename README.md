# Outfitly - AI-Powered Style Recommender

A modern, Pinterest-inspired web application that uses AI to analyze outfit photos and provide personalized styling recommendations. Users can upload outfit images, receive AI-generated suggestions for accessories and hairstyles, and organize their favorite styles into beautiful boards.

## ✨ Features

- **AI-Powered Analysis**: Upload outfit photos and receive intelligent recommendations for accessories, hairstyles, footwear, and makeup
- **Pinterest-Style Interface**: Beautiful grid layouts with smooth animations and hover effects
- **Personal Style Boards**: Create and organize collections of outfits and inspirations
- **User Authentication**: Secure sign-up and login system
- **Responsive Design**: Optimized for all devices from mobile to desktop
- **Dark/Light Theme**: Toggle between themes with smooth transitions
- **Image Upload**: Drag-and-drop interface with real-time preview

## 🚀 Tech Stack

- **Frontend**: React 18 + TypeScript + Tailwind CSS
- **Backend**: Supabase (Database, Auth, Storage)
- **AI Service**: Mock AI analyzer (simulates computer vision recommendations)
- **Build Tool**: Vite
- **Icons**: Lucide React
- **File Upload**: React Dropzone

## 📦 Installation & Setup

### Prerequisites
- Node.js 18+ and npm
- Supabase account (for database and authentication)

### 1. Clone and Install
```bash
git clone <repository-url>
cd outfitly
npm install
```

### 2. Supabase Setup
1. Create a new Supabase project at [supabase.com](https://supabase.com)
2. In your Supabase dashboard, click "Connect to Supabase" button in the top right
3. The environment variables will be automatically configured

### 3. Database Schema
Create the following tables in your Supabase SQL editor:

```sql
-- Users table is automatically handled by Supabase Auth

-- Outfits table
CREATE TABLE outfits (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES auth.users(id) ON DELETE CASCADE,
  image_url text NOT NULL,
  title text NOT NULL,
  description text,
  tags text[] DEFAULT '{}',
  created_at timestamptz DEFAULT now(),
  updated_at timestamptz DEFAULT now()
);

-- Recommendations table
CREATE TABLE recommendations (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  outfit_id uuid REFERENCES outfits(id) ON DELETE CASCADE,
  category text NOT NULL CHECK (category IN ('accessory', 'hairstyle', 'footwear', 'makeup')),
  title text NOT NULL,
  description text NOT NULL,
  image_url text NOT NULL,
  confidence decimal NOT NULL DEFAULT 0,
  created_at timestamptz DEFAULT now()
);

-- Boards table
CREATE TABLE boards (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid REFERENCES auth.users(id) ON DELETE CASCADE,
  title text NOT NULL,
  description text,
  cover_image text,
  is_private boolean DEFAULT false,
  created_at timestamptz DEFAULT now(),
  updated_at timestamptz DEFAULT now()
);

-- Board items table
CREATE TABLE board_items (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  board_id uuid REFERENCES boards(id) ON DELETE CASCADE,
  outfit_id uuid REFERENCES outfits(id) ON DELETE CASCADE,
  recommendation_id uuid REFERENCES recommendations(id) ON DELETE CASCADE,
  created_at timestamptz DEFAULT now()
);

-- Enable Row Level Security
ALTER TABLE outfits ENABLE ROW LEVEL SECURITY;
ALTER TABLE recommendations ENABLE ROW LEVEL SECURITY;
ALTER TABLE boards ENABLE ROW LEVEL SECURITY;
ALTER TABLE board_items ENABLE ROW LEVEL SECURITY;

-- Create policies
CREATE POLICY "Users can manage their own outfits" ON outfits
  FOR ALL TO authenticated
  USING (auth.uid() = user_id);

CREATE POLICY "Users can view recommendations for their outfits" ON recommendations
  FOR SELECT TO authenticated
  USING (outfit_id IN (SELECT id FROM outfits WHERE user_id = auth.uid()));

CREATE POLICY "Users can manage their own boards" ON boards
  FOR ALL TO authenticated
  USING (auth.uid() = user_id);

CREATE POLICY "Users can manage their own board items" ON board_items
  FOR ALL TO authenticated
  USING (board_id IN (SELECT id FROM boards WHERE user_id = auth.uid()));
```

### 4. Storage Setup
1. In your Supabase dashboard, go to Storage
2. Create a new bucket called `images`
3. Set the bucket to public
4. Configure the following policy for the bucket:

```sql
CREATE POLICY "Authenticated users can upload images" ON storage.objects
  FOR INSERT TO authenticated
  WITH CHECK (bucket_id = 'images');

CREATE POLICY "Images are publicly accessible" ON storage.objects
  FOR SELECT TO public
  USING (bucket_id = 'images');
```

### 5. Run the Application
```bash
npm run dev
```

The application will be available at `http://localhost:5173`

## 🎨 Design Features

- **Modern UI**: Clean, sophisticated interface inspired by Pinterest
- **Smooth Animations**: Subtle hover effects and transitions throughout
- **Responsive Grid**: Adaptive layouts for different screen sizes
- **Dark Mode**: Beautiful dark theme with proper contrast ratios
- **Micro-interactions**: Engaging button states and loading animations

## 🤖 AI Integration

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

## 🔐 Authentication

- Email/password authentication via Supabase Auth
- User profiles with avatar support
- Secure session management
- Protected routes and data access

## 📱 Mobile Experience

- Touch-optimized interface
- Bottom navigation for mobile devices
- Responsive image uploads
- Swipe-friendly interactions

## 🚀 Deployment

The app is ready for deployment to platforms like:
- Vercel
- Netlify
- Supabase Hosting

Remember to set up your production Supabase environment variables in your hosting platform.

## 🔧 Configuration

Key configuration files:
- `tailwind.config.js`: Tailwind CSS customization
- `src/lib/supabase.ts`: Supabase client configuration
- `src/types/index.ts`: TypeScript type definitions

## 📄 License

MIT License - feel free to use this project for personal or commercial purposes.