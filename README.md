# WorldWise 🌍

You can alredy access website by this [link](https://worldwise-learn.netlify.app/)

A modern, interactive travel tracking application built with React and powered by Supabase. Mark the locations you've visited on an interactive map, save travel memories, and keep your adventures organized in the cloud.

> **📚 Course-Based Project**  
> Built following [The Ultimate React Course](https://www.udemy.com/course/the-ultimate-react-course-2024-react-router-redux/) by Jonas Schmedtmann, with Supabase integration for real-world database functionality.

![React](https://img.shields.io/badge/React-18.3.1-61DAFB?logo=react)
![Vite](https://img.shields.io/badge/Vite-4.4.5-646CFF?logo=vite)
![Supabase](https://img.shields.io/badge/Supabase-Cloud%20Database-3ECF8E?logo=supabase)
![License](https://img.shields.io/badge/License-MIT-green)

## ✨ Features

- 🗺️ **Interactive World Map** - Click anywhere to mark cities and countries you've visited
- 🔍 **Smart Location Detection** - Automatically fetches city names and country info using reverse geocoding
- 💾 **Cloud Persistence** - All your travel data syncs across devices with Supabase
- 📅 **Travel Timeline** - Record the exact date of each visit
- 📝 **Travel Journal** - Add personal notes and memories for each location
- 🏳️ **Country Flags** - Visual emoji flags for every country
- 🎯 **City Management** - View all visited cities in an organized list, edit or delete entries
- ⚡ **Lightning Fast** - Built with Vite for optimal performance and instant reloads

## 🛠️ Tech Stack

| Layer              | Technologies                                     |
| ------------------ | ------------------------------------------------ |
| **Frontend**       | React 18, React Router v6, React Hooks           |
| **Build Tool**     | Vite                                             |
| **Database**       | Supabase (PostgreSQL)                            |
| **Maps**           | Leaflet, React Leaflet                           |
| **UI Components**  | React DatePicker, CSS Modules                    |
| **Authentication** | Built-in fake auth (extendable to Supabase Auth) |

## 📋 Prerequisites

Before you begin, ensure you have:

- **Node.js** 16.0 or higher ([Download](https://nodejs.org/))
- **npm** or **yarn** package manager
- A free **Supabase** account ([Sign up here](https://supabase.com))
- Basic knowledge of React and command line

## 🚀 Getting Started

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/worldwise.git
cd worldwise
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Configure Environment Variables

Create a `.env.local` file in the project root:

```bash
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your_anonymous_key_here
```

**How to get your credentials:**

1. Go to [supabase.com](https://supabase.com) and create/login to your project
2. Navigate to **Settings → API**
3. Copy your **Project URL** and **anon public** key
4. Paste them into `.env.local`

### 4️⃣ Create Supabase Database Table

In your Supabase dashboard (SQL Editor), run this query:

```sql
CREATE TABLE locations (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  cityName TEXT NOT NULL,
  country TEXT NOT NULL,
  emoji TEXT,
  date TIMESTAMP WITH TIME ZONE,
  notes TEXT,
  position JSONB,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security for public read access
ALTER TABLE locations ENABLE ROW LEVEL SECURITY;

-- Create policy for SELECT
CREATE POLICY "Anyone can read locations"
  ON locations FOR SELECT
  USING (true);

-- Create policy for INSERT
CREATE POLICY "Anyone can insert locations"
  ON locations FOR INSERT
  WITH CHECK (true);

-- Create policy for DELETE
CREATE POLICY "Anyone can delete locations"
  ON locations FOR DELETE
  USING (true);
```

### 5️⃣ Start the Development Server

```bash
npm run dev
```

Visit [http://localhost:5173](http://localhost:5173) in your browser.

## 📖 How to Use

1. **Explore** - Open the app and view the interactive world map
2. **Click on Map** - Click any location to add it to your travel history
3. **Auto-Fill** - The app automatically detects the city and country
4. **Add Details** - Choose the date you visited and add your personal notes
5. **Save** - Click "Add" to save the location to your database
6. **View List** - See all visited cities in the sidebar
7. **Manage** - Click on any city to view details or delete it

## 🎮 Available Commands

```bash
npm run dev          # Start development server (Vite)
npm run build        # Build for production
npm run preview      # Preview the production build locally
npm run lint         # Run ESLint to check code quality
```

## 📁 Project Structure

```
src/
├── components/           # Reusable React components
│   ├── AppNav.jsx       # Navigation bar
│   ├── Map.jsx          # Interactive Leaflet map
│   ├── Sidebar.jsx      # Left sidebar panel
│   ├── Form.jsx         # City add/edit form
│   ├── CityList.jsx     # List of visited cities
│   └── ...more components
├── contexts/            # React Context for state management
│   ├── CitiesContext.jsx # Cities data and Supabase queries
│   └── FakeAuthContext.jsx # Authentication context
├── hooks/              # Custom React hooks
│   ├── useUrlPosition.js # Extract coordinates from URL
│   └── useGeolocation.js # Browser geolocation API
├── pages/              # Page-level components
│   ├── AppLayout.jsx    # Main app layout
│   ├── Homepage.jsx     # Landing page
│   ├── Login.jsx        # Login page
│   └── ...more pages
├── App.jsx            # Root component with routing
└── main.jsx          # Application entry point
```

## 🔑 Key Features Explained

### Interactive Map with Leaflet

- Uses OpenStreetMap tiles for free, reliable map data
- Click to add cities, drag to navigate
- Each city marked with its country's flag emoji

### Real-time Geocoding

- Integrates BigDataCloud API for reverse geocoding
- Automatically fills city name and country from coordinates
- Validates that clicks are on valid locations

### Cloud Database with Supabase

- PostgreSQL database hosted on Supabase
- Real-time data sync across browser tabs
- Secure with Row Level Security policies

### Context API for State Management

- Uses React's built-in `useReducer` hook
- No Redux needed - clean and lightweight
- Provides global access to cities data

## 🔒 Security Considerations

- ✅ `.env.local` is in `.gitignore` - never commit secrets
- ✅ Using Supabase's anon key (public key) is safe
- ✅ Row Level Security policies are configured
- ⚠️ In production, implement proper authentication with Supabase Auth

## 🌱 Future Enhancements

- [ ] User authentication with Supabase Auth
- [ ] Multiple user accounts and shared travel lists
- [ ] Photo uploads for each location
- [ ] Travel statistics (countries count, total distance)
- [ ] Export trip data (PDF, CSV, GPX)
- [ ] Offline support with Service Workers
- [ ] Dark mode theme
- [ ] Mobile app with React Native

## 🐛 Troubleshooting

**Problem: Empty cities list**

- Check that RLS policies are enabled in Supabase
- Verify your `.env.local` has correct credentials
- Check browser console for errors (F12 → Console)

**Problem: Map not loading**

- Ensure Leaflet CSS is imported
- Check that browser allows geolocation
- Try refreshing the page

**Problem: Supabase connection error**

- Verify credentials in `.env.local`
- Check Supabase project is active
- Ensure table `locations` exists

## 📚 Learning Resources

- [React Documentation](https://react.dev)
- [Supabase Documentation](https://supabase.com/docs)
- [Leaflet Map Library](https://leafletjs.com)
- [Vite Guide](https://vitejs.dev)
- [The Ultimate React Course](https://www.udemy.com/course/the-ultimate-react-course-2024-react-router-redux/) by Jonas Schmedtmann

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 🙌 Credits

- **Course Instructor:** Jonas Schmedtmann - The Ultimate React Course
- **Map Library:** Leaflet
- **Backend Service:** Supabase
- **Build Tool:** Vite
