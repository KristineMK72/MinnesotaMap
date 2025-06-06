# MinnesotaMap 

library(httr)
library(jsonlite)
library(leaflet)
library(htmlwidgets).

# Your OpenWeather API key
api_key <- Sys.getenv("OPENWEATHER_API_KEY")
if (api_key == "") {
  stop("Error: OPENWEATHER_API_KEY environment variable is not set.")
}
api_key <- "2a38086dc2f585ac7817f626842e5d13"

# Base API URL for the 5-day forecast (OpenWeather's 3-hour intervals)
base_url <- "https://api.openweathermap.org/data/2.5/forecast"

# List of Minnesota cities and their coordinates
cities <- data.frame(
  name = c("Baxter, MN", "Duluth, MN", "Rochester, MN", "Moorhead, MN", "Mankato, MN"),
  lat = c(46.3467, 46.7867, 44.0121, 46.8739, 44.1636),
  lon = c(-94.2124, -92.1005, -92.4802, -96.7697, -93.9994),
  stringsAsFactors = FALSE
)

# Initialize an empty list to store weather data
weather_list <- list()

# Fetch forecast for each city
for (i in 1:nrow(cities)) {
  url <- paste0(base_url, "?lat=", cities$lat[i], "&lon=", cities$lon[i], "&units=imperial&appid=", api_key)
  response <- GET(url)
  if (status_code(response) == 200) {
    data <- fromJSON(content(response, "text", encoding = "UTF-8"))
    weather_list[[cities$name[i]]] <- data
  } else {
    warning(paste("Failed to retrieve data for", cities$name[i]))
  }
}

# Create leaflet map centered on Minnesota
weather_map <- leaflet(data = cities) %>%
  addTiles() %>%
  setView(lng = -94.6, lat = 46.8, zoom = 6)

# Add weather markers
for (i in 1:nrow(cities)) {
  city_name <- cities$name[i]
  forecast <- weather_list[[city_name]]$list
  
  # Check for valid forecast data
  if (!is.null(forecast) && length(forecast) > 0) {
    popup_info <- paste0(
      "<b>", city_name, "</b><br>",
      "Temperature: ", forecast[[1]]$main$temp, " °F<br>",
      "Weather: ", forecast[[1]]$weather[[1]]$description, "<br>",
      "Wind: ", forecast[[1]]$wind$speed, " mph"
    )
    
    weather_map <- weather_map %>%
      addMarkers(
        lng = cities$lon[i], lat = cities$lat[i],
        popup = popup_info
      )
  }
}

# Save map as HTML
saveWidget(weather_map, file = "minnesota_weather_forecast_map.html")Replace the hardcoded API key with:

