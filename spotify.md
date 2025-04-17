# spotify
import spotipy
from spotipy.oauth2 import SpotifyOAuth

# Replace these with your Spotify API credentials
CLIENT_ID = "your_client_id"
CLIENT_SECRET = "your_client_secret"
REDIRECT_URI = "http://localhost:8888/callback"

# Set up the Spotify API client
scope = "user-library-read"  # Example scope for accessing user's library
sp = spotipy.Spotify(auth_manager=SpotifyOAuth(client_id=CLIENT_ID,
                                               client_secret=CLIENT_SECRET,
                                               redirect_uri=REDIRECT_URI,
                                               scope=scope))

# Example: Get current user's saved tracks
def get_saved_tracks():
    results = sp.current_user_saved_tracks()
    for item in results['items']:
        track = item['track']
        print(f"{track['name']} by {', '.join(artist['name'] for artist in track['artists'])}")

# Example: Search for an artist
def search_artist(artist_name):
    results = sp.search(q=f"artist:{artist_name}", type="artist")
    for artist in results['artists']['items']:
        print(f"Found artist: {artist['name']} (Popularity: {artist['popularity']})")

# Run examples
if __name__ == "__main__":
    print("Fetching saved tracks:")
    get_saved_tracks()

    print("\nSearching for artist 'Taylor Swift':")
    search_artist("Taylor Swift")
