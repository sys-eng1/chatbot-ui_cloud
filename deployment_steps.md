# Deployment Guide for ChatBot UI

This guide explains how to deploy the ChatBot UI application using Vercel, Supabase, and GitHub.

## Prerequisites

- GitHub account
- Vercel account
- Supabase account
- Node.js installed locally
- Supabase CLI installed (`brew install supabase`)

## Step 1: GitHub Setup

1. Create a new repository on GitHub
2. Clone the repository locally
3. Copy your project files into the cloned repository
4. Push the code to GitHub

## Step 2: Supabase Setup

1. Create a new Supabase project
2. Go to Project Settings > Database to get your database credentials
3. Enable Email Authentication:
   - Go to Authentication > Providers
   - Enable Email provider
   - Configure Email settings (OTP, confirmation settings)
4. Set up URL Configuration:
   - Go to Authentication > URL Configuration
   - Add your Vercel deployment URL as the Site URL

## Step 3: Database Setup

1. Link your local project to Supabase:
```bash
supabase link --project-ref your-project-ref
```

2. Reset and initialize the database:
```bash
supabase db reset --linked
```

3. When prompted with "Do you want to reset the remote database? [y/N]", type:
```bash
y
```

This will:
- Apply all migrations
- Create necessary tables (workspaces, profiles, chats, etc.)
- Set up the database schema

## Step 4: Vercel Deployment

1. Import your GitHub repository in Vercel
2. Configure environment variables in Vercel:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
   SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
   ```
3. Deploy the application

## Step 5: Final Configuration

1. Verify all tables are created in Supabase
2. Test user authentication flow
3. Verify chat functionality

## Troubleshooting

If you encounter database-related issues:
1. Check Supabase table editor to ensure all tables exist
2. Verify database connections in Vercel environment variables
3. If tables are missing, run:
```bash
supabase db reset --linked
```

## Important Notes

- Always backup your database before running reset commands
- Keep your environment variables secure
- Update your site URL in Supabase when changing domains
- Monitor Vercel deployment logs for any errors