# 4 Origines Ambassador Program

A modern, responsive web application for managing an ambassador program built with Alpine.js, Pico.css, and Supabase.

## Features

- **Google Authentication**: Secure sign-in with Google OAuth
- **Ambassador Dashboard**: Personalized dashboard with referral tracking
- **Real-time Updates**: Live statistics updates without page refresh
- **Public Profiles**: Unique ambassador profile pages (`/a/{username}`)
- **Social Sharing**: Pre-configured share buttons for major platforms
- **Admin Panel**: Management interface for program administrators
- **Responsive Design**: Mobile-first design with Pico.css
- **Modular Architecture**: Clean, maintainable codebase

## Tech Stack

- **Frontend**: Vanilla HTML, Alpine.js, Pico.css
- **Backend**: Supabase (Database + Auth)
- **Deployment**: Netlify-ready static site
- **No Build Process**: Direct browser execution, no bundlers

## Setup Instructions

### 1. Create Supabase Project

1. Go to [Supabase](https://supabase.com) and create a new account
2. Create a new project
3. Wait for the project to be fully provisioned
4. Go to **Settings** → **API** and copy:
   - Project URL
   - Anon (public) key

### 2. Configure Database

1. In your Supabase dashboard, go to **SQL Editor**
2. Copy the contents of `supabase/migrations/create_ambassador_schema.sql`
3. Paste and run the SQL to create all necessary tables and policies

### 3. Enable Google OAuth

1. In Supabase dashboard, go to **Authentication** → **Providers**
2. Enable **Google** provider
3. In Google Cloud Console:
   - Create a new project or select existing
   - Enable Google+ API
   - Go to **Credentials** → **Create credentials** → **OAuth client ID**
   - Set application type to **Web application**
   - Add authorized redirect URIs:
     - `https://your-project.supabase.co/auth/v1/callback`
     - `http://localhost:3000/auth/v1/callback` (for development)
   - Copy **Client ID** and **Client Secret**
4. Back in Supabase, paste the Google credentials
5. Save the configuration

### 4. Configure Application

1. Open `js/supabase-client.js`
2. Replace the placeholder values:
   ```javascript
   const SUPABASE_URL = 'https://your-project.supabase.co';
   const SUPABASE_ANON_KEY = 'your-anon-key-here';
   ```

### 5. Local Development

1. Start a local server (required for OAuth to work):
   ```bash
   # Using Python
   python -m http.server 3000
   
   # Using Node.js
   npx http-server -p 3000
   
   # Using PHP
   php -S localhost:3000
   ```

2. Open `http://localhost:3000` in your browser

### 6. Deploy to Netlify

1. Push your code to a Git repository (GitHub, GitLab, etc.)
2. Connect your repository to Netlify:
   - Go to [Netlify](https://netlify.com)
   - Click "New site from Git"
   - Select your repository
   - Set build settings:
     - Build command: (leave empty)
     - Publish directory: (leave empty or set to `/`)
3. Deploy the site

### 7. Configure Environment Variables

If you want to use environment variables instead of hardcoded values:

1. In Netlify dashboard, go to **Site settings** → **Environment variables**
2. Add:
   - `VITE_SUPABASE_URL`: Your Supabase project URL
   - `VITE_SUPABASE_ANON_KEY`: Your Supabase anon key
3. Modify `js/supabase-client.js` to use environment variables if available

### 8. Update OAuth Redirect URLs

1. Add your Netlify domain to Google OAuth authorized redirect URIs:
   - `https://your-site.netlify.app`
2. Update Supabase Auth settings if needed

### 9. Create Admin User

1. Sign up through your deployed application
2. In Supabase dashboard, go to **Table Editor** → **user_profiles**
3. Find your user and set `is_admin = true`
4. You can now access the admin panel at `/admin`

## Project Structure

```
/
├── index.html                 # Main application file
├── js/
│   ├── app.js                # Main Alpine.js application
│   ├── auth.js               # Authentication module
│   ├── dashboard.js          # Dashboard functionality
│   ├── admin.js              # Admin panel functionality
│   ├── utils.js              # Utility functions
│   └── supabase-client.js    # Supabase configuration
├── supabase/
│   └── migrations/
│       └── create_ambassador_schema.sql
└── README.md
```

## Key Features Explained

### Authentication Flow
- Users sign in with Google OAuth through Supabase
- User profiles are automatically created on first sign-in
- Each user gets a unique referral code (format: `4O-XXXXXXXX`)

### Ambassador Dashboard
- Real-time statistics (referrals, link views, earnings)
- Personalized referral link generation
- Social media sharing integration
- Copy-to-clipboard functionality

### Public Profiles
- Access via `/a/{referral-code}`
- Records link views for analytics
- Displays ambassador's information
- Call-to-action for joining the program

### Admin Panel
- Overview statistics for all ambassadors
- Detailed ambassador performance metrics
- User management capabilities
- Recent activity tracking

### Real-time Updates
- Uses Supabase real-time subscriptions
- Automatically updates statistics without page refresh
- Efficient database change tracking

## Security Features

- Row Level Security (RLS) enabled on all tables
- Users can only access their own data
- Admin-only access to sensitive operations
- Secure authentication through Supabase Auth

## Customization

### Styling
- Built with Pico.css for clean, semantic styling
- CSS custom properties for easy theme customization
- Responsive design with mobile-first approach

### Branding
- Update colors in CSS custom properties
- Replace text content in `index.html`
- Modify social sharing messages in `js/dashboard.js`

### Features
- Add new metrics by extending the database schema
- Implement additional social platforms
- Create custom admin features

## Troubleshooting

### Common Issues

1. **"Configuration not set" warning**
   - Update `js/supabase-client.js` with your actual Supabase credentials

2. **OAuth redirect error**
   - Ensure redirect URLs are correctly configured in Google Cloud Console
   - Check Supabase Auth provider settings

3. **Database errors**
   - Ensure migration SQL has been run successfully
   - Check RLS policies are correctly applied

4. **Real-time updates not working**
   - Verify Supabase real-time is enabled for your project
   - Check browser console for subscription errors

### Getting Help

1. Check browser console for detailed error messages
2. Verify Supabase dashboard for authentication and database issues
3. Ensure all configuration steps have been completed
4. Test with a fresh incognito window to avoid cache issues

## Performance Considerations

- Static site deployment for optimal performance
- Efficient database queries with proper indexing
- Real-time subscriptions only for necessary data
- Responsive images and optimized assets

## Future Enhancements

- Email notifications for new referrals
- Advanced analytics and reporting
- Multi-language support
- Integration with payment systems
- Mobile app development

## License

This project is provided as-is for educational and commercial use. Modify and distribute as needed for your ambassador program.