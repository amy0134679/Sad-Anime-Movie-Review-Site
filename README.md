**Features**
- Movie Selection: Choose from a list of emotional anime films.
- Dynamic API Integration: Fetches real-time movie data from TMDB.
- Movie Details: Displays title, original title, country of origin, release date, runtime, language, status, rating, and overview.
- Visual Enhancements: Includes a background image, stylish UI, and movie posters.
- Embedded Trailer: Watch trailers directly within the app.

**Technologies Used**
- Vue.js (Composition API)
- Axios (for API requests)
- TMDB API (for movie data)
- HTML, CSS (for styling)

**Installation & Setup**
  Clone the repository:
 - git clone https://github.com/yourusername/anime-movies-app.git

  Navigate to the project directory:
 - cd anime-movies-app

  Install dependencies:
 - npm install

  Create a key.js file in the src directory and add your TMDB API key:
- export const TMDB_API_KEY = 'your_api_key_here';

  Start the development server:
- npm run dev

**Usage**
- Select a movie from the dropdown menu.
- Click the "GET" button to fetch and display movie details.
- Watch the trailer directly on the page.
