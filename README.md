Minnesota Weather Map

This R script creates an interactive weather map for multiple cities in Minnesota using the OpenWeather API and Leaflet. Each city is marked with real-time weather data, including temperature, humidity, and weather conditions.

Features

Fetches real-time weather data for multiple Minnesota cities

Visualizes data on an interactive Leaflet map

Saves the map as a standalone HTML file

Preview

The output is an interactive HTML map (minnesota_weather_map.html) that you can open in any browser.

Getting Started

1. Clone this Repository

git clone https://github.com/YOUR_USERNAME/minnesota-weather-map.git
cd minnesota-weather-map

2. Install Dependencies

Open R or RStudio and run:

install.packages(c("httr", "jsonlite", "leaflet", "dplyr", "htmlwidgets"))

3. Set Your OpenWeather API Key

In the script weather_map_mn.R, replace the line:

api_key <- "2a38086dc2f585ac7817f626842e5d13"

with your actual OpenWeather API key. You can get one by signing up at openweathermap.org.

4. Run the Script

You can run the script directly in RStudio or from the R console:

source("weather_map_mn.R")

This will generate minnesota_weather_map.html in your working directory.

Customization

You can modify the cities vector in the script to include any U.S. cities you want:

cities <- c("Minneapolis, MN", "Duluth, MN", "Rochester, MN")

Author

Kris Kahler
Feel free to use or modify this project. Attribution appreciated!

