# Practice-stuffs
import requests
import pandas as pd

url = "https://imdb236.p.rapidapi.com/api/imdb/top250-movies"

headers = {
	"x-rapidapi-key": "addbf1abd6msh463d835668750a1p11667bjsn6c757fe0b42d",
	"x-rapidapi-host": "imdb236.p.rapidapi.com"
}

response = requests.get(url, headers=headers)

print(response.json())

import pandas as pd

# Assume this returns a list of dictionaries (multiple movies)
data = response.json()

# Convert to DataFrame
df = pd.DataFrame(data)

# Select specific columns (use double square brackets)
columns = ["id", "primaryTitle", "originalTitle", "type", "description",
           "url", "primaryImage", "trailer", "contentRating", "startYear", "releaseDate"]

# Safely filter only available columns (in case some keys are missing)
df = df[[col for col in columns if col in df.columns]]

# Save to CSV
df.to_csv("movies.csv", index=False)


df = pd.read_csv("movies.csv")
df.head()  # Display first 5 rows



from google.colab import files
files.download("movies.csv")
