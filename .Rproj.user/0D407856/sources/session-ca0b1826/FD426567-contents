##Packages##

# install.packages("httr")
# install.packages("jsonlite")
library(httr)
library(jsonlite)

# Stadt und API-Key
city <- "Stuttgart"
api_key <- "37902b8224263aa490b5dee0c2574ea1"

# API-URL
url <- paste0(
  "https://api.openweathermap.org/data/2.5/weather?q=",
  URLencode(city),
  "&appid=", api_key,
  "&units=metric&lang=de"
)

# Daten holen
res <- GET(url)
json_text <- content(res, as = "text", encoding = "UTF-8")
data <- fromJSON(json_text)

# Wetterdaten extrahieren
wetterlage <- data$weather$description[1]
temperatur <- round(data$main$temp, 1)

# HTML-Vorlage laden
template_path <- "data/wetter_template.html"
template <- readLines(template_path, encoding = "UTF-8")

# Platzhalter ersetzen
output <- gsub("\\[STADT\\]", city, template)
output <- gsub("\\[WETTER\\]", wetterlage, output)
output <- gsub("\\[TEMP\\]", paste0(temperatur, " °C"), output)

# Ausgabe speichern
writeLines(output, "output/index.html", useBytes = TRUE)

cat("Wetterseite erfolgreich erstellt: output/index.html\n")

