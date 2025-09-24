# First React Movie Finder

A movie discovery app. It fetches catalog data from The Movie Database (TMDB) API, keeps track of popular search terms in Appwrite, and highlights trending movies so you can quickly find something to watch.

## Features
- **Search with Debounce** - Type in the search box to query TMDB without spamming requests.
- **Trending Searches** - Stores search activity in Appwrite and surfaces the top 5 most popular queries.
- **Movie Highlights** - Shows poster art, average rating, language, and release year with graceful fallbacks.
- **Loading States** - Displays a spinner while API calls are in flight and validates error scenarios.

## Tech Stack
- React 19
- Vite 7 development tooling
- TMDB REST API
- Appwrite (Database + SDK)

## Prerequisites
- Node.js 18 or higher
- npm 9+ (bundled with Node.js)
- TMDB account with a v4 API Read Access Token
- Appwrite project with Database service enabled

## Getting Started
1. Install dependencies:
   ```bash
   npm install
   ```
2. Create `.env.local` and provide your own keys:
   ```bash
   cp .env.local.example .env.local
   ```
3. Run the dev server:
   ```bash
   npm run dev
   ```
4. Open the printed local URL (typically `http://localhost:5173`).

## Environment Variables
Configure the following variables inside `.env.local` (values shown here are placeholders):

```bash
VITE_TMDB_API_KEY="<your_tmdb_v4_read_access_token>"
VITE_APPWRITE_ENDPOINT="https://sfo.cloud.appwrite.io/v1"
VITE_APPWRITE_PROJECT_ID="<your_appwrite_project_id>"
VITE_APPWRITE_DATABASE_ID="<movie_metrics_database_id>"
VITE_APPWRITE_TABLE_ID="<movie_metrics_collection_id>"
```

Restart `npm run dev` whenever you change environment variables.

## Appwrite Setup
1. Create (or reuse) a project in Appwrite and note the **Project ID**.
2. Enable the **Database** service and create a database (for example `movie-metrics`), recording its ID.
3. Inside that database, add a collection (table) with these attributes:
   - `searchTerm` - string, required
   - `count` - integer, required
   - `movie_id` - string, required
   - `poster_url` - string, required
4. Grant read permissions to anonymous (or your preferred auth role) and write permissions for the API key that the frontend uses.
5. (Optional) Add an index on `searchTerm` for quicker lookups.

## Available Scripts
- `npm run dev` - Start the Vite dev server.
- `npm run build` - Create a production build in `dist/`.
- `npm run preview` - Preview the production build locally.
- `npm run lint` - Run ESLint with the project rules.

## Project Structure
```
src/
  components/
    MovieCard.jsx     # Renders individual movie details
    Search.jsx        # Input with debounced search term handling
    Spinner.jsx       # Loading indicator SVG
  App.jsx             # Main page layout and API calls
  appwrite.js         # Appwrite client helpers for trending metrics
  index.css           # Global styles from the tutorial
```
